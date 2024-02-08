## Home Team Heroes - 2023 Basketball Drop
## Topps Living Collector's Set Santa-token Giveaway

### Holder Randomization

|||
|---|---|
| **Sorted Holder List** | [holder-list.expanded.sorted.csv](./holder-list.expanded.sorted.csv) |
| **VRF Consumer Contract** | [`0x18b9b62749Fcb227C493015244E6939d8F01d0f3`](https://etherscan.io/address/0x18b9b62749Fcb227C493015244E6939d8F01d0f3) |
| **Identity Hash** | `564a5e35e43acf7a16133a79f8896e28187eab330927227947779dd5ad0cb771` |
| **Random Request** | [`0x48cf7deae20b573ea3f34189266dc34f9ec1ae478dfc4f202abcf75604dea449`](https://etherscan.io/tx/0x48cf7deae20b573ea3f34189266dc34f9ec1ae478dfc4f202abcf75604dea449) |
| **Requested on** | Feb-08-2024 08:14:13 PM +UTC |
| **Response TX** | [`0x707a08fa010c88f3d7a22be149f25948bd6b343e9549f1f11228c0ae2a3f085a`](https://etherscan.io/tx/0x60db0dbe63976ab7171a547aafe93564a1e3d67e8f70bad4f782fba7e321996a) |
| **Random Number** | `59857375654086383524430088311433350246992184543859197540433990552369518566176` |
| **Shuffled Holder List** | [holder-list.shuffled.csv](./holder-list.shuffled.csv) |

### Prize Randomization

|||
|---|---|
| **Sorted Prize List** | [prize-list.csv](./prize-list.sorted.csv) |
| **VRF Consumer Contract** | [`0x18b9b62749Fcb227C493015244E6939d8F01d0f3`](https://etherscan.io/address/0x18b9b62749Fcb227C493015244E6939d8F01d0f3) |
| **Identity Hash** | `60b4915b2cb231c9cb0a0f57528adf409142d741002e434df72c36cc7be6709a` |
| **Random Request** | [`0x50b9a3d879248f01ced30ca77132ffe6908719c146c25b66bc175f226b074461`](https://etherscan.io/tx/0x50b9a3d879248f01ced30ca77132ffe6908719c146c25b66bc175f226b074461) |
| **Requested on** | Feb-08-2024 08:41:47 PM +UTC |
| **Response TX** | [`0xfae509cdf0b04935dd10a0c9fcd08b9c8c6abc270d39dea985652fa0bffa68d1`](https://etherscan.io/tx/0xfae509cdf0b04935dd10a0c9fcd08b9c8c6abc270d39dea985652fa0bffa68d1) |
| **Random Number** | `27358639250360761013501801010284283953851324384488364460560850173338349052801` |
| **Shuffled Prize List** | [prize-list.shuffled.csv](./prize-list.shuffled.csv) |

#### The Process

**Step 1**

Shuffle the holder list

1. Prefix the transaction hash of the last transaction that interacted directly with the VRF Consumer Contract to the holder-list.sorted.csv file.
1. Create a sha256 hash of the [holder-list](./holder-list.sorted.csv).
2. Request a random number from chainlink VRF (using contract [`0x18b9b62749Fcb227C493015244E6939d8F01d0f3`](https://etherscan.io/address/0x18b9b62749Fcb227C493015244E6939d8F01d0f3))
3. Retrieve random number from above contract
4. Shuffle the holder list from step 1, by feeding the random number retrieved in step #3 to the [shuffle](../scripts/shuffle) script

**Step 2**

Shuffle the prize list

1. Prefix the transaction hash of the transaction that requested the random number for the holder list (Step 1.1 above) to the prize-list.sorted.csv.
1. Create a sha256 hash of the [prize-list](./prize-list.sorted.csv).
2. Request a random number from chainlink VRF (using contract [`0x18b9b62749Fcb227C493015244E6939d8F01d0f3`](https://etherscan.io/address/0x18b9b62749Fcb227C493015244E6939d8F01d0f3)).
3. Retrieve random number from above contract.
4. Shuffle the prize list from step 1, by feeding the random number retrieved in step #3 to the [shuffle](../scripts/shuffle) script.

**Step 3**

Combine the shuffled holder list with the shuffle prize list. This combined file defines the winner of each prize (winner specified on line #1 wins prize specified on line #1, etc).

### Results

You can view the resulting combined shuffled holder + prize list here:

[holder-prize.final.csv](./holder-prize.final.csv)

You can view the resulting holder + prize list, sorted by username, here:

[holder-prize.sorted.csv](./holder-prize.sorted.csv)

| username          | prize                                                            |
| ----------------- | ---------------------------------------------------------------- |
| 2048              | 2018 Topps Living Jacob DeGrom - PSA 10 (Cert: 41647285)         |
| alphablok         | 2018 Topps Living A.J. Pollock - PSA 10 (Cert: 41195760)         |
| alphablok         | 2018 Topps Living Adrian Beltre - PSA 10 (Cert: 42130753)        |
| alphablok         | 2018 Topps Living Brad Peacock - PSA 10 (Cert: 41334207)         |
| alphablok         | 2018 Topps Living Brandon Morrow - PSA 10 (Cert: 41331885)       |
| alphablok         | 2018 Topps Living Max Scherzer - PSA 10 (Cert: 41964001)         |
| alphablok         | 2018 Topps Living Ryen Sandberg - PSA 10 (Cert: 41520100)        |
| alphablok         | 2018 Topps Living Shohei Ohtani - PSA 10 (Cert: 41224531)        |
| alphablok         | 2018 Topps Living Tyler O'Neill - PSA 10 (Cert: 42271660)        |
| alphablok         | 2018 Topps Living Victor Robles - PSA 10 (Cert: 41647281)        |
| balward           | 2018 Topps Living Chris Taylor - PSA 10 (Cert: 41266077)         |
| balward           | 2018 Topps Living David Bote - PSA 10 (Cert: 42130820)           |
| billcot           | 2018 Topps Living Andrew Benintendi - PSA 10 (Cert: 41830459)    |
| billcot           | 2018 Topps Living Ozzie Albies - PSA 10 (Cert: 41299086)         |
| bjamps            | 2018 Topps Living Babe Ruth - PSA 10 (Cert: 42237517)            |
| bjamps            | 2018 Topps Living David Wright - PSA 10 (Cert: 42112699)         |
| bjamps            | 2018 Topps Living Walker Buehler - PSA 10 (Cert: 41964024)       |
| bmw1909           | 2018 Topps Living Ryan McMahon - PSA 10 (Cert: 42261924)         |
| bpfergu           | 2018 Topps Living Freddy Peralta - PSA 10 (Cert: 41520052)       |
| byuofu            | 2018 Topps Living Lourdes Gurriel Jr. - PSA 10 (Cert: 42065267)  |
| cph626            | 2018 Topps Living Christian Yelich - PSA 10 (Cert: 42261843)     |
| cph626            | 2018 Topps Living Rickey Henderson - PSA 10 (Cert: 41298983)     |
| cryptoblogger     | 2018 Topps Living Austin Hedges - PSA 10 (Cert: 41334407)        |
| cryptoblogger     | 2018 Topps Living Daniel Murphy - PSA 10 (Cert: 41520121)        |
| cryptoblogger     | 2018 Topps Living Jack Flaherty - PSA 10 (Cert: 42138395)        |
| dangersc          | 2018 Topps Living Albert Pujols - PSA 10 (Cert: 41334063)        |
| danielblakely     | 2018 Topps Living Jose Ramirez - PSA 10 (Cert: 41334060)         |
| davbruce21        | 2018 Topps Living Miguel Andujar - PSA 10 (Cert: 41334377)       |
| davbruce21        | 2018 Topps Living Rafeal Devers - PSA 10 (Cert: 41484934)        |
| deleonlakers2000  | 2018 Topps Living Scott Kingery - PSA 10 (Cert: 41421360)        |
| dhoovey           | 2018 Topps Living Joey Votto - PSA 10 (Cert: 42130861)           |
| esotericpa        | 2018 Topps Living Jackie Robinson - PSA 10 (Cert: 41896210)      |
| eze-e312          | 2018 Topps Living Ian Happ - PSA 10 (Cert: 41117378)             |
| ghedoicy          | 2018 Topps Living Juan Soto - PSA 10 (Cert: 41334181)            |
| infininight       | 2018 Topps Living Dominic Smith - PSA 10 (Cert: 42261930)        |
| jdbeltz           | 2018 Topps Living J.D. Martinez - PSA 10 (Cert: 42109453)        |
| jenndunn12m       | 2018 Topps Living Don Mattingly - PSA 10 (Cert: 42181030)        |
| jenndunn12m       | 2018 Topps Living Manny Machado - PSA 10 (Cert: 41485052)        |
| johnnyclutchcards | 2018 Topps Living Amed Rosario - PSA 10 (Cert: 41519959)         |
| leighham          | 2018 Topps Living Cody Bellinger - PSA 10 (Cert: 41693433)       |
| mattcook          | 2018 Topps Living Jake Arrieta - PSA 10 (Cert: 42024220)         |
| mattcook          | 2018 Topps Living Jean Segura - PSA 10 (Cert: 41224595)          |
| mattcook          | 2018 Topps Living Jordy Mercer - PSA 10 (Cert: 41224735)         |
| me-degen          | 2018 Topps Living Yoan Moncada - PSA 10 (Cert: 41298933)         |
| metajungle        | 2018 Topps Living Adam Duvall - PSA 10 (Cert: 41890221)          |
| metajungle        | 2018 Topps Living Alex Gordon - PSA 10 (Cert: 41224589)          |
| metajungle        | 2018 Topps Living Anthony Rizzo - PSA 10 (Cert: 41520113)        |
| metajungle        | 2018 Topps Living Bartolo Colon - PSA 10 (Cert: 41334199)        |
| metajungle        | 2018 Topps Living Bo Jackson - PSA 10 (Cert: 41654881)           |
| metajungle        | 2018 Topps Living Charlie Blackmon - PSA 10 (Cert: 41104101)     |
| metajungle        | 2018 Topps Living Christian Villanueva - PSA 10 (Cert: 41889976) |
| metajungle        | 2018 Topps Living Derek Jeter - PSA 10 (Cert: 41409736)          |
| metajungle        | 2018 Topps Living Dustin Fowler - PSA 10 (Cert: 41754127)        |
| metajungle        | 2018 Topps Living Hank Aaron - PSA 10 (Cert: 41334283)           |
| metajungle        | 2018 Topps Living Ichiro Suzuki - PSA 10 (Cert: 41298914)        |
| metajungle        | 2018 Topps Living Jackie Bradley Jr. - PSA 10 (Cert: 42077692)   |
| metajungle        | 2018 Topps Living Jed Lowrie - PSA 10 (Cert: 41647272)           |
| metajungle        | 2018 Topps Living Jose Berrios - PSA 10 (Cert: 41104019)         |
| metajungle        | 2018 Topps Living Lewis Brinson - PSA 10 (Cert: 41872942)        |
| metajungle        | 2018 Topps Living Mallex Smith - PSA 10 (Cert: 41266891)         |
| metajungle        | 2018 Topps Living Nick Markakis  - PSA 10 (Cert: 41446977)       |
| metajungle        | 2018 Topps Living Paul DeJong - PSA 10 (Cert: 41266085)          |
| metajungle        | 2018 Topps Living Rhys Hoskins - PSA 10 (Cert: 41265830)         |
| metajungle        | 2018 Topps Living Sean Manaea - PSA 10 (Cert: 41907381)          |
| metajungle        | 2018 Topps Living Willy Adames - PSA 10 (Cert: 41520125)         |
| metajungle        | 2018 Topps Living Yasiel Puig - PSA 10 (Cert: 41754123)          |
| mgmonaco11        | 2018 Topps Living Kevin Pillar - PSA 10 (Cert: 41334301)         |
| mjno23goat        | 2018 Topps Living Chris Sale - PSA 10 (Cert: 42261979)           |
| mjno23goat        | 2018 Topps Living Noah Syndergaard - PSA 10 (Cert: 41334396)     |
| netbe171          | 2018 Topps Living Trevor Story - PSA 10 (Cert: 42130832)         |
| niftymetagirl     | 2018 Topps Living Chase Headley - PSA 10 (Cert: 41519958)        |
| niftymetagirl     | 2018 Topps Living Clayton Kershaw - PSA 10 (Cert: 42261891)      |
| niftymetagirl     | 2018 Topps Living Nick Williams - PSA 10 (Cert: 42130741)        |
| omgiwon           | 2018 Topps Living Jose Altuve - PSA 10 (Cert: 41224607)          |
| patelh121         | 2018 Topps Living Francisco Mejia - PSA 10 (Cert: 42109491)      |
| patelh121         | 2018 Topps Living Gleyber Torres - PSA 10 (Cert: 41334077)       |
| patelh121         | 2018 Topps Living Manny Machado - PSA 10 (Cert: 42434993)        |
| patelh121         | 2018 Topps Living Mitch Haniger - PSA 10 (Cert: 41954051)        |
| patelh121         | 2018 Topps Living Ronald Acuna Jr. - PSA 10 (Cert: 41298849)     |
| radishkabal6      | 2018 Topps Living Nick Castellanos - PSA 10 (Cert: 40978615)     |
| radishkabal6      | 2018 Topps Living Ted Williams - PSA 10 (Cert: 41964083)         |
| randorino99       | 2018 Topps Living Austin Meadows - PSA 10 (Cert: 41873089)       |
| ronfresco         | 2018 Topps Living Brian Anderson - PSA 10 (Cert: 41907418)       |
| ronfresco         | 2018 Topps Living Ender Inciarte - PSA 10 (Cert: 42261952)       |
| ronfresco         | 2018 Topps Living Joey Rickard - PSA 10 (Cert: 41409803)         |
| schmoe            | 2018 Topps Living Bryce Harper - PSA 10 (Cert: 41409744)         |
| schmoe            | 2018 Topps Living Evan Gattis - PSA 10 (Cert: 42109472)          |
| schmoe            | 2018 Topps Living Giancarlo Stanton - PSA 10 (Cert: 41872995)    |
| schmoe            | 2018 Topps Living Joe Panik - PSA 10 (Cert: 41027111)            |
| sheltronica       | 2018 Topps Living Eric Sogard - PSA 10 (Cert: 41890814)          |
| steffen2121       | 2018 Topps Living Russell Martin - PSA 10 (Cert: 41265890)       |
| titomachado       | 2018 Topps Living Matt Olson - PSA 10 (Cert: 41334061)           |
| titomachado       | 2018 Topps Living Pat Neshek - PSA 10 (Cert: 41520061)           |
| viking91107       | 2018 Topps Living Dereck Rodriguez - PSA 10 (Cert: 42024231)     |
| viking91107       | 2018 Topps Living Francisco Lindor - PSA 10 (Cert: 41873061)     |
| viking91107       | 2018 Topps Living Roberto Clemente - PSA 10 (Cert: 41693448)     |
| xheryk            | 2018 Topps Living Aaron Judge - PSA 10 (Cert: 41191564)          |
| xheryk            | 2018 Topps Living Avisail Garcia - PSA 10 (Cert: 41693460)       |
| xheryk            | 2018 Topps Living Jordan Hicks - PSA 10 (Cert: 41334296)         |
| yop7              | 2018 Topps Living Joe Mauer - PSA 10 (Cert: 42281591)            |



### References

**shuffle script**

The shuffle script utilizes the random numbered retrieved from the Chainlink VRF as a seed into the [Mersenne Twister](https://en.wikipedia.org/wiki/Mersenne_Twister) algorithm. This allows the resulting shuffled order to be re-created by using the same inputs (original sort order and sorting seed).

**ChainlinkVRF**

ChainlinkVRF is a blockchain powered random number generator. Blokpax uses the ChainlinkVRF as it's random number generator because it guarantees that we [Blokpax] have no prior knowledge of the random value and had no opportunity or capability of tampering with the result. You can read more about the ChainlinkVRF here: [https://docs.chain.link/vrf](https://docs.chain.link/vrf).
