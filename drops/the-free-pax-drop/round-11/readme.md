# Elimination Proof

|||
|---|---|
| **Drop** | The FREE Pax Drop |
| **Round** | 11 |
| **Started** | October 27, 2021 4:00 PM EDT |
| **Completed** | October 27, 2021 4:11 PM EDT |
| **Tokens remaining before round** | 24 |
| **&nbsp;&nbsp;&nbsp;&nbsp;Per Asset** | 2 |
| **Tokens remaining after round** | 12 |
| **&nbsp;&nbsp;&nbsp;&nbsp;Per Asset** | 1 |

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
    "salt": "Ogr45NNfJdN30JgHzscBqXpQsJZm7XYgqWoaT04EGfPN0699XTXK6sX2xJdbSe9s",

    // The collection_id is our internal ID for the drop. It will not change for
    // other eliminations in this drop.
    "collection_id": 7,

    // The round is what round of eliminations this is.
    "round": 11,

    "ledger": {
      "<asset_id1>": ["<entry1>", "<entry2>", ...],
      "<asset_id2>": ["<entry1>", "<entry2>", ...]
    }
  }
  ```

  - We minify the object (which is reproduced [here][ledger_full]), `sha256` the result and encode the result to hex.
    - Thus, our calculated hash is:
      ```plain
      e07380b22ef01f0d37325558a646d2da5cde83a0fcb4412876415402ca1ce297
      ```

### 3. We send our hash up to the on-chain random oracle to get our random number.
  - The transaction hash to retrieve this random number was: `0x428e1474b5b5028fdb76fff471f3c779f51759ae2a416e6502152193defd5098` ([polygonscan][random_txn])
  - The number we retrieved was: `38064103057214283600900400695385350412175450688613078948888324855325630213961`

### 4. Determine whether we eliminate evens or odds.
  
  - Our random number was **ODD**, so we eliminate tokens starting at index 1 (the second row of the ledger), then 3, then 5, and so on.
  
## 5. Mark tokens for elimination.
  - For each asset, step in order through each row of its ledger.
    - If the row is `UNOWNED`, mark it for elimination.
    - If the row index is **ODD**, _and we haven't yet eliminated 1 tokens_, mark it for elimination.
    - Otherwise, this token makes it through!

6. Eliminate tokens, burn them on-chain, and we're done!

## Hashed Ledger

> Identifiers in the ledger take the form of either `<blokpax_user_id>_` for custodial entries or `_<wallet_address>` for wallet entries.

You can find the exact ledger we hashed [here][ledger_full].

**Expected Hash (hex-encoded):**
```
e07380b22ef01f0d37325558a646d2da5cde83a0fcb4412876415402ca1ce297
```

To verify the hash, [download `ledger-full.json`][ledger_full] and then run the following in a Unix-y shell:

```bash
cat ledger-full.json | tr -d '\n' | shasum -a 256 | tr -d '-'
```

The hash you get should match exactly the one above.

---

# References

- Random number transaction: [Polygonscan][random_txn]

[random_txn]: https://polygonscan.com/tx/0x428e1474b5b5028fdb76fff471f3c779f51759ae2a416e6502152193defd5098
[ledger_full]: ledger-full.json
