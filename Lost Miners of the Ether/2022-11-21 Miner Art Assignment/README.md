## Lost Miners of the Ether
### Claim Pass Miner ID Token Assignment

|||
|---|---|
| **Sorted Token List** | [token-list.csv](./token-list.csv) |
| **VRF Consumer Contract** | [`0x18b9b62749Fcb227C493015244E6939d8F01d0f3`](https://etherscan.io/address/0x18b9b62749Fcb227C493015244E6939d8F01d0f3) |
| **Identity Hash** | `c64d66b9b194ef1d92aff1ba852ad392655e4e0434bb0fced15f961c760f2d19` |
| **Random Request** | [`0xe9618d2031ff018198db7ca0049601866ff8b3e9f5c59b3c4e3e505dab730a94`](https://etherscan.io/tx/0xe9618d2031ff018198db7ca0049601866ff8b3e9f5c59b3c4e3e505dab730a94) |
| **Requested on** | Nov-22-2022 03:46:59 AM +UTC |
| **Response TX** | [`0xa570bb72006aefc484d5e80dc67836c1ccc4f2f302da2a2a8791291e5e5773e4`](https://etherscan.io/tx/0xa570bb72006aefc484d5e80dc67836c1ccc4f2f302da2a2a8791291e5e5773e4) |
| **Random Number** | `27512205250187281851041293002907015496201594821208882660234264546083220778652` |
| **Shuffled Token List** | [token-list.shuffled.csv](./token-list.shuffled.csv) |
| **Re-numbered Token List** | [token-list.final.csv](./token-list.final.csv) |

### The Assignment Process

In most randomizations, the items that are being randomized are already known and are easily verified by a single identifier.

This allows us to establish a sort order that is easily re-creatable and straight forward to explain.

In the case of the Lost Miners, and randomizing the art, no one can know the art prior to reveal. But, we have to be sure that post-reveal, anyone can verify
that the assignment was indeed executed in a truly random, fair, and transparent way.

To achieve this, we will utilize the sha256 hash of the artwork contents itself. This hash is paired with a random, yet completely insignificant integer identifier, just simply so we can have a human parseable way to verify everything is accurate throughout the process.

This way, post reveal, anyone can take the sha256 of their miner art, verify where it landed in the randomization, and verify that the miner art they received was distributed equitably.

#### The Steps

1. Create a sha256 hash of the miner artwork, paired with an internal, temporary, token ID. (This allows us to map the artwork to the metadata, and the image file).
**Note**: We prepend _Attempt #2 - 2022-11-21_ to the sorted token list, to generate a _new_ identity hash, so we can retry the request. As, our VRF implementation does not allow _duplicate_ requests for any given identity hash. This guarantees that we are operating with complete transparency. Details on the first transaction are included below.
**Note 2**: We will _remove_ "_Attempt #2 - 2022-11-21_" from the token list prior to executing the sort (this way, the "Attempt #2" identifer is not included in the sorting algorithm.)
2. Sort the list of miner hashes + token ids, alphabetically, by the hash (using `sort` utility).
3. Create a hash of the sorted miner hash + token id map, [sorted token list](./token-list.sorted.csv).
4. Request a random number from chainlink VRF (using contract [`0x18b9b62749Fcb227C493015244E6939d8F01d0f3`](https://etherscan.io/address/0x18b9b62749Fcb227C493015244E6939d8F01d0f3))
5. Retrieve random number from above contract
6. Seed [Mersenne Twister](https://en.wikipedia.org/wiki/Mersenne_Twister) based shuffling algorithm using random value retrieved in #4, and shuffle the token list referenced in step 1 (using [shuffle](./scripts/shuffle) script). These will become the randomly sorted order of the Lost Miners artwork.
7. Using the [shuffled token list](./token-list.shuffled.csv), iterate through each art hash + [internal] token id, sequentially (starting at 0), and rename each image + metadata file to the current iteration. Thereby, distributing the miner artwork and metadata in the new shuffled order.

### Results

You can view the resulting art hash + new token id, here:

[token-list.final.csv](./token-list.final.csv)

#### Original Request

|||
|---|---|
| **Sorted Token List** | [token-list.csv](./token-list.csv) |
| **VRF Consumer Contract** | [`0x18b9b62749Fcb227C493015244E6939d8F01d0f3`](https://etherscan.io/address/0x18b9b62749Fcb227C493015244E6939d8F01d0f3) |
| **Identity Hash** | `b83496479ad79543e97dd48535a264cfbc1b5df13b68716717aa8a7c98451b16` |
| **Random Request** | [`0x40d02beca89e5c87c5f8c44af5b6e7133ba584093741dc040aa043a54b17e7c2`](https://etherscan.io/tx/0x40d02beca89e5c87c5f8c44af5b6e7133ba584093741dc040aa043a54b17e7c2) |
| **Requested on** | Nov-22-2022 03:32:11 AM +UTC |
| **Response TX** | [`0x403fc4cad0c97faaed4228c2a9a4f9d471ed48115e55731213fdccc205bbb12b`](https://etherscan.io/tx/0x403fc4cad0c97faaed4228c2a9a4f9d471ed48115e55731213fdccc205bbb12b) |
| **Random Number** | **FAILED** _(out of gas)_ |
