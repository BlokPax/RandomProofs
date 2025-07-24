## Bo Jackson Battle Arena - Signed Pack Giveaway - 07.24.2025

|                           |                                                                                                                                                                    |
| ------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **Entries**               | [entries.hashed.sorted.csv](./entries.hashed.sorted.csv)                                                                                                           |
| **VRF Consumer Contract** | [`0x18b9b62749Fcb227C493015244E6939d8F01d0f3`](https://etherscan.io/address/0x18b9b62749Fcb227C493015244E6939d8F01d0f3)                                            |
| **Identity Hash**         | `7b3a01c7eab5c404d191c5040a4411b05af9e1347b6c50c03a13cd86c0dc93fa`                                                                                                 |
| **Random Request**        | [`0xda2e840ea8d2c4741ee9291e7c027293bab8c9ebd6ba27f432fe0ff7c5c97a52`](https://etherscan.io/tx/0xda2e840ea8d2c4741ee9291e7c027293bab8c9ebd6ba27f432fe0ff7c5c97a52) |
| **Requested on**          |
| **Response TX**           | [`0x031360edc543035b3cfa3dff09eac0cfa7ba8d2e6c5178f76424e81293ccf02e`](https://etherscan.io/tx/0x031360edc543035b3cfa3dff09eac0cfa7ba8d2e6c5178f76424e81293ccf02e) |
| **Random Number**         | `69726698863455629211561017533049766905098233711380601145899765110811417779817`                                                                                    |
| **Shuffled Holder List**  | [entries.hashed.shuffled.csv](./entries.hashed.shuffled.csv)                                                                                                       |

To fairly and transparently select winners from our Mystery Giveaway, we used a cryptographically verifiable process grounded in SHA-256 hashing, on-chain randomness, and a Mersenne Twister shuffle. No dice rolls, no backroom deals—just math and math's best friend: more math.

## The Process

1. **Hashing Entries**  
   Every participant's entry was first normalized into the format:

   ```
   <email address>,<phone number>
   ```

   where:

   - Email addresses were fully lowercased.
   - Phone numbers were stripped of all non-numeric characters.

   Each entry was then SHA-256 hashed, resulting in anonymized strings that retained no personally identifiable information. These hash values were saved to [`entries.hashed.sorted.csv`](./entries.hashed.sorted.csv).

   > You can generate a hash for your entry using our [SHA256 Hash Generator](https://blokpax.github.io/RandomProofs/) at [https://blokpax.github.io/RandomProofs/](https://blokpax.github.io/RandomProofs/).

2. **Sorting & Identity Hash**  
   The list of hashed entries was sorted alphabetically to ensure consistent order and reproducibility. We then generated a single SHA-256 hash of the sorted list, known as the **identity hash**:

   ```
   7b3a01c7eab5c404d191c5040a4411b05af9e1347b6c50c03a13cd86c0dc93fa
   ```

3. **On-Chain Randomness Request**  
   This identity hash was submitted to our on-chain randomness contract at  
   [`0x18b9b62749Fcb227C493015244E6939d8F01d0f3`](https://etherscan.io/address/0x18b9b62749Fcb227C493015244E6939d8F01d0f3)  
   in [transaction 0xda2e84...c97a52](https://etherscan.io/tx/0xda2e840ea8d2c4741ee9291e7c027293bab8c9ebd6ba27f432fe0ff7c5c97a52).

4. **Obtaining the Random Number**  
   The resulting randomness was committed to the chain and is visible at:  
   [transaction 0x031360...f02e](https://etherscan.io/tx/0x031360edc543035b3cfa3dff09eac0cfa7ba8d2e6c5178f76424e81293ccf02e)  
   yielding the random seed:

   ```
   69726698863455629211561017533049766905098233711380601145899765110811417779817
   ```

5. **Shuffling Entries**  
   We used this random seed to initialize a [Mersenne Twister](https://en.wikipedia.org/wiki/Mersenne_Twister) pseudorandom number generator and shuffled the sorted entry list deterministically. The final shuffled result was saved in [`entries.hashed.shuffled.csv`](./entries.hashed.shuffled.csv).

6. **Selecting Winners**  
   From the top of the shuffled list, we assigned prizes to the first three unique hashes:

   - **Winner 1**: 1/1 Winner
   - **Winner 2**: #16 Winner
   - **Winner 3**: #34 Winner

---

This process ensures every entry was treated fairly, every transformation is verifiable, and the outcome can be independently audited at any point. Zero trust required. Just proof.

The following values represent the hashes for the 3 winners:

```
9546ed9d24c504c509e44f9d4843d13718010f2ce601f32d5d33ad396a732141
55efc341c0061be9aa91ce74053481a74928479b844586e881ca3385afad00f5
99fa5b44f628834cea37e3e2cc7059a1d00acfffd90e0c6da6f8d9e77f9d1dac

```
