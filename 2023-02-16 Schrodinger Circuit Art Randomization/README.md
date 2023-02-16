## Schrödingers Circuits
### Token Artwork Randomization

|||
|---|---|
| **Sorted Token List** | [tokens-start2.csv](./tokens.start2.csv) |
| **VRF Consumer Contract** | [`0x18b9b62749Fcb227C493015244E6939d8F01d0f3`](https://etherscan.io/address/0x18b9b62749Fcb227C493015244E6939d8F01d0f3) |
| **Identity Hash** | `3c19e81ec24351c31cbb2a66a4fa8ecc3afd92a711284fd6806dde7e7d2adf6e` |
| **Random Request** | [`0x26b1147bc2ca44c56c0f97daee4e6d8a2e15473ec6d71d5bd16723ddd807de95`](https://etherscan.io/tx/0x26b1147bc2ca44c56c0f97daee4e6d8a2e15473ec6d71d5bd16723ddd807de95) |
| **Requested on** | Feb-16-2023 08:34:23 PM +UTC |
| **Response TX** | [`0xdf61caccb39dc5587e6ce61588f78414821f310f42300e76c13bcf16624b3833`](https://etherscan.io/tx/0xdf61caccb39dc5587e6ce61588f78414821f310f42300e76c13bcf16624b3833) |
| **Random Number** | `89759316628325728014703998593283529820683673270101829808126812363337545849889` |
| **Shuffled Token List** | [tokens.shuffled.csv](./tokens.shuffled.csv) |
| **Re-numbered Token List** | [tokens.final.csv](./tokens.final.csv) |

1. Create a sha256 hash of the artwork, paired with an internal, temporary, token ID. (This allows us to map the artwork to the metadata, and the image file).
2. Sort the list of hashes + [temporary] token ids, alphabetically, by the hash (using `sort` utility).
3. Create a hash of the sorted hash + token id map, [sorted token list](./tokens.start.csv).
4. Request a random number from chainlink VRF (using contract [`0x18b9b62749Fcb227C493015244E6939d8F01d0f3`](https://etherscan.io/address/0x18b9b62749Fcb227C493015244E6939d8F01d0f3))
5. Retrieve random number from above contract
6. Seed [Mersenne Twister](https://en.wikipedia.org/wiki/Mersenne_Twister) based shuffling algorithm using random value retrieved in #4, and shuffle the token list referenced in step 1 (using [shuffle](./scripts/shuffle) script). These will become the randomly sorted order of the artwork.
7. Using the [shuffled token list](./tokens.shuffled.csv), iterate through each art hash + [internal] token id, sequentially (starting at 0), and rename each image + metadata file to the current iteration. Thereby, distributing the artwork and metadata in the new shuffled order.

### Results

You can view the resulting art hash + new token id, here:

[tokens.final.csv](./tokens.final.csv)

# Original Request

Due to a [`out of gas`](https://etherscan.io/tx/0xdbf1286a429162b294137f217aa359f5bbbc3bf82ba3802635d69180adb2bba7) error on the response from Chainlink VRF, we had to request a second random number to seed the randomization.

This requires a new identity hash be generated to identify the random request.

We prepended our sorted token list with the original Identity Hash (`7744b68fe73477038f821c0171b825f3e9494db1d4471d27f3e055e8bee60572`) and original Transaction Hash (`0xc2cf4dd0bc61fd5b0d381077f5d9bb54c4ba4de2ec9c1dba84eeb5db07cd8a45`) for the first request, proving that this second request came after the first.

|||
|---|---|
| **Sorted Token List** | [tokens-start.csv](./tokens.start.csv) |
| **VRF Consumer Contract** | [`0x18b9b62749Fcb227C493015244E6939d8F01d0f3`](https://etherscan.io/address/0x18b9b62749Fcb227C493015244E6939d8F01d0f3) |
| **Identity Hash** | `7744b68fe73477038f821c0171b825f3e9494db1d4471d27f3e055e8bee60572` |
| **Random Request** | [`0xc2cf4dd0bc61fd5b0d381077f5d9bb54c4ba4de2ec9c1dba84eeb5db07cd8a45`](https://etherscan.io/tx/0xc2cf4dd0bc61fd5b0d381077f5d9bb54c4ba4de2ec9c1dba84eeb5db07cd8a45) |
| **Requested on** | Feb-16-2023 08:15:11 PM +UTC |
| **Response TX** | [`0xdbf1286a429162b294137f217aa359f5bbbc3bf82ba3802635d69180adb2bba7`](https://etherscan.io/tx/0xdbf1286a429162b294137f217aa359f5bbbc3bf82ba3802635d69180adb2bba7) |
| **Random Number** | `Not Received` |
