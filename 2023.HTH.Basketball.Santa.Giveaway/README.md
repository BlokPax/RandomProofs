## Home Team Heroes - 2023 Basketball Drop
## Santa Token Giveaway

### Holder Randomization

|||
|---|---|
| **Sorted Holder List** | [holder-list.sorted.csv](./holder-list.sorted.csv) |
| **VRF Consumer Contract** | [`0x18b9b62749Fcb227C493015244E6939d8F01d0f3`](https://etherscan.io/address/0x18b9b62749Fcb227C493015244E6939d8F01d0f3) |
| **Identity Hash** | `045cb3a9388f779511f983625040a231fbd29d1503ec335b86dcf9ae7a808a75` |
| **Random Request** | [``](https://etherscan.io/tx/) |
| **Requested on** | |
| **Response TX** | [``](https://etherscan.io/tx/) |
| **Random Number** | `` |
| **Shuffled Holder List** | [holder-list.shuffled.csv](./holder-list.shuffled.csv) |

### Prize Randomization

|||
|---|---|
| **Sorted Prize List** | [prize-list.csv](./prize-list.sorted.csv) |
| **VRF Consumer Contract** | [`0x18b9b62749Fcb227C493015244E6939d8F01d0f3`](https://etherscan.io/address/0x18b9b62749Fcb227C493015244E6939d8F01d0f3) |
| **Identity Hash** | `` |
| **Random Request** | [``](https://etherscan.io/tx/) |
| **Requested on** | |
| **Response TX** | [``](https://etherscan.io/tx/) |
| **Random Number** | `` |
| **Shuffled Prize List** | [prize-list.shuffled.csv](./prize-list.shuffled.csv) |

#### The Process

**Step 1**

Shuffle the holder list

1. Prefix the transaction hash of the last transaction that interacted directly with the VRF Consumer Contract to the holder-list.sorted.csv file.
1. Create a sha256 hash of the [holder-list](./holder-list.sorted.csv).
2. Request a random number from chainlink VRF (using contract [`0x18b9b62749Fcb227C493015244E6939d8F01d0f3`](https://etherscan.io/address/0x18b9b62749Fcb227C493015244E6939d8F01d0f3))
3. Retrieve random number from above contract
4. Shuffle the holder list from step 1, by feeding the random number retrieved in step #3 to the [shuffle](./scripts/shuffle) script

**Step 2**

Shuffle the prize list

1. Prefix the transaction hash of the transaction that requested the random number for the holder list (Step 1.1 above) to the prize-list.sorted.csv.
1. Create a sha256 hash of the [prize-list](./prize-list.sorted.csv).
2. Request a random number from chainlink VRF (using contract [`0x18b9b62749Fcb227C493015244E6939d8F01d0f3`](https://etherscan.io/address/0x18b9b62749Fcb227C493015244E6939d8F01d0f3))
3. Retrieve random number from above contract
4. Shuffle the prize list from step 1, by feeding the random number retrieved in step #3 to the [shuffle](./scripts/shuffle) script

**Step 3**

Combine the shuffled holder list with the shuffle prize list. This combined file defines the winner of each prize (winner specified on line #1 wins prize specified on line #1, etc).

### Results

You can view the resulting combined shuffled holder + prize list here:

[holder-prize.final.csv](./holder-prize.final.csv)

### References

**shuffle script**

The shuffle script utilizes the random numbered retrieved from the Chainlink VRF as a seed into the [Mersenne Twister](https://en.wikipedia.org/wiki/Mersenne_Twister) algorithm. This
allows the resulting shuffled order to be re-created by using the same inputs (original sort order and sorting seed).

**ChainlinkVRF**

ChainlinkVRF is a blockchain powered random number generator. Blokpax uses the ChainlinkVRF as it's random number generator because it guarantees that we [Blokpax] have no prior knowledge of the random value and had no opportunity or capability of tampering with the result. You can read more about the ChainlinkVRF here: [https://docs.chain.link/vrf](https://docs.chain.link/vrf).
