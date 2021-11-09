# Giveaway Info

| Edition | # Entries | # Winners | Winning Entry / Wallet | Proof Link |
| ------- | --------- | --------- | ---------------------- | ---------- |
| Black   | 110       | 1         |  92	0xcbd14770ce571580e9e82b7188bf8b1e78bacd05 | [mamba-black/README.md](./mamba-black) |
| Amethyst | 109      | 1         |  12 0x205b9c652c418ae2979de938b6689da7c1b97db1 | [mamba-amethyst/README.md](./mamba-amethyst) |
| Ruby    | 108       | 1         | 31 0x2c815fdc7a76c2e508bd0359b5b7241c2f69cbff | [mamba-ruby/README.md](./mamba-ruby) |
| Gold    | 107       | 10        |                        | [mamba-gold/README.md](./mamba-gold) |
| Moonlight |     | 20        |                        | [mamba-moonlight/README.md](./mamba-moonlight) | 
| Sunlight |       | 40		| 			| [mamba-sunlight/README.md](./mamba-sunlight) |
 
# Reproduction Steps

1. Randomize the entries ([raw-entries.csv](raw-entries.csv)).

> Starting with the sorted entry list, where each line = 1 entry, we shuffled the entries, placing the now-randomized wallet entries in `mamba-TIER/entries.shuffled.csv`.

2. Generate a hash for the random entries.

> Using the [sha256](../sha256) tool, we generate a [SHA256 Hash](https://en.wikipedia.org/wiki/SHA-2) hash of the _randomized_ entry file created in step 1. This becomes the provenance hash, proving that this file was shuffled prior to random number generation being executed. This shows that the entry list was known prior to random number generation, and has not been tampered with.

3. Generate a random number using the Chainlink VRF on Polygon.

> A random number is then requested from the Chainlink VRF, via our RandomRequest contract. This contract lives on the Polygon blockchain and expects a SHA256 hash to identify the random request. This is important because it is verifiable proof that the provenance hash (and therefore, the shuffled entry list) was generated prior to a random number being obtained.
> 
4. Retrieve the random number from Chainlink.

> Once we request the random number, the Chainlink VRF takes some time to generate the random number and deliver it back to our smart contract. Once Chainlink delivers the number, we can retrieve it.

5. Generate the starting position for winner selection

> With the random number in hand, we execute a [Modulo Operation](https://en.wikipedia.org/wiki/Modulo_operation) using the random number and the number of entries by utilizing our [bcmod](../bcmod) utilty. The result of this operation is then used as the starting position in the randomized entry list to choose the winners.

6. Using the starting position, select the appropriate number of winning entries.

> Using the result of the modulo operation in Step 4, we identify the entry in the resulting value's respective position in the shuffled entry file (step 1). From there, using the entry we just identified, we select _n_ consecutive winners (including the starting-position entry), where _n_ is the number of winners in the specific drawing.

# Winners

```
