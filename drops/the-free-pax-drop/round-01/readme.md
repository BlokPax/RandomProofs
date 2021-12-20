# Elimination Proof

|||
|---|---|
| **Drop** | The FREE Pax Drop |
| **Round** | 1 |
| **Started** | October 20, 2021 4:00 PM EDT |
| **Completed** | October 20, 2021 4:31 PM EDT |
| **Tokens remaining before round** | 24,576 |
| **&nbsp;&nbsp;&nbsp;&nbsp;Per Asset** | 2,048 |
| **Tokens remaining after round** | 12,288 |
| **&nbsp;&nbsp;&nbsp;&nbsp;Per Asset** | 1,024 |

## Assets

- [T. Brady &#039;00 PSA 8](asset-243.md)
- [Neymar Jr. &#039;20 PSA 8.5](asset-244.md)
- [J. Elway &#039;84 PSA 9](asset-245.md)
- [M. Trout &#039;12 PSA 10](asset-246.md)
- [J. Koosman/N. Ryan &#039;68 PSA 4](asset-247.md)
- [L. Jackson &#039;18 PSA 10](asset-248.md)
- [L. James &#039;03 BGS 9](asset-249.md)
- [W. Gretzky &#039;79 PSA 5](asset-250.md)
- [K. Bryant &#039;96 PSA 10](asset-251.md)
- [M. Johnson &#039;86 PSA 9](asset-252.md)
- [C. Charizard &#039;16 PSA 9](asset-253.md)
- [M. Mantle &#039;59 PSA 7](asset-254.md)

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
    "salt": "iOVJJUOw7RauP5UDNteLqTsdthAbc5UeZFlmSRAh6fgKDstEkZx5omm6izm4VzP1",

    // The collection_id is our internal ID for the drop. It will not change for
    // other eliminations in this drop.
    "collection_id": 7,

    // The round is what round of eliminations this is.
    "round": 1,

    "ledger": {
      "<asset_id1>": ["<entry1>", "<entry2>", ...],
      "<asset_id2>": ["<entry1>", "<entry2>", ...]
    }
  }
  ```

  - We minify the object (which is reproduced [here][ledger_full]), `sha256` the result and encode the result to hex.
    - Thus, our calculated hash is:
      ```plain
      61c78b526c9df7c647edadddd8d89f4cb76692cf54f2aa273b53a99239f94035
      ```

### 3. We send our hash up to the on-chain random oracle to get our random number.
  - The transaction hash to retrieve this random number was: `0x87def9bd2fb8b08d83557a9e2d5a2ec2b80e8d78ff08e6ba75f1f5651d193f89` ([polygonscan][random_txn])
  - The number we retrieved was: `81794765550045445307420302577786537766496871522822628674870132650959562260804`

### 4. Determine whether we eliminate evens or odds.
  
  - Our random number was **EVEN**, so we eliminate tokens starting at index 0 (the first row of the ledger), then 2, then 4, and so on.
  
## 5. Mark tokens for elimination.
  - For each asset, step in order through each row of its ledger.
    - If the row is `UNOWNED`, mark it for elimination.
    - If the row index is **EVEN**, _and we haven't yet eliminated 1,024 tokens_, mark it for elimination.
    - Otherwise, this token makes it through!

6. Eliminate tokens, burn them on-chain, and we're done!

## Hashed Ledger

> Identifiers in the ledger take the form of either `<blokpax_user_id>_` for custodial entries or `_<wallet_address>` for wallet entries.

You can find the exact ledger we hashed [here][ledger_full].

**Expected Hash (hex-encoded):**
```
61c78b526c9df7c647edadddd8d89f4cb76692cf54f2aa273b53a99239f94035
```

To verify the hash, [download `ledger-full.json`][ledger_full] and then run the following in a Unix-y shell:

```bash
cat ledger-full.json | tr -d '\n' | shasum -a 256 | tr -d '-'
```

The hash you get should match exactly the one above.

---

# References

- Random number transaction: [Polygonscan][random_txn]

[random_txn]: https://polygonscan.com/tx/0x87def9bd2fb8b08d83557a9e2d5a2ec2b80e8d78ff08e6ba75f1f5651d193f89
[ledger_full]: ledger-full.json
