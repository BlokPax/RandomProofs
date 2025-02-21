## Lost Miners of the Ether
### Claim Pass Miner ID Token Assignment

|||
|---|---|
| **Sorted Token IDs** | [sorted-token-ids.csv](./sorted-token-ids) |
| **VRF Consumer Contract** | [`0x18b9b62749Fcb227C493015244E6939d8F01d0f3`](https://etherscan.io/address/0x18b9b62749Fcb227C493015244E6939d8F01d0f3) |
| **Identity Hash** | `0xa658f34417004048e470697bf202006272fd1e2f99bf3b9051a56fbef15a586c` |
| **Random Request** | [`0xeddb737119da4519c728734ef2a458084d6034de7f737cc0ea38324fc233bf01`](https://etherscan.io/tx/0xeddb737119da4519c728734ef2a458084d6034de7f737cc0ea38324fc233bf01) |
| **Requested on** | Oct-27-2022 06:28:47 PM +UTC |
| **Response TX** | [`0x93056a12cadd88a381bfc69cabacde859210ba1cdaad64b8b8b9990049e7a1d3`](https://etherscan.io/tx/0x93056a12cadd88a381bfc69cabacde859210ba1cdaad64b8b8b9990049e7a1d3) |
| **Random Numbers** | 1. `28809301718383836162468199079047574739093099642634210059213475222909752644512` |
| | 2. `36115605100643441482820141935674441935448150371601616345660517384293457622291` |
| **Shuffled Claim Passes** | [shuffled-claim-passes.csv](./shuffled-claim-passes.csv) |
| **Shuffled Miners** | [shuffled-miners.csv](./shuffled-miners.csv) |
| **Token Mapping** | [token-mapping-results.csv](./token-mapping-results.csv) |

### The Assignment Process

1. Create a hash of the [sorted token IDs](./sorted-token-ids.csv) (using [hashEntries](./scripts/hashEntries) script)
3. Request two random numbers from chainlink VRF (using contract [`0x18b9b62749Fcb227C493015244E6939d8F01d0f3`](https://etherscan.io/address/0x18b9b62749Fcb227C493015244E6939d8F01d0f3))
4. Retrieve random numbers from above contract
5. Seed [Mersenne Twister](https://en.wikipedia.org/wiki/Mersenne_Twister) based shuffling algorithm using _first_ random number, and shuffle the token IDs referenced in step 1 (using [shuffle](./scripts/shuffle) script). These will become the randomly ordered Lost Miner Claim Pass IDs.
6. Re-seed shuffling algorithm using _second_ random number, and shuffle the token IDs referenced in step 1 (using [shuffle](./scripts/shuffle) script). These will become the randomly ordered Lost Miners of the Ether Token IDs.
7. Pair the files created from steps 5 and 6 such that the claim pass ID on line 1 (of the file generated in step 5) is assigned the Lost Miner token ID on line 1 (of the file generated in step 6). Then line 2 matches to line 2, and so on until we assign all 10,000 token ids.

### Results

You can view the token mapping here:

[token-mapping-results.csv](./token-mapping-results.csv)
