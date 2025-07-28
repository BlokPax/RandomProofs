## Bo Jackson Battle Arena - Signed BoJax Brawler Promo Cards

|                           |                                                                                                                                                                    |
| ------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **Entries**               | [entries.sorted.csv](./entries.sorted.csv)                                                                                                                         |
| **VRF Consumer Contract** | [`0x18b9b62749Fcb227C493015244E6939d8F01d0f3`](https://etherscan.io/address/0x18b9b62749Fcb227C493015244E6939d8F01d0f3)                                            |
| **Identity Hash**         | `362b78691bae1704fb25de5ef625d558d847cfc624ae8f81335f53e59cbaa016`                                                                                                 |
| **Random Request**        | [`0x8f940168bc0e5d6f34b26fc66888ef6167714a682367ffc9036b38675c1ba74f`](https://etherscan.io/tx/0x8f940168bc0e5d6f34b26fc66888ef6167714a682367ffc9036b38675c1ba74f) |
| **Requested on**          | Jul-28-2025 08:22:47 PM UTC                                                                                                                                        |
| **Response TX**           | [`0xc9da1fb528826879e081c8ea393149c23e41013355c9befae32fc97ea109ab1f`](https://etherscan.io/tx/0xc9da1fb528826879e081c8ea393149c23e41013355c9befae32fc97ea109ab1f) |
| **Random Number**         | `64172532396436495387997170717147370890334131811412260826210246081559668042692`                                                                                    |
| **Shuffled Holder List**  | [entries.shuffled.csv](./entries.shuffled.csv)                                                                                                                     |

To fairly and transparently select winners from our Mystery Giveaway, we used a cryptographically verifiable process grounded in SHA-256 hashing, on-chain randomness, and a Mersenne Twister shuffle. No dice rolls, no backroom deals—just math and math's best friend: more math.

## The Process

1. **Hashing Entries**  
   Star City provided all entries in the format of "Customer #x,# Promo Cards". Since this data is already anonymized, we don't have to anonymize it any further. We can simply use the Customer ID that SCG Provided. Customer IDs are placed 1 per line, for each promo card they get as part of the promotion. So, if Customer 999 received 10 promo cards, there would be 10 lines for "Customer 999".

2. **Sorting & Identity Hash**  
   Once all customers are recorded according to the amount of promo cards they receive, we sort the file so we have a consistent and reproducible starting point for randomization. We then compute the SHA-256 hash of the sorted entries to create a unique identity hash for this giveaway. This identity hash is:

   ```
   362b78691bae1704fb25de5ef625d558d847cfc624ae8f81335f53e59cbaa016
   ```

3. **On-Chain Randomness Request**  
   This identity hash was submitted to our on-chain randomness contract at  
   [`0x18b9b62749Fcb227C493015244E6939d8F01d0f3`](https://etherscan.io/address/0x18b9b62749Fcb227C493015244E6939d8F01d0f3) in [transaction 0x8f9401...ba74f](https://etherscan.io/tx/0x8f940168bc0e5d6f34b26fc66888ef6167714a682367ffc9036b38675c1ba74f).

4. **Obtaining the Random Number**  
   The resulting randomness was committed to the chain and is visible at:  
   [transaction 0xc9da1fb...09ab1f](https://etherscan.io/tx/0xc9da1fb528826879e081c8ea393149c23e41013355c9befae32fc97ea109ab1f) yielding the random seed:

   ```
   64172532396436495387997170717147370890334131811412260826210246081559668042692
   ```

5. **Shuffling Entries**  
   We used this random seed to initialize a [Mersenne Twister](https://en.wikipedia.org/wiki/Mersenne_Twister) pseudorandom number generator and shuffled the sorted entry list deterministically. The final shuffled result was saved in [`entries.shuffled.csv`](./entries.shuffled.csv).

6. **Selecting Winners**  
   From the top of the shuffled list, we assigned prizes to the first ten [shuffled] customer entries.

   There are two variants of the promo card. The first five winners will receive Variant 1, last five will receive Variant 2.

   - Variant 1: Inspired Ink BoJax Brawler - 180 Power
   - Variant 2: Inspired Ink Bojax Brawler - 150 Power

   The winners selected are:

   - Customer 84 - Variant 1 (BoJax Brawler - 180 Power)
   - Customer 177 - Variant 1 (BoJax Brawler - 180 Power)
   - Customer 117 - Variant 1 (BoJax Brawler - 180 Power)
   - Customer 150 - Variant 1 (BoJax Brawler - 180 Power)
   - Customer 108 - Variant 1 (BoJax Brawler - 180 Power)
   - Customer 152 - Variant 2 (BoJax Brawler - 150 Power)
   - Customer 150 - Variant 2 (BoJax Brawler - 150 Power)
   - Customer 207 - Variant 2 (BoJax Brawler - 150 Power)
   - Customer 17 - Variant 2 (BoJax Brawler - 150 Power)
   - Customer 108 - Variant 2 (BoJax Brawler - 150 Power)

---

This process ensures every entry was treated fairly, every transformation is verifiable, and the outcome can be independently audited at any point. Zero trust required. Just proof.
