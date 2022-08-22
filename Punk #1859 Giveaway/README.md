# Punk 1859 Giveaway by Blokpax

Blokpax is giving away CryptoPunk #1859!

To read about how this giveaway works, visit [blokpax.com/cryptopunk-giveaway](https://blokpax.com/cryptopunk-giveaway).

This repository exists as a way to prove, and let anyone in the community audit, that the winner of the Punk is chosen at random.

### The Selection Process

1. Sort the remaining (unrevealed) token IDs in numerical order, ascending.
2. Create a hash of the sorted token IDs from step 1 (using [hashEntries](./scripts/hashEntries) script)
3. Request random number from chainlink VRF (using contract [`0x10e4F1873617f2bd5F92F06970e1CB5C95D5aaC5`](https://etherscan.io/address/0x10e4F1873617f2bd5F92F06970e1CB5C95D5aaC5))
4. Retrieve random number from above contract
5. Seed [Mersenne Twister](https://en.wikipedia.org/wiki/Mersenne_Twister) based shuffling algorithm using random number, and shuffle the (sorted) token IDs (using [shuffle](./scripts/shuffle) script)
6. Select first _n_ token IDs from the resulting shuffled tokens. These become the revealed tokens for the round.

### The Results

| Round | Tier | Tokens to Reveal | Date/Time ||
|---|---|---|---|---|
| One | Common | 1600 | August 22, 2022 @ 12:00pm EDT | [Round 1 - Commons](./Round%201%20-%20Commons) |
| Two | Aqua | 500 | TBD ||
| Three | Blue | 250 | TBD ||
| Four | Red | 99 | TBD ||
| Five | Gold | 50 | TBD ||
| Five | Black Hologram | 1 | TBD ||
