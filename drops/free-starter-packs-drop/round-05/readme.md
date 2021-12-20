# Elimination Proof

|||
|---|---|
| **Drop** | Free Starter Packs Drop |
| **Round** | 5 |
| **Started** | December 10, 2021 5:00 PM EST |
| **Completed** | December 10, 2021 5:11 PM EST |
| **Tokens remaining before round** | 3,200 |
| **&nbsp;&nbsp;&nbsp;&nbsp;Per Asset** | 128 |
| **Tokens remaining after round** | 1,600 |
| **&nbsp;&nbsp;&nbsp;&nbsp;Per Asset** | 64 |

## Assets

- [M. Trout &#039;11 BGS 8.5](asset-368.md)
- [T. Brady &#039;04 PSA 10](asset-369.md)
- [T. Brady &#039;00 PSA 10](asset-370.md)
- [B. Mayfield &#039;18 PSA 10](asset-371.md)
- [T. Duncan &#039;97 PSA 10](asset-372.md)
- [K. Durant &#039;09 BGS 9](asset-373.md)
- [J. Montana &#039;81 PSA 8](asset-374.md)
- [T. Brady &#039;14 PSA 10](asset-375.md)
- [J. Burrow &#039;20 PSA 10](asset-376.md)
- [C. Johnson &#039;07 BGS 9.5](asset-377.md)
- [L. James &#039;17 PSA 10](asset-378.md)
- [Z. Williamson &#039;19 BGS 10](asset-379.md)
- [T. Tagovailoa &#039;20 PSA 10](asset-380.md)
- [M. Mantle &#039;62 PSA 6](asset-381.md)
- [L. James &#039;18 PSA 10](asset-382.md)
- [M. Jordan &#039;97 BGS 9.5](asset-383.md)
- [L. Jackson &#039;18 PSA 10](asset-384.md)
- [D. Jeter &#039;94 PSA 9](asset-385.md)
- [J. Allen &#039;18 PSA 10](asset-386.md)
- [M. Trout &#039;12 PSA 10](asset-387.md)
- [T. Woods &#039;01 PSA 10](asset-388.md)
- [Glurak &#039;99 PSA 8](asset-389.md)
- [K. Bryant &#039;96 PSA 10](asset-390.md)
- [B. Harper &#039;19 PSA 10](asset-391.md)
- [A. Olajuwon &#039;86 PSA 9](asset-392.md)

## Overview

### 1. For each asset, we assemble a ledger that counts each token remaining by wallet address or custodial owner. Then we shuffle this ledger.
- The number of rows in the ledger should equal the number of tokens remaining. For example, if wallet A owns 5 tokens of a given asset, wallet A will appear in the ledger exactly five times.
- The randomness in the shuffle comes from the Mersenne Twister algorithm.
- **Note:** If tokens remain uneliminated that are not owned by anyone, they are flagged as `UNOWNED`, sorted to the top and set to be eliminated first.

### 2. Create the hash.
- We use the hash as an identifier to attach to our random number request because that way we can prove that the random number we used to eliminate tokens is the exact number tied to this elimination.
- To build the hash, we start with this object:
  ```jsonc
  {
    // The salt is just some random data to make sure this hash is unique.
    "salt": "uFPJm3dsiPko7orVcmMFjJtAZ643k8IgFqNkiJaJhRyFYakrpluubWYiVkxgO3fk",

    // The collection_id is our internal ID for the drop. It will not change for
    // other eliminations in this drop.
    "collection_id": 9,

    // The round is what round of eliminations this is.
    "round": 5,

    "ledger": {
      "<asset_id1>": ["<entry1>", "<entry2>", ...],
      "<asset_id2>": ["<entry1>", "<entry2>", ...]
    }
  }
  ```

  - We minify the object (which is reproduced [here][ledger_full]), `sha256` the result and encode the result to hex.
    - Thus, our calculated hash is:
      ```plain
      8439dc5b63acf319f75ebcc9140190a1f2511645bef89813e2b1703cafcf8840
      ```

### 3. We send our hash up to the on-chain random oracle to get our random number.
  - The transaction hash to retrieve this random number was: `0x1e1c1907618bc400021a5a81e311ed77f5a2abba115353f0af5665e97d7ec50f` ([polygonscan][random_txn])
  - The number we retrieved was: `84325412169170102033530744419474199126642101726436569102527827361951530636478`

### 4. Determine whether we eliminate evens or odds.
  
  - Our random number was **EVEN**, so we eliminate tokens starting at index 0 (the first row of the ledger), then 2, then 4, and so on.
  
## 5. Mark tokens for elimination.
  - For each asset, step in order through each row of its ledger.
    - If the row is `UNOWNED`, mark it for elimination.
    - If the row index is **EVEN**, _and we haven't yet eliminated 64 tokens_, mark it for elimination.
    - Otherwise, this token makes it through!

6. Eliminate tokens, burn them on-chain, and we're done!

## Hashed Ledger

> Identifiers in the ledger take the form of either `<blokpax_user_id>_` for custodial entries or `_<wallet_address>` for wallet entries.

You can find the exact ledger we hashed [here][ledger_full].

**Expected Hash (hex-encoded):**
```
8439dc5b63acf319f75ebcc9140190a1f2511645bef89813e2b1703cafcf8840
```

To verify the hash, [download `ledger-full.json`][ledger_full] and then run the following in a Unix-y shell:

```bash
cat ledger-full.json | tr -d '\n' | shasum -a 256 | tr -d '-'
```

The hash you get should match exactly the one above.

---

# References

- Random number transaction: [Polygonscan][random_txn]

[random_txn]: https://polygonscan.com/tx/0x1e1c1907618bc400021a5a81e311ed77f5a2abba115353f0af5665e97d7ec50f
[ledger_full]: ledger-full.json
