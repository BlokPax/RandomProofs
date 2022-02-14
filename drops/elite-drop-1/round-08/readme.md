# Elimination Proof

|||
|---|---|
| **Drop** | Elite Drop #1 |
| **Round** | 8 |
| **Started** | February 14, 2022 5:00 PM EST |
| **Completed** | February 14, 2022 5:02 PM EST |
| **Tokens remaining before round** | 400 |
| **&nbsp;&nbsp;&nbsp;&nbsp;Per Asset** | 16 |
| **Tokens remaining after round** | 200 |
| **&nbsp;&nbsp;&nbsp;&nbsp;Per Asset** | 8 |

## Assets

- [B. Ruth &#039;48 PSA 1.5](asset-847.md)
- [B. Adebayo &#039;17 PSA 10](asset-848.md)
- [B. Jackson &#039;13 PSA 10](asset-849.md)
- [Charizard &#039;99 PSA 8](asset-850.md)
- [C. Pulisic &#039;17 BGS 8](asset-851.md)
- [C. McGregor &#039;21 PSA 10](asset-852.md)
- [D. Jeter &#039;01 BGS 9.5](asset-853.md)
- [E. Haaland &#039;19 PSA 10](asset-854.md)
- [F. Tatís Jr. &#039;19 BGS 10](asset-855.md)
- [H. Aaron &#039;54 SGC A](asset-856.md)
- [J. Morant &#039;19 BGS 9](asset-857.md)
- [J. Robinson &#039;52 SGC A](asset-858.md)
- [J. Burrow &#039;20 PSA 10](asset-859.md)
- [J. Herbert &#039;20 PSA 9](asset-860.md)
- [K. Griffey Jr. &#039;21 PSA 10](asset-861.md)
- [K. Bryant &#039;13 BGS 9.5](asset-862.md)
- [L. James &#039;19 BGS 10](asset-863.md)
- [M. Ryan &#039;08 PSA 10](asset-864.md)
- [M. Mantle &#039;52 PSA 1](asset-865.md)
- [M. Mantle &#039;54 PSA 5](asset-866.md)
- [R. Moss &#039;98 PSA 10](asset-867.md)
- [S. Curry &#039;09 PSA 9](asset-868.md)
- [T. Brady &#039;00 PSA Authentic](asset-869.md)
- [V. Carter &#039;98 BGS 9](asset-870.md)
- [Z. Williamson &#039;19 BGS 10](asset-871.md)

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
    "salt": "HLsFWxurboSyz8RxJEsHxwNSnF9OFnmJe80x9gz1seqz3m9WBx9wz9sHc8nLeUrn",

    // The collection_id is our internal ID for the drop. It will not change for
    // other eliminations in this drop.
    "collection_id": 13,

    // The round is what round of eliminations this is.
    "round": 8,

    "ledger": {
      "<asset_id1>": ["<entry1>", "<entry2>", ...],
      "<asset_id2>": ["<entry1>", "<entry2>", ...]
    }
  }
  ```

  - We minify the object (which is reproduced [here][ledger_full]), `sha256` the result and encode the result to hex.
    - Thus, our calculated hash is:
      ```plain
      6606f6f5b2d05194ca4cead7ab3ac62cf96590fc7367a0b504069052723c6bca
      ```

### 3. We send our hash up to the on-chain random oracle to get our random number.
  - The transaction hash to retrieve this random number was: `0x49179693504bd09c93f3a30200e1c10932c2e15690e214f913e902ba8f0c47e0` ([polygonscan][random_txn])
  - The number we retrieved was: `5383975847419820360821080898627750590236272356373845686427812233980966139976`

### 4. Determine whether we eliminate evens or odds.
  
  - Our random number was **EVEN**, so we eliminate tokens starting at index 0 (the first row of the ledger), then 2, then 4, and so on.
  
## 5. Mark tokens for elimination.
  - For each asset, step in order through each row of its ledger.
    - If the row is `UNOWNED`, mark it for elimination.
    - If the row index is **EVEN**, _and we haven't yet eliminated 8 tokens_, mark it for elimination.
    - Otherwise, this token makes it through!

6. Eliminate tokens, burn them on-chain, and we're done!

## Hashed Ledger

> Identifiers in the ledger take the form of either `<blokpax_user_id>_` for custodial entries or `_<wallet_address>` for wallet entries.

You can find the exact ledger we hashed [here][ledger_full].

**Expected Hash (hex-encoded):**
```
6606f6f5b2d05194ca4cead7ab3ac62cf96590fc7367a0b504069052723c6bca
```

To verify the hash, [download `ledger-full.json`][ledger_full] and then run the following in a Unix-y shell:

```bash
cat ledger-full.json | tr -d '\n' | shasum -a 256 | tr -d '-'
```

The hash you get should match exactly the one above.

---

# References

- Random number transaction: [Polygonscan][random_txn]

[random_txn]: https://polygonscan.com/tx/0x49179693504bd09c93f3a30200e1c10932c2e15690e214f913e902ba8f0c47e0
[ledger_full]: ledger-full.json
