# Elite Drop #3 Distribution Proof

|                   |                                                 |
| ----------------- | ----------------------------------------------- |
| **Drop**          | Elite Drop #3                         |
| **Ripping Began** | May 15, 2022 4:00 PM EDT |

## Assets

There are 74,400 total tokens spread across 48 assets.

| Name | Amount |
|:---- | ------ |
| A. Judge &#039;13 BGS 10 | 2048 |
| A. Edwards &#039;20 PSA 10 | 2048 |
| B. Ruth &#039;99 SGC A | 2048 |
| B. Jackson/K. Griffey Jr./F. Thomas &#039;13 PSA 10 | 2048 |
| Charizard &#039;02 PSA 9 | 2048 |
| C. McGregor &#039;13 PSA 10 | 2048 |
| C. Monster R &#039;20 BGS 9 | 2048 |
| D. Samuel &#039;19 PSA 10 | 2048 |
| H. Aaron &#039;54 SGC 8 | 2048 |
| J. Robinson &#039;53 PSA 2.5 | 2048 |
| J. Burrow &#039;20 PSA 8 | 2048 |
| J. Unitas &#039;00 PSA 10 | 2048 |
| J. Allen &#039;18 PSA 10 | 2048 |
| J. Soto &#039;16 BGS 9.5 | 2048 |
| J. Herbert &#039;20 PSA 9 | 2048 |
| K. Durant &#039;07 BGS 9 | 2048 |
| K. Bryant &#039;09 BGS 8.5 | 2048 |
| L. Fitzgerald &#039;04 BGS 9 | 2048 |
| L. James &#039;08 PSA 10 | 2048 |
| Legend Geek Mint Pass | 2048 |
| L. Messi &#039;17 PSA 10 | 2048 |
| L. Pikachu &#039;16 PSA 10 | 2048 |
| L. Robert &#039;18 BGS 9.5 | 2048 |
| M. Jordan &#039;97 PSA 10 | 2048 |
| M. Trout &#039;11 BGS 10 | 2048 |
| Moonbird #3645 | 2048 |
| R. Nadal &#039;03 PSA 10 | 2048 |
| Spider-Man &#039;84 CGC 9.8 | 2048 |
| Spider-Man &#039;95 PSA 10 | 2048 |
| S. Mario Bros. &#039;85 WATA 8 | 2048 |
| T. Brady &#039;00 BGS 9.5 | 2048 |
| T. Hawk &#039;15 BGS 9.5 | 2048 |
| T. Lawrence &#039;21 PSA 10 | 2048 |
| VaynerSports Pass #11830 | 2048 |
| VeeFriends Series 2 - Like a Sponge #35902 | 2048 |
| W. Gretzky &#039;97 SGC 8.5 | 2048 |
| Abe Collision.art Great Emancipator Edition Mint Spot (1/1) | 1 |
| Abe Collision.art Diamond Edition Mint Spot (1/5) | 2 |
| Abe Collision.art Ruby Edition Mint Spot (1/25) | 6 |
| Abe Collision.art Gold Edition Mint Spot (1/150) | 30 |
| Abe Collision.art Moonlight Edition Mint Spot (1/360) | 100 |
| &#039;93 MTG Mox Sapphire BGS 9.5 Crowdslabs Unit | 293 |
| Elite Drop #3 Instant Winner | 50 |
| Secret Society of Whales Instant Winner | 20 |
| VIP Ticket to National Sports Collector Convention 2022 | 45 |
| Barefoot Parrots Instant Winner | 20 |
| Blokpax Hat Instant Winner | 100 |
| Hero Geek Mint Pass | 5 |

## Overview

### Building the card list

