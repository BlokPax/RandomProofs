# Unclaimed Lost Miners Dispersal

At the end of the Lost Miners claim period, we sent all unclaimed Lost Miners to random Ethereum addresses, a process we called The Dispersal. These miners are the Forever Lost, impossible to find without the private key associated with the wallet it lives in. (It is possible that one day these private keys will be derived or guessed, but it's statisically extremely unlikely to happen for a very long time.)

## The Process

1. After the claim window ended, we [requested five random numbers](https://etherscan.io/tx/0xf1d7beebc2851076987421be787d2c63ffdaa58cb70aa244f2841f2d5754f3e2) from our on-chain random contract.
2. We separated the 432 unclaimed Miners into batches of 100 each at most (the last batch contained 32), and submitted [transactions](#transactions) to our [Disperse](0xDF9C04D9eC2AD46CeC6593Fd00A26572207391D9) contract.
3. Each transaction calculated an address for each Lost Miner on-chain, using a hash of the random seed, the timestamp of the current block, and the index of the Lost Miner in the submitted batch. Then we truncated the hash to 160 bits and converted the result into an address. Because the address was derived in this way, no private key ever existed and thus was never known to anyone.

## The Forever Lost Miners

| Token |
| ----- |
| 97    |
| 175   |
| 178   |
| 179   |
| 230   |
| 253   |
| 268   |
| 311   |
| 344   |
| 366   |
| 378   |
| 415   |
| 421   |
| 423   |
| 444   |
| 482   |
| 509   |
| 514   |
| 576   |
| 597   |
| 599   |
| 603   |
| 629   |
| 657   |
| 667   |
| 674   |
| 678   |
| 688   |
| 694   |
| 703   |
| 718   |
| 731   |
| 743   |
| 754   |
| 796   |
| 809   |
| 815   |
| 864   |
| 927   |
| 1002  |
| 1022  |
| 1033  |
| 1057  |
| 1060  |
| 1066  |
| 1068  |
| 1111  |
| 1121  |
| 1124  |
| 1128  |
| 1151  |
| 1180  |
| 1204  |
| 1213  |
| 1226  |
| 1245  |
| 1251  |
| 1294  |
| 1323  |
| 1327  |
| 1328  |
| 1354  |
| 1388  |
| 1400  |
| 1403  |
| 1441  |
| 1469  |
| 1470  |
| 1511  |
| 1551  |
| 1596  |
| 1599  |
| 1650  |
| 1660  |
| 1708  |
| 1724  |
| 1806  |
| 1819  |
| 1840  |
| 1855  |
| 1856  |
| 1880  |
| 1912  |
| 1916  |
| 1930  |
| 1966  |
| 1997  |
| 2002  |
| 2033  |
| 2054  |
| 2061  |
| 2063  |
| 2126  |
| 2138  |
| 2183  |
| 2184  |
| 2188  |
| 2195  |
| 2205  |
| 2238  |
| 2245  |
| 2251  |
| 2283  |
| 2285  |
| 2321  |
| 2358  |
| 2368  |
| 2391  |
| 2405  |
| 2425  |
| 2433  |
| 2491  |
| 2495  |
| 2563  |
| 2653  |
| 2662  |
| 2664  |
| 2685  |
| 2696  |
| 2725  |
| 2728  |
| 2738  |
| 2754  |
| 2755  |
| 2761  |
| 2766  |
| 2772  |
| 2780  |
| 2786  |
| 2794  |
| 2816  |
| 2833  |
| 2844  |
| 2867  |
| 2910  |
| 2912  |
| 2942  |
| 2990  |
| 2996  |
| 2998  |
| 3000  |
| 3041  |
| 3078  |
| 3092  |
| 3120  |
| 3122  |
| 3133  |
| 3135  |
| 3136  |
| 3145  |
| 3162  |
| 3163  |
| 3192  |
| 3240  |
| 3253  |
| 3289  |
| 3305  |
| 3309  |
| 3373  |
| 3377  |
| 3386  |
| 3404  |
| 3417  |
| 3434  |
| 3437  |
| 3441  |
| 3442  |
| 3544  |
| 3546  |
| 3549  |
| 3577  |
| 3588  |
| 3602  |
| 3680  |
| 3684  |
| 3759  |
| 3761  |
| 3771  |
| 3788  |
| 3799  |
| 3826  |
| 3865  |
| 3891  |
| 3900  |
| 3930  |
| 3939  |
| 3953  |
| 3958  |
| 3971  |
| 4046  |
| 4050  |
| 4060  |
| 4091  |
| 4124  |
| 4139  |
| 4150  |
| 4189  |
| 4191  |
| 4243  |
| 4288  |
| 4292  |
| 4354  |
| 4358  |
| 4422  |
| 4433  |
| 4468  |
| 4517  |
| 4531  |
| 4552  |
| 4571  |
| 4578  |
| 4580  |
| 4585  |
| 4630  |
| 4633  |
| 4636  |
| 4638  |
| 4641  |
| 4666  |
| 4698  |
| 4705  |
| 4719  |
| 4720  |
| 4762  |
| 4847  |
| 4865  |
| 4887  |
| 4890  |
| 4905  |
| 4926  |
| 4932  |
| 4940  |
| 4953  |
| 4998  |
| 4999  |
| 5008  |
| 5019  |
| 5041  |
| 5058  |
| 5079  |
| 5100  |
| 5172  |
| 5191  |
| 5205  |
| 5267  |
| 5280  |
| 5296  |
| 5340  |
| 5341  |
| 5397  |
| 5410  |
| 5430  |
| 5503  |
| 5521  |
| 5527  |
| 5555  |
| 5577  |
| 5635  |
| 5730  |
| 5756  |
| 5822  |
| 5831  |
| 5844  |
| 5870  |
| 5883  |
| 5897  |
| 6028  |
| 6040  |
| 6080  |
| 6089  |
| 6125  |
| 6141  |
| 6162  |
| 6263  |
| 6269  |
| 6270  |
| 6300  |
| 6340  |
| 6344  |
| 6353  |
| 6375  |
| 6378  |
| 6400  |
| 6456  |
| 6458  |
| 6484  |
| 6499  |
| 6503  |
| 6539  |
| 6557  |
| 6576  |
| 6582  |
| 6583  |
| 6590  |
| 6602  |
| 6603  |
| 6604  |
| 6652  |
| 6678  |
| 6681  |
| 6712  |
| 6719  |
| 6730  |
| 6832  |
| 6942  |
| 6987  |
| 6988  |
| 6992  |
| 7011  |
| 7054  |
| 7084  |
| 7108  |
| 7110  |
| 7139  |
| 7148  |
| 7239  |
| 7244  |
| 7282  |
| 7295  |
| 7301  |
| 7360  |
| 7365  |
| 7379  |
| 7391  |
| 7395  |
| 7425  |
| 7451  |
| 7461  |
| 7465  |
| 7475  |
| 7486  |
| 7497  |
| 7527  |
| 7540  |
| 7548  |
| 7573  |
| 7666  |
| 7683  |
| 7757  |
| 7762  |
| 7767  |
| 7779  |
| 7781  |
| 7789  |
| 7795  |
| 7806  |
| 7848  |
| 7853  |
| 7862  |
| 7883  |
| 7917  |
| 7940  |
| 7965  |
| 7998  |
| 8005  |
| 8010  |
| 8044  |
| 8068  |
| 8094  |
| 8097  |
| 8168  |
| 8214  |
| 8244  |
| 8278  |
| 8293  |
| 8369  |
| 8380  |
| 8384  |
| 8395  |
| 8426  |
| 8495  |
| 8513  |
| 8545  |
| 8579  |
| 8646  |
| 8660  |
| 8691  |
| 8738  |
| 8755  |
| 8756  |
| 8775  |
| 8801  |
| 8848  |
| 8899  |
| 8941  |
| 8942  |
| 8949  |
| 8950  |
| 8957  |
| 8974  |
| 8987  |
| 8990  |
| 9020  |
| 9072  |
| 9076  |
| 9079  |
| 9090  |
| 9094  |
| 9109  |
| 9113  |
| 9125  |
| 9162  |
| 9196  |
| 9216  |
| 9225  |
| 9303  |
| 9338  |
| 9361  |
| 9363  |
| 9366  |
| 9390  |
| 9405  |
| 9581  |
| 9645  |
| 9677  |
| 9704  |
| 9742  |
| 9782  |
| 9796  |
| 9797  |
| 9804  |
| 9805  |
| 9843  |
| 9845  |
| 9861  |
| 9868  |
| 9869  |
| 9887  |
| 9911  |
| 9915  |
| 9916  |
| 9998  |

## Transactions

| Description | Transaction Hash                                                                                                                                                   |
| ----------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Random      | [`0xf1d7beebc2851076987421be787d2c63ffdaa58cb70aa244f2841f2d5754f3e2`](https://etherscan.io/tx/0xf1d7beebc2851076987421be787d2c63ffdaa58cb70aa244f2841f2d5754f3e2) |
| Batch 1     | [`0xc1fffe9f23873d161455df490e4cfce41ada40c1ff901ea450755886008db0f0`](https://etherscan.io/tx/0xc1fffe9f23873d161455df490e4cfce41ada40c1ff901ea450755886008db0f0) |
| Batch 2     | [`0x0d5d313a6c73bfdf88a1480f708fd7f6b39c88949e07eeacde5c1c085f6a0770`](https://etherscan.io/tx/0x0d5d313a6c73bfdf88a1480f708fd7f6b39c88949e07eeacde5c1c085f6a0770) |
| Batch 3     | [`0xc7b7cd73b597b5ece624614cc626a1b473ff01f2a7d0cc3f2418b10c3c43cd6a`](https://etherscan.io/tx/0xc7b7cd73b597b5ece624614cc626a1b473ff01f2a7d0cc3f2418b10c3c43cd6a) |
| Batch 4     | [`0x7797f45b9a70f952c18c240c26e9068b6c82f6f2d9a4cf68dda784db9d26602c`](https://etherscan.io/tx/0x7797f45b9a70f952c18c240c26e9068b6c82f6f2d9a4cf68dda784db9d26602c) |
| Batch 5     | [`0x02eff40c71d3300c2be0c0c78ca2d5f521d8320ce4a991d4aff35d722e53a3a0`](https://etherscan.io/tx/0x02eff40c71d3300c2be0c0c78ca2d5f521d8320ce4a991d4aff35d722e53a3a0) |