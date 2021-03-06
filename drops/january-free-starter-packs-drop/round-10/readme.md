# Elimination Proof

|||
|---|---|
| **Drop** | January Free Starter Packs Drop |
| **Round** | 10 |
| **Started** | January 14, 2022 3:00 PM EST |
| **Completed** | January 14, 2022 3:29 PM EST |
| **Tokens remaining before round** | 100 |
| **&nbsp;&nbsp;&nbsp;&nbsp;Per Asset** | 4 |
| **Tokens remaining after round** | 50 |
| **&nbsp;&nbsp;&nbsp;&nbsp;Per Asset** | 2 |

## Assets

- [J. Herbert &#039;20 PSA 9](asset-442.md)
- [M. Trout &#039;12 PSA 10](asset-443.md)
- [C. McCaffrey &#039;17 PSA 10](asset-444.md)
- [H. Aaron &#039;58 PSA 6](asset-445.md)
- [Koosman/Ryan &#039;68 BVG 2.5](asset-446.md)
- [R. Gobert &#039;13 PSA 9](asset-447.md)
- [K. Mbappé &#039;18 PSA 9](asset-448.md)
- [K. Leonard &#039;12 BGS 9.5](asset-449.md)
- [C. Barkley &#039;86 PSA 9](asset-450.md)
- [E. Banks &#039;63 PSA 8](asset-451.md)
- [P. Mahomes II &#039;17 PSA 9](asset-452.md)
- [J. Elway &#039;84 PSA 9](asset-453.md)
- [K. Bryant &#039;08 PSA 9](asset-454.md)
- [M. Mantle &#039;57 PSA 6](asset-455.md)
- [P. Manning &#039;98 SGC 98](asset-456.md)
- [Venusaur &#039;99 PSA 9](asset-457.md)
- [G. Torres &#039;18 PSA 10](asset-458.md)
- [C. Wentz &#039;16 BGS 9.5](asset-459.md)
- [Z. Williamson &#039;19 BGS 9.5](asset-460.md)
- [Lugia &#039;00 BGS 9](asset-461.md)
- [A. Davis &#039;12 PSA 9](asset-462.md)
- [L. Dončić &#039;18 PSA 9](asset-463.md)
- [Charizard &#039;99 PSA 8](asset-464.md)
- [K. Bryant &#039;96 PSA 10](asset-465.md)
- [A. Judge &#039;18 BGS 9.5](asset-466.md)

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
    "salt": "wUFtbKjeA8HswfknIZQhyolGeYAePcWOAb90pT7wELs7HjExZyBbFppI3sGK7JTo",

    // The collection_id is our internal ID for the drop. It will not change for
    // other eliminations in this drop.
    "collection_id": 11,

    // The round is what round of eliminations this is.
    "round": 10,

    "ledger": {
      "<asset_id1>": ["<entry1>", "<entry2>", ...],
      "<asset_id2>": ["<entry1>", "<entry2>", ...]
    }
  }
  ```

  - We minify the object (which is reproduced [here][ledger_full]), `sha256` the result and encode the result to hex.
    - Thus, our calculated hash is:
      ```plain
      533e24c20eca7f5a938b9777c4a07914e845eb0d3ee5b2a3ccf7b6b1bab3e519
      ```

### 3. We send our hash up to the on-chain random oracle to get our random number.
  - The transaction hash to retrieve this random number was: `0xa114333c1f461f2f47bd068e2a72430b24b3fe5639be636c0f029b1d7bace1b9` ([polygonscan][random_txn])
  - The number we retrieved was: `77727517701006485632932530872503007454064865650093187657113102431493530941908`

### 4. Determine whether we eliminate evens or odds.
  
  - Our random number was **EVEN**, so we eliminate tokens starting at index 0 (the first row of the ledger), then 2, then 4, and so on.
  
## 5. Mark tokens for elimination.
  - For each asset, step in order through each row of its ledger.
    - If the row is `UNOWNED`, mark it for elimination.
    - If the row index is **EVEN**, _and we haven't yet eliminated 2 tokens_, mark it for elimination.
    - Otherwise, this token makes it through!

6. Eliminate tokens, burn them on-chain, and we're done!

## Hashed Ledger

> Identifiers in the ledger take the form of either `<blokpax_user_id>_` for custodial entries or `_<wallet_address>` for wallet entries.

You can find the exact ledger we hashed [here][ledger_full].

**Expected Hash (hex-encoded):**
```
533e24c20eca7f5a938b9777c4a07914e845eb0d3ee5b2a3ccf7b6b1bab3e519
```

To verify the hash, [download `ledger-full.json`][ledger_full] and then run the following in a Unix-y shell:

```bash
cat ledger-full.json | tr -d '\n' | shasum -a 256 | tr -d '-'
```

The hash you get should match exactly the one above.

---

# References

- Random number transaction: [Polygonscan][random_txn]

[random_txn]: https://polygonscan.com/tx/0xa114333c1f461f2f47bd068e2a72430b24b3fe5639be636c0f029b1d7bace1b9
[ledger_full]: ledger-full.json