1. For each asset, we create `n` cards, where `n` is the amount of each asset that will be issued.
2. We get a random number from the blockchain (using the process described [below](#collection-random)). We use that number, `17897866774206174622852599286316699309306291299498196629121912367361720555170`, to seed our PRNG and shuffle our list of cards. By using the blockchain random number to seed our PRNG, we guarantee that our shuffle is deterministic and that its randomness comes from the blockchain.

### Fulfilling orders

1. Orders are fulfilled in order they were created. For each order, we request a random number from the blockchain (using the process described [below](#order-random)).

2. Each order has a number of tickets that function as a placeholder for a card; we use the random number for the order to seed the PRNG and shuffle this list of tickets.

   > Note: sometimes the number of orders for a drop isn't the same as the number of participants. This can happen because participants can gain entries into the drop some other way than buying Pax directly, like buying Moments Boxes, or buying Moments on OpenSea. We still use orders internally to keep track of tickets as they're allocated and assigned to users.

3. We gather a list of all _unassigned_ cards, in the order they were originally randomized. By rule there will be at least as many unassigned cards as there are tickets in this given order.

4. We calculate a starting index using the same random number, like so:

   ```
   startIndex = randomNumber % numberOfUnassignedCards
   ```

5. Starting on the `startingIndex`th entry in the list of cards, we assign all of the order's tickets sequentially. If the index exceeds the number of unassigned cards, we roll over to the top of the list (index 0).

#### Example

Say our order has `13` tickets, there are `30` unassigned cards, and our random number is `441`. Our `startIndex` is `441 % 30 = 21`. We assign our tickets to cards `21-29`, and then roll over to the top of the list and assign `0-3`, giving us `13` cards for our `13` tickets.

| Index | Assigned? |     |
| ----- | --------- | --- |
| `0` | ✅ |  |
| `1` | ✅ |  |
| `2` | ✅ |  |
| `3` | ✅ |  |
| `4` |  |  |
| `5` |  |  |
| `6` |  |  |
| `7` |  |  |
| `8` |  |  |
| `9` |  |  |
| `10` |  |  |
| `11` |  |  |
| `12` |  |  |
| `13` |  |  |
| `14` |  |  |
| `15` |  |  |
| `16` |  |  |
| `17` |  |  |
| `18` |  |  |
| `19` |  |  |
| `20` |  |  |
| `21` | ✅ | ⬅️ Start |
| `22` | ✅ |  |
| `23` | ✅ |  |
| `24` | ✅ |  |
| `25` | ✅ |  |
| `26` | ✅ |  |
| `27` | ✅ |  |
| `28` | ✅ |  |
| `29` | ✅ |  |

## Appendix A: Getting the random number for a drop

1. We create our hash using a minified version of this object:

   ```json
   {
       "collection": 26,
       "assets": {
           "1754": 2048,
           "1755": 2048,
           "1756": 2048,
           "1757": 2048,
           "1758": 2048,
           "1759": 2048,
           "1760": 2048,
           "1761": 2048,
           "1762": 2048,
           "1763": 2048,
           "1764": 2048,
           "1765": 2048,
           "1766": 2048,
           "1767": 2048,
           "1768": 2048,
           "1769": 2048,
           "1770": 2048,
           "1771": 2048,
           "1772": 2048,
           "1773": 2048,
           "1774": 2048,
           "1775": 2048,
           "1776": 2048,
           "1777": 2048,
           "1778": 2048,
           "1779": 2048,
           "1780": 2048,
           "1781": 2048,
           "1782": 2048,
           "1783": 2048,
           "1784": 2048,
           "1785": 2048,
           "1786": 2048,
           "1787": 2048,
           "1788": 2048,
           "1789": 2048,
           "1840": 1,
           "1841": 2,
           "1842": 6,
           "1843": 30,
           "1844": 100,
           "1845": 293,
           "1846": 50,
           "1847": 20,
           "1848": 45,
           "1849": 20,
           "1850": 100,
           "1851": 5
       }
   }
   ```

2. We `sha256` that object, which yields a result of `254757a10fb0f3a7b6453c6849538576d74fd30c3a850337cf067466be0badd4`.

3. We send that hash up to the on-chain random oracle to request our random number.

4. We use the contract method [`getGeneratedRandomNumber`](https://polygonscan.com/readContract?m=normal&a=0xff5521e314871bcc672bcde1b83b7d3c194a5d35&v=0xff5521e314871bcc672bcde1b83b7d3c194a5d35&t=false#readCollapse2) to return the random number tied to our hash. (You can supply `0x254757a10fb0f3a7b6453c6849538576d74fd30c3a850337cf067466be0badd4` to retrieve this number from the linked page.)

   |     |     |
   | --- | --- |
   | Hash          | `254757a10fb0f3a7b6453c6849538576d74fd30c3a850337cf067466be0badd4`                                                                             |
   | Transaction   | [`0xf85b2ef562341436280a1a82a4bdc6d5decfafa5c10d527a5f900f0bf019fc80`](https://polygonscan.com/tx/0xf85b2ef562341436280a1a82a4bdc6d5decfafa5c10d527a5f900f0bf019fc80) |
   | Random Number | `17897866774206174622852599286316699309306291299498196629121912367361720555170`                                                                            |

## Appendix B: Getting a random number for an order

1. We create our hash using the hash content for the order (listed in appendix D), minifying it and sha256-ing it.
2. We send that hash up to the on-chain random oracle to request our random number.
3. We use the contract method [`getGeneratedRandomNumber`](https://polygonscan.com/readContract?m=normal&a=0xff5521e314871bcc672bcde1b83b7d3c194a5d35&v=0xff5521e314871bcc672bcde1b83b7d3c194a5d35&t=false#readCollapse2) to return the random number tied to our hash. (You can supply `0x254757a10fb0f3a7b6453c6849538576d74fd30c3a850337cf067466be0badd4` to retrieve this number from the linked page.)

   > All orders have their hash content and derived hash included in the table in Appendix D.

## Appendix C: Seeding the PRNG

To seed the PRNG, we need to pass a random number into PHP's `mt_srand` function. The random number that comes back from the chain is too large, so we modulus it against `PHP_INT_MAX`, like so:

```php
$seed = gmp_intval(gmp_mod(gmp_init($randomNumber, 10), PHP_INT_MAX));
mt_srand($seed);

// The PRNG is now seeded, we can now use the shuffle built-in function.
```

## Appendix D: Orders

| ID /<br>Date | Quantity | Hash Content | Hash | Random Number | Transaction |
| --- | --- | --- | --- | --- | --- |
| `H4XY-YXYJ-0QWB`<br>5/12/22 16:39:51 EDT | 74,400 | <details><summary>Show</summary> `{"hash_secret":"3f6a80a00e5210dbed357a3abe7ef5c43ff9ef7c0e0116f23780e6a1e03604fd","order_id":12668,"username":"blokpaxdealer","created_time":"2022-05-12 20:39:51","ordered_items":{"26":74400}}`</details> | <details><summary>Show</summary> `1a280b1ed85e73eeb4493698c6602cae08e31a36e3a7402da3e491daf9084d6c`</details> | <details><summary>Show</summary> `83194885066578440810285638061767553708955259781689751864198596674036263282173`</details> | [`0xd312723c640def0156bc0fcadc045250ce1ff7c94acc686e523548070e82f04e`](https://polygonscan.com/tx/0xd312723c640def0156bc0fcadc045250ce1ff7c94acc686e523548070e82f04e) |

## Appendix E: Cards

Here's the list of cards we distributed to users based on the randomized sort order and randomized order fulfillment(s). It's separated into segments of 5000 cards each to make it easier to display.

- [0 - 2499](cards-0.md)
- [2500 - 4999](cards-2500.md)
- [5000 - 7499](cards-5000.md)
- [7500 - 9999](cards-7500.md)
- [10000 - 12499](cards-10000.md)
- [12500 - 14999](cards-12500.md)
- [15000 - 17499](cards-15000.md)
- [17500 - 19999](cards-17500.md)
- [20000 - 22499](cards-20000.md)
- [22500 - 24999](cards-22500.md)
- [25000 - 27499](cards-25000.md)
- [27500 - 29999](cards-27500.md)
- [30000 - 32499](cards-30000.md)
- [32500 - 34999](cards-32500.md)
- [35000 - 37499](cards-35000.md)
- [37500 - 39999](cards-37500.md)
- [40000 - 42499](cards-40000.md)
- [42500 - 44999](cards-42500.md)
- [45000 - 47499](cards-45000.md)
- [47500 - 49999](cards-47500.md)
- [50000 - 52499](cards-50000.md)
- [52500 - 54999](cards-52500.md)
- [55000 - 57499](cards-55000.md)
- [57500 - 59999](cards-57500.md)
- [60000 - 62499](cards-60000.md)
- [62500 - 64999](cards-62500.md)
- [65000 - 67499](cards-65000.md)
- [67500 - 69999](cards-67500.md)
- [70000 - 72499](cards-70000.md)
- [72500 - 74399](cards-72500.md)
