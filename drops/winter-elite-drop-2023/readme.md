# Winter Elite Drop Distribution Proof

|                   |                                                 |
| ----------------- | ----------------------------------------------- |
| **Drop**          | Winter Elite Drop                         |
| **Ripping Began** | January 31, 2023 3:46 PM EST |

## Assets

There are 74,851 total tokens spread across 71 assets.

| Name | Amount |
|:---- | ------ |
|  T. Brady &#039;02 PSA 7 | 2048 |
|  L. James &#039;03 BGS 10 | 2048 |
|  V. Guerrero Jr. &#039;16 PSA 10 | 2048 |
|  Pudgy Penguin #4734 | 2048 |
|  M. Jordan &#039;96 BGS 9.5 | 2048 |
|  P. Mahomes II &#039;17 BGS 8 | 2048 |
|  L. Bird/J. Erving/M. Johnson ’80 PSA 5 | 2048 |
|  K. Durant &#039;07 PSA 10 | 2048 |
|  W. Gretzky/Gordie Howe &#039;02 BGS 9.5 | 2048 |
|  D. Marino &#039;84 BGS 10 | 2048 |
|  J. Soto &#039;18 PSA 10 | 2048 |
|  H. Aaron &#039;54 SGC 5 | 2048 |
|  K. Mbappé/Corentin Jean &#039;16 PSA 10 | 2048 |
|  M. Jordan/D. Rodman &#039;07 BGS 8 | 2048 |
|  L. Messi &#039;14 PSA 10 | 2048 |
|  J. Herbert &#039;20 BGS 9.5 | 2048 |
|  J. Allen &#039;18 PSA 10 | 2048 |
|  M. Jordan &#039;86 PSA 9 | 2048 |
|  C. Jones &#039;91 PSA 10 | 2048 |
|  L. Dončić &#039;18 PSA 9 | 2048 |
|  T. Brady &#039;00 SGC 10 | 2048 |
|  B. Ruth &#039;99 PSA 9 | 2048 |
|  Silver Eagle &#039;19 PCGS PR70 | 2048 |
|  Bean #468 | 2048 |
|  P. Manning/J. Elway &#039;09 PSA 6 | 2048 |
|  M. Jordan &#039;97 PSA 10 | 2048 |
|  K. Durant &#039;07 BGS 9.5 | 2048 |
|  M. Betts &#039;14 BGS 10 | 2048 |
|  Blokpax First Edition - Punk Trading Cards #10365 | 2048 |
|  L. Dončić &#039;18 PSA 10 | 2048 |
|  M. Trout &#039;11 PSA 10 | 2048 |
|  A. Judge &#039;13 BGS 9.5 | 2048 |
|  K. Griffey Jr. &#039;89 PSA 10 | 2048 |
|  J. Herbert &#039;20 PSA 10 | 2048 |
|  J. Brown &#039;58 PSA 3 | 2048 |
|  Friendship Bracelets by Alexis André #247 &amp; #4881 | 2048 |
|  T. Brady &#039;00 PSA 10 | 16 |
|  Silver Eagle &#039;19 PCGS PR69 | 16 |
|  D. Fox &#039;17 PSA 10 | 16 |
|  G. Antetokounmpo &#039;13 BGS 9 | 16 |
|  M. Machado &#039;10 BGS 9.5 | 16 |
|  T. Lawrence &#039;21 BGS 8 | 16 |
|  K. Durant &#039;07 PSA 10 | 16 |
|  B. Bonds &#039;93 PSA 9 | 16 |
|  P. Mahomes &#039;17 PSA 10 | 16 |
|  J. Butler &#039;12 PSA Auth | 16 |
|  Z. Williamson &#039;19 PSA 10 | 16 |
|  D. Maradona &#039;82 PSA 7 | 16 |
|  A. Edwards &#039;20 PSA 9 | 16 |
|  J. Brown &#039;01 BGS 9 | 16 |
|  J. Fields &#039;20 PSA 10 | 16 |
|  W. Mays &#039;58 PSA 5 | 16 |
|  S. Ohtani &#039;18 BGS 9.5 | 16 |
|  J. Herbert &#039;20 PSA 10 | 16 |
|  T. Williams &#039;55 PSA 5 | 16 |
|  R. Clemens &#039;85 PSA 10 | 16 |
|  L. Hamilton &#039;20 PSA 10 | 16 |
|  S. Bird &#039;05 PSA 10 | 16 |
|  J. Morant &#039;19 PSA 10 | 16 |
|  K. Griffey Jr. &#039;89 PSA 10 | 16 |
|  J. Burrow &#039;20 SGC 10 | 16 |
|  Tesla Allow List Spot | 500 |
|  Bored &amp; Dangerous: Money Train | 23 |
|  Lost Miner #2019 | 1 |
|  Lost Miner | 20 |
|  Bobby Jones Aqua Tier Collision Mint Spot | 100 |
|  Bobby Jones Blue Tier Collision Mint Spot | 30 |
|  Bobby Jones Red Tier Collision Mint Spot | 6 |
|  Bobby Jones Gold Tier Collision Mint Spot | 2 |
|  Bobby Jones Black Tier (1/1) Collision Mint Spot | 1 |
|  Winter Elite Drop Instant Winner | 40 |

