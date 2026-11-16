## Bo Sliding Super Auto - Random Proof - 11.16.2026

|                           |                                                                                                                                                                    |
| ------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **Entries**               | [entries-sorted.txt](./entries-sorted.txt) (196 entries, numbered 1 to 196)                                                                                        |
| **VRF Consumer Contract** | [`0x18b9b62749Fcb227C493015244E6939d8F01d0f3`](https://etherscan.io/address/0x18b9b62749Fcb227C493015244E6939d8F01d0f3)                                            |
| **Identity Hash**         | `4638a8631c0239f6346155c533c6f7d2ddb5b9f17576950b484452f82b0ad49c` ([hash.txt](./hash.txt))                                                                        |
| **Random Request**        | [`0x61458dfda5b946f37428b84c7d31088c61206317623a6bf43404ef5141b0b7c2`](https://etherscan.io/tx/0x61458dfda5b946f37428b84c7d31088c61206317623a6bf43404ef5141b0b7c2) |
| **Requested on**          | Nov-16-2026 04:34:11 PM UTC (block 26428814)                                                                                                                       |
| **Response TX**           | [`0x5950b27aa58194f92e23706a163a108af0fecae2af9561385d2d49ed02a595be`](https://etherscan.io/tx/0x5950b27aa58194f92e23706a163a108af0fecae2af9561385d2d49ed02a595be) |
| **Responded on**          | Nov-16-2026 04:34:59 PM UTC (block 26428818)                                                                                                                       |
| **VRF Request ID**        | `78380353245184789696030688022925912655741771669465281909803898767204387933268`                                                                                    |
| **Random Number**         | `87423417313758109743917554343696267424316294766161878294155329313926688761580`                                                                                    |
| **Shuffled List**         | [entries-shuffled.txt](./entries-shuffled.txt)                                                                                                                     |
| **Raw VRF Output**        | [results.txt](./results.txt)                                                                                                                                       |

## The Short Version

We put 196 numbered entries in a list. We locked that list so it could not be changed. We then asked a public, tamper-proof service for a random number, and used that number to shuffle the list.

We could not pick the random number. We could not change the list after asking for it. Anyone can re-run every step and get the exact same result.

## Why You Can Trust It

Think of it like a lottery drawing on live TV.

- **The tickets are sealed first.** Before the draw, we publish a "fingerprint" of the entry list. If even one entry were added, removed, or changed later, the fingerprint would no longer match.
- **Someone else draws the number.** The random number comes from [Chainlink VRF](https://docs.chain.link/vrf), an independent service that runs on the Ethereum blockchain. It comes with a mathematical proof that nobody, including us, picked or tampered with it.
- **The tape is public forever.** Both the request and the answer are recorded on Ethereum. They are timestamped and cannot be edited or deleted.
- **The shuffle has no wiggle room.** The same list plus the same random number always gives the same shuffled order. There is nothing for us to choose.

## The Process

1. **Build the entry list**  
   Each entry is a number from 1 to 196, one per line, in order. This is saved as [`entries-sorted.txt`](./entries-sorted.txt).

   Keeping the list sorted matters. It gives everyone the same starting point, so the shuffle can be repeated exactly.

2. **Fingerprint the list (the Identity Hash)**  
   We ran the list through SHA-256. SHA-256 turns any file into a short string of letters and numbers, like a fingerprint. The same file always gives the same fingerprint. A different file gives a completely different one.

   The fingerprint for this list is:

   ```
   4638a8631c0239f6346155c533c6f7d2ddb5b9f17576950b484452f82b0ad49c
   ```

3. **Ask the blockchain for a random number**  
   We sent that fingerprint to our randomness contract at
   [`0x18b9b62749Fcb227C493015244E6939d8F01d0f3`](https://etherscan.io/address/0x18b9b62749Fcb227C493015244E6939d8F01d0f3) in [transaction 0x61458d...b0b7c2](https://etherscan.io/tx/0x61458dfda5b946f37428b84c7d31088c61206317623a6bf43404ef5141b0b7c2).

   This is the "sealing" step. The fingerprint is now on the blockchain with a timestamp, **before** any random number exists. That proves the list was final before the draw.

4. **Receive the random number**  
   About 48 seconds (4 blocks) later, Chainlink VRF answered in [transaction 0x5950b2...a595be](https://etherscan.io/tx/0x5950b27aa58194f92e23706a163a108af0fecae2af9561385d2d49ed02a595be). The random number it delivered was:

   ```
   87423417313758109743917554343696267424316294766161878294155329313926688761580
   ```

   The answer is tied to our request by the request ID and by the same fingerprint, so it cannot be swapped for a different draw.

5. **Shuffle the list**  
   We used the random number as the starting point ("seed") for a [Mersenne Twister](https://en.wikipedia.org/wiki/Mersenne_Twister) shuffle. A seeded shuffle is like a recipe: the same ingredients always produce the same dish.

   The result is saved as [`entries-shuffled.txt`](./entries-shuffled.txt).

6. **Read the results**  
   The shuffled list is the final order. Line 1 is the first position, line 2 is the second, and so on through line 196.

   The first ten positions are:

   | Position | Entry |
   | -------- | ----- |
   | 1        | 83    |
   | 2        | 54    |
   | 3        | 187   |
   | 4        | 69    |
   | 5        | 128   |
   | 6        | 28    |
   | 7        | 24    |
   | 8        | 141   |
   | 9        | 166   |
   | 10       | 150   |

   The full order is in [`entries-shuffled.txt`](./entries-shuffled.txt).

## Check It Yourself

You do not have to take our word for any of this. Each step can be repeated.

1. **Check the fingerprint.** Run this from this folder. The output should match the Identity Hash above.

   ```
   shasum -a 256 entries-sorted.txt
   ```

   No command line? Paste the file's contents into our [SHA-256 Hash Generator](https://blokpax.github.io/RandomProofs/) instead. The file ends with a line break after `196`, so the pasted text must too, or the fingerprint will differ.

2. **Check the request.** Open the [request transaction](https://etherscan.io/tx/0x61458dfda5b946f37428b84c7d31088c61206317623a6bf43404ef5141b0b7c2) on Etherscan. The input data ends with the Identity Hash.

3. **Check the random number.** Open the [response transaction](https://etherscan.io/tx/0x5950b27aa58194f92e23706a163a108af0fecae2af9561385d2d49ed02a595be) and look at the Logs tab. The event from our contract contains the Identity Hash and the random number. Etherscan shows the number in hex as `c147e694249ec90140fd443b02426c963dedbd66d005ed70eb8a7abd1f2b66ec`, which is the same value as the Random Number above.

4. **Check the shuffle.** Run our [shuffle script](../shuffle) from the root of this repository (requires PHP with the GMP extension, and `composer install`):

   ```
   ./shuffle "2026.11.16-bo-sliding-super-auto/entries-sorted.txt" 87423417313758109743917554343696267424316294766161878294155329313926688761580
   ```

   The output should match [`entries-shuffled.txt`](./entries-shuffled.txt) line for line.

### Technical Notes

- The random number is larger than PHP can use directly as a seed. The script reduces it first: `random number mod 9223372036854775807` (PHP's largest integer). For this draw, the seed is `8474150622801116220`.
- That seed is passed to `mt_srand()`, and the list is shuffled with PHP's built-in `shuffle()`.
- The random number was delivered by the Chainlink VRF Coordinator at [`0x271682DEB8C4E0901D1a1550aD2e64D568E69909`](https://etherscan.io/address/0x271682DEB8C4E0901D1a1550aD2e64D568E69909), which verifies the proof on-chain before passing the number to our contract.

---

This process ensures every entry was treated fairly, every step is verifiable, and the outcome can be independently audited at any point. Zero trust required. Just proof.
