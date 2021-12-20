# Elimination Proof

|||
|---|---|
| **Drop** | Jordan Card Drop |
| **Round** | 3 |
| **Started** | December 19, 2021 10:00 AM EST |
| **Completed** | December 19, 2021 10:13 AM EST |
| **Tokens remaining before round** | 11,776 |
| **&nbsp;&nbsp;&nbsp;&nbsp;Per Asset** | 512 |
| **Tokens remaining after round** | 5,888 |
| **&nbsp;&nbsp;&nbsp;&nbsp;Per Asset** | 256 |

## Assets

- [12 - &#039;96 Fleer Jordan PSA 9](asset-393.md)
- [10 - &#039;99 Upper Deck Jordan PSA 10](asset-394.md)
- [15 - &#039;94 Upper Deck Jordan PSA 10](asset-395.md)
- [8 - &#039;88 Fleer Jordan PSA 9](asset-396.md)
- [17 - &#039;94 Upper Deck Jordan PSA 10](asset-397.md)
- [20 - &#039;94 Upper Deck Jordan PSA 10](asset-398.md)
- [3 - &#039;86 Fleer Jordan PSA 8](asset-399.md)
- [4 - &#039;86 Fleer Jordan PSA 6](asset-400.md)
- [11 - &#039;97 Topps Jordan PSA 8](asset-401.md)
- [16 - &#039;94 Upper Deck Jordan PSA 10](asset-402.md)
- [7 - &#039;86 Fleer Jordan PSA 6](asset-403.md)
- [21 - &#039;94 Upper Deck Jordan PSA 10](asset-404.md)
- [19 - &#039;94 Upper Deck Jordan PSA 10](asset-405.md)
- [5 - &#039;86 Fleer Jordan PSA 8](asset-406.md)
- [1 - &#039;86 Fleer Jordan SGC 96](asset-407.md)
- [18 - &#039;94 Upper Deck Jordan PSA 10](asset-408.md)
- [23 - &#039;94 Upper Deck Jordan PSA 10](asset-409.md)
- [22 - &#039;94 Upper Deck Jordan PSA 10](asset-410.md)
- [6 - &#039;86 Fleer Jordan SGC 8](asset-411.md)
- [2 - &#039;86 Fleer Jordan PSA 9](asset-412.md)
- [14 - &#039;94 Upper Deck Jordan PSA 10](asset-413.md)
- [13 - &#039;94 Upper Deck Jordan PSA 10](asset-414.md)
- [9 - &#039;97 Upper Deck Jordan PSA 9](asset-415.md)

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
    "salt": "gBSfNO0ZqJnSHM98J67GKoFrB11npexYRPRsaDgZEah5oA0o2vA2bmQXqF3taKsg",

    // The collection_id is our internal ID for the drop. It will not change for
    // other eliminations in this drop.
    "collection_id": 10,

    // The round is what round of eliminations this is.
    "round": 3,

    "ledger": {
      "<asset_id1>": ["<entry1>", "<entry2>", ...],
      "<asset_id2>": ["<entry1>", "<entry2>", ...]
    }
  }
  ```

  - We minify the object (which is reproduced [here][ledger_full]), `sha256` the result and encode the result to hex.
    - Thus, our calculated hash is:
      ```plain
      6aee615a744f7cc7dfe0f2918c5668fbfdf286761d4df4d4b602ebabb00a9e3d
      ```

### 3. We send our hash up to the on-chain random oracle to get our random number.
  - The transaction hash to retrieve this random number was: `0x09a040475a6ef45d20596b556ce15e0616f6b151c09449edfef3696f0dfd72d7` ([polygonscan][random_txn])
  - The number we retrieved was: `8506877246665048661791757067436213340056611894016223021817245687763360783452`

### 4. Determine whether we eliminate evens or odds.
  
  - Our random number was **EVEN**, so we eliminate tokens starting at index 0 (the first row of the ledger), then 2, then 4, and so on.
  
## 5. Mark tokens for elimination.
  - For each asset, step in order through each row of its ledger.
    - If the row is `UNOWNED`, mark it for elimination.
    - If the row index is **EVEN**, _and we haven't yet eliminated 256 tokens_, mark it for elimination.
    - Otherwise, this token makes it through!

6. Eliminate tokens, burn them on-chain, and we're done!

## Hashed Ledger

> Identifiers in the ledger take the form of either `<blokpax_user_id>_` for custodial entries or `_<wallet_address>` for wallet entries.

You can find the exact ledger we hashed [here][ledger_full].

**Expected Hash (hex-encoded):**
```
6aee615a744f7cc7dfe0f2918c5668fbfdf286761d4df4d4b602ebabb00a9e3d
```

To verify the hash, [download `ledger-full.json`][ledger_full] and then run the following in a Unix-y shell:

```bash
cat ledger-full.json | tr -d '\n' | shasum -a 256 | tr -d '-'
```

The hash you get should match exactly the one above.

---

# References

- Random number transaction: [Polygonscan][random_txn]

[random_txn]: https://polygonscan.com/tx/0x09a040475a6ef45d20596b556ce15e0616f6b151c09449edfef3696f0dfd72d7
[ledger_full]: ledger-full.json
