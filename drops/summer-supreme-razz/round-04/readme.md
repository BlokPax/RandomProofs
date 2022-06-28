# Elimination Proof

|||
|---|---|
| **Drop** | Summer Supreme Razz |
| **Round** | 4 |
| **Started** | June 28, 2022 10:00 AM EDT |
| **Completed** | June 28, 2022 10:03 AM EDT |
| **Tokens remaining before round** | 3,456 |
| **&nbsp;&nbsp;&nbsp;&nbsp;Per Asset** | 128 |
| **Tokens remaining after round** | 1,728 |
| **&nbsp;&nbsp;&nbsp;&nbsp;Per Asset** | 64 |

## Assets

- [A. Pujols &#039;01 BGS 9.5](asset-1852.md)
- [B. Aiyuk &#039;20 PSA 10](asset-1853.md)
- [G. Antetokounmpo &#039;13 BGS 9](asset-1854.md)
- [J. Burrow &#039;20 PSA 10](asset-1855.md)
- [J. Allen &#039;17 PSA 10](asset-1856.md)
- [J. Soto &#039;18 PSA 10](asset-1857.md)
- [J. Rodriguez &#039;19 BGS 10](asset-1858.md)
- [L. Ball &#039;20 PSA 10](asset-1859.md)
- [L. James &#039;03 PSA 10](asset-1860.md)
- [L. Hamilton &#039;20 PSA 10](asset-1861.md)
- [M. Mantle &#039;52 PSA 4](asset-1862.md)
- [M. Trout &#039;09 BGS 9.5](asset-1863.md)
- [Pikachu &#039;99 PSA 10](asset-1864.md)
- [R. Barrett &#039;19 BGS 9.5](asset-1865.md)
- [R. Rousey &#039;17 BGS 9.5](asset-1866.md)
- [R. Wilson &#039;12 PSA 10](asset-1867.md)
- [T. Brady &#039;00 BGS 9](asset-1868.md)
- [T. Lawrence &#039;21 BGS 9](asset-1869.md)
- [V. Guerrero Jr. &#039;16 BGS 9.5](asset-1870.md)
- [W. Franco &#039;19 PSA 10](asset-1871.md)
- [B. Favre/J. Rice &#039;00 BGS 9 Auto](asset-2176.md)
- [J. Hurts &#039;20 PSA 10](asset-2177.md)
- [K. Malone &#039;98 PSA 10](asset-2178.md)
- [K. Griffey Jr. &#039;20 BGS 9.5](asset-2179.md)
- [N. Chubb &#039;18 PSA 10](asset-2180.md)
- [P. Manning &#039;03 BGS 9.5](asset-2181.md)
- [W. Gretzky &#039;20 PSA 8](asset-2182.md)

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
    "salt": "5O5dFQlson4MlM4nwZZFCnzmHLASGJAdW2iFkvYTx0CjryPYPmk0UYyUpbTXORkh",

    // The collection_id is our internal ID for the drop. It will not change for
    // other eliminations in this drop.
    "collection_id": 30,

    // The round is what round of eliminations this is.
    "round": 4,

    "ledger": {
      "<asset_id1>": ["<entry1>", "<entry2>", ...],
      "<asset_id2>": ["<entry1>", "<entry2>", ...]
    }
  }
  ```

  - We minify the object (which is reproduced [here][ledger_full]), `sha256` the result and encode the result to hex.
    - Thus, our calculated hash is:
      ```plain
      19aba48607d6792e42b36f40f6e3daefaffff748f6dbb7fc000b31e5e7423af3
      ```

### 3. We send our hash up to the on-chain random oracle to get our random number.
  - The transaction hash to retrieve this random number was: `0xe3393dc652417ce5faf6500b12745b80e1e58f549ab016d83191d4051d5c46b5` ([polygonscan][random_txn])
  - The number we retrieved was: `68067450926482105838597047761042182218984192815171678669312813160681946898004`

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
19aba48607d6792e42b36f40f6e3daefaffff748f6dbb7fc000b31e5e7423af3
```

To verify the hash, [download `ledger-full.json`][ledger_full] and then run the following in a Unix-y shell:

```bash
cat ledger-full.json | tr -d '\n' | shasum -a 256 | tr -d '-'
```

The hash you get should match exactly the one above.

---

# References

- Random number transaction: [Polygonscan][random_txn]

[random_txn]: https://polygonscan.com/tx/0xe3393dc652417ce5faf6500b12745b80e1e58f549ab016d83191d4051d5c46b5
[ledger_full]: ledger-full.json
