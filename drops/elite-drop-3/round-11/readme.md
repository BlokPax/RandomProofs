# Elimination Proof

|||
|---|---|
| **Drop** | Elite Drop #3 |
| **Round** | 11 |
| **Started** | May 24, 2022 10:00 PM EDT |
| **Completed** | May 24, 2022 10:01 PM EDT |
| **Tokens remaining before round** | 72 |
| **&nbsp;&nbsp;&nbsp;&nbsp;Per Asset** | 2 |
| **Tokens remaining after round** | 36 |
| **&nbsp;&nbsp;&nbsp;&nbsp;Per Asset** | 1 |

## Assets

- [A. Judge &#039;13 BGS 10](asset-1754.md)
- [A. Edwards &#039;20 PSA 10](asset-1755.md)
- [B. Ruth &#039;99 SGC A](asset-1756.md)
- [B. Jackson/K. Griffey Jr./F. Thomas &#039;13 PSA 10](asset-1757.md)
- [Charizard &#039;02 PSA 9](asset-1758.md)
- [C. McGregor &#039;13 PSA 10](asset-1759.md)
- [C. Monster R &#039;20 BGS 9](asset-1760.md)
- [D. Samuel &#039;19 PSA 10](asset-1761.md)
- [H. Aaron &#039;54 SGC 8](asset-1762.md)
- [J. Robinson &#039;53 PSA 2.5](asset-1763.md)
- [J. Burrow &#039;20 PSA 8](asset-1764.md)
- [J. Unitas &#039;00 PSA 10](asset-1765.md)
- [J. Allen &#039;18 PSA 10](asset-1766.md)
- [J. Soto &#039;16 BGS 9.5](asset-1767.md)
- [J. Herbert &#039;20 PSA 9](asset-1768.md)
- [K. Durant &#039;07 BGS 9](asset-1769.md)
- [K. Bryant &#039;09 BGS 8.5](asset-1770.md)
- [L. Fitzgerald &#039;04 BGS 9](asset-1771.md)
- [L. James &#039;08 PSA 10](asset-1772.md)
- [Legend Geek Mint Pass](asset-1773.md)
- [L. Messi &#039;17 PSA 10](asset-1774.md)
- [L. Pikachu &#039;16 PSA 10](asset-1775.md)
- [L. Robert &#039;18 BGS 9.5](asset-1776.md)
- [M. Jordan &#039;97 PSA 10](asset-1777.md)
- [M. Trout &#039;11 BGS 10](asset-1778.md)
- [Moonbird #3645](asset-1779.md)
- [R. Nadal &#039;03 PSA 10](asset-1780.md)
- [Spider-Man &#039;84 CGC 9.8](asset-1781.md)
- [Spider-Man &#039;95 PSA 10](asset-1782.md)
- [S. Mario Bros. &#039;85 WATA 8](asset-1783.md)
- [T. Brady &#039;00 BGS 9.5](asset-1784.md)
- [T. Hawk &#039;15 BGS 9.5](asset-1785.md)
- [T. Lawrence &#039;21 PSA 10](asset-1786.md)
- [VaynerSports Pass #11830](asset-1787.md)
- [VeeFriends Series 2 - Like a Sponge #35902](asset-1788.md)
- [W. Gretzky &#039;97 SGC 8.5](asset-1789.md)

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
    "salt": "nRZxwNrZMhPUxfsWXnCvPAuGGJkkOsRfKiAUasl8rageuhZQLQm3wXxYXh4PCnfD",

    // The collection_id is our internal ID for the drop. It will not change for
    // other eliminations in this drop.
    "collection_id": 26,

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
      560c8010656053708be3b380a88ffa7cc0f6d238801c7ce3f86e90abca17b967
      ```

### 3. We send our hash up to the on-chain random oracle to get our random number.
  - The transaction hash to retrieve this random number was: `0x3ffdcc8dbd53a50d2a4382add4fc2f1e351047469e55f53a0cd252238c849692` ([polygonscan][random_txn])
  - The number we retrieved was: `80314089551654578261414205643265044610778790278468054819142906010545503950402`

### 4. Determine whether we eliminate evens or odds.
  
  - Our random number was **EVEN**, so we eliminate tokens starting at index 0 (the first row of the ledger), then 2, then 4, and so on.
  
## 5. Mark tokens for elimination.
  - For each asset, step in order through each row of its ledger.
    - If the row is `UNOWNED`, mark it for elimination.
    - If the row index is **EVEN**, _and we haven't yet eliminated 1 tokens_, mark it for elimination.
    - Otherwise, this token makes it through!

6. Eliminate tokens, burn them on-chain, and we're done!

## Hashed Ledger

> Identifiers in the ledger take the form of either `<blokpax_user_id>_` for custodial entries or `_<wallet_address>` for wallet entries.

You can find the exact ledger we hashed [here][ledger_full].

**Expected Hash (hex-encoded):**
```
560c8010656053708be3b380a88ffa7cc0f6d238801c7ce3f86e90abca17b967
```

To verify the hash, [download `ledger-full.json`][ledger_full] and then run the following in a Unix-y shell:

```bash
cat ledger-full.json | tr -d '\n' | shasum -a 256 | tr -d '-'
```

The hash you get should match exactly the one above.

---

# References

- Random number transaction: [Polygonscan][random_txn]

[random_txn]: https://polygonscan.com/tx/0x3ffdcc8dbd53a50d2a4382add4fc2f1e351047469e55f53a0cd252238c849692
[ledger_full]: ledger-full.json
