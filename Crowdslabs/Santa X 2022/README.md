# Santa X 2022

|                           |                                                                                                                                                                    |
| ------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **Inputs**                | [inputs.json](./inputs.json)                                                                                                                                       |
| **VRF Consumer Contract** | [`0x18b9b62749Fcb227C493015244E6939d8F01d0f3`](https://etherscan.io/address/0x18b9b62749Fcb227C493015244E6939d8F01d0f3)                                            |
| **Identity Hash**         | `0x2c7d75787693278a6d301d8b4058490883b31ee95f448861e2ff78515eeccf81`                                                                                               |
| **Random Request**        | [`0x1822a6cf1dc9754f836f20823decbed3868b2dc61ba2e59da3979556d6625141`](https://etherscan.io/tx/0x1822a6cf1dc9754f836f20823decbed3868b2dc61ba2e59da3979556d6625141) |
| **Requested on**          | Dec-19-2022 04:38:23 PM +UTC                                                                                                                                       |
| **Response TX**           | [`0xb0a206f6693cf63ba739ad9bab4d18cbd754cfb6a6354693fabb1297316e2ec6`](https://etherscan.io/tx/0xb0a206f6693cf63ba739ad9bab4d18cbd754cfb6a6354693fabb1297316e2ec6) |
| **Random Number**         | `50169832453334368514355063473275391559475919919824185449390716630497829740106`                                                                                    |
|                           |
| **Winners**               | [winners.json](./shuffled-claim-passes.csv)                                                                                                                        |
| **Consolation Winners**   | [consolation.json](./consolation.json)                                                                                                                             |

## Reproduction steps

1. Each participant (represented by a wallet address) received one entry for every Point staked. From this list, build a list of all entries such that each participant receives _n_ entries for _n_ Points staked. (The total number of points staked, and the total number of entries, was 11,170,150.)
2. Sort the list alphabetically (case-insensitive).
3. With the random number obtained, seed a random number generator with that number % `9223372036854775807` (the maximum value a 64-bit integer can hold). (In this case, the derived seed is: `4286751031954211492`.)
4. With the seeded random number generator, get a new random number % the number of entries and look up which participant this corresponds to on the entries list. If this participant hasn't already won, they are now a winner, and continue. If they _have_ already won, discard this random number and choose again. Repeat this process until 85 winners are chosen. (The first winner chosen receives the highest-valued prize, and the last winner chosen receives the lowest-valued prize.)

## Consolation prizes

1. There were 133 participants and 85 winners, meaning, regrettably, there were 48 participants who did not win. There are three additional prizes that are each split between those participants. To determine the amounts, repeat the following process for each prize.
2. Derive a list of the 48 participants who did not win and sort it alphabetically (case-insensitive).
3. Using the seeded random number generator from the winners process, shuffle this list 1000 times using a `rand() < 0.5` predicate as a comparator.
4. For each `i` of the 200 Crowdslabs available, assign it to the `i%len(participants)`th participant.
5. This means that each consolation prize recipient gets at least 4 Crowdslabs apiece, and 8 participants (per prize) get 5 Crowdslabs.
