# Elimination Proof

|||
|---|---|
| **Drop** | Drop 3 |
| **Round** | 11 |
| **Started** | November 19, 2021 5:00 PM EST |
| **Completed** | November 19, 2021 5:17 PM EST |
| **Tokens remaining before round** | 60 |
| **➡️  Per Asset** | 2 |
| **Tokens remaining after round** | 30 |
| **➡️  Per Asset** | 1 |

## Assets

- [Williams/Ruth/Robinson &#039;18 BGS 9.5](asset-263.md)
- [A. Iverson &#039;98 PSA 9](asset-264.md)
- [M. Mantle &#039;58 PSA 6](asset-265.md)
- [L. Jackson &#039;18 PSA 10](asset-266.md)
- [L. James &#039;03 PSA 10](asset-267.md)
- [S. O&#039;Neal &#039;92 PSA 10](asset-268.md)
- [M. Jordan &#039;86 PSA 10 FRAX 1 of 6](asset-269.md)
- [P. Manning &#039;98 BGS 9.5](asset-270.md)
- [J. Herbert &#039;20 PSA 10](asset-271.md)
- [J. Soto &#039;18 PSA 10](asset-272.md)
- [B. Roethlisberger &#039;04 PSA 7](asset-273.md)
- [K. Murray &#039;19 PSA 10](asset-274.md)
- [P. Mahomes II &#039;17 PSA 10](asset-275.md)
- [L. James &#039;12 PSA 10](asset-276.md)
- [K. Bryant &#039;12 BGS 9.5](asset-277.md)
- [W. McKennie &#039;18 PSA 8](asset-278.md)
- [W. Gretzky &#039;79 PSA 1.5](asset-279.md)
- [T. Brady &#039;00 PSA 10](asset-280.md)
- [L. Dončić &#039;18 BGS 8.5](asset-281.md)
- [A. Ovechkin &#039;05 PSA 10](asset-282.md)
- [D. Jeter &#039;96 SGC 10](asset-283.md)
- [B. Mayfield &#039;18 BGS 9.5](asset-284.md)
- [T. Cobb &#039;09-11 PSA 4](asset-285.md)
- [L. Bird &#039;86 PSA 9](asset-286.md)
- [T. Brady &#039;00 BGS 9](asset-287.md)
- [J. Robinson &#039;54 PSA 5](asset-288.md)
- [K. Bryant &#039;96 PSA 10 FRAX 1 of 8](asset-289.md)
- [V. Guerrero Jr. &#039;19 BGS 9.5](asset-290.md)
- [K. Bryant &#039;96 BGS 9](asset-291.md)
- [Blastoise &#039;99 BGS 8](asset-292.md)

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
    "salt": "Y6T1X4hZqZWme0ygG6DF0Q42yFmaXB9JqZe5evU41HmpP2ceASJu7EA21uzikCVE",

    // The collection_id is our internal ID for the drop. It will not change for
    // other eliminations in this drop.
    "collection_id": 8,

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
      c08a5eeb9ccd4add830f3452a20a21801933bce5765f8762cf6df93af99656f0
      ```

### 3. We send our hash up to the on-chain random oracle to get our random number.
  - The transaction hash to retrieve this random number was: `0x54773092d7bb5ea2db436a9674a6df822472edb7885dec94a7b0e2a7c7347574` ([polygonscan][random_txn])
  - The number we retrieved was: `36181163787568680403423994674506019926004269853430145358504940952577008403120`

### 4. Determine whether we eliminate evens or odds.
  
  - Our random number was **ODD**, so we eliminate tokens starting at index 1 (the second row of the ledger), then 3, then 5, and so on.
  
## 5. Mark tokens for elimination.
  - For each asset, step in order through each row of its ledger.
    - If the row is `UNOWNED`, mark it for elimination.
    - If the row index is **ODD**, _and we haven't yet eliminated 1 tokens_, mark it for elimination.
    - Otherwise, this token makes it through!

6. Eliminate tokens, burn them on-chain, and we're done!

## Hashed Ledger

> Identifiers in the ledger take the form of either `<blokpax_user_id>_` for custodial entries or `_<wallet_address>` for wallet entries.

You can find the exact ledger we hashed [here][ledger_full].

**Expected Hash (hex-encoded):**
```
c08a5eeb9ccd4add830f3452a20a21801933bce5765f8762cf6df93af99656f0
```

To verify the hash, [download `ledger-full.json`][ledger_full] and then run the following in a Unix-y shell:

```bash
cat ledger-full.json | tr -d '\n' | shasum -a 256 | tr -d '-'
```

The hash you get should match exactly the one above.

---

# References

- Random number transaction: [Polygonscan][random_txn]

[random_txn]: https://polygonscan.com/tx/0x54773092d7bb5ea2db436a9674a6df822472edb7885dec94a7b0e2a7c7347574
[ledger_full]: ledger-full.json