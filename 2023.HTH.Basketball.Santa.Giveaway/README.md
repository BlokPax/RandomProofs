## Home Team Heroes - 2023 Basketball Drop
## Santa Token Giveaway

### Holder Randomization

|||
|---|---|
| **Sorted Holder List** | [holder-list.sorted.csv](./holder-list.sorted.csv) |
| **VRF Consumer Contract** | [`0x18b9b62749Fcb227C493015244E6939d8F01d0f3`](https://etherscan.io/address/0x18b9b62749Fcb227C493015244E6939d8F01d0f3) |
| **Identity Hash** | `045cb3a9388f779511f983625040a231fbd29d1503ec335b86dcf9ae7a808a75` |
| **Random Request** | [`0x5ec43b7fdd7d8ecfa146d19f682e2fecbe10b4483aa1c0f6fda2fbf8d5d89bd4`](https://etherscan.io/tx/0x5ec43b7fdd7d8ecfa146d19f682e2fecbe10b4483aa1c0f6fda2fbf8d5d89bd4) |
| **Requested on** | Jan-19-2024 03:51:59 PM +UTC |
| **Response TX** | [`0x707a08fa010c88f3d7a22be149f25948bd6b343e9549f1f11228c0ae2a3f085a`](https://etherscan.io/tx/0x707a08fa010c88f3d7a22be149f25948bd6b343e9549f1f11228c0ae2a3f085a) |
| **Random Number** | `69165167868116923661514089460175962185869526237898403976016013719167137724581` |
| **Shuffled Holder List** | [holder-list.shuffled.csv](./holder-list.shuffled.csv) |

### Prize Randomization

|||
|---|---|
| **Sorted Prize List** | [prize-list.csv](./prize-list.sorted.csv) |
| **VRF Consumer Contract** | [`0x18b9b62749Fcb227C493015244E6939d8F01d0f3`](https://etherscan.io/address/0x18b9b62749Fcb227C493015244E6939d8F01d0f3) |
| **Identity Hash** | `401bb53ee228fd641694f67edb0f58dacaaa40abbce34bb39c136d1f2113cb13` |
| **Random Request** | [`0xd60e312019e1390db108ef4f36c60759b5facacf97a9c1809342b6df686dbd51`](https://etherscan.io/tx/0xd60e312019e1390db108ef4f36c60759b5facacf97a9c1809342b6df686dbd51) |
| **Requested on** | Jan-19-2024 04:05:11 PM +UTC |
| **Response TX** | [`0x7f2238dfec7805a93048a083fc6e6f3ecc6a678ab825d87fd7b03e3966f7e6b7`](https://etherscan.io/tx/0x7f2238dfec7805a93048a083fc6e6f3ecc6a678ab825d87fd7b03e3966f7e6b7) |
| **Random Number** | `20152433981675918074379307541549520476011063677699754463039780886931010692510` |
| **Shuffled Prize List** | [prize-list.shuffled.csv](./prize-list.shuffled.csv) |

### Round 2 Holder Randomization

|||
|---|---|
| **Sorted Prize List** | [holder-list.round2.expanded.csv](./holder-list.round2.expanded.csv) |
| **VRF Consumer Contract** | [`0x18b9b62749Fcb227C493015244E6939d8F01d0f3`](https://etherscan.io/address/0x18b9b62749Fcb227C493015244E6939d8F01d0f3) |
| **Identity Hash** | `d432153b640ea14797df07bc255dce46f73df48eb5a27d57e90f34c021de86a3` |
| **Random Request** | [`0x67d53777148d780a382ab9df790c96a841f64957639ee28bc01c32360f4a3313`](https://etherscan.io/tx/0x67d53777148d780a382ab9df790c96a841f64957639ee28bc01c32360f4a3313) |
| **Requested on** | Jan-20-2024 03:31:35 PM +UTC |
| **Response TX** | [`0x8b001e1b5ea1834a7ec9dbfba9916114a06431fbca1f3d2c3d4138c0541f2a1c`](https://etherscan.io/tx/) |
| **Random Number** | `45207826098370896515338165021102798705514017777416019732801321180651431517157` |
| **Shuffled Prize List** | [holder-list.round2.shuffled.csv](./holder-list.round2.shuffled) |

#### The Process

**Step 1**

Shuffle the holder list

1. Prefix the transaction hash of the last transaction that interacted directly with the VRF Consumer Contract to the holder-list.sorted.csv file.
1. Create a sha256 hash of the [holder-list](./holder-list.sorted.csv).
2. Request a random number from chainlink VRF (using contract [`0x18b9b62749Fcb227C493015244E6939d8F01d0f3`](https://etherscan.io/address/0x18b9b62749Fcb227C493015244E6939d8F01d0f3))
3. Retrieve random number from above contract
4. Shuffle the holder list from step 1, by feeding the random number retrieved in step #3 to the [shuffle](./scripts/shuffle) script

**Step 2**

Shuffle the prize list

1. Prefix the transaction hash of the transaction that requested the random number for the holder list (Step 1.1 above) to the prize-list.sorted.csv.
1. Create a sha256 hash of the [prize-list](./prize-list.sorted.csv).
2. Request a random number from chainlink VRF (using contract [`0x18b9b62749Fcb227C493015244E6939d8F01d0f3`](https://etherscan.io/address/0x18b9b62749Fcb227C493015244E6939d8F01d0f3)).
3. Retrieve random number from above contract.
4. Shuffle the prize list from step 1, by feeding the random number retrieved in step #3 to the [shuffle](./scripts/shuffle) script.

**Step 3**

Combine the shuffled holder list with the shuffle prize list. This combined file defines the winner of each prize (winner specified on line #1 wins prize specified on line #1, etc).

**Step 4**

Prepare a second randomized selection of winners that were accidentally omitted from the first set of entries.

1. After identifying the missing entries, publish the list for community audit. [holder-list.round2.csv](./holder-list.round2.csv).
2. Expand entries after audit, to give the missing entries equal odds as the original. [holder-list.round2.expanded.csv](./holder-list.round2.expanded.csv)
3. Hash the expanded entries to create an identity hash.
4. Request a random number from chainlink VRF.
5. Shuffle holder list from step 2, by feeding the random number retrieved in step #4 into the [shuffle](./scripts/shuffle) script. [holder-list.round2.shuffled.csv](./holder-list.round2.shuffled.csv)
6. Combine the shuffled list into the originally shuffled prize list (from step 2.4)


### Results

You can view the resulting combined shuffled holder + prize list here:

[holder-prize.final.csv](./holder-prize.final.csv)

You can view the resulting holder + prize list, sorted by username, here:

[holder-prize.sorted.csv](./holder-prize.sorted.csv)

| username          | prize            | round2 username |
| ----------------- | ---------------- | --------------- |
| BigDobs           | $5 Store Credit  |                 |
| Schmoe            | $10 Store Credit |                 |
| DangerSC          | $5 Store Credit  |                 |
| Newlin99          | $5 Store Credit  |                 |
| mattcook          | $10 Store Credit |                 |
| Guvv              | $5 Store Credit  |                 |
| Mvenekam          | $5 Store Credit  |                 |
| Jalbo1            | $2500 USDC       |                 |
| bmw1909           | $10 Store Credit |                 |
| MetaJungle        | $10 Store Credit |                 |
| Ronfresco         | $5 Store Credit  |                 |
| Billcot           | $5 Store Credit  |                 |
| MetaJungle        | $5 Store Credit  |                 |
| Chicagows213      | $5 Store Credit  |                 |
| MetaJungle        | $5 Store Credit  | dfeog           |
| Roux1310          | $5 Store Credit  |                 |
| Patelh121         | $5 Store Credit  |                 |
| JohnnyClutchCards | $5 Store Credit  |                 |
| MetaJungle        | $5 Store Credit  |                 |
| AlphaBlok         | $10 Store Credit |                 |
| floreski          | $5 Store Credit  |                 |
| cookiemonster     | $10 Store Credit |                 |
| mattcook          | $25 Store Credit |                 |
| AlphaBlok         | $10 Store Credit |                 |
| accordingtohen    | $5 Store Credit  |                 |
| mattcook          | $10 Store Credit |                 |
| Mikeyj10          | $5 Store Credit  |                 |
| Xheryk            | $5 Store Credit  |                 |
| Patelh121         | $10 Store Credit |                 |
| Eldun             | $5 Store Credit  |                 |
| BigDobs           | $25 Store Credit |                 |
| Patelh121         | $10 Store Credit |                 |
| Schmoe            | $10 Store Credit |                 |
| jbbasics          | $25 Store Credit |                 |
| Jjmccann2121      | $5 Store Credit  |                 |
| MetaJungle        | $25 Store Credit |                 |
| Bjamps            | $5 Store Credit  |                 |
| MetaJungle        | $25 Store Credit |                 |
| mattcook          | $25 Store Credit |                 |
| Ronfresco         | $25 Store Credit |                 |
| MetaJungle        | $5 Store Credit  |                 |
| Titomachado       | $5 Store Credit  |                 |
| MetaJungle        | $10 Store Credit |                 |
| Coloradoboy2      | $5 Store Credit  |                 |
| mattcook          | $5 Store Credit  |                 |
| jenndunn12m       | $25 Store Credit |                 |
| MetaJungle        | $150 USDC        |                 |
| EsotericPA        | $5 Store Credit  |                 |
| MetaJungle        | $5 Store Credit  |                 |
| AlphaBlok         | $5 Store Credit  | smashngrab77    |
| mattcook          | $10 Store Credit |                 |
| PhillyWill        | $5 Store Credit  |                 |
| jdbeltz           | $10 Store Credit |                 |
| SDYote            | $10 Store Credit |                 |
| Centerpiece       | $10 Store Credit |                 |
| MetaJungle        | $5 Store Credit  |                 |
| Patelh121         | $5 Store Credit  |                 |
| Johnnykpoker      | $25 Store Credit |                 |
| FlyingNinja       | $10 Store Credit |                 |
| BigDobs           | $5 Store Credit  |                 |
| eZe-E312          | $10 Store Credit |                 |
| Bjamps            | $5 Store Credit  |                 |
| ginobili_fan      | $5 Store Credit  |                 |
| Billcot           | $5 Store Credit  |                 |
| BigDobs           | $5 Store Credit  |                 |
| bpfergu           | $10 Store Credit |                 |
| MetaJungle        | $5 Store Credit  | smashngrab77    |
| bpfergu           | $10 Store Credit | smashngrab77    |
| MetaJungle        | $5 Store Credit  |                 |
| Schmoe            | $5 Store Credit  |                 |
| MetaJungle        | $5 Store Credit  |                 |
| MetaJungle        | $5 Store Credit  |                 |
| eZe-E312          | $25 Store Credit |                 |
| iiiericiii        | $10 Store Credit |                 |
| Roux1310          | $5 Store Credit  |                 |
| mjzastrow1        | $5 Store Credit  |                 |
| AlphaBlok         | $10 Store Credit |                 |
| 0000              | $10 Store Credit |                 |
| Bjamps            | $5 Store Credit  |                 |
| jenndunn12m       | $5 Store Credit  |                 |
| bmw1909           | $5 Store Credit  |                 |
| Patelh121         | $5 Store Credit  |                 |
| Omgiwon           | $5 Store Credit  |                 |
| Roux1310          | $5 Store Credit  | subhubgrading   |
| cph626            | $5 Store Credit  |                 |
| TheStranger       | $5 Store Credit  |                 |
| Patelh121         | $25 Store Credit |                 |
| Xheryk            | $5 Store Credit  |                 |
| autom8ed          | $10 Store Credit |                 |
| Xheryk            | $10 Store Credit |                 |
| Aaron             | $5 Store Credit  |                 |
| SDYote            | $5 Store Credit  |                 |
| wisrhino          | $5 Store Credit  |                 |
| MetaJungle        | $25 Store Credit |                 |
| cph626            | $5 Store Credit  |                 |
| Crispjb           | $5 Store Credit  |                 |
| accordingtohen    | $5 Store Credit  |                 |
| Ronfresco         | $5 Store Credit  |                 |
| Madvolker         | $5 Store Credit  |                 |
| Omgiwon           | $5 Store Credit  |                 |
| MetaJungle        | $5 Store Credit  | mjno23goat      |
| Madvolker         | $5 Store Credit  |                 |
| bpfergu           | $5 Store Credit  | davidpatrick08  |
| Ronfresco         | $10 Store Credit |                 |
| Guvv              | $10 Store Credit |                 |
| Bjamps            | $5 Store Credit  |                 |
| Jimmys75          | $5 Store Credit  |                 |
| Ronfresco         | $5 Store Credit  |                 |
| MetaJungle        | $5 Store Credit  |                 |
| Charlotteann      | $5 Store Credit  |                 |
| Omgiwon           | $5 Store Credit  |                 |
| Xheryk            | $5 Store Credit  |                 |
| Schmoe            | $10 Store Credit |                 |
| MetaJungle        | $5 Store Credit  |                 |
| Jeffslugs         | $5 Store Credit  |                 |
| mambaout          | $10 Store Credit |                 |
| cryptoblogger     | $5 Store Credit  |                 |
| jdbeltz           | $5 Store Credit  |                 |
| cph626            | $5 Store Credit  |                 |
| mjzastrow1        | $25 Store Credit |                 |
| SDYote            | $5 Store Credit  |                 |
| MetaJungle        | $25 Store Credit |                 |
| MetaJungle        | $125 USDC        |                 |
| cryptoblogger     | $10 Store Credit |                 |
| bpfergu           | $5 Store Credit  |                 |
| Xheryk            | $5 Store Credit  | davidpatrick08  |
| jmyers81          | $5 Store Credit  |                 |
| Schmoe            | $10 Store Credit |                 |
| Robertk           | $5 Store Credit  |                 |
| Roux1310          | $5 Store Credit  |                 |
| MetaJungle        | $10 Store Credit |                 |
| MetaJungle        | $5 Store Credit  |                 |
| AlphaBlok         | $10 Store Credit |                 |
| Ronfresco         | $5 Store Credit  |                 |
| MetaJungle        | $5 Store Credit  |                 |
| MetaJungle        | $5 Store Credit  |                 |
| AlphaBlok         | $5 Store Credit  |                 |
| Bsusko            | $500 USDC        |                 |
| MetaJungle        | $25 Store Credit |                 |
| Andrewgarrett41   | $5 Store Credit  |                 |
| jenndunn12m       | $5 Store Credit  |                 |
| deleonlakers2000  | $5 Store Credit  |                 |
| MetaJungle        | $5 Store Credit  |                 |
| cph626            | $5 Store Credit  |                 |
| Xheryk            | $10 Store Credit | smashngrab77    |
| Bjamps            | $5 Store Credit  |                 |
| Donk3ykong81      | $10 Store Credit |                 |
| AlphaBlok         | $5 Store Credit  |                 |
| Jjmccann2121      | $10 Store Credit |                 |
| mattcook          | $5 Store Credit  |                 |
| MetaJungle        | $5 Store Credit  |                 |
| Patelh121         | $5 Store Credit  |                 |
| Ronfresco         | $10 Store Credit |                 |
| sheltronica       | $25 Store Credit |                 |
| MetaJungle        | $5 Store Credit  |                 |
| ghedoicy          | $10 Store Credit | galileo         |
| jenndunn12m       | $5 Store Credit  |                 |
| Madvolker         | $10 Store Credit |                 |
| JohnnyClutchCards | $10 Store Credit |                 |
| DangerSC          | $5 Store Credit  |                 |
| cph626            | $5 Store Credit  |                 |
| Patelh121         | $25 Store Credit |                 |
| cryptoblogger     | $5 Store Credit  |                 |
| Uahjames          | $25 Store Credit |                 |
| LandoLakes        | $5 Store Credit  |                 |
| MetaJungle        | $10 Store Credit |                 |
| Bjamps            | $5 Store Credit  |                 |
| Bjamps            | $5 Store Credit  |                 |
| cph626            | $5 Store Credit  |                 |
| Omgiwon           | $10 Store Credit |                 |
| heffery           | $5 Store Credit  |                 |
| AlphaBlok         | $5 Store Credit  |                 |
| davejr81          | $5 Store Credit  |                 |
| bmw1909           | $5 Store Credit  |                 |
| Bjamps            | $10 Store Credit |                 |
| AlphaBlok         | $5 Store Credit  |                 |
| heffery           | $10 Store Credit |                 |
| MetaJungle        | $10 Store Credit |                 |
| Omgiwon           | $10 Store Credit |                 |
| cph626            | $5 Store Credit  |                 |
| Patelh121         | $5 Store Credit  |                 |
| Steffen2121       | $5 Store Credit  |                 |
| Jjmccann2121      | $5 Store Credit  | radishkabal6    |
| Jjmccann2121      | $5 Store Credit  |                 |
| Ruxy              | $5 Store Credit  |                 |
| cryptoblogger     | $5 Store Credit  |                 |
| Xheryk            | $10 Store Credit |                 |
| mattcook          | $5 Store Credit  |                 |
| cryptoblogger     | $25 Store Credit |                 |
| thampster         | $25 Store Credit |                 |
| eZe-E312          | $5 Store Credit  |                 |
| MetaJungle        | $5 Store Credit  | milvec          |
| MetaJungle        | $5 Store Credit  |                 |
| Schmoe            | $5 Store Credit  | galileo         |
| bmw1909           | $250 USDC        |                 |
| MetaJungle        | $5 Store Credit  |                 |
| Kyled005          | $5 Store Credit  |                 |
| Schmoe            | $5 Store Credit  |                 |
| Ronfresco         | $10 Store Credit |                 |
| AlphaBlok         | $10 Store Credit |                 |
| MetaJungle        | $5 Store Credit  |                 |
| mattcook          | $125 USDC        |                 |
| cph626            | $10 Store Credit |                 |
| bpfergu           | $5 Store Credit  | dstix11         |
| jenkins           | $5 Store Credit  | yoyo909         |
| NiftyMetaGirl     | $5 Store Credit  |                 |
| heffery           | $10 Store Credit |                 |
| TheStranger       | $25 Store Credit |                 |
| Gamerchick39      | $25 Store Credit |                 |
| Bjamps            | $25 Store Credit | milvec          |
| MetaJungle        | $25 Store Credit |                 |
| Ronfresco         | $10 Store Credit |                 |
| AlphaBlok         | $25 Store Credit |                 |
| Xheryk            | $25 Store Credit |                 |
| Mvenekam          | $10 Store Credit |                 |
| DangerSC          | $10 Store Credit |                 |
| Patelh121         | $5 Store Credit  |                 |
| AlphaBlok         | $5 Store Credit  |                 |
| MetaJungle        | $10 Store Credit |                 |
| Bjamps            | $10 Store Credit |                 |
| wisrhino          | $5 Store Credit  |                 |
| ghedoicy          | $25 Store Credit |                 |
| MetaJungle        | $5 Store Credit  |                 |
| accordingtohen    | $5 Store Credit  |                 |
| NiftyMetaGirl     | $5 Store Credit  |                 |
| pcahiwat          | $10 Store Credit |                 |
| Bjamps            | $10 Store Credit |                 |
| Schmoe            | $5 Store Credit  |                 |
| Bjamps            | $5 Store Credit  |                 |
| Patelh121         | $5 Store Credit  |                 |
| Charlotteann      | $25 Store Credit |                 |
| heffery           | $5 Store Credit  |                 |
| Shudog            | $10 Store Credit |                 |
| MetaJungle        | $5 Store Credit  |                 |
| Xheryk            | $5 Store Credit  |                 |
| gozags            | $10 Store Credit |                 |
| JBAtlFalcons      | $5 Store Credit  | milvec          |
| MetaJungle        | $5 Store Credit  | smashngrab77    |
| Schmoe            | $25 Store Credit |                 |
| cryptoblogger     | $5 Store Credit  |                 |
| cryptoblogger     | $5 Store Credit  |                 |
| Omgiwon           | $10 Store Credit |                 |
| MetaJungle        | $25 Store Credit |                 |
| akicks            | $5 Store Credit  |                 |
| bmw1909           | $10 Store Credit |                 |
| Patelh121         | $5 Store Credit  |                 |
| MetaJungle        | $5 Store Credit  |                 |
| Bsusko            | $10 Store Credit |                 |
| mattcook          | $5 Store Credit  |                 |
| Billcot           | $5 Store Credit  |                 |
| MetaJungle        | $5 Store Credit  |                 |
| AlphaBlok         | $10 Store Credit |                 |
| AlphaBlok         | $10 Store Credit |                 |
| Schmoe            | $10 Store Credit |                 |
| cryptoblogger     | $5 Store Credit  |                 |
| MetaJungle        | $5 Store Credit  |                 |
| BennyZ            | $10 Store Credit | smashngrab77    |
| NiftyMetaGirl     | $5 Store Credit  |                 |
| MetaJungle        | $10 Store Credit |                 |
| Titomachado       | $25 Store Credit |                 |
| Jeffslugs         | $10 Store Credit | radishkabal6    |
| MetaJungle        | $10 Store Credit |                 |
| Ronfresco         | $5 Store Credit  |                 |
| Ronfresco         | $5 Store Credit  |                 |
| jbbasics          | $10 Store Credit | smashngrab77    |
| Jjmccann2121      | $250 USDC        |                 |
| MetaJungle        | $5 Store Credit  |                 |
| AlphaBlok         | $5 Store Credit  |                 |
| Omgiwon           | $5 Store Credit  |                 |
| Patelh121         | $5 Store Credit  |                 |
| AlphaBlok         | $25 Store Credit |                 |
| netbe171          | $5 Store Credit  |                 |
| Mikeyj10          | $25 Store Credit |                 |
| MetaJungle        | $5 Store Credit  |                 |
| eZe-E312          | $10 Store Credit |                 |
| Bjamps            | $5 Store Credit  |                 |
| Xheryk            | $5 Store Credit  |                 |
| Patelh121         | $5 Store Credit  |                 |
| MetaJungle        | $5 Store Credit  |                 |
| MetaJungle        | $10 Store Credit |                 |
| MetaJungle        | $5 Store Credit  |                 |
| Cloud             | $10 Store Credit |                 |
| MetaJungle        | $25 Store Credit |                 |
| Me-Degen          | $5 Store Credit  |                 |
| MetaJungle        | $10 Store Credit | radishkabal6    |
| Leighham          | $25 Store Credit |                 |
| gozags            | $5 Store Credit  |                 |
| Birdman03         | $5 Store Credit  |                 |
| bpfergu           | $5 Store Credit  |                 |
| Bjamps            | $5 Store Credit  |                 |
| PhillyWill        | $10 Store Credit |                 |
| MetaJungle        | $10 Store Credit |                 |
| PhillyWill        | $10 Store Credit |                 |
| thampster         | $10 Store Credit |                 |
| AlphaBlok         | $5 Store Credit  |                 |
| Schmoe            | $25 Store Credit |                 |
| AlphaBlok         | $5 Store Credit  |                 |
| cph626            | $25 Store Credit |                 |
| mattcook          | $5 Store Credit  |                 |
| jenndunn12m       | $10 Store Credit |                 |
| Xheryk            | $10 Store Credit |                 |
| MetaJungle        | $5 Store Credit  |                 |
| Daveliz55         | $1000 USDC       | radishkabal6    |
| TheStranger       | $5 Store Credit  |                 |
| Billcot           | $5 Store Credit  |                 |
| MetaJungle        | $5 Store Credit  |                 |
| Ronfresco         | $5 Store Credit  |                 |
| Centerpiece       | $5 Store Credit  |                 |
| Chicagows213      | $5 Store Credit  |                 |
| MetaJungle        | $10 Store Credit |                 |
| Ronfresco         | $125 USDC        |                 |
| MetaJungle        | $5 Store Credit  |                 |
| thampster         | $10 Store Credit | smashngrab77    |
| Xheryk            | $5 Store Credit  |                 |
| JohnnyClutchCards | $10 Store Credit |                 |
| OG151             | $10 Store Credit |                 |
| MetaJungle        | $25 Store Credit |                 |
| Madvolker         | $5 Store Credit  | subhubgrading   |
| MetaJungle        | $10 Store Credit |                 |
| AlphaBlok         | $10 Store Credit |                 |
| Ronfresco         | $5 Store Credit  |                 |
| Ronfresco         | $10 Store Credit |                 |
| AlphaBlok         | $25 Store Credit |                 |
| MetaJungle        | $5 Store Credit  |                 |
| MetaJungle        | $5 Store Credit  |                 |
| MetaJungle        | $5 Store Credit  |                 |
| Patelh121         | $25 Store Credit |                 |
| AlphaBlok         | $10 Store Credit |                 |
| AlphaBlok         | $5 Store Credit  |                 |
| Bjamps            | $5 Store Credit  |                 |
| mattcook          | $5 Store Credit  |                 |
| CookEMnstR22      | $5 Store Credit  |                 |
| Kyled005          | $10 Store Credit |                 |
| Schmoe            | $5 Store Credit  |                 |
| MetaJungle        | $5 Store Credit  |                 |
| Ronfresco         | $5 Store Credit  |                 |
| MetaJungle        | $10 Store Credit |                 |
| Kphamilton        | $10 Store Credit |                 |
| PhillyWill        | $5 Store Credit  |                 |
| AlphaBlok         | $10 Store Credit |                 |
| NiftyMetaGirl     | $10 Store Credit |                 |
| accordingtohen    | $10 Store Credit | smashngrab77    |
| big_bees          | $25 Store Credit | yoyo909         |
| SDYote            | $5 Store Credit  |                 |
| Steffen2121       | $5 Store Credit  |                 |
| Omgiwon           | $10 Store Credit |                 |
| Newlin99          | $10 Store Credit |                 |
| Mvenekam          | $10 Store Credit |                 |
| Schmoe            | $10 Store Credit |                 |
| cph626            | $10 Store Credit |                 |
| cph626            | $5 Store Credit  |                 |
| AlphaBlok         | $5 Store Credit  | smashngrab77    |
| DangerSC          | $5 Store Credit  |                 |
| cph626            | $5 Store Credit  |                 |
| Rockitect         | $5 Store Credit  |                 |
| MetaJungle        | $10 Store Credit |                 |
| BigDobs           | $5 Store Credit  |                 |
| accordingtohen    | $25 Store Credit |                 |
| AlphaBlok         | $5 Store Credit  |                 |
| Ronfresco         | $5 Store Credit  |                 |
| AlphaBlok         | $10 Store Credit |                 |
| MetaJungle        | $5 Store Credit  |                 |
| Brian             | $25 Store Credit |                 |
| Cloud             | $5 Store Credit  |                 |
| Patelh121         | $10 Store Credit |                 |
| MetaJungle        | $5 Store Credit  |                 |
| Ronfresco         | $5 Store Credit  |                 |
| Jjmccann2121      | $5 Store Credit  |                 |
| Xheryk            | $5 Store Credit  |                 |
| bmw1909           | $25 Store Credit |                 |
| MetaJungle        | $5 Store Credit  |                 |
| Patelh121         | $5 Store Credit  | bluetitans19    |
| AlphaBlok         | $10 Store Credit |                 |
| jbbasics          | $5 Store Credit  |                 |
| Guvv              | $10 Store Credit |                 |
| Bjamps            | $5 Store Credit  |                 |
| Schmoe            | $5 Store Credit  |                 |
| AlphaBlok         | $5 Store Credit  |                 |
| NiftyMetaGirl     | $10 Store Credit |                 |
| Daveliz55         | $10 Store Credit | viking91107     |
| AlphaBlok         | $5 Store Credit  |                 |
| Billcot           | $10 Store Credit |                 |
| Ronfresco         | $5 Store Credit  |                 |
| Jalbo1            | $5 Store Credit  |                 |
| Jalbo1            | $25 Store Credit |                 |
| MetaJungle        | $10 Store Credit |                 |
| mattcook          | $5 Store Credit  |                 |
| TexHooper         | $5 Store Credit  |                 |
| Bjamps            | $5 Store Credit  |                 |
| cryptoblogger     | $5 Store Credit  |                 |
| College31         | $10 Store Credit |                 |
| Kyled005          | $10 Store Credit |                 |
| thampster         | $10 Store Credit | smashngrab77    |
| College31         | $10 Store Credit |                 |
| SDYote            | $5 Store Credit  |                 |
| Leighham          | $25 Store Credit | davidpatrick08  |
| iiiericiii        | $5 Store Credit  |                 |
| AlphaBlok         | $5 Store Credit  |                 |
| rilbiz            | $5 Store Credit  |                 |
| mattcook          | $10 Store Credit |                 |
| Billcot           | $10 Store Credit |                 |
| MetaJungle        | $5 Store Credit  |                 |
| Me-Degen          | $5 Store Credit  |                 |
| BennyZ            | $10 Store Credit | davidpatrick08  |
| Daveliz55         | $5 Store Credit  |                 |
| TheRipper         | $5 Store Credit  |                 |
| EsotericPA        | $125 USDC        |                 |
| Billcot           | $5 Store Credit  |                 |
| Schmoe            | $5 Store Credit  |                 |
| MetaJungle        | $5 Store Credit  |                 |
| MetaJungle        | $5 Store Credit  |                 |
| gozags            | $10 Store Credit |                 |
| drcrazy           | $10 Store Credit |                 |
| FlyingNinja       | $10 Store Credit |                 |
| Madvolker         | $10 Store Credit |                 |
| Patelh121         | $10 Store Credit |                 |
| MetaJungle        | $5 Store Credit  |                 |
| Phisigfsu         | $5 Store Credit  |                 |
| AlphaBlok         | $5 Store Credit  |                 |
| AlphaBlok         | $5 Store Credit  |                 |
| cph626            | $10 Store Credit |                 |
| Madvolker         | $5 Store Credit  |                 |
| mattcook          | $5 Store Credit  |                 |
| MetaJungle        | $5 Store Credit  |                 |
| AlphaBlok         | $10 Store Credit |                 |
| Patelh121         | $5 Store Credit  |                 |
| Donk3ykong81      | $5 Store Credit  |                 |
| MetaJungle        | $10 Store Credit |                 |
| pcahiwat          | $10 Store Credit |                 |
| Nymcards          | $10 Store Credit |                 |
| Bsusko            | $5 Store Credit  |                 |
| Jalbo1            | $10 Store Credit |                 |
| MetaJungle        | $5 Store Credit  |                 |
| Patelh121         | $25 Store Credit |                 |
| Ronfresco         | $5 Store Credit  | viking91107     |
| EpsilonDelta1203  | $10 Store Credit |                 |
| AlphaBlok         | $10 Store Credit |                 |
| MetaJungle        | $5 Store Credit  |                 |
| Patelh121         | $10 Store Credit | radishkabal6    |
| MetaJungle        | $5 Store Credit  |                 |
| Schmoe            | $250 USDC        | radishkabal6    |
| bmw1909           | $10 Store Credit |                 |
| Ronfresco         | $10 Store Credit |                 |
| cryptoblogger     | $5 Store Credit  | viking91107     |
| Patelh121         | $5 Store Credit  |                 |
| Schmoe            | $5 Store Credit  |                 |
| mattcook          | $5 Store Credit  |                 |
| Brftw             | $25 Store Credit |                 |
| mjzastrow1        | $5 Store Credit  |                 |
| 2048              | $10 Store Credit |                 |
| Rooktiss          | $5 Store Credit  |                 |
| Me-Degen          | $5 Store Credit  |                 |
| MetaJungle        | $5 Store Credit  |                 |
| sheltronica       | $5 Store Credit  |                 |
| AlphaBlok         | $5 Store Credit  |                 |
| mattcook          | $5 Store Credit  |                 |
| Charlotteann      | $25 Store Credit |                 |
| cph626            | $25 Store Credit |                 |
| jdbeltz           | $10 Store Credit |                 |
| MetaJungle        | $10 Store Credit |                 |
| AlphaBlok         | $10 Store Credit |                 |
| cph626            | $5 Store Credit  |                 |
| PhillyWill        | $5 Store Credit  |                 |
| MetaJungle        | $25 Store Credit |                 |
| MetaJungle        | $5 Store Credit  |                 |
| Jjmccann2121      | $5 Store Credit  | viking91107     |
| drcrazy           | $5 Store Credit  |                 |
| MetaJungle        | $5 Store Credit  |                 |
| College31         | $10 Store Credit |                 |
| AlphaBlok         | $10 Store Credit |                 |
| MetaJungle        | $10 Store Credit |                 |
| MetaJungle        | $5 Store Credit  |                 |
| MetaJungle        | $5 Store Credit  |                 |
| MetaJungle        | $5 Store Credit  |                 |
| MetaJungle        | $10 Store Credit |                 |
| AlphaBlok         | $5 Store Credit  |                 |
| Ronfresco         | $5 Store Credit  | billfd          |
| MetaJungle        | $5 Store Credit  |                 |
| Jjmccann2121      | $5 Store Credit  |                 |
| BigDobs           | $10 Store Credit |                 |
| jdbeltz           | $5 Store Credit  |                 |
| cph626            | $10 Store Credit |                 |
| eZe-E312          | $10 Store Credit |                 |
| Bjamps            | $10 Store Credit |                 |
| MetaJungle        | $10 Store Credit |                 |
| Madvolker         | $5 Store Credit  |                 |
| Roux1310          | $25 Store Credit |                 |
| davejr81          | $5 Store Credit  |                 |
| 0000              | $5 Store Credit  |                 |
| Ronfresco         | $250 USDC        |                 |
| bmw1909           | $5 Store Credit  |                 |
| EsotericPA        | $10 Store Credit |                 |
| akicks            | $25 Store Credit |                 |
| Newlin99          | $5 Store Credit  |                 |
| MetaJungle        | $5 Store Credit  |                 |
| Schmoe            | $5 Store Credit  |                 |
| TheGOAT           | $5 Store Credit  |                 |
| MetaJungle        | $5 Store Credit  | chgolitigator   |
| MetaJungle        | $5 Store Credit  |                 |
| njzastrow1        | $10 Store Credit |                 |
| AlphaBlok         | $5 Store Credit  |                 |
| Roux1310          | $5 Store Credit  |                 |
| JohnnyClutchCards | $5 Store Credit  |                 |
| Ronfresco         | $5 Store Credit  |                 |
| bmw1909           | $25 Store Credit |                 |
| Ronfresco         | $5 Store Credit  |                 |
| Rjj007            | $25 Store Credit |                 |
| MetaJungle        | $10 Store Credit |                 |
| Steffen2121       | $25 Store Credit | galileo         |
| cryptoblogger     | $25 Store Credit |                 |
| cph626            | $5 Store Credit  |                 |
| MetaJungle        | $10 Store Credit |                 |
| MetaJungle        | $5 Store Credit  |                 |
| MetaJungle        | $10 Store Credit |                 |
| mattcook          | $5 Store Credit  |                 |
| MetaJungle        | $5 Store Credit  |                 |
| Gamerchick39      | $5 Store Credit  |                 |
| MetaJungle        | $5 Store Credit  |                 |
| AlphaBlok         | $10 Store Credit |                 |
| jdbeltz           | $10 Store Credit |                 |
| Leighham          | $5 Store Credit  |                 |
| MetaJungle        | $5 Store Credit  |                 |
| MetaJungle        | $10 Store Credit |                 |
| 2048              | $10 Store Credit | radishkabal6    |
| MetaJungle        | $10 Store Credit |                 |
| Xheryk            | $5 Store Credit  |                 |
| MetaJungle        | $25 Store Credit |                 |
| Xheryk            | $5 Store Credit  |                 |
| MetaJungle        | $10 Store Credit |                 |
| Bjamps            | $5 Store Credit  |                 |
| Patelh121         | $5 Store Credit  |                 |
| AlphaBlok         | $5 Store Credit  |                 |
| mattcook          | $5 Store Credit  |                 |
| NiftyMetaGirl     | $10 Store Credit |                 |
| MetaJungle        | $5 Store Credit  |                 |
| Jbrown1310        | $10 Store Credit |                 |
| AlphaBlok         | $5 Store Credit  |                 |
| Patelh121         | $10 Store Credit |                 |
| cryptoblogger     | $10 Store Credit |                 |
| AlphaBlok         | $5 Store Credit  |                 |
| MetaJungle        | $5 Store Credit  |                 |
| Andrewgarrett41   | $5 Store Credit  |                 |
| MetaJungle        | $10 Store Credit |                 |
| cph626            | $10 Store Credit |                 |
| MetaJungle        | $10 Store Credit | milvec          |
| MetaJungle        | $25 Store Credit |                 |
| MetaJungle        | $10 Store Credit |                 |
| deleonlakers2000  | $10 Store Credit | radishkabal6    |
| Billcot           | $150 USDC        |                 |
| Schmoe            | $5 Store Credit  |                 |
| Patelh121         | $5 Store Credit  |                 |
| big_bees          | $5 Store Credit  |                 |
| MetaJungle        | $10 Store Credit |                 |
| SDYote            | $5 Store Credit  |                 |
| Xheryk            | $10 Store Credit |                 |
| AlphaBlok         | $25 Store Credit | yoyo909         |
| MetaJungle        | $25 Store Credit |                 |
| cph626            | $5 Store Credit  |                 |
| Kphamilton        | $5 Store Credit  | smashngrab77    |
| Bjamps            | $10 Store Credit |                 |
| Schmoe            | $5 Store Credit  |                 |
| jbbasics          | $10 Store Credit |                 |
| mattcook          | $10 Store Credit |                 |
| Xheryk            | $5 Store Credit  |                 |
| Steffen2121       | $25 Store Credit |                 |
| MetaJungle        | $5 Store Credit  |                 |
| westau            | $5 Store Credit  | radishkabal6    |
| MetaJungle        | $25 Store Credit |                 |
| MetaJungle        | $5 Store Credit  |                 |
| cph626            | $5 Store Credit  |                 |
| mattcook          | $25 Store Credit |                 |
| NiftyMetaGirl     | $10 Store Credit |                 |
| cryptoblogger     | $10 Store Credit | radishkabal6    |
| Xheryk            | $5 Store Credit  |                 |
| NiftyMetaGirl     | $25 Store Credit |                 |
| Kyled005          | $10 Store Credit |                 |
| jdbeltz           | $5 Store Credit  |                 |
| Bjamps            | $5 Store Credit  |                 |
| Xheryk            | $10 Store Credit |                 |
| NiftyMetaGirl     | $5 Store Credit  |                 |
| Bjamps            | $5 Store Credit  |                 |
| Billcot           | $10 Store Credit |                 |
| AlphaBlok         | $5 Store Credit  |                 |
| thampster         | $10 Store Credit |                 |
| Madvolker         | $25 Store Credit |                 |
| 0000              | $10 Store Credit |                 |
| MetaJungle        | $5 Store Credit  | chgolitigator   |
| deleonlakers2000  | $25 Store Credit |                 |
| Ronfresco         | $5 Store Credit  |                 |
| Bjamps            | $5 Store Credit  |                 |
| BigDobs           | $10 Store Credit |                 |
| MetaJungle        | $5 Store Credit  |                 |
| Steffen2121       | $10 Store Credit |                 |
| Bjamps            | $10 Store Credit |                 |
| Ronfresco         | $25 Store Credit |                 |
| Jalbo1            | $25 Store Credit |                 |
| mattcook          | $5 Store Credit  | radishkabal6    |
| BigDobs           | $5 Store Credit  |                 |
| Madvolker         | $10 Store Credit |                 |
| Mikeyj10          | $10 Store Credit |                 |
| MetaJungle        | $25 Store Credit |                 |
| MetaJungle        | $5 Store Credit  |                 |
| Ronfresco         | $10 Store Credit |                 |
| gozags            | $25 Store Credit | smashngrab77    |
| cph626            | $5 Store Credit  |                 |
| AlphaBlok         | $10 Store Credit |                 |
| MetaJungle        | $10 Store Credit |                 |
| 0000              | $5 Store Credit  |                 |
| Omgiwon           | $10 Store Credit |                 |
| AlphaBlok         | $10 Store Credit |                 |
| vinnymac11        | $5 Store Credit  |                 |
| MetaJungle        | $5 Store Credit  |                 |
| AlphaBlok         | $5 Store Credit  |                 |
| Patelh121         | $10 Store Credit |                 |
| Schmoe            | $10 Store Credit |                 |
| TheStranger       | $5 Store Credit  |                 |
| MetaJungle        | $5 Store Credit  |                 |
| College31         | $5 Store Credit  |                 |
| Schmoe            | $10 Store Credit |                 |
| Crispjb           | $10 Store Credit |                 |
| MetaJungle        | $25 Store Credit |                 |
| Patelh121         | $10 Store Credit |                 |
| Tsage225          | $10 Store Credit |                 |
| ginobili_fan      | $5 Store Credit  |                 |
| Davbruce21        | $5 Store Credit  |                 |
| Madvolker         | $5 Store Credit  | galileo         |
| 1of1_sportscards  | $10 Store Credit |                 |
| AlphaBlok         | $10 Store Credit |                 |
| JohnnyClutchCards | $5 Store Credit  |                 |
| Phisigfsu         | $10 Store Credit |                 |
| Brian             | $5 Store Credit  |                 |
| gozags            | $25 Store Credit |                 |
| Patelh121         | $5 Store Credit  |                 |
| AlphaBlok         | $25 Store Credit |                 |
| Schmoe            | $5 Store Credit  | bluetitans19    |
| EsotericPA        | $5 Store Credit  | billfd          |
| mattcook          | $5 Store Credit  |                 |
| MetaJungle        | $5 Store Credit  |                 |
| Ronfresco         | $5 Store Credit  |                 |
| mattcook          | $10 Store Credit |                 |
| Titomachado       | $5 Store Credit  |                 |
| gozags            | $150 USDC        |                 |
| Schmoe            | $5 Store Credit  |                 |
| Billcot           | $5 Store Credit  |                 |
| El_Camino         | $5 Store Credit  |                 |
| bmw1909           | $10 Store Credit | galileo         |
| eZe-E312          | $10 Store Credit |                 |
| davejr81          | $5 Store Credit  | byuofu          |
| Mvenekam          | $25 Store Credit |                 |
| MetaJungle        | $10 Store Credit |                 |
| Ronfresco         | $10 Store Credit |                 |
| Schmoe            | $5 Store Credit  |                 |
| Patelh121         | $5 Store Credit  |                 |
| 1of1_sportscards  | $5 Store Credit  |                 |
| mattcook          | $5 Store Credit  |                 |
| AlphaBlok         | $5 Store Credit  |                 |
| RobP343           | $5 Store Credit  |                 |
| AlphaBlok         | $5 Store Credit  |                 |
| MetaJungle        | $5 Store Credit  |                 |
| jenndunn12m       | $25 Store Credit |                 |
| MetaJungle        | $5 Store Credit  |                 |
| jdbeltz           | $5 Store Credit  |                 |
| PhillyWill        | $5 Store Credit  |                 |
| MetaJungle        | $5 Store Credit  |                 |
| MetaJungle        | $25 Store Credit |                 |
| mattcook          | $5 Store Credit  |                 |
| deleonlakers2000  | $25 Store Credit |                 |
| Billcot           | $10 Store Credit |                 |
| AlphaBlok         | $5 Store Credit  |                 |
| Roux1310          | $5 Store Credit  |                 |
| mattcook          | $5 Store Credit  |                 |
| BigDobs           | $25 Store Credit |                 |
| Schmoe            | $5 Store Credit  |                 |
| Xheryk            | $5 Store Credit  |                 |
| cryptoblogger     | $5 Store Credit  |                 |
| Bjamps            | $10 Store Credit |                 |
| College31         | $5 Store Credit  |                 |
| MetaJungle        | $25 Store Credit |                 |
| AlphaBlok         | $5 Store Credit  |                 |
| 0000              | $10 Store Credit |                 |
| Schmoe            | $5 Store Credit  |                 |
| AlphaBlok         | $5 Store Credit  |                 |
| MetaJungle        | $5 Store Credit  |                 |
| Guvv              | $5 Store Credit  |                 |
| Ronfresco         | $10 Store Credit |                 |
| MetaJungle        | $10 Store Credit |                 |
| MetaJungle        | $5 Store Credit  |                 |
| bmw1909           | $50 USDC         |                 |
| Tsage225          | $25 Store Credit |                 |
| Xheryk            | $10 Store Credit |                 |
| Billcot           | $25 Store Credit |                 |
| Newlin99          | $10 Store Credit |                 |
| mattcook          | $25 Store Credit |                 |
| mattcook          | $10 Store Credit |                 |
| Schmoe            | $10 Store Credit |                 |
| Omgiwon           | $5 Store Credit  |                 |
| timmay_castags    | $5 Store Credit  |                 |
| bmw1909           | $10 Store Credit |                 |
| AlphaBlok         | $10 Store Credit |                 |
| BigDobs           | $5 Store Credit  |                 |
| iiiericiii        | $5 Store Credit  |                 |
| netbe171          | $5 Store Credit  |                 |
| Bjamps            | $10 Store Credit |                 |
| MetaJungle        | $5 Store Credit  |                 |
| bmw1909           | $10 Store Credit |                 |
| wisrhino          | $150 USDC        |                 |
| 0000              | $10 Store Credit |                 |
| TexHooper         | $10 Store Credit |                 |
| AlphaBlok         | $25 Store Credit |                 |
| Bjamps            | $5 Store Credit  |                 |
| Crispjb           | $5 Store Credit  |                 |
| gozags            | $10 Store Credit |                 |
| Ronfresco         | $5 Store Credit  |                 |
| AlphaBlok         | $5 Store Credit  |                 |
| jdbeltz           | $5 Store Credit  |                 |
| PhillyWill        | $10 Store Credit |                 |
| College31         | $10 Store Credit |                 |
| MetaJungle        | $10 Store Credit |                 |
| bmw1909           | $10 Store Credit | galileo         |
| AlphaBlok         | $10 Store Credit |                 |
| Infininight       | $5 Store Credit  |                 |
| jmyers81          | $5 Store Credit  |                 |
| MetaJungle        | $10 Store Credit |                 |
| rilbiz            | $10 Store Credit |                 |
| AlphaBlok         | $10 Store Credit | yoyo909         |
| NiftyMetaGirl     | $5 Store Credit  |                 |
| Madvolker         | $5 Store Credit  |                 |
| PhillyWill        | $5 Store Credit  |                 |
| Madvolker         | $50 USDC         |                 |
| Schmoe            | $25 Store Credit | milvec          |
| MetaJungle        | $5 Store Credit  |                 |
| AlphaBlok         | $10 Store Credit |                 |
| MetaJungle        | $5 Store Credit  |                 |
| GIAunit           | $10 Store Credit |                 |
| Schmoe            | $5 Store Credit  |                 |
| Patelh121         | $5 Store Credit  |                 |
| Bjamps            | $10 Store Credit |                 |
| netbe171          | $5 Store Credit  |                 |
| Roux1310          | $5 Store Credit  |                 |
| Ronfresco         | $10 Store Credit |                 |
| MetaJungle        | $10 Store Credit |                 |
| AlphaBlok         | $5 Store Credit  |                 |
| College31         | $10 Store Credit |                 |
| Patelh121         | $10 Store Credit |                 |
| MetaJungle        | $5 Store Credit  |                 |
| Bjamps            | $5 Store Credit  |                 |
| AlphaBlok         | $5 Store Credit  |                 |
| ghedoicy          | $25 Store Credit | thecardfarmers  |
| MetaJungle        | $250 USDC        |                 |
| BigDobs           | $5 Store Credit  |                 |
| AlphaBlok         | $10 Store Credit |                 |
| MetaJungle        | $5 Store Credit  |                 |
| Omgiwon           | $25 Store Credit |                 |
| Mgmonaco11        | $10 Store Credit | bbv00248        |
| Billcot           | $5 Store Credit  |                 |
| EsotericPA        | $10 Store Credit |                 |
| Xheryk            | $5 Store Credit  |                 |
| mattcook          | $5 Store Credit  |                 |
| AlphaBlok         | $10 Store Credit |                 |
| MetaJungle        | $10 Store Credit |                 |
| PhillyWill        | $5 Store Credit  |                 |
| MetaJungle        | $10 Store Credit |                 |
| Cloud             | $5 Store Credit  | davidpatrick08  |
| AlphaBlok         | $5 Store Credit  |                 |
| eZe-E312          | $5 Store Credit  |                 |
| Brftw             | $5 Store Credit  |                 |
| NiftyMetaGirl     | $5 Store Credit  |                 |
| Bjamps            | $10 Store Credit |                 |
| Omgiwon           | $5 Store Credit  |                 |
| Xheryk            | $10 Store Credit |                 |
| Omgiwon           | $5 Store Credit  |                 |
| Brftw             | $5 Store Credit  | smashngrab77    |
| mattcook          | $10 Store Credit |                 |
| MetaJungle        | $5 Store Credit  |                 |
| Tsage225          | $10 Store Credit |                 |
| AlphaBlok         | $5 Store Credit  |                 |
| Crispjb           | $5 Store Credit  |                 |
| Schmoe            | $5 Store Credit  |                 |
| MetaJungle        | $10 Store Credit |                 |
| cph626            | $5 Store Credit  |                 |
| Madvolker         | $5 Store Credit  |                 |
| Jjmccann2121      | $5 Store Credit  |                 |
| MetaJungle        | $5 Store Credit  |                 |
| bpfergu           | $5 Store Credit  |                 |
| cph626            | $25 Store Credit |                 |
| Ronfresco         | $10 Store Credit |                 |
| Patelh121         | $25 Store Credit |                 |
| BigDobs           | $25 Store Credit |                 |
| heffery           | $5 Store Credit  |                 |
| Phisigfsu         | $5 Store Credit  |                 |
| mattcook          | $10 Store Credit |                 |
| AlphaBlok         | $25 Store Credit |                 |
| JohnnyClutchCards | $5 Store Credit  |                 |
| Schmoe            | $10 Store Credit |                 |
| MetaJungle        | $25 Store Credit |                 |
| MetaJungle        | $5 Store Credit  |                 |
| Omgiwon           | $5 Store Credit  |                 |
| MetaJungle        | $5 Store Credit  |                 |
| cph626            | $5 Store Credit  |                 |
| AlphaBlok         | $10 Store Credit |                 |
| cph626            | $25 Store Credit |                 |
| MetaJungle        | $5 Store Credit  |                 |
| Patelh121         | $10 Store Credit | viking91107     |
| Bjamps            | $5 Store Credit  |                 |
| BigDobs           | $5 Store Credit  |                 |
| Omgiwon           | $5 Store Credit  |                 |
| Charlotteann      | $5 Store Credit  |                 |
| MetaJungle        | $5 Store Credit  |                 |
| bmw1909           | $10 Store Credit | smashngrab77    |
| TheGOAT           | $5 Store Credit  |                 |
| MetaJungle        | $10 Store Credit |                 |
| thampster         | $5 Store Credit  |                 |
| dhoovey           | $25 Store Credit |                 |
| Andrewgarrett41   | $5 Store Credit  |                 |
| MetaJungle        | $25 Store Credit |                 |
| AlphaBlok         | $25 Store Credit |                 |
| Patelh121         | $5 Store Credit  |                 |
| Xheryk            | $5 Store Credit  |                 |
| cph626            | $10 Store Credit |                 |
| Xheryk            | $5 Store Credit  |                 |
| TheStranger       | $5 Store Credit  |                 |
| SDYote            | $5 Store Credit  |                 |
| Xheryk            | $5 Store Credit  |                 |
| MetaJungle        | $125 USDC        |                 |
| Roux1310          | $25 Store Credit |                 |
| AlphaBlok         | $5 Store Credit  |                 |
| MetaJungle        | $5 Store Credit  |                 |
| MetaJungle        | $5 Store Credit  |                 |
| MetaJungle        | $5 Store Credit  | smashngrab77    |
| Ronfresco         | $5 Store Credit  |                 |
| MetaJungle        | $5 Store Credit  |                 |
| bpfergu           | $5 Store Credit  | radishkabal6    |
| Steffen2121       | $5 Store Credit  |                 |
| balward           | $10 Store Credit |                 |
| Ronfresco         | $5 Store Credit  |                 |
| MetaJungle        | $10 Store Credit |                 |
| NiftyMetaGirl     | $5 Store Credit  |                 |
| Ronfresco         | $10 Store Credit | galileo         |
| cph626            | $5 Store Credit  |                 |
| MetaJungle        | $10 Store Credit |                 |
| GIAunit           | $5 Store Credit  |                 |
| Bjamps            | $5 Store Credit  |                 |
| Charlotteann      | $5 Store Credit  |                 |
| Ronfresco         | $25 Store Credit |                 |
| antimatter        | $5 Store Credit  |                 |
| Gamerchick39      | $10 Store Credit |                 |
| SDYote            | $5 Store Credit  |                 |
| Ronfresco         | $25 Store Credit |                 |
| BigDobs           | $5 Store Credit  |                 |
| Patelh121         | $10 Store Credit |                 |
| Ronfresco         | $25 Store Credit | galileo         |
| DangerSC          | $5 Store Credit  |                 |
| NiftyMetaGirl     | $5 Store Credit  |                 |
| Bsusko            | $5 Store Credit  |                 |
| Roux1310          | $10 Store Credit |                 |
| AlphaBlok         | $5 Store Credit  |                 |
| MetaJungle        | $25 Store Credit |                 |
| heffery           | $5 Store Credit  |                 |
| Me-Degen          | $5 Store Credit  |                 |
| Jeffslugs         | $10 Store Credit |                 |
| Crispjb           | $5000 USDC       |                 |
| Schmoe            | $25 Store Credit |                 |
| MetaJungle        | $10 Store Credit |                 |
| MetaJungle        | $5 Store Credit  |                 |
| Steffen2121       | $5 Store Credit  |                 |
| OG151             | $5 Store Credit  |                 |
| MetaJungle        | $5 Store Credit  |                 |
| iiiericiii        | $150 USDC        |                 |
| Schmoe            | $25 Store Credit |                 |
| Billcot           | $5 Store Credit  |                 |
| MetaJungle        | $25 Store Credit |                 |
| Bjamps            | $5 Store Credit  |                 |
| Patelh121         | $5 Store Credit  |                 |
| big_bees          | $5 Store Credit  |                 |
| Schmoe            | $5 Store Credit  |                 |
| MetaJungle        | $5 Store Credit  |                 |
| pcahiwat          | $5 Store Credit  |                 |
| MetaJungle        | $5 Store Credit  |                 |
| accordingtohen    | $5 Store Credit  |                 |
| MetaJungle        | $10 Store Credit |                 |
| AlphaBlok         | $10 Store Credit |                 |
| AlphaBlok         | $25 Store Credit |                 |
| Xheryk            | $10 Store Credit |                 |
| Jjmccann2121      | $5 Store Credit  |                 |
| gozags            | $10 Store Credit |                 |
| mattcook          | $25 Store Credit |                 |
| Patelh121         | $10 Store Credit |                 |
| gozags            | $5 Store Credit  |                 |
| mattcook          | $10 Store Credit |                 |
| ghedoicy          | $5 Store Credit  |                 |
| Kyled005          | $25 Store Credit |                 |
| MetaJungle        | $5 Store Credit  | milvec          |
| Billcot           | $10 Store Credit |                 |
| MetaJungle        | $5 Store Credit  |                 |
| Xheryk            | $5 Store Credit  |                 |
| wisrhino          | $25 Store Credit |                 |
| DangerSC          | $25 Store Credit | mjno23goat      |
| MetaJungle        | $25 Store Credit | bbv00248        |
| Bjamps            | $10 Store Credit | milvec          |
| Schmoe            | $10 Store Credit |                 |
| Ronfresco         | $5 Store Credit  | radishkabal6    |
| Patelh121         | $5 Store Credit  |                 |
| cryptoblogger     | $10 Store Credit |                 |
| Billcot           | $5 Store Credit  |                 |
| Bjamps            | $25 Store Credit |                 |
| MetaJungle        | $25 Store Credit |                 |
| mattcook          | $5 Store Credit  |                 |
| MetaJungle        | $25 Store Credit |                 |
| jbbasics          | $10 Store Credit |                 |
| AlphaBlok         | $5 Store Credit  |                 |
| Schmoe            | $10 Store Credit |                 |
| Johnnykpoker      | $25 Store Credit |                 |
| bpfergu           | $10 Store Credit |                 |
| Ronfresco         | $5 Store Credit  |                 |
| Topherjack        | $5 Store Credit  |                 |
| Billcot           | $5 Store Credit  |                 |
| Titomachado       | $5 Store Credit  | radishkabal6    |
| Sashka25          | $5 Store Credit  |                 |
| MetaJungle        | $5 Store Credit  | varcak          |
| Xheryk            | $10 Store Credit |                 |
| cryptoblogger     | $10 Store Credit |                 |
| MetaJungle        | $5 Store Credit  |                 |
| Leighham          | $25 Store Credit |                 |
| MetaJungle        | $10 Store Credit |                 |
| Patelh121         | $25 Store Credit |                 |
| Ronfresco         | $25 Store Credit |                 |
| Ronfresco         | $5 Store Credit  |                 |
| BigDobs           | $5 Store Credit  |                 |
| Billcot           | $5 Store Credit  |                 |
| Kyled005          | $5 Store Credit  |                 |
| MetaJungle        | $25 Store Credit |                 |
| MetaJungle        | $5 Store Credit  |                 |
| Charlotteann      | $25 Store Credit |                 |
| bpfergu           | $5 Store Credit  |                 |
| AlphaBlok         | $5 Store Credit  |                 |
| MetaJungle        | $10 Store Credit |                 |
| Schmoe            | $10 Store Credit |                 |
| BigDobs           | $25 Store Credit |                 |
| iiiericiii        | $5 Store Credit  |                 |
| JohnnyClutchCards | $5 Store Credit  |                 |
| Billcot           | $5 Store Credit  |                 |
| MetaJungle        | $50 USDC         |                 |
| MetaJungle        | $25 Store Credit |                 |
| Roux1310          | $5 Store Credit  |                 |
| Xheryk            | $10 Store Credit |                 |
| mattcook          | $5 Store Credit  |                 |
| Xheryk            | $10 Store Credit |                 |
| bmw1909           | $5 Store Credit  |                 |
| wisrhino          | $5 Store Credit  |                 |
| Phisigfsu         | $5 Store Credit  |                 |
| Kyled005          | $5 Store Credit  |                 |
| Xheryk            | $5 Store Credit  |                 |
| tt9s              | $5 Store Credit  |                 |
| MetaJungle        | $10 Store Credit |                 |
| Bjamps            | $5 Store Credit  |                 |
| bpfergu           | $5 Store Credit  |                 |
| OG151             | $5 Store Credit  |                 |
| Birdman03         | $5 Store Credit  |                 |
| Patelh121         | $5 Store Credit  | co-d            |
| MetaJungle        | $10 Store Credit |                 |
| NiftyMetaGirl     | $5 Store Credit  |                 |
| Rodie4            | $25 Store Credit | smashngrab77    |
| mattcook          | $5 Store Credit  |                 |
| Schmoe            | $5 Store Credit  |                 |
| TexHooper         | $10 Store Credit |                 |
| Billcot           | $25 Store Credit |                 |
| mattcook          | $5 Store Credit  |                 |
| Odin7557          | $5 Store Credit  |                 |
| 0000              | $5 Store Credit  |                 |
| MetaJungle        | $5 Store Credit  |                 |
| Jimmys75          | $5 Store Credit  |                 |
| MetaJungle        | $5 Store Credit  |                 |
| gozags            | $5 Store Credit  |                 |
| JohnnyClutchCards | $5 Store Credit  |                 |
| Billcot           | $10 Store Credit |                 |
| Guvv              | $5 Store Credit  |                 |
| accordingtohen    | $5 Store Credit  |                 |
| Billcot           | $25 Store Credit | yoyo909         |
| Charlotteann      | $5 Store Credit  |                 |
| Ronfresco         | $25 Store Credit |                 |
| MetaJungle        | $5 Store Credit  |                 |
| Ronfresco         | $10 Store Credit |                 |
| MetaJungle        | $5 Store Credit  |                 |
| Crispjb           | $25 Store Credit |                 |
| Xheryk            | $10 Store Credit |                 |
| Mvenekam          | $10 Store Credit |                 |
| MetaJungle        | $10 Store Credit |                 |
| MetaJungle        | $10 Store Credit |                 |
| Steffen2121       | $5 Store Credit  |                 |
| MetaJungle        | $5 Store Credit  |                 |
| AlphaBlok         | $10 Store Credit |                 |
| MetaJungle        | $5 Store Credit  |                 |
| mattcook          | $10 Store Credit |                 |
| MetaJungle        | $5 Store Credit  |                 |
| MetaJungle        | $150 USDC        |                 |
| Brftw             | $25 Store Credit |                 |
| Schmoe            | $5 Store Credit  |                 |
| Ronfresco         | $10 Store Credit |                 |
| Omgiwon           | $10 Store Credit |                 |
| cryptoblogger     | $5 Store Credit  |                 |
| MetaJungle        | $10 Store Credit |                 |
| 1of1_sportscards  | $5 Store Credit  | radishkabal6    |
| Schmoe            | $5 Store Credit  |                 |
| Billcot           | $10 Store Credit |                 |
| MetaJungle        | $10 Store Credit |                 |
| MetaJungle        | $5 Store Credit  |                 |
| jbbasics          | $10 Store Credit |                 |
| AlphaBlok         | $25 Store Credit |                 |
| MetaJungle        | $25 Store Credit | smashngrab77    |
| Xheryk            | $5 Store Credit  |                 |
| Ronfresco         | $5 Store Credit  |                 |
| MetaJungle        | $25 Store Credit |                 |
| bpfergu           | $5 Store Credit  |                 |
| MetaJungle        | $5 Store Credit  |                 |
| MetaJungle        | $25 Store Credit |                 |
| AlphaBlok         | $5 Store Credit  |                 |
| MetaJungle        | $25 Store Credit |                 |
| Ronfresco         | $250 USDC        |                 |
| AlphaBlok         | $25 Store Credit |                 |
| MetaJungle        | $5 Store Credit  |                 |
| big_bees          | $5 Store Credit  | viking91107     |
| bpfergu           | $25 Store Credit |                 |
| Roux1310          | $5 Store Credit  |                 |
| Bjamps            | $5 Store Credit  |                 |
| MetaJungle        | $10 Store Credit |                 |
| Patelh121         | $150 USDC        |                 |
| mattcook          | $10 Store Credit |                 |
| MetaJungle        | $10 Store Credit |                 |
| MetaJungle        | $10 Store Credit |                 |
| MetaJungle        | $5 Store Credit  |                 |
| bmw1909           | $10 Store Credit |                 |
| Kphamilton        | $5 Store Credit  |                 |
| cryptoblogger     | $5 Store Credit  |                 |
| Xheryk            | $10 Store Credit |                 |
| MetaJungle        | $25 Store Credit |                 |
| JBAtlFalcons      | $25 Store Credit |                 |
| TheGOAT           | $5 Store Credit  | viking91107     |
| MetaJungle        | $10 Store Credit |                 |
| FlyingNinja       | $5 Store Credit  |                 |
| MetaJungle        | $25 Store Credit |                 |
| Kyled005          | $25 Store Credit | galileo         |
| MetaJungle        | $5 Store Credit  |                 |
| AlphaBlok         | $25 Store Credit |                 |
| Schmoe            | $5 Store Credit  |                 |
| Bjamps            | $5 Store Credit  |                 |
| cryptoblogger     | $5 Store Credit  |                 |
| Jjmccann2121      | $5 Store Credit  |                 |
| drpineapplez      | $5 Store Credit  |                 |
| EpsilonDelta1203  | $5 Store Credit  |                 |
| 2048              | $5 Store Credit  |                 |
| JohnnyClutchCards | $5 Store Credit  |                 |
| MetaJungle        | $5 Store Credit  |                 |
| BigDobs           | $5 Store Credit  |                 |
| Ronfresco         | $10 Store Credit | smashngrab77    |
| AlphaBlok         | $10 Store Credit |                 |
| AlphaBlok         | $10 Store Credit |                 |
| Omgiwon           | $5 Store Credit  | radishkabal6    |
| Xheryk            | $150 USDC        |                 |
| cph626            | $5 Store Credit  |                 |
| Phisigfsu         | $25 Store Credit |                 |
| cph626            | $5 Store Credit  |                 |
| AlphaBlok         | $10 Store Credit |                 |
| mattcook          | $5 Store Credit  |                 |
| AlphaBlok         | $25 Store Credit |                 |
| Sashka25          | $5 Store Credit  |                 |
| gozags            | $5 Store Credit  |                 |
| MetaJungle        | $5 Store Credit  |                 |
| Bjamps            | $10 Store Credit |                 |
| MetaJungle        | $5 Store Credit  |                 |
| cryptoblogger     | $5 Store Credit  |                 |
| JohnnyClutchCards | $25 Store Credit |                 |
| bmw1909           | $5 Store Credit  |                 |
| DangerSC          | $10 Store Credit |                 |
| DangerSC          | $10 Store Credit | dog29           |
| AlphaBlok         | $10 Store Credit |                 |
| EsotericPA        | $5 Store Credit  |                 |
| Ronfresco         | $5 Store Credit  |                 |
| accordingtohen    | $5 Store Credit  |                 |
| bmw1909           | $10 Store Credit |                 |
| Ronfresco         | $5 Store Credit  |                 |
| bmw1909           | $5 Store Credit  | bbv00248        |
| Carofine          | $5 Store Credit  |                 |
| MetaJungle        | $5 Store Credit  | galileo         |
| Steffen2121       | $25 Store Credit |                 |
| MetaJungle        | $5 Store Credit  |                 |
| TheGOAT           | $5 Store Credit  |                 |
| Ronfresco         | $5 Store Credit  |                 |
| AlphaFIVE         | $25 Store Credit |                 |
| MetaJungle        | $10 Store Credit | yoyo909         |
| mattcook          | $5 Store Credit  |                 |
| PhillyWill        | $500 USDC        |                 |
| LandoLakes        | $5 Store Credit  |                 |
| jbbasics          | $5 Store Credit  |                 |
| Billcot           | $10 Store Credit |                 |
| bpfergu           | $10 Store Credit |                 |
| MetaJungle        | $5 Store Credit  |                 |
| Phisigfsu         | $10 Store Credit |                 |
| FlyingNinja       | $10 Store Credit |                 |
| Jimmys75          | $10 Store Credit |                 |
| bpfergu           | $5 Store Credit  |                 |
| MetaJungle        | $10 Store Credit |                 |
| AlphaBlok         | $25 Store Credit |                 |
| jdbeltz           | $25 Store Credit |                 |
| timmay_castags    | $5 Store Credit  | byuofu          |
| Jconc13           | $5 Store Credit  |                 |
| mattcook          | $25 Store Credit |                 |
| AlphaBlok         | $10 Store Credit |                 |
| Patelh121         | $25 Store Credit |                 |
| Xheryk            | $10 Store Credit | radishkabal6    |
| MetaJungle        | $5 Store Credit  |                 |
| AlphaBlok         | $5 Store Credit  | radishkabal6    |
| AlphaBlok         | $5 Store Credit  |                 |
| Billcot           | $10 Store Credit |                 |
| MetaJungle        | $25 Store Credit | mjno23goat      |
| MetaJungle        | $10 Store Credit |                 |
| AlphaBlok         | $5 Store Credit  |                 |
| Kobelaker824      | $5 Store Credit  |                 |
| Roux1310          | $5 Store Credit  |                 |
| MetaJungle        | $5 Store Credit  |                 |
| FlyingNinja       | $5 Store Credit  |                 |
| AlphaBlok         | $5 Store Credit  |                 |
| MetaJungle        | $5 Store Credit  | viking91107     |
| BigDobs           | $25 Store Credit |                 |
| 1of1_sportscards  | $5 Store Credit  |                 |
| Roux1310          | $10 Store Credit |                 |
| MetaJungle        | $25 Store Credit | mjno23goat      |
| AlphaBlok         | $5 Store Credit  | dfeog           |
| AlphaBlok         | $5 Store Credit  |                 |
| MetaJungle        | $5 Store Credit  |                 |
| MetaJungle        | $5 Store Credit  |                 |
| Billcot           | $10 Store Credit |                 |
| mattcook          | $10 Store Credit |                 |
| bmw1909           | $10 Store Credit |                 |
| Skybo53           | $10 Store Credit |                 |
| Madvolker         | $25 Store Credit |                 |
| mattcook          | $250 USDC        |                 |
| BennyZ            | $5 Store Credit  |                 |
| Patelh121         | $25 Store Credit |                 |
| NiftyMetaGirl     | $5 Store Credit  |                 |
| MetaJungle        | $5 Store Credit  |                 |
| JohnnyClutchCards | $25 Store Credit |                 |
| AlphaBlok         | $5 Store Credit  |                 |
| Xheryk            | $10 Store Credit |                 |
| james             | $5 Store Credit  |                 |
| MetaJungle        | $10 Store Credit |                 |
| Jjmccann2121      | $25 Store Credit | davidpatrick08  |
| tt9s              | $5 Store Credit  |                 |
| bpfergu           | $5 Store Credit  |                 |
| yop7              | $5 Store Credit  |                 |
| AlphaBlok         | $25 Store Credit |                 |
| TheStranger       | $5 Store Credit  |                 |
| Tsage225          | $5 Store Credit  |                 |
| MetaJungle        | $10 Store Credit |                 |
| MetaJungle        | $5 Store Credit  |                 |
| MetaJungle        | $5 Store Credit  |                 |
| MetaJungle        | $5 Store Credit  |                 |
| Schmoe            | $25 Store Credit |                 |
| 0000              | $10 Store Credit |                 |
| Bsusko            | $25 Store Credit |                 |
| AlphaBlok         | $5 Store Credit  |                 |
| Bjamps            | $5 Store Credit  |                 |
| Davbruce21        | $5 Store Credit  |                 |
| JohnnyClutchCards | $10 Store Credit |                 |
| Patelh121         | $5 Store Credit  |                 |
| Infininight       | $5 Store Credit  |                 |
| mattcook          | $5 Store Credit  | viking91107     |
| MetaJungle        | $5 Store Credit  |                 |
| Kphamilton        | $25 Store Credit |                 |
| wisrhino          | $125 USDC        |                 |
| AlphaBlok         | $5 Store Credit  |                 |
| Omgiwon           | $10 Store Credit |                 |
| RobP343           | $5 Store Credit  |                 |
| JohnnyClutchCards | $5 Store Credit  |                 |
| PhillyWill        | $5 Store Credit  |                 |
| cryptoblogger     | $5 Store Credit  | davidpatrick08  |
| cph626            | $5 Store Credit  |                 |
| SDYote            | $5 Store Credit  |                 |
| Bjamps            | $5 Store Credit  |                 |
| 2048              | $5 Store Credit  |                 |
| MetaJungle        | $10 Store Credit |                 |
| Patelh121         | $5 Store Credit  |                 |
| Schmoe            | $10 Store Credit |                 |
| AlphaBlok         | $25 Store Credit |                 |
| Patelh121         | $10 Store Credit |                 |
| Schmoe            | $10 Store Credit |                 |
| MetaJungle        | $5 Store Credit  |                 |
| 2048              | $5 Store Credit  |                 |
| Bjamps            | $5 Store Credit  |                 |
| DangerSC          | $5 Store Credit  |                 |
| Phisigfsu         | $10 Store Credit |                 |
| balward           | $5 Store Credit  | milvec          |
| Omgiwon           | $10 Store Credit |                 |
| bmw1909           | $10 Store Credit |                 |
| eZe-E312          | $10 Store Credit |                 |
| MetaJungle        | $5 Store Credit  |                 |
| MetaJungle        | $5 Store Credit  |                 |
| jbbasics          | $5 Store Credit  |                 |
| Ronfresco         | $25 Store Credit |                 |
| NiftyMetaGirl     | $5 Store Credit  |                 |
| Xheryk            | $5 Store Credit  |                 |
| MetaJungle        | $5 Store Credit  |                 |
| wisrhino          | $10 Store Credit |                 |
| Kyled005          | $10 Store Credit |                 |
| gozags            | $5 Store Credit  |                 |
| Tsage225          | $5 Store Credit  |                 |
| MetaJungle        | $25 Store Credit |                 |
| Xheryk            | $5 Store Credit  |                 |
| Patelh121         | $5 Store Credit  |                 |
| Charlotteann      | $5 Store Credit  |                 |
| Ronfresco         | $10 Store Credit | radishkabal6    |
| cph626            | $10 Store Credit |                 |
| mattcook          | $5 Store Credit  |                 |
| accordingtohen    | $5 Store Credit  | viking91107     |
| mattcook          | $10 Store Credit |                 |
| MetaJungle        | $5 Store Credit  |                 |
| MetaJungle        | $5 Store Credit  |                 |
| Crypt_OvO         | $10 Store Credit |                 |
| Patelh121         | $25 Store Credit |                 |
| Donk3ykong81      | $10 Store Credit | byuofu          |
| Ronfresco         | $5 Store Credit  |                 |
| Jalbo1            | $5 Store Credit  |                 |
| Patelh121         | $5 Store Credit  |                 |
| MetaJungle        | $5 Store Credit  |                 |
| MetaJungle        | $10 Store Credit |                 |
| NiftyMetaGirl     | $5 Store Credit  |                 |
| MetaJungle        | $5 Store Credit  |                 |
| OG151             | $25 Store Credit |                 |
| MetaJungle        | $5 Store Credit  |                 |
| jdbeltz           | $5 Store Credit  |                 |
| 2048              | $5 Store Credit  |                 |
| Ronfresco         | $5 Store Credit  | radishkabal6    |
| MetaJungle        | $25 Store Credit |                 |
| Billcot           | $5 Store Credit  |                 |
| SDYote            | $5 Store Credit  |                 |
| Billcot           | $5 Store Credit  |                 |
| accordingtohen    | $10 Store Credit |                 |
| Schmoe            | $5 Store Credit  |                 |
| 1of1_sportscards  | $5 Store Credit  |                 |
| Patelh121         | $5 Store Credit  |                 |
| Daveliz55         | $10 Store Credit |                 |
| netbe171          | $25 Store Credit |                 |
| Omgiwon           | $5 Store Credit  |                 |
| mattcook          | $5 Store Credit  |                 |
| heffery           | $10 Store Credit | galileo         |
| AlphaBlok         | $10 Store Credit |                 |
| Kyled005          | $5 Store Credit  |                 |
| Skybo53           | $5 Store Credit  |                 |
| eZe-E312          | $5 Store Credit  |                 |
| Billcot           | $5 Store Credit  |                 |
| mattcook          | $10 Store Credit |                 |
| MetaJungle        | $5 Store Credit  |                 |
| cph626            | $5 Store Credit  |                 |
| Jbrown1310        | $5 Store Credit  |                 |
| AlphaBlok         | $5 Store Credit  | viking91107     |
| Xheryk            | $5 Store Credit  |                 |
| MetaJungle        | $5 Store Credit  |                 |
| OG151             | $5 Store Credit  |                 |
| Billcot           | $5 Store Credit  |                 |
| Patelh121         | $5 Store Credit  |                 |
| Schmoe            | $5 Store Credit  |                 |
| College31         | $5 Store Credit  |                 |
| bpfergu           | $5 Store Credit  |                 |
| AlphaBlok         | $5 Store Credit  | viking91107     |
| cryptoblogger     | $5 Store Credit  |                 |
| Crispjb           | $10 Store Credit |                 |
| Ronfresco         | $5 Store Credit  |                 |
| Daveliz55         | $5 Store Credit  |                 |
| todaysspecial     | $5 Store Credit  |                 |
| Titomachado       | $10 Store Credit |                 |
| cph626            | $5 Store Credit  |                 |
| bpfergu           | $10 Store Credit |                 |
| MetaJungle        | $5 Store Credit  | galileo         |
| Shudog            | $5 Store Credit  |                 |
| Andtercel         | $5 Store Credit  |                 |
| cph626            | $5 Store Credit  |                 |
| shawn120          | $10 Store Credit |                 |
| bmw1909           | $10 Store Credit |                 |
| TheStranger       | $5 Store Credit  |                 |
| MetaJungle        | $10 Store Credit |                 |
| 0000              | $25 Store Credit |                 |
| MetaJungle        | $5 Store Credit  |                 |
| mattcook          | $25 Store Credit |                 |
| Titomachado       | $10 Store Credit |                 |
| College31         | $5 Store Credit  |                 |
| Ronfresco         | $10 Store Credit |                 |
| MetaJungle        | $10 Store Credit |                 |
| SDYote            | $5 Store Credit  |                 |
| Bjamps            | $5 Store Credit  |                 |
| MetaJungle        | $5 Store Credit  |                 |
| rilbiz            | $50 USDC         |                 |
| Daveliz55         | $5 Store Credit  |                 |
| AlphaBlok         | $10 Store Credit |                 |
| mjzastrow1        | $5 Store Credit  | chgolitigator   |
| MetaJungle        | $10 Store Credit |                 |
| AlphaBlok         | $5 Store Credit  |                 |
| Xheryk            | $5 Store Credit  |                 |
| mattcook          | $10 Store Credit | billfd          |
| MetaJungle        | $5 Store Credit  |                 |
| mjzastrow1        | $5 Store Credit  |                 |
| Patelh121         | $10 Store Credit |                 |
| deleonlakers2000  | $25 Store Credit |                 |
| iiiericiii        | $5 Store Credit  |                 |
| MetaJungle        | $10 Store Credit |                 |
| Ronfresco         | $10 Store Credit |                 |
| MetaJungle        | $10 Store Credit |                 |
| Ronfresco         | $5 Store Credit  |                 |
| AlphaBlok         | $50 USDC         |                 |
| Xheryk            | $25 Store Credit | milvec          |
| Bjamps            | $5 Store Credit  |                 |
| AlphaBlok         | $10 Store Credit |                 |
| Schmoe            | $5 Store Credit  |                 |
| Kphamilton        | $10 Store Credit |                 |
| ghedoicy          | $5 Store Credit  |                 |
| MetaJungle        | $10 Store Credit |                 |
| mattcook          | $10 Store Credit |                 |
| LandoLakes        | $5 Store Credit  |                 |
| AlphaBlok         | $5 Store Credit  |                 |
| Mikeyj10          | $5 Store Credit  |                 |
| MetaJungle        | $25 Store Credit |                 |
| AlphaBlok         | $5 Store Credit  |                 |
| MetaJungle        | $5 Store Credit  |                 |
| Centerpiece       | $5 Store Credit  |                 |
| Leighham          | $10 Store Credit |                 |
| AlphaBlok         | $5 Store Credit  |                 |
| big_bees          | $10 Store Credit |                 |
| NiftyMetaGirl     | $5 Store Credit  |                 |
| mattcook          | $5 Store Credit  |                 |
| mattcook          | $25 Store Credit |                 |
| thampster         | $10 Store Credit |                 |
| AlphaBlok         | $25 Store Credit |                 |
| akicks            | $5 Store Credit  |                 |
| cph626            | $10 Store Credit |                 |
| cryptoblogger     | $5 Store Credit  |                 |
| Patelh121         | $5 Store Credit  |                 |
| mattcook          | $10 Store Credit |                 |
| mattcook          | $10 Store Credit | billfd          |
| Daveliz55         | $10 Store Credit |                 |
| bmw1909           | $5 Store Credit  |                 |
| cph626            | $5 Store Credit  |                 |
| Patelh121         | $5 Store Credit  |                 |
| jenndunn12m       | $10 Store Credit |                 |
| Charlotteann      | $10 Store Credit |                 |
| gozags            | $10 Store Credit |                 |
| MetaJungle        | $5 Store Credit  |                 |
| Schmoe            | $5 Store Credit  |                 |
| Daveliz55         | $25 Store Credit |                 |
| TheGOAT           | $5 Store Credit  |                 |
| FlyingNinja       | $5 Store Credit  |                 |
| BigDobs           | $5 Store Credit  | chgolitigator   |
| DangerSC          | $5 Store Credit  |                 |
| MetaJungle        | $5 Store Credit  |                 |
| gozags            | $5 Store Credit  |                 |
| jenndunn12m       | $5 Store Credit  |                 |
| FlyingNinja       | $5 Store Credit  |                 |
| MetaJungle        | $5 Store Credit  |                 |
| MetaJungle        | $10 Store Credit |                 |
| BigDobs           | $10 Store Credit |                 |
| Ronfresco         | $5 Store Credit  |                 |
| TexHooper         | $5 Store Credit  |                 |
| gozags            | $5 Store Credit  |                 |
| LandoLakes        | $5 Store Credit  |                 |
| pcahiwat          | $5 Store Credit  |                 |
| NiftyMetaGirl     | $5 Store Credit  | billfd          |
| MetaJungle        | $5 Store Credit  |                 |
| TheGOAT           | $25 Store Credit |                 |
| big_bees          | $5 Store Credit  |                 |
| Omgiwon           | $5 Store Credit  |                 |
| RobP343           | $5 Store Credit  |                 |
| Whodat13          | $5 Store Credit  |                 |
| mattcook          | $5 Store Credit  |                 |
| Bjamps            | $10 Store Credit |                 |
| bmw1909           | $25 Store Credit |                 |
| jdbeltz           | $10 Store Credit | radishkabal6    |
| MetaJungle        | $250 USDC        |                 |
| MetaJungle        | $10 Store Credit |                 |
| Patelh121         | $5 Store Credit  |                 |
| MetaJungle        | $5 Store Credit  |                 |
| Phisigfsu         | $5 Store Credit  |                 |
| MetaJungle        | $5 Store Credit  |                 |
| Steffen2121       | $10 Store Credit |                 |
| 2048              | $5 Store Credit  | bluetitans19    |
| Ronfresco         | $10 Store Credit |                 |
| Bjamps            | $5 Store Credit  |                 |
| NiftyMetaGirl     | $10 Store Credit |                 |
| MetaJungle        | $5 Store Credit  |                 |
| Schmoe            | $10 Store Credit |                 |
| Jjmccann2121      | $10 Store Credit |                 |
| Patelh121         | $25 Store Credit |                 |
| thampster         | $5 Store Credit  |                 |
| MetaJungle        | $5 Store Credit  |                 |
| Bjamps            | $5 Store Credit  |                 |
| AlphaBlok         | $5 Store Credit  | milvec          |
| BennyZ            | $5 Store Credit  |                 |
| MetaJungle        | $25 Store Credit |                 |
| Patelh121         | $5 Store Credit  |                 |
| AlphaBlok         | $5 Store Credit  |                 |
| MetaJungle        | $10 Store Credit | smashngrab77    |
| Titomachado       | $10 Store Credit |                 |
| 0000              | $10 Store Credit |                 |
| iiiericiii        | $5 Store Credit  |                 |
| gozags            | $10 Store Credit |                 |
| AlphaBlok         | $10 Store Credit |                 |
| Brian             | $5 Store Credit  |                 |
| Xheryk            | $5 Store Credit  |                 |
| MetaJungle        | $5 Store Credit  |                 |
| bmw1909           | $5 Store Credit  | chgolitigator   |
| Ronfresco         | $10 Store Credit |                 |
| Schmoe            | $5 Store Credit  |                 |
| pcahiwat          | $25 Store Credit |                 |
| AlphaBlok         | $25 Store Credit |                 |
| Mikeyj10          | $5 Store Credit  |                 |
| MetaJungle        | $10 Store Credit |                 |
| AlphaBlok         | $5 Store Credit  |                 |
| Bjamps            | $5 Store Credit  |                 |
| MetaJungle        | $5 Store Credit  |                 |
| bmw1909           | $10 Store Credit |                 |
| Omgiwon           | $5 Store Credit  |                 |
| Ronfresco         | $5 Store Credit  |                 |
| Xheryk            | $10 Store Credit |                 |
| Rodie4            | $10 Store Credit |                 |
| mattcook          | $5 Store Credit  |                 |
| MetaJungle        | $10 Store Credit |                 |
| jbbasics          | $25 Store Credit |                 |
| Kphamilton        | $5 Store Credit  |                 |
| 2048              | $10 Store Credit |                 |
| mojaveo           | $10 Store Credit |                 |
| MetaJungle        | $25 Store Credit |                 |
| Schmoe            | $5 Store Credit  |                 |
| Weasel368         | $10 Store Credit | yoyo909         |
| Mgmonaco11        | $25 Store Credit |                 |
| MetaJungle        | $10 Store Credit |                 |
| PhillyWill        | $10 Store Credit | radishkabal6    |
| Ronfresco         | $5 Store Credit  | bbv00248        |
| jbbasics          | $10 Store Credit | davidpatrick08  |
| Ronfresco         | $10 Store Credit |                 |
| 0000              | $5 Store Credit  | byuofu          |
| cph626            | $5 Store Credit  |                 |
| bpfergu           | $5 Store Credit  |                 |
| Odin7557          | $5 Store Credit  |                 |
| danielblakely     | $25 Store Credit |                 |
| BigDobs           | $5 Store Credit  |                 |
| eZe-E312          | $10 Store Credit |                 |
| Shua              | $5 Store Credit  |                 |
| Patelh121         | $5 Store Credit  |                 |
| BigDobs           | $10 Store Credit |                 |
| MetaJungle        | $5 Store Credit  |                 |
| RobP343           | $5 Store Credit  |                 |
| Patelh121         | $10 Store Credit |                 |
| MetaJungle        | $10 Store Credit |                 |
| eZe-E312          | $10 Store Credit |                 |
| Daveliz55         | $5 Store Credit  |                 |
| NiftyMetaGirl     | $10 Store Credit |                 |
| MetaJungle        | $10 Store Credit |                 |
| mattcook          | $5 Store Credit  | davidpatrick08  |
| AlphaBlok         | $5 Store Credit  |                 |
| Mvenekam          | $5 Store Credit  |                 |
| RadishDijital     | $5 Store Credit  |                 |
| Centerpiece       | $5 Store Credit  |                 |
| Ronfresco         | $5 Store Credit  |                 |
| accordingtohen    | $5 Store Credit  |                 |
| MetaJungle        | $25 Store Credit |                 |
| cph626            | $10 Store Credit |                 |
| Xheryk            | $10 Store Credit | mjno23goat      |
| Crispjb           | $10 Store Credit |                 |
| Patelh121         | $5 Store Credit  |                 |
| MetaJungle        | $5 Store Credit  |                 |
| MetaJungle        | $5 Store Credit  | mjno23goat      |
| AlphaBlok         | $10 Store Credit |                 |
| AlphaBlok         | $10 Store Credit |                 |
| Me-Degen          | $25 Store Credit |                 |
| NiftyMetaGirl     | $5 Store Credit  |                 |
| Ronfresco         | $5 Store Credit  |                 |
| Bjamps            | $5 Store Credit  | radishkabal6    |
| mattcook          | $5 Store Credit  |                 |
| Brftw             | $10 Store Credit |                 |
| wisrhino          | $50 USDC         |                 |
| AlphaBlok         | $5 Store Credit  |                 |
| Jjmccann2121      | $25 Store Credit | smashngrab77    |
| Xheryk            | $5 Store Credit  |                 |
| AlphaBlok         | $25 Store Credit |                 |
| accordingtohen    | $25 Store Credit |                 |
| balward           | $25 Store Credit |                 |
| jmyers81          | $5 Store Credit  |                 |
| AlphaBlok         | $5 Store Credit  |                 |
| Xheryk            | $5 Store Credit  |                 |
| MetaJungle        | $10 Store Credit |                 |
| MetaJungle        | $10 Store Credit |                 |
| MetaJungle        | $5 Store Credit  |                 |
| Xheryk            | $10 Store Credit |                 |
| Patelh121         | $125 USDC        |                 |
| MetaJungle        | $5 Store Credit  |                 |
| MetaJungle        | $5 Store Credit  |                 |
| MetaJungle        | $10 Store Credit |                 |
| MetaJungle        | $10 Store Credit |                 |
| MetaJungle        | $10 Store Credit | radishkabal6    |
| MetaJungle        | $5 Store Credit  |                 |
| cph626            | $25 Store Credit |                 |
| Patelh121         | $5 Store Credit  |                 |
| MetaJungle        | $10 Store Credit |                 |
| DangerSC          | $25 Store Credit |                 |
| MetaJungle        | $10 Store Credit |                 |
| BigDobs           | $5 Store Credit  |                 |
| mattcook          | $5 Store Credit  |                 |
| cph626            | $5 Store Credit  |                 |
| Billcot           | $10 Store Credit |                 |
| Phisigfsu         | $5 Store Credit  |                 |
| MetaJungle        | $10 Store Credit |                 |
| NiftyMetaGirl     | $10 Store Credit |                 |
| big_bees          | $5 Store Credit  |                 |
| MetaJungle        | $5 Store Credit  |                 |
| Ronfresco         | $25 Store Credit |                 |
| MetaJungle        | $5 Store Credit  |                 |
| AlphaBlok         | $5 Store Credit  |                 |
| Ronfresco         | $5 Store Credit  | radishkabal6    |
| Bjamps            | $10 Store Credit |                 |
| Madvolker         | $10 Store Credit |                 |
| 0000              | $5 Store Credit  |                 |
| Xheryk            | $10 Store Credit |                 |
| wisrhino          | $5 Store Credit  |                 |
| Infininight       | $10 Store Credit |                 |
| BigDobs           | $5 Store Credit  |                 |
| mattcook          | $10 Store Credit |                 |
| Xheryk            | $10 Store Credit |                 |
| NiftyMetaGirl     | $10 Store Credit |                 |
| MetaJungle        | $5 Store Credit  |                 |
| TheStranger       | $5 Store Credit  |                 |
| wisrhino          | $5 Store Credit  |                 |
| PhillyWill        | $5 Store Credit  |                 |
| Patelh121         | $5 Store Credit  |                 |
| thampster         | $5 Store Credit  |                 |
| NiftyMetaGirl     | $25 Store Credit |                 |
| Roux1310          | $500 USDC        |                 |
| cryptoblogger     | $10 Store Credit |                 |
| Centerpiece       | $25 Store Credit |                 |
| wisrhino          | $5 Store Credit  |                 |
| Shudog            | $5 Store Credit  |                 |
| BigDobs           | $25 Store Credit |                 |
| Phisigfsu         | $5 Store Credit  |                 |
| AlphaBlok         | $1000 USDC       | chgolitigator   |
| Titomachado       | $5 Store Credit  |                 |
| Bsusko            | $5 Store Credit  |                 |
| MetaJungle        | $5 Store Credit  |                 |
| mattcook          | $25 Store Credit |                 |
| MetaJungle        | $5 Store Credit  |                 |
| Schmoe            | $5 Store Credit  |                 |
| BigDobs           | $10 Store Credit |                 |
| MetaJungle        | $10 Store Credit |                 |
| Ronfresco         | $5 Store Credit  | bbv00248        |
| 2048              | $10 Store Credit |                 |
| MetaJungle        | $5 Store Credit  |                 |
| Jjmccann2121      | $10 Store Credit |                 |
| AlphaBlok         | $25 Store Credit |                 |
| Patelh121         | $10 Store Credit |                 |
| deleonlakers2000  | $5 Store Credit  |                 |
| SDYote            | $10 Store Credit |                 |
| MetaJungle        | $5 Store Credit  |                 |
| MetaJungle        | $10 Store Credit |                 |
| MetaJungle        | $10 Store Credit | radishkabal6    |
| AlphaBlok         | $10 Store Credit |                 |
| Patelh121         | $5 Store Credit  |                 |
| MetaJungle        | $5 Store Credit  |                 |
| MetaJungle        | $5 Store Credit  |                 |
| MetaJungle        | $5 Store Credit  |                 |
| MetaJungle        | $5 Store Credit  | smashngrab77    |
| Billcot           | $5 Store Credit  |                 |
| MetaJungle        | $25 Store Credit | mjno23goat      |
| EpsilonDelta1203  | $5 Store Credit  |                 |
| cryptoblogger     | $5 Store Credit  |                 |
| Ronfresco         | $5 Store Credit  |                 |
| wisrhino          | $10 Store Credit |                 |
| MetaJungle        | $5 Store Credit  |                 |
| Xheryk            | $5 Store Credit  |                 |
| mattcook          | $5 Store Credit  |                 |
| Xheryk            | $5 Store Credit  |                 |
| Ronfresco         | $10 Store Credit |                 |
| Bjamps            | $25 Store Credit | viking91107     |
| College31         | $5 Store Credit  |                 |
| mjzastrow1        | $25 Store Credit |                 |
| cryptoblogger     | $5 Store Credit  |                 |
| bmw1909           | $10 Store Credit |                 |
| MetaJungle        | $5 Store Credit  |                 |
| 0000              | $10 Store Credit |                 |
| RobP343           | $5 Store Credit  |                 |
| Patelh121         | $10 Store Credit |                 |
| MetaJungle        | $5 Store Credit  |                 |
| AlphaBlok         | $10 Store Credit |                 |
| Bjamps            | $5 Store Credit  |                 |
| Bjamps            | $5 Store Credit  |                 |
| AlphaBlok         | $25 Store Credit |                 |
| cryptoblogger     | $25 Store Credit | smashngrab77    |
| Jtpaving          | $5 Store Credit  |                 |
| Ronfresco         | $5 Store Credit  |                 |
| Ronfresco         | $25 Store Credit |                 |
| EpsilonDelta1203  | $5 Store Credit  |                 |
| AlphaBlok         | $5 Store Credit  |                 |
| Patelh121         | $5 Store Credit  |                 |
| MetaJungle        | $5 Store Credit  |                 |
| TheRipper         | $25 Store Credit |                 |
| Titomachado       | $10 Store Credit |                 |
| NiftyMetaGirl     | $10 Store Credit |                 |
| Crypt_OvO         | $25 Store Credit |                 |
| Schmoe            | $10 Store Credit | mjno23goat      |
| DoctaBre          | $10 Store Credit |                 |
| jdbeltz           | $10 Store Credit |                 |
| MetaJungle        | $25 Store Credit |                 |
| bpfergu           | $5 Store Credit  |                 |
| BigDobs           | $5 Store Credit  |                 |
| MetaJungle        | $150 USDC        |                 |
| MetaJungle        | $5 Store Credit  |                 |
| MetaJungle        | $5 Store Credit  |                 |
| Odin7557          | $5 Store Credit  |                 |
| MetaJungle        | $5 Store Credit  |                 |
| AlphaBlok         | $5 Store Credit  |                 |
| Patelh121         | $5 Store Credit  |                 |
| Schmoe            | $5 Store Credit  |                 |
| BigDobs           | $5 Store Credit  |                 |
| MetaJungle        | $5 Store Credit  |                 |
| Leighham          | $10 Store Credit |                 |
| Patelh121         | $5 Store Credit  |                 |
| Ronfresco         | $5 Store Credit  |                 |
| jdbeltz           | $5 Store Credit  |                 |
| Mvenekam          | $5 Store Credit  |                 |
| Ronfresco         | $5 Store Credit  |                 |
| netbe171          | $5 Store Credit  |                 |
| NiftyMetaGirl     | $5 Store Credit  |                 |
| bmw1909           | $10 Store Credit |                 |
| MetaJungle        | $10 Store Credit |                 |
| Billcot           | $10 Store Credit |                 |
| College31         | $5 Store Credit  |                 |
| cryptoblogger     | $25 Store Credit |                 |
| jdbeltz           | $10 Store Credit |                 |
| accordingtohen    | $5 Store Credit  |                 |
| wisrhino          | $5 Store Credit  |                 |
| TheGOAT           | $5 Store Credit  |                 |
| Jalbo1            | $10 Store Credit |                 |
| mattcook          | $5 Store Credit  |                 |
| jenndunn12m       | $25 Store Credit |                 |
| Ronfresco         | $5 Store Credit  |                 |
| BigDobs           | $5 Store Credit  |                 |
| MetaJungle        | $10 Store Credit |                 |
| Xheryk            | $10 Store Credit |                 |
| Omgiwon           | $10 Store Credit |                 |
| balward           | $10 Store Credit |                 |
| Mgmonaco11        | $5 Store Credit  |                 |
| Xheryk            | $25 Store Credit |                 |
| AlphaBlok         | $5 Store Credit  |                 |
| Schmoe            | $5 Store Credit  |                 |
| Bjamps            | $10 Store Credit | smashngrab77    |
| AlphaBlok         | $10 Store Credit |                 |
| Schmoe            | $5 Store Credit  |                 |
| cryptoblogger     | $5 Store Credit  |                 |
| jbbasics          | $25 Store Credit |                 |
| MetaJungle        | $25 Store Credit |                 |
| jmyers81          | $10 Store Credit |                 |
| Jjmccann2121      | $5 Store Credit  |                 |
| SDYote            | $5 Store Credit  |                 |
| cryptoblogger     | $10 Store Credit |                 |
| Omgiwon           | $5 Store Credit  |                 |
| Newlin99          | $5 Store Credit  |                 |
| EpsilonDelta1203  | $5 Store Credit  |                 |
| Daveliz55         | $25 Store Credit |                 |
| Schmoe            | $5 Store Credit  |                 |
| MetaJungle        | $5 Store Credit  |                 |
| Schmoe            | $25 Store Credit |                 |
| AlphaBlok         | $5 Store Credit  |                 |
| Crispjb           | $5 Store Credit  |                 |
| AlphaBlok         | $5 Store Credit  |                 |
| MetaJungle        | $5 Store Credit  | smashngrab77    |
| mattcook          | $5 Store Credit  |                 |
| Rjj007            | $10 Store Credit |                 |
| Madvolker         | $5 Store Credit  |                 |
| Jeffslugs         | $5 Store Credit  |                 |
| jdbeltz           | $10 Store Credit |                 |
| Andtercel         | $10 Store Credit |                 |
| mattcook          | $5 Store Credit  |                 |
| the_Legend        | $5 Store Credit  |                 |
| AlphaBlok         | $25 Store Credit |                 |
| BigDobs           | $10 Store Credit |                 |
| rilbiz            | $5 Store Credit  |                 |
| Bjamps            | $10 Store Credit |                 |
| gozags            | $10 Store Credit |                 |
| mattcook          | $5 Store Credit  |                 |
| BigDobs           | $10 Store Credit |                 |
| MetaJungle        | $5 Store Credit  |                 |
| tt9s              | $25 Store Credit |                 |
| NiftyMetaGirl     | $10 Store Credit |                 |
| rilbiz            | $5 Store Credit  |                 |
| Schmoe            | $10 Store Credit |                 |
| Patelh121         | $10 Store Credit | radishkabal6    |
| TheStranger       | $5 Store Credit  | yoyo909         |
| Bjamps            | $5 Store Credit  |                 |
| MetaJungle        | $5 Store Credit  | jimmyd          |
| Jeffslugs         | $10 Store Credit |                 |
| MetaJungle        | $5 Store Credit  |                 |
| AlphaBlok         | $10 Store Credit |                 |
| AlphaBlok         | $10 Store Credit |                 |
| Patelh121         | $5 Store Credit  |                 |
| Xheryk            | $10 Store Credit |                 |
| Patelh121         | $10 Store Credit |                 |
| BennyZ            | $5 Store Credit  |                 |
| MetaJungle        | $10 Store Credit |                 |
| Schmoe            | $25 Store Credit |                 |
| MetaJungle        | $5 Store Credit  | milvec          |
| mattcook          | $10 Store Credit | smashngrab77    |
| Patelh121         | $10 Store Credit |                 |
| cryptoblogger     | $5 Store Credit  | radishkabal6    |
| dhoovey           | $5 Store Credit  | galileo         |
| Schmoe            | $5 Store Credit  |                 |
| Crypt_OvO         | $5 Store Credit  |                 |
| MetaJungle        | $10 Store Credit |                 |
| RobP343           | $5 Store Credit  |                 |
| MetaJungle        | $10 Store Credit |                 |
| Patelh121         | $5 Store Credit  |                 |
| EsotericPA        | $5 Store Credit  |                 |
| MetaJungle        | $10 Store Credit |                 |
| Patelh121         | $5 Store Credit  |                 |
| NiftyMetaGirl     | $5 Store Credit  |                 |
| MetaJungle        | $10 Store Credit | bbv00248        |
| Patelh121         | $10 Store Credit | bluetitans19    |
| Titomachado       | $10 Store Credit |                 |
| 2048              | $10 Store Credit |                 |
| drcrazy           | $5 Store Credit  |                 |
| Schmoe            | $10 Store Credit |                 |
| gozags            | $10 Store Credit |                 |
| cryptoblogger     | $5 Store Credit  | misterdylan420  |
| MetaJungle        | $5 Store Credit  |                 |
| Ronfresco         | $5 Store Credit  |                 |
| MetaJungle        | $5 Store Credit  |                 |
| jbbasics          | $5 Store Credit  | viking91107     |
| MetaJungle        | $5 Store Credit  | normclark       |
| AlphaBlok         | $5 Store Credit  |                 |
| Bjamps            | $5 Store Credit  |                 |
| NiftyMetaGirl     | $10 Store Credit | radishkabal6    |
| Ronfresco         | $5 Store Credit  |                 |
| Birdman03         | $25 Store Credit | smashngrab77    |
| Schmoe            | $5 Store Credit  |                 |
| TheStranger       | $10 Store Credit |                 |
| MetaJungle        | $10 Store Credit |                 |
| Patelh121         | $5 Store Credit  |                 |
| MetaJungle        | $25 Store Credit |                 |
| Jjmccann2121      | $25 Store Credit | viking91107     |
| cryptoblogger     | $5 Store Credit  |                 |
| BigDobs           | $25 Store Credit | yoyo909         |
| shawn120          | $5 Store Credit  |                 |
| Jjmccann2121      | $25 Store Credit | yoyo909         |
| Jjmccann2121      | $5 Store Credit  |                 |
| NiftyMetaGirl     | $25 Store Credit |                 |
| TheGOAT           | $5 Store Credit  |                 |
| Infininight       | $125 USDC        |                 |
| Schmoe            | $10 Store Credit |                 |
| eZe-E312          | $5 Store Credit  |                 |
| Donk3ykong81      | $10 Store Credit | chgolitigator   |
| Patelh121         | $10 Store Credit |                 |
| 2048              | $10 Store Credit |                 |
| cryptoblogger     | $10 Store Credit |                 |
| Ronfresco         | $10 Store Credit | milvec          |
| MetaJungle        | $5 Store Credit  |                 |
| MetaJungle        | $25 Store Credit |                 |
| MetaJungle        | $10 Store Credit |                 |
| AlphaBlok         | $5 Store Credit  |                 |
| AlphaBlok         | $25 Store Credit |                 |
| cryptoblogger     | $5 Store Credit  |                 |
| SDYote            | $2500 USDC       |                 |
| Schmoe            | $10 Store Credit |                 |
| AlphaBlok         | $5 Store Credit  |                 |
| AlphaBlok         | $10 Store Credit |                 |
| Schmoe            | $5 Store Credit  |                 |
| MetaJungle        | $5 Store Credit  |                 |
| JohnnyClutchCards | $5 Store Credit  |                 |
| Ronfresco         | $5 Store Credit  | ginganinja8     |
| cryptoblogger     | $10 Store Credit |                 |
| MetaJungle        | $5 Store Credit  |                 |
| AlphaBlok         | $5 Store Credit  |                 |
| Centerpiece       | $10 Store Credit |                 |
| AlphaBlok         | $5 Store Credit  |                 |
| Bjamps            | $5 Store Credit  |                 |
| Jjmccann2121      | $25 Store Credit |                 |
| BigDobs           | $125 USDC        |                 |
| mattcook          | $5 Store Credit  |                 |
| Sbbears           | $5 Store Credit  |                 |
| cryptoblogger     | $5 Store Credit  |                 |
| Ruxy              | $5 Store Credit  |                 |
| cph626            | $10 Store Credit |                 |
| Phisigfsu         | $10 Store Credit | chgolitigator   |
| accordingtohen    | $5 Store Credit  |                 |
| Xheryk            | $5 Store Credit  |                 |
| MetaJungle        | $5 Store Credit  |                 |
| jetopps           | $25 Store Credit |                 |
| Xheryk            | $5 Store Credit  |                 |
| AlphaBlok         | $5 Store Credit  |                 |
| Charlotteann      | $5 Store Credit  |                 |
| MetaJungle        | $10 Store Credit |                 |
| jdbeltz           | $5 Store Credit  |                 |
| MetaJungle        | $10 Store Credit |                 |
| cph626            | $10 Store Credit |                 |
| EpsilonDelta1203  | $5 Store Credit  |                 |
| bpfergu           | $5 Store Credit  |                 |
| Daveliz55         | $10 Store Credit |                 |
| EsotericPA        | $25 Store Credit |                 |
| MetaJungle        | $5 Store Credit  |                 |
| cryptoblogger     | $5 Store Credit  |                 |
| TheGOAT           | $5 Store Credit  |                 |
| sheltronica       | $5 Store Credit  | radishkabal6    |
| JohnnyClutchCards | $5 Store Credit  |                 |
| MetaJungle        | $5 Store Credit  |                 |
| Daveliz55         | $5 Store Credit  | smashngrab77    |
| NiftyMetaGirl     | $10 Store Credit |                 |
| Omgiwon           | $5 Store Credit  |                 |
| JohnnyClutchCards | $5 Store Credit  |                 |
| Patelh121         | $10 Store Credit |                 |
| Xheryk            | $10 Store Credit |                 |
| DoctaBre          | $5 Store Credit  |                 |
| MetaJungle        | $10 Store Credit |                 |
| Ronfresco         | $5 Store Credit  |                 |
| Jjmccann2121      | $5 Store Credit  |                 |
| Ronfresco         | $10 Store Credit |                 |
| MetaJungle        | $5 Store Credit  |                 |
| mambaout          | $10 Store Credit |                 |
| Phanatik          | $25 Store Credit |                 |
| Schmoe            | $5 Store Credit  | smashngrab77    |
| Xheryk            | $5 Store Credit  |                 |
| eZe-E312          | $5 Store Credit  |                 |
| Ronfresco         | $5 Store Credit  |                 |
| Schmoe            | $5 Store Credit  |                 |
| Xheryk            | $5 Store Credit  |                 |
| MetaJungle        | $5 Store Credit  |                 |
| MetaJungle        | $10 Store Credit |                 |
| Ronfresco         | $5 Store Credit  |                 |
| AlphaBlok         | $5 Store Credit  |                 |
| Bjamps            | $10 Store Credit |                 |
| MetaJungle        | $5 Store Credit  |                 |
| mambaout          | $5 Store Credit  |                 |
| MetaJungle        | $25 Store Credit |                 |
| Billcot           | $5 Store Credit  |                 |
| MetaJungle        | $10 Store Credit |                 |
| AlphaBlok         | $5 Store Credit  |                 |
| 0000              | $10 Store Credit |                 |
| Omgiwon           | $5 Store Credit  |                 |
| Patelh121         | $10 Store Credit |                 |
| bmw1909           | $25 Store Credit |                 |
| AlphaBlok         | $10 Store Credit |                 |
| Jjmccann2121      | $25 Store Credit |                 |
| Patelh121         | $10 Store Credit | chgolitigator   |
| BigDobs           | $5 Store Credit  | davidpatrick08  |
| MetaJungle        | $5 Store Credit  |                 |
| Phisigfsu         | $5 Store Credit  |                 |
| MetaJungle        | $5 Store Credit  |                 |
| Roux1310          | $5 Store Credit  |                 |
| mattcook          | $150 USDC        |                 |
| cryptoblogger     | $5 Store Credit  |                 |
| TheStranger       | $25 Store Credit |                 |
| JBAtlFalcons      | $10 Store Credit |                 |
| Billcot           | $5 Store Credit  |                 |
| Ronfresco         | $5 Store Credit  |                 |
| netbe171          | $10 Store Credit |                 |
| AlphaBlok         | $25 Store Credit |                 |
| MetaJungle        | $25 Store Credit |                 |
| mattcook          | $25 Store Credit |                 |
| Billcot           | $10 Store Credit |                 |
| MetaJungle        | $50 USDC         |                 |
| Bjamps            | $10 Store Credit |                 |
| Jalbo1            | $5 Store Credit  |                 |
| Ronfresco         | $5 Store Credit  |                 |
| MetaJungle        | $5 Store Credit  |                 |
| MetaJungle        | $5 Store Credit  |                 |
| Patelh121         | $5 Store Credit  |                 |
| Schmoe            | $5 Store Credit  |                 |
| mattcook          | $5 Store Credit  |                 |
| Tsage225          | $10 Store Credit |                 |
| cph626            | $10 Store Credit |                 |
| MetaJungle        | $25 Store Credit |                 |
| Ronfresco         | $10 Store Credit |                 |
| Patelh121         | $10 Store Credit | chgolitigator   |
| Ronfresco         | $10 Store Credit |                 |
| jbbasics          | $50 USDC         |                 |
| MetaJungle        | $10 Store Credit |                 |
| Patelh121         | $5 Store Credit  |                 |
| Ronfresco         | $5 Store Credit  |                 |
| MetaJungle        | $10 Store Credit |                 |
| Jjmccann2121      | $10 Store Credit |                 |
| Schmoe            | $5 Store Credit  | milvec          |
| MetaJungle        | $5 Store Credit  |                 |
| Ronfresco         | $5 Store Credit  |                 |
| MetaJungle        | $5 Store Credit  |                 |
| EpsilonDelta1203  | $5 Store Credit  | chgolitigator   |
| deleonlakers2000  | $25 Store Credit |                 |
| BigDobs           | $5 Store Credit  |                 |
| AlphaBlok         | $10 Store Credit |                 |
| jbbasics          | $25 Store Credit |                 |
| mjzastrow1        | $5 Store Credit  |                 |
| Leighham          | $10 Store Credit |                 |
| jmyers81          | $10 Store Credit |                 |
| Omgiwon           | $10 Store Credit |                 |
| MetaJungle        | $25 Store Credit |                 |
| Roux1310          | $10 Store Credit |                 |
| NiftyMetaGirl     | $25 Store Credit | smashngrab77    |
| Ronfresco         | $5 Store Credit  |                 |
| mjzastrow1        | $10 Store Credit |                 |
| MetaJungle        | $10 Store Credit |                 |
| AlphaBlok         | $25 Store Credit |                 |
| bpfergu           | $5 Store Credit  | ginganinja8     |
| cph626            | $5 Store Credit  |                 |
| MetaJungle        | $5 Store Credit  |                 |
| Donk3ykong81      | $5 Store Credit  |                 |
| cph626            | $25 Store Credit |                 |
| MetaJungle        | $5 Store Credit  |                 |
| MetaJungle        | $10 Store Credit |                 |
| Schmoe            | $5 Store Credit  |                 |
| Phisigfsu         | $5 Store Credit  |                 |
| Schmoe            | $5 Store Credit  |                 |
| OG151             | $10 Store Credit |                 |
| Mvenekam          | $20000 USDC      |                 |
| Billcot           | $5 Store Credit  |                 |
| BennyZ            | $5 Store Credit  |                 |
| Titomachado       | $5 Store Credit  |                 |
| jdbeltz           | $5 Store Credit  |                 |
| JBAtlFalcons      | $5 Store Credit  |                 |
| accordingtohen    | $25 Store Credit |                 |
| 0000              | $25 Store Credit |                 |
| Rodie4            | $10 Store Credit |                 |
| MetaJungle        | $5 Store Credit  |                 |
| Bjamps            | $5 Store Credit  |                 |
| Bjamps            | $25 Store Credit |                 |
| Ronfresco         | $25 Store Credit |                 |
| mattcook          | $25 Store Credit |                 |
| Bjamps            | $25 Store Credit |                 |
| Billcot           | $5 Store Credit  |                 |
| mattcook          | $25 Store Credit |                 |
| Brftw             | $25 Store Credit |                 |
| Patelh121         | $25 Store Credit | bbv00248        |
| mattcook          | $10 Store Credit |                 |
| MetaJungle        | $5 Store Credit  |                 |
| Jimmys75          | $5 Store Credit  |                 |
| AlphaBlok         | $5 Store Credit  |                 |
| mattcook          | $5 Store Credit  |                 |
| MetaJungle        | $25 Store Credit | galileo         |
| NiftyMetaGirl     | $5 Store Credit  |                 |
| MetaJungle        | $5 Store Credit  |                 |
| Bjamps            | $25 Store Credit |                 |
| MetaJungle        | $25 Store Credit |                 |
| AlphaBlok         | $10 Store Credit |                 |
| MetaJungle        | $5 Store Credit  |                 |
| AlphaBlok         | $5 Store Credit  |                 |
| Ronfresco         | $5 Store Credit  |                 |
| MetaJungle        | $5 Store Credit  |                 |
| Patelh121         | $5 Store Credit  |                 |
| PhillyWill        | $5 Store Credit  |                 |
| MetaJungle        | $10 Store Credit | galileo         |
| cph626            | $5 Store Credit  |                 |
| MetaJungle        | $10 Store Credit |                 |
| danielblakely     | $10 Store Credit | galileo         |
| MetaJungle        | $5 Store Credit  |                 |
| big_bees          | $5 Store Credit  |                 |
| Donk3ykong81      | $5 Store Credit  |                 |
| MetaJungle        | $25 Store Credit |                 |
| Patelh121         | $10 Store Credit | viking91107     |
| cryptoblogger     | $5 Store Credit  |                 |
| Kyled005          | $5 Store Credit  |                 |
| Jimmys75          | $5 Store Credit  |                 |
| aaronahaddad      | $5 Store Credit  |                 |
| MetaJungle        | $5 Store Credit  |                 |
| AlphaBlok         | $25 Store Credit |                 |
| MetaJungle        | $5 Store Credit  |                 |
| Ronfresco         | $10 Store Credit |                 |
| Patelh121         | $5 Store Credit  |                 |
| mattcook          | $25 Store Credit |                 |
| AlphaBlok         | $5 Store Credit  |                 |
| Skybo53           | $5 Store Credit  |                 |
| thampster         | $5 Store Credit  |                 |
| MetaJungle        | $10 Store Credit |                 |
| Chicagows213      | $10 Store Credit |                 |
| MetaJungle        | $5 Store Credit  |                 |
| MetaJungle        | $5 Store Credit  |                 |
| Donk3ykong81      | $5 Store Credit  |                 |
| MetaJungle        | $10 Store Credit | radishkabal6    |
| Randorino99       | $25 Store Credit |                 |
| accordingtohen    | $25 Store Credit |                 |
| MetaJungle        | $10 Store Credit | radishkabal6    |
| MetaJungle        | $10 Store Credit |                 |
| Omgiwon           | $5 Store Credit  |                 |
| wisrhino          | $5 Store Credit  |                 |
| Tsage225          | $25 Store Credit |                 |
| FlyingNinja       | $10 Store Credit |                 |
| Roux1310          | $5 Store Credit  |                 |
| Phisigfsu         | $5 Store Credit  |                 |
| yop7              | $5 Store Credit  |                 |
| MetaJungle        | $25 Store Credit |                 |
| Xheryk            | $10 Store Credit |                 |
| thampster         | $10 Store Credit |                 |
| Omgiwon           | $5 Store Credit  |                 |
| MetaJungle        | $25 Store Credit |                 |
| 0000              | $25 Store Credit |                 |
| Jalbo1            | $25 Store Credit |                 |
| Ronfresco         | $5 Store Credit  |                 |
| MetaJungle        | $5 Store Credit  |                 |
| Bjamps            | $5 Store Credit  |                 |
| 2048              | $5 Store Credit  |                 |
| Patelh121         | $5 Store Credit  |                 |
| DangerSC          | $5 Store Credit  |                 |
| MetaJungle        | $25 Store Credit |                 |
| iiiericiii        | $10 Store Credit |                 |
| MetaJungle        | $5 Store Credit  |                 |
| MetaJungle        | $10 Store Credit |                 |
| Xheryk            | $10 Store Credit |                 |
| AlphaBlok         | $5 Store Credit  |                 |
| OG151             | $10 Store Credit |                 |
| MetaJungle        | $125 USDC        |                 |
| MetaJungle        | $5 Store Credit  |                 |
| Schmoe            | $10 Store Credit |                 |
| AlphaBlok         | $25 Store Credit |                 |
| Bjamps            | $10 Store Credit |                 |
| Schmoe            | $5 Store Credit  |                 |
| MetaJungle        | $5 Store Credit  |                 |
| Infininight       | $10 Store Credit |                 |
| MetaJungle        | $25 Store Credit |                 |
| AlphaBlok         | $10 Store Credit |                 |
| Daveliz55         | $5 Store Credit  |                 |
| MetaJungle        | $10 Store Credit | viking91107     |
| Ronfresco         | $5 Store Credit  |                 |
| Steffen2121       | $25 Store Credit |                 |
| MetaJungle        | $5 Store Credit  |                 |
| Patelh121         | $10 Store Credit |                 |
| Schmoe            | $25 Store Credit |                 |
| AlphaBlok         | $5 Store Credit  | smashngrab77    |
| Aaron             | $5 Store Credit  |                 |
| Bjamps            | $10 Store Credit |                 |
| Ronfresco         | $10 Store Credit |                 |
| Billcot           | $10 Store Credit |                 |
| Billcot           | $25 Store Credit |                 |
| Jimmys75          | $5 Store Credit  |                 |
| MetaJungle        | $10000 USDC      | milvec          |
| Patelh121         | $5 Store Credit  |                 |
| MetaJungle        | $5 Store Credit  |                 |
| Daveliz55         | $5 Store Credit  |                 |
| MetaJungle        | $5 Store Credit  |                 |
| MetaJungle        | $5 Store Credit  |                 |
| AlphaBlok         | $5 Store Credit  |                 |
| Guvv              | $25 Store Credit |                 |
| Kyled005          | $5 Store Credit  |                 |
| AlphaBlok         | $5 Store Credit  |                 |
| BigDobs           | $5 Store Credit  | radishkabal6    |
| AlphaBlok         | $10 Store Credit |                 |
| Ntrprzr           | $25 Store Credit |                 |
| MetaJungle        | $5 Store Credit  |                 |
| MetaJungle        | $25 Store Credit |                 |
| DangerSC          | $5 Store Credit  |                 |
| MetaJungle        | $5 Store Credit  |                 |
| mattcook          | $5 Store Credit  |                 |
| bmw1909           | $5 Store Credit  |                 |
| Ronfresco         | $5 Store Credit  | smashngrab77    |
| cryptoblogger     | $25 Store Credit |                 |
| Schmoe            | $10 Store Credit |                 |
| Billcot           | $10 Store Credit |                 |
| MetaJungle        | $5 Store Credit  |                 |
| MetaJungle        | $25 Store Credit |                 |
| cryptoblogger     | $5 Store Credit  |                 |
| 1of1_sportscards  | $5 Store Credit  |                 |
| BennyZ            | $5 Store Credit  |                 |
| Bjamps            | $5 Store Credit  | galileo         |
| Schmoe            | $10 Store Credit |                 |
| Ronfresco         | $5 Store Credit  |                 |
| MetaJungle        | $10 Store Credit |                 |
| Andrewgarrett41   | $5 Store Credit  |                 |
| MetaJungle        | $10 Store Credit |                 |
| bmw1909           | $10 Store Credit |                 |
| AlphaBlok         | $5 Store Credit  |                 |
| Omgiwon           | $5 Store Credit  |                 |
| MetaJungle        | $5 Store Credit  |                 |
| Ronfresco         | $5 Store Credit  |                 |
| MetaJungle        | $5 Store Credit  |                 |
| MetaJungle        | $5 Store Credit  |                 |
| AlphaBlok         | $5 Store Credit  |                 |
| tt9s              | $10 Store Credit |                 |
| Jalbo1            | $25 Store Credit |                 |
| cph626            | $25 Store Credit |                 |
| Schmoe            | $5 Store Credit  | viking91107     |
| Bsusko            | $5 Store Credit  |                 |
| Schmoe            | $5 Store Credit  |                 |
| MetaJungle        | $5 Store Credit  |                 |
| MetaJungle        | $10 Store Credit |                 |
| Shudog            | $5 Store Credit  |                 |
| AlphaBlok         | $25 Store Credit |                 |
| bpfergu           | $5 Store Credit  |                 |
| bpfergu           | $5 Store Credit  |                 |
| heffery           | $5 Store Credit  |                 |
| Andrewgarrett41   | $5 Store Credit  |                 |
| MetaJungle        | $10 Store Credit |                 |
| MetaJungle        | $25 Store Credit |                 |
| Infininight       | $10 Store Credit |                 |
| TheStranger       | $5 Store Credit  |                 |
| MetaJungle        | $10 Store Credit |                 |
| mattcook          | $25 Store Credit |                 |
| Chicagows213      | $25 Store Credit |                 |
| MetaJungle        | $10 Store Credit |                 |
| Daveliz55         | $25 Store Credit |                 |
| deleonlakers2000  | $5 Store Credit  |                 |
| Kyled005          | $5 Store Credit  |                 |
| MetaJungle        | $5 Store Credit  |                 |
| AlphaBlok         | $5 Store Credit  |                 |
| FlyingNinja       | $5 Store Credit  |                 |
| Davbruce21        | $25 Store Credit |                 |
| Patelh121         | $5 Store Credit  |                 |
| Pajh07840         | $5 Store Credit  |                 |
| BigDobs           | $5 Store Credit  |                 |
| Jjmccann2121      | $5 Store Credit  |                 |
| Titomachado       | $5 Store Credit  |                 |
| MetaJungle        | $5 Store Credit  |                 |
| MetaJungle        | $5 Store Credit  |                 |
| MetaJungle        | $25 Store Credit |                 |
| AlphaBlok         | $10 Store Credit |                 |
| Jeffslugs         | $250 USDC        |                 |
| MetaJungle        | $10 Store Credit |                 |
| cryptoblogger     | $10 Store Credit |                 |
| AlphaBlok         | $10 Store Credit |                 |
| jenndunn12m       | $5 Store Credit  |                 |
| 2048              | $5 Store Credit  |                 |
| mattcook          | $25 Store Credit |                 |
| cryptoblogger     | $10 Store Credit |                 |
| Nymcards          | $5 Store Credit  |                 |
| MetaJungle        | $25 Store Credit |                 |
| mattcook          | $5 Store Credit  |                 |
| mattcook          | $10 Store Credit | galileo         |
| Patelh121         | $5 Store Credit  |                 |
| BigDobs           | $5 Store Credit  |                 |
| wisrhino          | $10 Store Credit | mjno23goat      |
| mattcook          | $5 Store Credit  |                 |
| sheltronica       | $10 Store Credit |                 |
| MetaJungle        | $10 Store Credit |                 |
| MetaJungle        | $5 Store Credit  |                 |
| Ronfresco         | $5 Store Credit  |                 |
| MetaJungle        | $5 Store Credit  |                 |
| big_bees          | $5 Store Credit  | radishkabal6    |
| Schmoe            | $10 Store Credit |                 |
| iiiericiii        | $10 Store Credit |                 |
| MetaJungle        | $5 Store Credit  |                 |
| MetaJungle        | $5 Store Credit  |                 |
| sheltronica       | $5 Store Credit  |                 |
| MetaJungle        | $5 Store Credit  |                 |
| BigDobs           | $25 Store Credit |                 |
| Leighham          | $5 Store Credit  |                 |
| MetaJungle        | $5 Store Credit  |                 |
| Xheryk            | $5 Store Credit  |                 |
| Schmoe            | $5 Store Credit  |                 |
| Schmoe            | $25 Store Credit |                 |
| mattcook          | $10 Store Credit |                 |
| Omgiwon           | $5 Store Credit  |                 |
| cph626            | $10 Store Credit |                 |
| Aaron             | $10 Store Credit |                 |
| Ronfresco         | $25 Store Credit |                 |
| jbbasics          | $5 Store Credit  |                 |
| Bjamps            | $5 Store Credit  |                 |
| MetaJungle        | $5 Store Credit  |                 |
| BigDobs           | $10 Store Credit |                 |
| Xheryk            | $5 Store Credit  |                 |
| Crispjb           | $5 Store Credit  | milvec          |
| cryptoblogger     | $25 Store Credit |                 |
| MetaJungle        | $5 Store Credit  |                 |
| AlphaBlok         | $5 Store Credit  |                 |
| MetaJungle        | $25 Store Credit |                 |
| thampster         | $10 Store Credit |                 |
| Ronfresco         | $25 Store Credit |                 |
| big_bees          | $50 USDC         |                 |
| Bjamps            | $10 Store Credit |                 |
| Ronfresco         | $5 Store Credit  |                 |
| gozags            | $5 Store Credit  | smashngrab77    |
| BigDobs           | $10 Store Credit |                 |
| NiftyMetaGirl     | $5 Store Credit  |                 |
| cph626            | $10 Store Credit |                 |
| Omgiwon           | $10 Store Credit |                 |
| balward           | $5 Store Credit  | radishkabal6    |
| cryptoblogger     | $25 Store Credit |                 |
| mattcook          | $10 Store Credit |                 |
| cryptoblogger     | $5 Store Credit  |                 |
| Infininight       | $5 Store Credit  | chgolitigator   |
| MetaJungle        | $5 Store Credit  | subhubgrading   |
| Aaron             | $25 Store Credit |                 |
| TheRipper         | $25 Store Credit |                 |
| NiftyMetaGirl     | $25 Store Credit |                 |
| Guvv              | $10 Store Credit |                 |
| Ntrprzr           | $25 Store Credit |                 |
| Daveliz55         | $25 Store Credit | galileo         |
| Billcot           | $5 Store Credit  |                 |
| Mvenekam          | $5 Store Credit  |                 |
| Patelh121         | $5 Store Credit  |                 |
| Ronfresco         | $5 Store Credit  |                 |
| accordingtohen    | $5 Store Credit  |                 |
| Pajh07840         | $5 Store Credit  | smashngrab77    |
| cryptoblogger     | $10 Store Credit |                 |
| MetaJungle        | $5 Store Credit  | davidpatrick08  |
| 2048              | $25 Store Credit |                 |
| mattcook          | $25 Store Credit |                 |
| MetaJungle        | $5 Store Credit  |                 |
| tt9s              | $5 Store Credit  |                 |
| RobP343           | $5 Store Credit  |                 |
| Schmoe            | $5 Store Credit  |                 |
| AlphaBlok         | $5 Store Credit  |                 |
| Schmoe            | $5 Store Credit  |                 |
| Billcot           | $5 Store Credit  |                 |
| Mvenekam          | $10 Store Credit |                 |
| Roux1310          | $500 USDC        | acebright86     |
| MetaJungle        | $10 Store Credit |                 |
| Ronfresco         | $5 Store Credit  |                 |
| MetaJungle        | $25 Store Credit |                 |
| Omgiwon           | $10 Store Credit |                 |
| Xheryk            | $5 Store Credit  |                 |
| EpsilonDelta1203  | $10 Store Credit |                 |
| Billcot           | $5 Store Credit  |                 |
| AlphaBlok         | $10 Store Credit |                 |
| Billcot           | $10 Store Credit |                 |
| Patelh121         | $5 Store Credit  |                 |
| Schmoe            | $10 Store Credit |                 |
| 0000              | $5 Store Credit  |                 |
| SDYote            | $10 Store Credit |                 |
| AlphaBlok         | $25 Store Credit |                 |
| Kphamilton        | $5 Store Credit  |                 |
| Schmoe            | $5 Store Credit  |                 |
| MetaJungle        | $5 Store Credit  |                 |
| BigDobs           | $10 Store Credit |                 |
| Patelh121         | $5 Store Credit  |                 |
| Ronfresco         | $25 Store Credit |                 |
| bmw1909           | $5 Store Credit  |                 |
| Xheryk            | $5 Store Credit  |                 |
| Patelh121         | $5 Store Credit  | yoyo909         |
| Patelh121         | $5 Store Credit  |                 |
| MetaJungle        | $5 Store Credit  |                 |
| Ronfresco         | $10 Store Credit |                 |
| yop7              | $5 Store Credit  |                 |
| MetaJungle        | $5 Store Credit  |                 |
| Bjamps            | $5 Store Credit  | smashngrab77    |
| Schmoe            | $25 Store Credit |                 |
| AlphaBlok         | $10 Store Credit |                 |
| Billcot           | $5 Store Credit  |                 |
| Patelh121         | $5 Store Credit  |                 |
| MetaJungle        | $5 Store Credit  |                 |
| jenndunn12m       | $5 Store Credit  |                 |
| Patelh121         | $10 Store Credit |                 |
| AlphaBlok         | $5 Store Credit  |                 |
| Infininight       | $5 Store Credit  |                 |
| MetaJungle        | $10 Store Credit |                 |
| Odin7557          | $5 Store Credit  |                 |
| MetaJungle        | $5 Store Credit  |                 |
| MetaJungle        | $25 Store Credit |                 |
| AlphaBlok         | $5 Store Credit  |                 |
| Ronfresco         | $5 Store Credit  |                 |
| Ronfresco         | $10 Store Credit | davidpatrick08  |
| Ronfresco         | $10 Store Credit |                 |
| deleonlakers2000  | $25 Store Credit |                 |
| Infininight       | $10 Store Credit |                 |
| AlphaBlok         | $25 Store Credit |                 |
| BigDobs           | $10 Store Credit |                 |
| MetaJungle        | $5 Store Credit  |                 |
| Newlin99          | $10 Store Credit | radishkabal6    |
| Bsusko            | $5 Store Credit  |                 |
| College31         | $5 Store Credit  |                 |
| MetaJungle        | $5 Store Credit  |                 |
| PhillyWill        | $25 Store Credit |                 |
| drcrazy           | $5 Store Credit  |                 |
| MetaJungle        | $10 Store Credit |                 |
| Schmoe            | $25 Store Credit |                 |
| bpfergu           | $5 Store Credit  |                 |
| Patelh121         | $5 Store Credit  |                 |
| Schmoe            | $25 Store Credit |                 |
| MetaJungle        | $25 Store Credit |                 |
| deleonlakers2000  | $5 Store Credit  |                 |
| AlphaBlok         | $25 Store Credit |                 |
| tt9s              | $5 Store Credit  |                 |
| Donk3ykong81      | $5 Store Credit  | radishkabal6    |
| bmw1909           | $5 Store Credit  |                 |
| Xheryk            | $5 Store Credit  |                 |
| gozags            | $10 Store Credit |                 |
| Omgiwon           | $25 Store Credit | milvec          |
| Daveliz55         | $5 Store Credit  |                 |
| MetaJungle        | $10 Store Credit |                 |
| Crispjb           | $5 Store Credit  |                 |
| Kyled005          | $10 Store Credit |                 |
| Roux1310          | $10 Store Credit |                 |
| MetaJungle        | $5 Store Credit  |                 |
| Patelh121         | $5 Store Credit  |                 |
| cryptoblogger     | $5 Store Credit  |                 |
| MetaJungle        | $25 Store Credit |                 |
| MetaJungle        | $10 Store Credit |                 |
| NiftyMetaGirl     | $5 Store Credit  |                 |
| Ronfresco         | $25 Store Credit |                 |
| TheGOAT           | $10 Store Credit |                 |
| MetaJungle        | $10 Store Credit |                 |
| SDYote            | $5 Store Credit  |                 |
| Ronfresco         | $5 Store Credit  |                 |
| bmw1909           | $25 Store Credit |                 |
| NiftyMetaGirl     | $5 Store Credit  |                 |
| Kyled005          | $10 Store Credit |                 |
| AlphaBlok         | $10 Store Credit |                 |
| MetaJungle        | $10 Store Credit |                 |
| MetaJungle        | $5 Store Credit  |                 |
| Xheryk            | $5 Store Credit  |                 |
| MetaJungle        | $10 Store Credit |                 |
| Centerpiece       | $10 Store Credit |                 |
| MetaJungle        | $10 Store Credit |                 |
| Patelh121         | $10 Store Credit |                 |
| Brftw             | $10 Store Credit |                 |
| Schmoe            | $5 Store Credit  |                 |
| Schmoe            | $10 Store Credit | viking91107     |
| MetaJungle        | $10 Store Credit |                 |
| Patelh121         | $10 Store Credit |                 |
| EsotericPA        | $5 Store Credit  |                 |
| MetaJungle        | $5 Store Credit  |                 |
| big_bees          | $10 Store Credit |                 |
| Mvenekam          | $500 USDC        |                 |
| heffery           | $25 Store Credit |                 |
| ghedoicy          | $10 Store Credit |                 |
| Schmoe            | $5 Store Credit  |                 |
| BigDobs           | $5 Store Credit  |                 |
| MetaJungle        | $5 Store Credit  |                 |
| Patelh121         | $5 Store Credit  |                 |
| MetaJungle        | $5 Store Credit  |                 |
| BennyZ            | $5 Store Credit  |                 |
| DangerSC          | $5 Store Credit  |                 |
| MetaJungle        | $5 Store Credit  |                 |
| Dublin17          | $25 Store Credit |                 |
| MetaJungle        | $5 Store Credit  |                 |
| MetaJungle        | $5 Store Credit  |                 |
| aaronahaddad      | $5 Store Credit  |                 |
| RobP343           | $10 Store Credit | jimmyd          |
| EpsilonDelta1203  | $10 Store Credit |                 |
| jbbasics          | $5 Store Credit  |                 |
| Leighham          | $50 USDC         |                 |
| MetaJungle        | $5 Store Credit  | radishkabal6    |
| balward           | $5 Store Credit  |                 |
| Billcot           | $25 Store Credit | davidpatrick08  |
| ghedoicy          | $10 Store Credit |                 |
| MetaJungle        | $5 Store Credit  |                 |
| Skybo53           | $10 Store Credit |                 |
| Tsage225          | $5 Store Credit  |                 |
| NiftyMetaGirl     | $5 Store Credit  |                 |
| MetaJungle        | $10 Store Credit |                 |
| MetaJungle        | $5 Store Credit  | radishkabal6    |
| MetaJungle        | $25 Store Credit |                 |
| balward           | $10 Store Credit | bluetitans19    |
| bmw1909           | $5 Store Credit  |                 |
| Schmoe            | $10 Store Credit |                 |
| cph626            | $5 Store Credit  |                 |
| mojaveo           | $5 Store Credit  |                 |
| MetaJungle        | $10 Store Credit |                 |
| AlphaBlok         | $25 Store Credit |                 |
| MetaJungle        | $10 Store Credit |                 |
| jdbeltz           | $5 Store Credit  |                 |
| BigDobs           | $5 Store Credit  |                 |
| AlphaBlok         | $5 Store Credit  |                 |
| heffery           | $25 Store Credit |                 |
| accordingtohen    | $25 Store Credit |                 |
| Omgiwon           | $5 Store Credit  |                 |
| cph626            | $5 Store Credit  |                 |
| james             | $25 Store Credit |                 |
| Titomachado       | $5 Store Credit  |                 |
| Ronfresco         | $5 Store Credit  |                 |
| Patelh121         | $25 Store Credit |                 |
| Newlin99          | $25 Store Credit |                 |
| deleonlakers2000  | $5 Store Credit  |                 |


### References

**shuffle script**

The shuffle script utilizes the random numbered retrieved from the Chainlink VRF as a seed into the [Mersenne Twister](https://en.wikipedia.org/wiki/Mersenne_Twister) algorithm. This allows the resulting shuffled order to be re-created by using the same inputs (original sort order and sorting seed).

**ChainlinkVRF**

ChainlinkVRF is a blockchain powered random number generator. Blokpax uses the ChainlinkVRF as it's random number generator because it guarantees that we [Blokpax] have no prior knowledge of the random value and had no opportunity or capability of tampering with the result. You can read more about the ChainlinkVRF here: [https://docs.chain.link/vrf](https://docs.chain.link/vrf).
