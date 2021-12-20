# Elimination Proof

|||
|---|---|
| **Drop** | Blokpax 2021 Series 2 |
| **Round** | 3 |
| **Started** | October 8, 2021 6:00 PM EDT |
| **Completed** | October 8, 2021 7:01 PM EDT |
| **Tokens remaining before round** | 30,720 |
| **&nbsp;&nbsp;&nbsp;&nbsp;Per Asset** | 512 |
| **Tokens remaining after round** | 15,360 |
| **&nbsp;&nbsp;&nbsp;&nbsp;Per Asset** | 256 |

## Assets

- [K. Leonard &#039;18 PSA 10](asset-183.md)
- [A. Rodgers &#039;18 PSA 10](asset-184.md)
- [J. Robinson &#039;55 SGC 6](asset-185.md)
- [P. Manning &#039;98 PSA 9](asset-186.md)
- [F. Lindor &#039;15 PSA 10](asset-187.md)
- [P. Mahomes II &#039;17 PSA 10](asset-188.md)
- [P. Manning &#039;98 BGS 8](asset-189.md)
- [J. Robinson &#039;53 PSA 6.5](asset-190.md)
- [L. Jackson &#039;18 PSA 10](asset-191.md)
- [B. Bonds &#039;86 BGS 9.5](asset-192.md)
- [T. Brady &#039;00 BGS 9.5](asset-193.md)
- [K. Bryant &#039;96 PSA 9](asset-194.md)
- [T. Woods &#039;01 BGS 9.5](asset-195.md)
- [J. Soto &#039;18 PSA 10](asset-196.md)
- [L. James &#039;13-&#039;14 BGS 9.5](asset-197.md)
- [J. Elway &#039;84 PSA 9](asset-198.md)
- [S. Gilgeous-Alexander &#039;18 PSA 10](asset-199.md)
- [T. Brady &#039;14 PSA 10](asset-200.md)
- [L. James &#039;03 BGS 9.5](asset-201.md)
- [T. Young &#039;18 PSA 10](asset-202.md)
- [M. Jordan &#039;86 PSA 6](asset-203.md)
- [Z. Ibrahimović &#039;06 PSA 10](asset-204.md)
- [M. Trout &#039;11 BGS 8](asset-205.md)
- [C. Ronaldo &#039;14 PSA 10](asset-206.md)
- [M. Mantle &#039;53 PSA 4 (MK)](asset-207.md)
- [J. Erving &#039;86 PSA 10](asset-208.md)
- [M. Jordan &#039;97 PSA 9](asset-209.md)
- [H. Aaron &#039;55 PSA 6](asset-210.md)
- [K. Mbappé &#039;17 PSA 10](asset-211.md)
- [K. Griffey Jr. &#039;89 PSA 10](asset-212.md)
- [J. Herbert &#039;20 PSA 10](asset-213.md)
- [K. Durant &#039;07 PSA 10](asset-214.md)
- [M. Mantle &#039;52 PSA 4](asset-215.md)
- [K. Bryant &#039;96 PSA 10](asset-216.md)
- [K. Bryant &#039;96 PSA 10](asset-217.md)
- [P. Mahomes II &#039;17 BGS 9](asset-218.md)
- [M. Jordan &#039;86 PSA 10 Diamond FRAX 1/6](asset-219.md)
- [B. Mayfield &#039;18 BGS 9.5](asset-220.md)
- [D. Wade &#039;03 BGS 9.5](asset-221.md)
- [C. Charizard &#039;99 BGS 9](asset-222.md)
- [G. Antetokounmpo &#039;13 BGS 10](asset-223.md)
- [J. Burrow &#039;20 PSA 10](asset-224.md)
- [V. Guerrero Jr. &#039;19 BGS 10](asset-225.md)
- [M. Salah &#039;18 PSA 10](asset-226.md)
- [F. Tatís Jr. &#039;19 BGS 10](asset-227.md)
- [Giannis &#039;14-15 BGS 9](asset-228.md)
- [K. Bryant &#039;96 PSA 9](asset-229.md)
- [D. Jeter &#039;94 PSA 8](asset-230.md)
- [L. James &#039;03-04 BGS 9.5](asset-231.md)
- [V. Venusaur &#039;99 PSA 6](asset-232.md)
- [D. Jones &#039;19 BGS 9.5](asset-233.md)
- [T. Brady &#039;00 PSA 10](asset-234.md)
- [M. Trout &#039;11 PSA 9](asset-235.md)
- [Z. Williamson &#039;19-&#039;20 BGS 9.5](asset-236.md)
- [L. Dončić &#039;18 PSA 9](asset-237.md)
- [R. Wilson &#039;12 PSA 10](asset-238.md)
- [K. Durant &#039;13-&#039;14 BGS 9](asset-239.md)
- [J. Morant &#039;19 BGS 9.5](asset-240.md)
- [W. Gretzky &#039;79 PSA 5](asset-241.md)
- [C. McDavid &#039;15 PSA 10](asset-242.md)

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
    "salt": "6sGPbF830haOR2C7iJRHdw5rhmEeiBcy45akTLWhuwbk0hZ2VJQbDQXiGThLlwbt",

    // The collection_id is our internal ID for the drop. It will not change for
    // other eliminations in this drop.
    "collection_id": 4,

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
      cc86a10a098e5088d42842ec9affbde3133fa47622433901b508c150d6e6ec10
      ```

### 3. We send our hash up to the on-chain random oracle to get our random number.
  - The transaction hash to retrieve this random number was: `0xf0223f731e9edd4c11f9fdf94818e287b8f047a8b5c0fcc48f186f6b1631bd88` ([polygonscan][random_txn])
  - The number we retrieved was: `104690413392636078841031805720873342933848164944125794142980596233059755687857`

### 4. Determine whether we eliminate evens or odds.
  
  - Our random number was **ODD**, so we eliminate tokens starting at index 1 (the second row of the ledger), then 3, then 5, and so on.
  
## 5. Mark tokens for elimination.
  - For each asset, step in order through each row of its ledger.
    - If the row is `UNOWNED`, mark it for elimination.
    - If the row index is **ODD**, _and we haven't yet eliminated 256 tokens_, mark it for elimination.
    - Otherwise, this token makes it through!

6. Eliminate tokens, burn them on-chain, and we're done!

## Hashed Ledger

> Identifiers in the ledger take the form of either `<blokpax_user_id>_` for custodial entries or `_<wallet_address>` for wallet entries.

You can find the exact ledger we hashed [here][ledger_full].

**Expected Hash (hex-encoded):**
```
cc86a10a098e5088d42842ec9affbde3133fa47622433901b508c150d6e6ec10
```

To verify the hash, [download `ledger-full.json`][ledger_full] and then run the following in a Unix-y shell:

```bash
cat ledger-full.json | tr -d '\n' | shasum -a 256 | tr -d '-'
```

The hash you get should match exactly the one above.

---

# References

- Random number transaction: [Polygonscan][random_txn]

[random_txn]: https://polygonscan.com/tx/0xf0223f731e9edd4c11f9fdf94818e287b8f047a8b5c0fcc48f186f6b1631bd88
[ledger_full]: ledger-full.json
