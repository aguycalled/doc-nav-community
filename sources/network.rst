.. _network:

Network parameters
==================

========================= =========================================================================== ===========================================================================
Parameter                 Mainnet                                                                     Testnet
========================= =========================================================================== ===========================================================================
P2P Port                  44440                                                                       15556
RPC Port                  44444                                                                       44445
Message Start             0x80503420                                                                  0x3224f217
Genesis Block             0x00006a4e3e18c71c6d48ad6c261e2254fa764cf29607a4357c99b712dfbb8e6a          0x0000e0870ba071bb91a28a624f39d92959c4b6fd539d269b0dfcc46f253c3104
Genesis Merkle Root       0xc507eec6ccabfd5432d764afceafba42d2d946594b8a60570cb2358a7392c61a          0x97148c18a758d7b06b25294d25e86608d7619f0eab79ab855691233050d6687f
Genesis Timestamp         1460561040                                                                  1606327577
Genesis Nonce             6945                                                                        2043919587
DNS Seed                  seed.nav.community, seed2.nav.community                                     testseed.nav.community
========================= =========================================================================== ===========================================================================

.. _network-version-bytes:

Version bytes
-------------

========================= =========================================================================== ===========================================================================
Address type              Mainnet                                                                     Testnet
========================= =========================================================================== ===========================================================================
Public Key Legacy         53                                                                          111
Private Key Legacy        150                                                                         239
BLSCT Public Address      73, 33                                                                      73, 33
BLSCT Secret View Key     151, 181                                                                    151, 181
BLSCT Secret Spending Key 152, 20                                                                     152, 20
Cold Staking v1           21                                                                          8
Cold Staking v2           36                                                                          32
Script Address            85                                                                          196
Raw Script Address        60                                                                          60
Extended Public Key       0x0488B21E                                                                  0x0488B21E
Extended Private Key      0x0x88ADE4                                                                  0x0x88ADE4
========================= =========================================================================== ===========================================================================

.. _network-addresses:

Address Formats for Mainnet
---------------------------

Exchanges and wallets are required to allow withdrawals to the following type of addresses:

========================= ============= ========== ===========================================================================================================================================
Address type              Starts with   Length     Example                                                       
========================= ============= ========== ===========================================================================================================================================
Public Key Legacy         N             34         NiMNbr141gHve9ER2i64S9nbR1USBbALji                                                             
BLSCT Public Address      xN            139        xNU4LXCWHvYXYGG2i8X4QhFRH4FoCRd4q5bJUQLF4crnnnuCDPPXMK5gD78wU7cJ9VQMawMNSbtpwgQUnXmZTkJK9fUfJnSUFYxDaQcdSA5MaN8ghPrNxGnMNsuz7ywwaxVboWXRo95                                                             
Cold Staking v1           X             61         Xfm2AbCgLBjk792bTXwzFRvWDazszidsfy4xg2HMPnEjZYN87mGBREXwLNWee
Cold Staking v1           Y             61         YR6W9iTiwFrRXkySu5jGyP8rjqfbNXj7AZ9ugPHhiNnPMSKdxHzbSmFnBGA8D                                                  
Cold Staking v2           4             89         4DtQXPrQz3nXV1iGQgrdnFv5AT1ouDzbfmd6yBVrVhAtPL6jE3ofebTygGbJbSGmTUd9wBH3WDoyAJkS9vQ2KtKCd                                                                          
========================= ============= ========== ===========================================================================================================================================
