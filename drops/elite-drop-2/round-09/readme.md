# Elimination Proof

|||
|---|---|
| **Drop** | Elite Drop #2 |
| **Round** | 9 |
| **Started** | April 5, 2022 6:00 PM EDT |
| **Completed** | April 5, 2022 6:01 PM EDT |
| **Tokens remaining before round** | 208 |
| **&nbsp;&nbsp;&nbsp;&nbsp;Per Asset** | 8 |
| **Tokens remaining after round** | 104 |
| **&nbsp;&nbsp;&nbsp;&nbsp;Per Asset** | 4 |

## Assets

- [A. Pujols &#039;01 PSA 9](asset-1370.md)
- [A. Iverson &#039;20 BGS 9](asset-1371.md)
- [Autographed Ted Williams Ball](asset-1372.md)
- [B. Bonds &#039;00 BGS 9](asset-1373.md)
- [Beyoncé &#039;07 PSA 10](asset-1374.md)
- [Black Lotus R A &#039;93 BGS 8](asset-1375.md)
- [Blue - Eyes White Dragon &#039;02 BGS 9](asset-1376.md)
- [C. Ronaldo &#039;06 BGS 9.5](asset-1377.md)
- [D. Jeter &#039;93 PSA 8.5](asset-1378.md)
- [Fantastic Four #52 CGC 5](asset-1379.md)
- [J. Allen &#039;18 PSA 10](asset-1380.md)
- [K. Abdul-Jabbar &#039;12 PSA 10](asset-1381.md)
- [K. Murray &#039;19 BGS 9.5](asset-1382.md)
- [L. James &#039;04 BGS 9](asset-1383.md)
- [Legend Geek Mint Pass](asset-1384.md)
- [L. Messi &#039;06 BGS 9.5](asset-1385.md)
- [L. Dončić &#039;18 PSA 10](asset-1386.md)
- [M. Johnson &#039;03 PSA 9](asset-1387.md)
- [M. Jordan &#039;98 BGS 8.5](asset-1388.md)
- [R. Moss &#039;00 BGS 9](asset-1389.md)
- [R. Henderson &#039;80 PSA 9](asset-1390.md)
- [S. Williams &#039;03 PSA 10](asset-1391.md)
- [S. Crosby &#039;05 PSA 10](asset-1392.md)
- [The Masters &#039;97 PSA 8](asset-1393.md)
- [T. Woods &#039;01 BGS 9](asset-1394.md)
- [T. Brady &#039;03 BGS 9](asset-1395.md)

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
    "salt": "eOZ2z58Z3ZNd3QhRueLtkRx9X3vD8h4V3UdOI34iEP2dwmjpbov1fpKhNu80zso0",

    // The collection_id is our internal ID for the drop. It will not change for
    // other eliminations in this drop.
    "collection_id": 23,

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
      0087890db1213a1beffa4e848695e3c30e108523186fa77555396f9d0102ece5
      ```

### 3. We send our hash up to the on-chain random oracle to get our random number.
  - The transaction hash to retrieve this random number was: `0xea3dea022d83d341d35a347080365da130eda3ad377f721d054c4b76794428a2` ([polygonscan][random_txn])
  - The number we retrieved was: `99049008095331206665446906962903629182318421930960391914400137848269623880110`

### 4. Determine whether we eliminate evens or odds.
  
  - Our random number was **EVEN**, so we eliminate tokens starting at index 0 (the first row of the ledger), then 2, then 4, and so on.
  
## 5. Mark tokens for elimination.
  - For each asset, step in order through each row of its ledger.
    - If the row is `UNOWNED`, mark it for elimination.
    - If the row index is **EVEN**, _and we haven't yet eliminated 4 tokens_, mark it for elimination.
    - Otherwise, this token makes it through!

6. Eliminate tokens, burn them on-chain, and we're done!

## Hashed Ledger

> Identifiers in the ledger take the form of either `<blokpax_user_id>_` for custodial entries or `_<wallet_address>` for wallet entries.

You can find the exact ledger we hashed [here][ledger_full].

**Expected Hash (hex-encoded):**
```
0087890db1213a1beffa4e848695e3c30e108523186fa77555396f9d0102ece5
```

To verify the hash, [download `ledger-full.json`][ledger_full] and then run the following in a Unix-y shell:

```bash
cat ledger-full.json | tr -d '\n' | shasum -a 256 | tr -d '-'
```

The hash you get should match exactly the one above.

---

# References

- Random number transaction: [Polygonscan][random_txn]

[random_txn]: https://polygonscan.com/tx/0xea3dea022d83d341d35a347080365da130eda3ad377f721d054c4b76794428a2
[ledger_full]: ledger-full.json
