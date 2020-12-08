.. _coldstaking:

Cold Staking
============

Cold Staking is the process of staking using a key that does not have spending rights, thus allowing the participation in the staking with cold stored coins. Users can refer to `The Ultimate Guide to Staking <https://navcoin.medium.com/navcoin-the-ultimate-guide-to-staking-its-never-been-so-easy-c0ef2f9983c8>`_ for a guide on how to setup a node together with NavCash and optionally the Ledger Hardware wallet. If you are a SaaS (Staking as a Service) provider, please read this page.

Setting up a staking node
-------------------------

The first step is to run a staking node. Please refer to :ref:`get_nav` for detailed instructions on how to set up a node. A staking node is no other than a NavCoin Core node with the flag ``staking`` set to ``1``. This is the default setting if none is specified. See :ref:`passing_options` to learn how to pass a setting to the daemon. This node has **to stay online** to participate in staking.

Once this node is running, you need to get a public address ``PK_Staking`` whose private key is owned by the node. This is possible using the RPC command ``getnewaddress`` or in the ``Receive`` tab of the GUI wallet.

Generating the spending key
---------------------------

Second step is to generate a spending key ``PK_Spending``. It is recommended to generate this key using an off-line enviroment for maximum security. This key will only come online whenever the coins are going to be spent, namely, sent out of the Cold Staking.

Recommended methods for generating an offline key is running an instance of NavCoin Core or using `NavPaper <https://paper.navcoin.org/>`_ in an airgapped device.

Sending coins to Cold Staking (v1)
----------------------------------

.. note::

   Using Cold Staking v1, ``PK_Staking`` will hold both the staking and voting rights of the coins. If you are running a staking node as a SaaS (Staking as a Service), because you are a staking pool or exchange, and you won't participate in the DAO votings or allow your delegators to set up individual votes or allow your delegators to specify their own voting address, you need to set the ``excludevote`` flag to ``1``, in order to exclude your blocks from the DAO quorum.

To obtain a Cold Staking v1 address, you can use the following RPC command::

   getcoldstakingaddress <PK_Staking> <PK_Spending>

Alternatively, you can construct a Cold Staking v1 address encoding the address prefix (refer to :ref:`network`) and :ref:`payloads` using :ref:`base58check`.

The output will be the Cold Staking address, where you will able to send the coins to cold stake. If you do not use RPC commands or a compatible library for the transfer of coins, please refer to :ref:`p2cs` to learn how to build the standard script for P2CS.

Sending coins to Cold Staking (v2)
----------------------------------

.. note::

   This is the preferred mode for SaaS (Staking as a Service) providers, or if you are an user and want to be able to vote from a light wallet like `NavCash <https://navcash.nav.community>`_.

For setting Cold Staking v2, you will need a third address ``PK_Voting``. If you are a SaaS provider, you must get this address from your delegator. If you use NavCash, you can get this address creating a ``Voting Wallet``.

To obtain a Cold Staking v2 address, you can use the following RPC command::

   getcoldstakingaddress <PK_Staking> <PK_Spending> <PK_Voting>

Alternatively, you can construct a Cold Staking v2 address encoding the address prefix (refer to :ref:`network`) and :ref:`payloads` using :ref:`base58check`.

The output will be the Cold Staking address, where you will able to send the coins to cold stake while having the voting rights delegated to ``PK_Voting``. If you do not use RPC commands or a compatible library for the transfer of coins, please refer to :ref:`p2cs2` to learn how to build the standard script for P2CS2.

Withdrawing coins from Cold Staking
-----------------------------------

You can normally withdraw coins from a Cold Staking address using the normal methods in a wallet which holds the private key of ``PK_Spending``. Please consider additional security measures when bringing online the ``PK_Spending`` private key.
