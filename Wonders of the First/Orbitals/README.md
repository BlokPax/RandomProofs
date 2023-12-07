# Orbitals Winners selection process and proof

1. Create a random salt, hash it and publish it: `4791036b5cf79e9f17e89ded57fe193e743661a476f1b94cf06292cccc121432` ([tweet](https://twitter.com/WondersOTF/status/1732800007626174744)).
2. Prepare corpus with plaintext random salt and each eligible token ID, one on each line ([corpus.txt](./corpus.txt)).
3. sha256 the corpus: `34f487e3fc3212ec78b1ed82c9082ce810376126eda203d07871f4f0ea1ebd77`.
4. Request a random number for the corpus hash, retrieve it: `37427507857235775382472272104758999404293607742417964656245918846864537528276`
5. Using the shuffle script in this repo, shuffle the input (which is the same as the corpus, except no salt) ([input.txt](./input.txt) -> [result.txt](./result.txt)).
6. Winners are the owners of the first seven token IDs, in order, at the block when the random number was fulfilled ([18736213](https://etherscan.io/block/18736213), [tx](https://etherscan.io/tx/0x8fef2aa8e0896ff4626a7b9694ea689ccd84c84688d64a22dfeed641ac00fc89)).

| Token ID | Owner                                        | Orbital Token Received |
| -------- | -------------------------------------------- | ---------------------- |
| 881      | `0xB7759A43F615362c54c65eb7c10e3997Dda98532` | 0                      |
| 2176     | `0x96613d73FBEf04F91A32e5489c9c0Ad23Ea6fD93` | 1                      |
| 1966     | `0xe7C5393b6c6Ce8Ce5a8C48fB65Cfe6B5b065c175` | 2                      |
| 2898     | `0x36337998611C162d4f9c933AbD5615522731f105` | 3                      |
| 1057     | `0x940F4cDE80b1C2d33bc651b469dCC7653296344d` | 4                      |
| 2928     | `0xB48E7F68f782e6B67289284f5c86eD32c43D5AD1` | 5                      |
| 1246     | `0x3A40B0d2D4bd528147f33EC5CDd1b7167850eB11` | 6                      |
