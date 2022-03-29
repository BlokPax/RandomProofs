# Elimination Proof

|                                       |                             |
| ------------------------------------- | --------------------------- |
| **Drop**                              | Kobe Drop                   |
| **Round**                             | 5                           |
| **Started**                           | March 23, 2022 10:00 AM EDT |
| **Completed**                         | March 23, 2022 10:01 AM EDT |
| **Tokens remaining before round**     | 160                         |
| **&nbsp;&nbsp;&nbsp;&nbsp;Per Asset** | 16                          |
| **Tokens remaining after round**      | 80                          |
| **&nbsp;&nbsp;&nbsp;&nbsp;Per Asset** | 8                           |

## Assets

-   [\#1 - K. Bryant &\#039;96 PSA 10](asset-1285.md)
-   [\#2 - K. Bryant &\#039;96 PSA 10](asset-1286.md)
-   [\#3 - K. Bryant &\#039;96 PSA 10](asset-1287.md)
-   [\#4 - K. Bryant &\#039;96 PSA 10](asset-1288.md)
-   [\#5 - K. Bryant &\#039;96 PSA 9](asset-1289.md)
-   [\#6 - K. Bryant &\#039;96 PSA 10](asset-1290.md)
-   [\#7 - K. Bryant &\#039;96 PSA 10](asset-1291.md)
-   [\#8 - K. Bryant &\#039;96 BGS 9.5](asset-1292.md)
-   [\#9 - K. Bryant &\#039;96 PSA 10](asset-1293.md)
-   [\#10 - K. Bryant &\#039;96 BGS 9.5](asset-1294.md)

## Overview

### 1. For each asset, we assemble a ledger that counts each token remaining by wallet address or custodial owner. Then we shuffle this ledger.

-   The number of rows in the ledger should equal the number of tokens remaining. For example, if wallet A owns 5 tokens of a given asset, wallet A will appear in the ledger exactly five times.
-   The randomness in the shuffle comes from the Mersenne Twister algorithm.
-   **Note:** If tokens remain uneliminated that are not owned by anyone, they are flagged as `UNOWNED`, sorted to the top and set to be eliminated first.

### 2. Create the hash.

-   We use the hash as an identifier to attach to our random number request because that way we can prove that the random number we used to eliminate tokens is the exact number tied to this elimination.
-   To build the hash, we start with this object:

    ```jsonc
    {
      // The salt is just some random data to make sure this hash is unique.
      "salt": "0WeOfGJ8jXjlqmAPoWlU3IjbMnIByIbABGSXp7nfRX7NIQ3qnSgInkRJbtUj5aSh",

      // The collection_id is our internal ID for the drop. It will not change for
      // other eliminations in this drop.
      "collection_id": 22,

      // The round is what round of eliminations this is.
      "round": 5,

      "ledger": {
        "<asset_id1>": ["<entry1>", "<entry2>", ...],
        "<asset_id2>": ["<entry1>", "<entry2>", ...]
      }
    }
    ```

    -   We minify the object (which is reproduced [here][ledger_full]), `sha256` the result and encode the result to hex.
        -   Thus, our calculated hash is:
            ```plain
            3bcf33feee69b13819401119af03fc80578b9f31907095e4131e1c98cad63977
            ```

### 3. We send our hash up to the on-chain random oracle to get our random number.

-   The transaction hash to retrieve this random number was: `0x34b0a62308ac8bf82bf743d340b79fae551eb524a28ef885ddcf3d1a3fe71cd9` ([polygonscan][random_txn])
-   The number we retrieved was: `21250645109280568205233653200675777174222205511016388394605925734554036027284`

### 4. Determine whether we eliminate evens or odds.

-   Our random number was **EVEN**, so we eliminate tokens starting at index 0 (the first row of the ledger), then 2, then 4, and so on.

## 5. Mark tokens for elimination.

-   For each asset, step in order through each row of its ledger.
    -   If the row is `UNOWNED`, mark it for elimination.
    -   If the row index is **EVEN**, _and we haven't yet eliminated 8 tokens_, mark it for elimination.
    -   Otherwise, this token makes it through!

6. Eliminate tokens, burn them on-chain, and we're done!

## Hashed Ledger

> Identifiers in the ledger take the form of either `<blokpax_user_id>_` for custodial entries or `_<wallet_address>` for wallet entries.

You can find the exact ledger we hashed [here][ledger_full].

**Expected Hash (hex-encoded):**

```
3bcf33feee69b13819401119af03fc80578b9f31907095e4131e1c98cad63977
```

To verify the hash, [download `ledger-full.json`][ledger_full] and then run the following in a Unix-y shell:

```bash
cat ledger-full.json | tr -d '\n' | shasum -a 256 | tr -d '-'
```

The hash you get should match exactly the one above.

---

# References

-   Random number transaction: [Polygonscan][random_txn]

[random_txn]: https://polygonscan.com/tx/0x34b0a62308ac8bf82bf743d340b79fae551eb524a28ef885ddcf3d1a3fe71cd9
[ledger_full]: ledger-full.json
