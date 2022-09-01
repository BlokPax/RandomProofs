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
| | Randomness: [`29401357001243232101409340116266268484223155764119003170838324770726389200946`](https://etherscan.io/tx/0x26caed7782c874ba39f4132b1bae47ec8e894b37fd84a35d8b525b433252b77d)
| | Hash Source: [Hash Sources/Round 1.txt](./Hash%20Sources/Round%201.txt)
| | Hash: `b26c17ee660cea492109541895c5a451c387db52384911cf8a80471ece475af1`
| Ship 2 | Salty Bottom | | |
| Ship 3 | Scorcher | | |
| Ship 4 | Coconut Commander | | |
| Ship 5 | Skull Crusher | | |
| Ship 6 | White Pearl | | |
| Ship 7 | Gliding Ghost | | |
| Ship 8 | Treasure Raider | | |
| Ship 9 | Defiant | | |
| Ship 10 | Golden Barnacle | | |
