.. _payloads:

Address Payloads
================

Public Key Legacy         
--------------------

20 bytes of the public key hash

Private Key Legacy        
--------------------

32 bytes of the private key

BLSCT Public Address      
--------------------

48 bytes of the public view key ``C`` and 48 bytes of the public spending key ``D``

BLSCT Secret View Key     
---------------------

32 bytes of the private view key ``vmk``

BLSCT Secret Spending Key 
-------------------------

32 bytes of the private spending key ``smk``

Cold Staking v1           
--------------------

20 bytes of the staking public key hash ``PKH_1`` from the ``PK_Staking`` and 20 bytes of the spending public key hash ``PKH_2`` from the public key ``PK_Spending``

Cold Staking v2           
--------------------

20 bytes of the staking public key hash ``PKH_1`` from the public key ``PK_Staking``, 20 bytes of the spending public key hash ``PKH_2`` from the public key ``PK_Spending`` and 20 bytes of the voting public key hash ``PKH_3`` from the public key ``PK_Voting``

Script Address            
--------------------

20 bytes of the script hash

Raw Script Address        
--------------------

The raw encoding of the script

Extended Public Key       
-------------------

1 byte of byte depth, 4 byte of fingerprint, 4 byte of child number, 32 bytes of chain code, 32 bytes of public key

Extended Private Key      
--------------------

1 byte of byte depth, 4 byte of fingerprint, 4 byte of child number, 32 bytes of chain code, 32 bytes of private key