## Overview

### Building the card list

1. For each asset, we create `n` cards, where `n` is the amount of each asset that will be issued.
2. We get a random number from the blockchain (using the process described [below](#collection-random)). We use that number, `108366388455798059830830269081476012863892403535492303770594357879143278561165`, to seed our PRNG and shuffle our list of cards. By using the blockchain random number to seed our PRNG, we guarantee that our shuffle is deterministic and that its randomness comes from the blockchain.

### Assigning cards to participants

1. Using the method described in Appendix B, we derive a list of entry tickets for the participants, hash it, and submit that hash up to the on-chain random oracle to request a random number. (Each participant gets 1 ticket per pack/card owed.)
2. Using the method described in Appendix C, we seed our PRNG with the random number and shuffle the list of tickets.
3. Finally, we join the shuffled list of tickets with the randomized list of cards. Ticket #1 gets Card #1, Ticket #2 gets Card #2, and so on.

> ℹ️ This process may be repeated if there are tickets that are initially unowned. The second operation will only operate on unassigned tickets and unassigned cards, using the existing sort order for the cards. All fulfillment operations are detailed in [Appendix E](#appendix-e-ticket-fulfillments).

## Appendix A: Getting the random number for a drop

1. We create our hash using a minified version of this object:

   ```json
   {
       "collection": 45,
       "assets": {
           "4520": 2048,
           "4521": 2048,
           "4522": 2048,
           "4523": 2048,
           "4524": 2048,
           "4525": 2048,
           "4526": 2048,
           "4527": 2048,
           "4528": 2048,
           "4529": 2048,
           "4530": 2048,
           "4531": 2048,
           "4532": 2048,
           "4533": 2048,
           "4534": 2048,
           "4535": 2048,
           "4536": 2048,
           "4537": 2048,
           "4538": 2048,
           "4539": 2048,
           "4540": 2048,
           "4541": 2048,
           "4542": 2048,
           "4543": 2048,
           "4544": 2048,
           "4545": 2048,
           "4546": 2048,
           "4547": 2048,
           "4548": 2048,
           "4549": 2048,
           "4550": 2048,
           "4551": 2048,
           "4552": 2048,
           "4553": 2048,
           "4554": 2048,
           "4555": 2048,
           "4556": 16,
           "4557": 16,
           "4558": 16,
           "4559": 16,
           "4560": 16,
           "4561": 16,
           "4562": 16,
           "4563": 16,
           "4564": 16,
           "4565": 16,
           "4566": 16,
           "4567": 16,
           "4568": 16,
           "4569": 16,
           "4570": 16,
           "4571": 16,
           "4572": 16,
           "4573": 16,
           "4574": 16,
           "4575": 16,
           "4576": 16,
           "4577": 16,
           "4578": 16,
           "4579": 16,
           "4580": 16,
           "4621": 500,
           "4622": 23,
           "4623": 1,
           "4624": 20,
           "4625": 100,
           "4626": 30,
           "4627": 6,
           "4628": 2,
           "4629": 1,
           "4631": 40
       }
   }
   ```

2. We `sha256` that object, which yields a result of `91ee42127f684f6c424aee34d50f21c963541561da18d4436e0f29c06745631e`.

3. We send that hash up to the on-chain random oracle to request our random number.

4. We use the contract method [`getGeneratedRandomNumber`](https://polygonscan.com/readContract?m=normal&a=0xff5521e314871bcc672bcde1b83b7d3c194a5d35&v=0xff5521e314871bcc672bcde1b83b7d3c194a5d35&t=false#readCollapse2) to return the random number tied to our hash. (You can supply `0x91ee42127f684f6c424aee34d50f21c963541561da18d4436e0f29c06745631e` to retrieve this number from the linked page.)

   |     |     |
   | --- | --- |
   | Hash          | `91ee42127f684f6c424aee34d50f21c963541561da18d4436e0f29c06745631e` |
   | Transaction   | [`0xcb54e5d5aff716a4ed95f89c547f6d774acc07bb2aa9bd0f8dbfaf18e6f13b0c`](https://polygonscan.com/tx/0xcb54e5d5aff716a4ed95f89c547f6d774acc07bb2aa9bd0f8dbfaf18e6f13b0c) |
   | Random Number | `108366388455798059830830269081476012863892403535492303770594357879143278561165` |

## Appendix B: Getting a random number for a collection of entry tickets

1. Every participant has one or more tickets assigned to them in a 1:1 ratio with how many cards/packs they are owed. We start with a list of these tickets, sorted by user ID, and exclude any tickets that have already been assigned. Then we produce an object containing this list, a nonce, and the tickets.

2. We minify this object and `sha256` it to produce our hash. For example: `76c218477db7823f67814130074a93ae3e99e6822291961a6b577b08fefa6550`.

3. We submit that hash to the on-chain random oracle to request our random number ([transaction](https://polygonscan.com/tx/0x31a96cd3a1cc07ff5fc7328d598496c8fb2406057d9a59e0a8935b1023548e39)).

4. We use the contract method [`getGeneratedRandomNumber`](https://polygonscan.com/readContract?m=normal&a=0xff5521e314871bcc672bcde1b83b7d3c194a5d35&v=0xff5521e314871bcc672bcde1b83b7d3c194a5d35&t=false#readCollapse2) to return the random number tied to our hash. (You can supply `0x76c218477db7823f67814130074a93ae3e99e6822291961a6b577b08fefa6550` to retrieve this number from the linked page.)

## Appendix C: Seeding the PRNG

To seed the PRNG, we need to pass a random number into PHP's `mt_srand` function. The random number that comes back from the chain is too large, so we modulus it against `PHP_INT_MAX`, like so:

```php
$seed = gmp_intval(gmp_mod(gmp_init($randomNumber, 10), PHP_INT_MAX));
mt_srand($seed);

// The PRNG is now seeded, we can now use the shuffle built-in function.
```

## Appendix D: Cards

Here's the list of cards we distributed to users based on the randomized sort order and randomized order fulfillment(s). It's separated into segments of 2,500 cards each to make it easier to display.

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
- [72500 - 74850](cards-72500.md)

## Appendix E: Ticket Fulfillments


|     |     |
| --- | --- |
| **Fulfillment ID** | `11` |
| **Content** | [fulfillment-11.json](./fulfillment-11.json) |
| **Hash**           | `76c218477db7823f67814130074a93ae3e99e6822291961a6b577b08fefa6550` |
| **Transaction**    | [`0x31a96cd3a1cc07ff5fc7328d598496c8fb2406057d9a59e0a8935b1023548e39`](https://polygonscan.com/tx/0x31a96cd3a1cc07ff5fc7328d598496c8fb2406057d9a59e0a8935b1023548e39) |
| **Random Number**  | `7080180811481138093834144454793310198104933793374971848332571049426764552455` |
| **Created**        | January 31, 2023 2:01 PM EST |
