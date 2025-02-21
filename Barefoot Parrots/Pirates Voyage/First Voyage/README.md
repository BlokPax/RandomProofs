### Ship Shuffle

|||
|---|---|
| **source** | [ship-seed-hash-source.txt](./ship-seed-hash-source.txt) |
| **hash** | `0xfaa8d0f3127fe22f68f09a0a852ea3c77679347019197f07815f3e6dd67efb8e` |
| **request** | [`0x7d7c9afa366194af3100eb43cb44842390030be659498366404e0c3f09082793`](https://etherscan.io/tx/0x7d7c9afa366194af3100eb43cb44842390030be659498366404e0c3f09082793) |
| **rand** | `43592704143011435364180225224607751629233572819604777517530508486652778690860a` |
| **shuffled** | [ships-shuffled.txt](./ships-shuffled.txt) |

### Pirate Shuffle

|||
|---|---|
| **source** | [pirate-seed-hash-source.txt](./pirate-seed-hash-source.txt) |
| **hash** | `0xc78a04c42d80d4cb32e623df83e34801e93b0d24d8f41f2aed381a29255be196` |
| **request** | [`0x2938c5cd91d32a6dfc12a16c9af673e6c1828a0830e0693274e6f4a30aecd339`](https://etherscan.io/tx/0x2938c5cd91d32a6dfc12a16c9af673e6c1828a0830e0693274e6f4a30aecd339) |
| **rand** | `48980245733362312010295633814357996883731576117188012338804232643504882592603` |
| **shuffled** | [ships-shuffled.txt](./ships-shuffled.txt) |

### Ship Assignments
|||
|---|---|
| **csv** | [pirate-assignments.csv](./pirate-assignments.csv) |
| **json** | [pirate-assignments.json](./pirate-assignments.json)

### Ship Results

**Reproduction Steps**

1. Hash the file specified as the hash source. This is your random value identifier.
2. Request randomness from the VRF
3. Execute the [`roll`](../scripts/roll) command: `roll <RANDOMNESS> <ODDS NUMERATOR> <ODDS DENOMINATOR>`
	```
	// example:
	roll 29401357001243232101409340116266268484223155764119003170838324770726389200946 1 10
	```
4. Done

| Ship Position | Ship | Result |
|---|---|---|
| Ship 1 | Reef Crusher | **SUNK** |
| | Randomness: [`29401357001243232101409340116266268484223155764119003170838324770726389200946`](https://etherscan.io/tx/0x26caed7782c874ba39f4132b1bae47ec8e894b37fd84a35d8b525b433252b77d) |
| | Hash Source: [Hash Sources/Round 1.txt](./Hash%20Sources/Round%201.txt) |
| | Hash: `b26c17ee660cea492109541895c5a451c387db52384911cf8a80471ece475af1` |
| Ship 2 | Salty Bottom | **SUNK** |
| | Randomness: [`93489813983995755603503254181681196939822248248818314025822544981779801577905`](https://etherscan.io/tx/0x6db2a47162c41da8d4a8089dc6b2f4ba3a3a661cc36c165c2ae5a47ed363cbd3) |
| | Hash Source: [Hash Sources/Round 2.txt](./Hash%20Sources/Round%202.txt) |
| | Hash: `09da68cc63b11f38ddb406d30098b7f853dc03ad57d715a333705c3569429931` |
| Ship 3 | Scorcher | **SUNK** |
| | Randomness: [`39917980828121727761911060749442396083804809394478101440406467716447895530513`](https://etherscan.io/tx/0x650520fe233a63bcedca3ebc6a3d58d5c46b3c03b5dd0a1c90d03fc8bc3eec26) |
| | Hash Source: [Hash Sources/Round 3.txt](./Hash%20Sources/Round%203.txt) |
| | Hash: `901db66d2f77317351a472787233faa46fce817f01cb99198643a346012ab1d1` |
| Ship 4 | Coconut Commander | **SUNK** |
| | Randomness: [`15389461003815869532516672427927789011665238293393477938936410757844262247144`](https://etherscan.io/tx/0x2ec0db5d30fe25a8c4dff300ab5e3ab75681bb6802d3067205e86b4b4ecb6d47) |
| | Hash Source: [Hash Sources/Round 4.txt](./Hash%20Sources/Round%204.txt) |
| | Hash: `437bcd131e45c4cd6d6e218c58444c633cb610698bd1f91752666a3ecc271b21` |
| Ship 5 | Skull Crusher | **SUNK** |
| | Randomness: [`105566928581040549170120376357327015963808090290186774611704897982415943520361`](https://etherscan.io/tx/0x3f7fd2b679e689e677ba402a17ff9fbd7ce218f1ab153bb045a20150673876d3) |
| | Hash Source: [Hash Sources/Round 5.txt](./Hash%20Sources/Round%205.txt) |
| | Hash: `2af559d51d1b8ffb8a3aad43e55c417251e375179ec049d3dd2d11359986033e` |
| Ship 6 | White Pearl | **SUNK** |
| | Randomness: [`59061894766995623207156938327320357168244114006788400456757254206114538101194`](https://etherscan.io/tx/0xb45f583ce690946353a20802c7f0fbc97a9f0326273481199463acd206a3492b) |
| | Hash Source: [Hash Sources/Round 6.txt](./Hash%20Sources/Round%206.txt) |
| | Hash: `bfc5d4359acb0c115aa58850657737f4dc925014b75bd78f92f5eebb674b780f` |
| Ship 7 | Gliding Ghost | **SUNK** |
| | Randomness: [`14017048478927392338992969977732053420128684287025719443876130390302378881426`](https://etherscan.io/tx/0xfb87ff33fa881ae74f126d59f13fd497de28964abf25838538c90ad1e7b0fd99) |
| | Hash Source: [Hash Sources/Round 7.txt](./Hash%20Sources/Round%207.txt) |
| | Hash: `b5d6d453f9f854d3f65493fce2b2e7a973bb62362a05c186e70d068ac4a9b031` |
| Ship 8 | Treasure Raider | **SUNK** |
| | Randomness: [`113046479939977125283096325716752124348376815035794501443781976102383414940211`](https://etherscan.io/tx/0x1443f73e32efbb6427fa68009293191c68d1d5b488c50e1eb69f542c253e7b42) |
| | Hash Source: [Hash Sources/Round 8.txt](./Hash%20Sources/Round%208.txt) |
| | Hash: `9897e8bc93754d8d62c02a9c14ffce99a415f9a1a7a23970a4e471ba4126f3f5` |
| Ship 9 | Defiant | **SUNK** |
| | Randomness: [`12263501614570569396597011518961067224845681537458528921900664255066262936307`](https://etherscan.io/tx/0x645e580d3c6b3e798b443b001ccf563786e0913c82c4675190ee9cda43c325cb) |
| | Hash Source: [Hash Sources/Round 9.txt](./Hash%20Sources/Round%209.txt) |
| | Hash: `bc1e7eed244fc893b33da0e97f6b29d6adbf5b079afa75c0de7e9de71676d253` |
| Ship 10 | Golden Barnacle | **VICTOR** |
