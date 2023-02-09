# Winter Elite Instant Winner Bonus Random

When we mint pax to distribute as part of a drop, all pax are initially distributed to our Custodian (address: `0x8930eb231a1e1873319e79fec684133de08cf4d3`). There are usually more pax minted than participating entries, as was the case in the Winter Elite Drop. In this case, one of the Pax the custodian happened to hit (more technically, it wasn't hit by anyone else) was an Instant Winner, which was randomed into a [Babe Ruth](https://opensea.io/assets/matic/0xa9810db43691811f5ca00c051e0ff370843fb366/2147484544) card.

The following is the process which was used to determine a winner for the Babe Ruth card, as well as a Tom Brady card that was added as a compensation. All entrants who ripped cards (or had them auto-ripped) from Blokpax at the beginning of the drop were eligible for the Babe Ruth, pro-rated to the number of pax they ripped. All participants who held an Instant Winner token at the end of the drop were eligible for the Tom Brady card, pro-rated to the number of tokens they held. The process was the same for both cards and entrants, just different parameters.

## Process

1. Build a list of wallet addresses that are eligible, repeated for multiple entries and one wallet address per line. Sort by wallet address. Include a header of `wallet_address`. (The attached CSVs do not have the `wallet_address` header to simplify presentation.)
2. Hash that file using the `sha256` algorithm.
3. Provide that hash to our random contract, ensuring that we can only produce one random number for each set of entrants (see transaction below).
4. Retrieve the random number, and take its modulus of the number of participants.
5. The winning index is `randomNumber % modulus`. Add `1` to this value to determine which row of the input file wins (index 0 = row 1, etc., not including header).

## Babe Ruth Instant Winner

|                    |                                                                                                                                                                       |
| ------------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Entries            | [`bonus-rippers.csv`](./bonus-rippers.csv)                                                                                                                            |
| Hash (sha256)      | `0xe1cc7c4acff38093b16d374bb161b35fc9500b0339a4ada4049f1d7a60d3f293`                                                                                                  |
| Random Transaction | [`0x72cd78afb77d8e3847e41a3ddc86d52587ab9f2d066b5b434d4f3992e6e48dd2`](https://polygonscan.com/tx/0x72cd78afb77d8e3847e41a3ddc86d52587ab9f2d066b5b434d4f3992e6e48dd2) |
| Random Number      | `92234195620242952604112191381395690192122061086764384540736736654760319472823`                                                                                       |
| Modulus            | `73259`                                                                                                                                                               |
| Winner             | `6453`: `0x1b2416353a6b71cd6b0c8291d863b376776bbd01`                                                                                                                  |

## Tom Brady Compensation Card

|                    |                                                                                                                                                                       |
| ------------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Entries            | [`bonus-instant-winners.csv`](./bonus-instant-winners.csv)                                                                                                            |
| Hash (sha256)      | `0xb8421dbdaeafb2428ef4d1ad50b5e47cec29d5d94a136caf7c994eda2f92ae91`                                                                                                  |
| Random Transaction | [`0x5d0efb7a33e0977d998fe7dc02525e652e76d5b8b921b1e55ff4b79846b00a02`](https://polygonscan.com/tx/0x5d0efb7a33e0977d998fe7dc02525e652e76d5b8b921b1e55ff4b79846b00a02) |
| Random Number      | `86652787187153267725704776735793233996081739154902014496923235895098548344538`                                                                                       |
| Modulus            | `40`                                                                                                                                                                  |
| Winner             | `18`: `0x8338c39b1314B110E1c09534efc0AE0BCB9bFA4E`                                                                                                                    |
