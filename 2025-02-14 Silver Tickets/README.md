# Silver Ticket winner selection process and proof

1. Create a random salt, hash it and publish it: `ec140cc80fed19da8ab3a3e5da2fe4a520864f583d5ffe91ee0bf15798a35ac6` (posted in Blokpax Discord: https://discord.com/channels/857294212872929292/918885040564351026/1340009973517779106).
2. Prepare corpus with plaintext random salt and each eligible token ID, one on each line ([corpus.txt](./corpus.txt)).
3. sha256 the corpus: `e8b2af22afe15fec0a87c8e02e86e684312a9af30972956cafe17b3780637f88`.
4. Request a random number for the corpus hash, retrieve it: `97412543307895298640269617999206352769968662764366687341797403123317045475371`
5. Using the shuffle script in this repo, shuffle the input (which is the same as the corpus, except no salt) ([input.txt](./input.txt) -> [result.txt](./result.txt)).
6. Winner is the first username listed in [result.txt](./result.txt).
