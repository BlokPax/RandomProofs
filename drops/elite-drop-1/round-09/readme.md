# Elimination Proof

|||
|---|---|
| **Drop** | Elite Drop #1 |
| **Round** | 9 |
| **Started** | February 15, 2022 6:00 PM EST |
| **Completed** | February 15, 2022 6:03 PM EST |
| **Tokens remaining before round** | 200 |
| **&nbsp;&nbsp;&nbsp;&nbsp;Per Asset** | 8 |
| **Tokens remaining after round** | 100 |
| **&nbsp;&nbsp;&nbsp;&nbsp;Per Asset** | 4 |

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
    "salt": "20YID2liX3DbjgWMibJdiMHhRiERjL7yJOeP4jQyWK0LjmwElGQxDnAG8Eabl8so",

    // The collection_id is our internal ID for the drop. It will not change for
    // other eliminations in this drop.
    "collection_id": 13,

    // The round is what round of eliminations this is.
    "round": 9,

    "ledger": {
      "<asset_id1>": ["<entry1>", "<entry2>", ...],
      "<asset_id2>": ["<entry1>", "<entry2>", ...]
    }
  }
  ```

  - We minify the object (which is reproduced [here][ledger_full]), `sha256` the result and encode the result to hex.
    - Thus, our calculated hash is:
      ```plain
      0d502749f020bbdc97896971a562d441a0ff6e0a09c31986092a280a0383f3ca
      ```

### 3. We send our hash up to the on-chain random oracle to get our random number.
  - The transaction hash to retrieve this random number was: `0xad21a3a0a2ede21d3b19c9ae295341c81e7fccbfeee029dadbac2f56d8107e3a` ([polygonscan][random_txn])
  - The number we retrieved was: `100768606261553404835213068353957762711608224140322587377667364980395028762887`

### 4. Determine whether we eliminate evens or odds.
  
  - Our random number was **ODD**, so we eliminate tokens starting at index 1 (the second row of the ledger), then 3, then 5, and so on.
  
## 5. Mark tokens for elimination.
  - For each asset, step in order through each row of its ledger.
    - If the row is `UNOWNED`, mark it for elimination.
    - If the row index is **ODD**, _and we haven't yet eliminated 4 tokens_, mark it for elimination.
    - Otherwise, this token makes it through!

6. Eliminate tokens, burn them on-chain, and we're done!

## Hashed Ledger

> Identifiers in the ledger take the form of either `<blokpax_user_id>_` for custodial entries or `_<wallet_address>` for wallet entries.

You can find the exact ledger we hashed [here][ledger_full].

**Expected Hash (hex-encoded):**
```
0d502749f020bbdc97896971a562d441a0ff6e0a09c31986092a280a0383f3ca
```

To verify the hash, [download `ledger-full.json`][ledger_full] and then run the following in a Unix-y shell:

```bash
cat ledger-full.json | tr -d '\n' | shasum -a 256 | tr -d '-'
```

The hash you get should match exactly the one above.

---

# References

- Random number transaction: [Polygonscan][random_txn]

[random_txn]: https://polygonscan.com/tx/0xad21a3a0a2ede21d3b19c9ae295341c81e7fccbfeee029dadbac2f56d8107e3a
[ledger_full]: ledger-full.json
