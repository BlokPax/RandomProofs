# Token randomization process and proof

1. Create a random salt, hash it and publish it: `6d4a3697fdf2e10ae53ae1b75cf5d622d0c66d22abde4e6314b4f711e0cfcec7` ([tweet](https://twitter.com/WondersOTF/status/1732800007626174744)).
2. Prepare corpus with plaintext random salt and each eligible token ID, one on each line ([corpus.txt](./corpus.txt)).
3. sha256 the corpus: `dcdf2b36b8e7742a3cafa83c0e1148d6297be23a4491fe8a3d582fb4b8b849d3`.
4. Request a random number for the corpus hash, retrieve it: `35597318155460363549812616131454388392742180696501225692664609307699380266640`.
5. Using the shuffle script in this repo, shuffle the input (which is the same as the corpus, except no salt) ([input.txt](./input.txt) -> [result.txt](./result.txt)).
6. Assign tokens in order, starting at token 7. (Tokens 0-6 are not part of this randomization process.)
