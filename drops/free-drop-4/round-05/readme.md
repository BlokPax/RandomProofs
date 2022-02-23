# Elimination Proof

|||
|---|---|
| **Drop** | Free Drop 4 |
| **Round** | 5 |
| **Started** | February 2, 2022 5:00 PM EST |
| **Completed** | February 2, 2022 5:11 PM EST |
| **Tokens remaining before round** | 3,840 |
| **&nbsp;&nbsp;&nbsp;&nbsp;Per Asset** | 128 |
| **Tokens remaining after round** | 1,920 |
| **&nbsp;&nbsp;&nbsp;&nbsp;Per Asset** | 64 |

## Assets

- [J. Kelenic &#039;18 PSA 10](asset-795.md)
- [R. Hachimura &#039;19 BGS 9.5](asset-796.md)
- [T. Brady &#039;20 PSA 9](asset-797.md)
- [G. Lux &#039;16 PSA 9](asset-798.md)
- [Charizard &#039;99 PSA 9](asset-799.md)
- [B. Larkin &#039;87 PSA 10](asset-800.md)
- [M. Mantle &#039;55 PSA 4](asset-801.md)
- [L. James &#039;03 PSA 10](asset-802.md)
- [L. James &#039;03 PSA 10](asset-803.md)
- [Z. Williamson &#039;19 PSA 10](asset-804.md)
- [Blastoise &#039;99 PSA 3](asset-805.md)
- [D. Robinson &#039;92 PSA 10](asset-806.md)
- [I. Suzuki &#039;01 PSA 9](asset-807.md)
- [L. James &#039;03 PSA 10](asset-808.md)
- [H. Olajuwon &#039;92 PSA 10](asset-809.md)
- [A. Davis &#039;12 PSA 10](asset-810.md)
- [Venusaur &#039;99 PSA 3](asset-811.md)
- [F. Tatís Jr. &#039;19 PSA 10](asset-812.md)
- [T. Woods &#039;01 PSA 10](asset-813.md)
- [J. Herbert &#039;20 PSA 9](asset-814.md)
- [K. Bryant &#039;96 PSA 10](asset-815.md)
- [K. Bryant &#039;96 BGS 9.5](asset-816.md)
- [I. Thomas &#039;19 PSA 9](asset-817.md)
- [L. James &#039;03 PSA 10](asset-818.md)
- [C. VMax &#039;20 BGS 10](asset-819.md)
- [Hero Geek #3](asset-842.md)
- [Hero Geek #2](asset-843.md)
- [Hero Geek #5](asset-844.md)
- [Hero Geek #1](asset-845.md)
- [Hero Geek #4](asset-846.md)

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
    "salt": "ArUwjuV8yuHApW8UwixrnNUB8YJJFTGTkUfxcguNeUSRZubOcngcn1PgV88dF1k1",

    // The collection_id is our internal ID for the drop. It will not change for
    // other eliminations in this drop.
    "collection_id": 12,

    // The round is what round of eliminations this is.
    "round": 5,

    "ledger": {
      "<asset_id1>": ["<entry1>", "<entry2>", ...],
      "<asset_id2>": ["<entry1>", "<entry2>", ...]
    }
  }
  ```

  - We minify the object (which is reproduced [here][ledger_full]), `sha256` the result and encode the result to hex.
    - Thus, our calculated hash is:
      ```plain
      b3c1888d2d499a00c35168d88d7859ca377373b205f152ee65164e5e95c37ee0
      ```

### 3. We send our hash up to the on-chain random oracle to get our random number.
  - The transaction hash to retrieve this random number was: `0xb7594bd991cc32d12bfa05de1a88f96c14cdd8c1929f2197eb88c3e1934b4676` ([polygonscan][random_txn])
  - The number we retrieved was: `15107572923601941251805638849106085629300277570298767641065804752778486817215`

### 4. Determine whether we eliminate evens or odds.
  
  - Our random number was **ODD**, so we eliminate tokens starting at index 1 (the second row of the ledger), then 3, then 5, and so on.
  
## 5. Mark tokens for elimination.
  - For each asset, step in order through each row of its ledger.
    - If the row is `UNOWNED`, mark it for elimination.
    - If the row index is **ODD**, _and we haven't yet eliminated 64 tokens_, mark it for elimination.
    - Otherwise, this token makes it through!

6. Eliminate tokens, burn them on-chain, and we're done!

## Hashed Ledger

> Identifiers in the ledger take the form of either `<blokpax_user_id>_` for custodial entries or `_<wallet_address>` for wallet entries.

You can find the exact ledger we hashed [here][ledger_full].

**Expected Hash (hex-encoded):**
```
b3c1888d2d499a00c35168d88d7859ca377373b205f152ee65164e5e95c37ee0
```

To verify the hash, [download `ledger-full.json`][ledger_full] and then run the following in a Unix-y shell:

```bash
cat ledger-full.json | tr -d '\n' | shasum -a 256 | tr -d '-'
```

The hash you get should match exactly the one above.

---

# References

- Random number transaction: [Polygonscan][random_txn]

[random_txn]: https://polygonscan.com/tx/0xb7594bd991cc32d12bfa05de1a88f96c14cdd8c1929f2197eb88c3e1934b4676
[ledger_full]: ledger-full.json
