.. NavCoin Core Documentation documentation master file, created by
   sphinx-quickstart on Fri Dec  4 17:18:15 2020.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

Welcome to NavCoin Core Documentation!
======================================================

About NavCoin
-------------

NavCoin is an open-sourced digital currency with privacy-enhanced features. Transactions that occur on the blockchain of NavCoin are made in a peer-to-peer fashion with no need for intermediaries. With NavCoin, one can choose to store and transact coins publicly (NAV) and privately (xNAV). If one chooses to transact privately, it will not be possible to link a transaction to its sender or receiver, or even view the amount that was sent. This has been made possible by NavCoin's self-developed privacy protocol called Boneh-Lynn-Shacham Confidential Transactions (blsCT).

NavCoin was invented in 2014 and had no pre-mine or ICO. With block times of 30 seconds, one can stake their coins to earn rewards through Proof of Stake Version 3 (PoSv3) for helping to secure the network. NavCoin's current supply is 66,768,000 NAV with a block reward of 2.5 NAV, hence a decreasing inflation model. From the 2,5 NAV, 2 NAV are redirected to the staker who found the block, and 0,5 NAV are accumulated in a decentralized treasury used to fund community initiatives based on the outcome of DAO votings. NavCoin’s decentralized autonomous organization (DAO) enables the community to be self-funded its treasury, self-guided through consultations, and self-governed through consensus changes. Anyone who holds coins on the public side (NAV) can participate in the DAO by staking their coins. Each stake is the equivalent of one vote, and there is no minimum amount required to take part.

NavCoin Core is forked from bitcoin core v13.0, and as such, it inherits its P2P protocol and most of the RPC commands. This documment will reflect the new methods and implementations.

The official repository hosting the soruce code is located on `GitHub <http://github.com/navcoin/navcoin-core>`_.

Latest Release
--------------

The current last version of NavCoin Core is 5.0.1.


Connect with the community
--------------------------

- The main website of `NavCoin <https://www.navcoin.org>`_ has a general overview of the project.
- The `Discord server <https://discord.gg/y4Vu9jw>`_ is where most of the discussion happens related to development.
- `Reddit <https://www.reddit.com/r/NavCoin>`_.
- `Telegram <https://t.me/navcoin>`_.
- `Twitter <https://twitter.com/NavCoin>`_.
- Many articles and updates are posted on `Medium <http://medium.com/nav-coin>`_.

Other resources
---------------

- `NavExplorer <https://navexplorer.com>`_  is the independent block explorer maintained by the community.
- `Cryptoid <https://chainz.cryptoid.info/nav/>`_ hosts a basic block explorer which does not cover all the functionality of NavCoin's blockchain.
- You can find various statistics in `index.nav.community/stats.html <https://index.nav.community/stats.html>`_.
- A `staking rewards calculator <http://static-rewards.nav.community/>`_.
- Register an `openalias address <http://openalias.nav.community/>`_.

.. toctree::
   :maxdepth: 2
   :caption: Getting started:

   get.rst
   use.rst

.. toctree::
   :maxdepth: 2
   :caption: Documentation:

   options.rst
   rpc.rst
   network.rst
   base58check.rst
   payloads.rst
   serialization.rst
   opcodes.rst
   standard_script.rst
   special_tx.rst
   blsct.rst
   coldstaking.rst

.. toctree::
   :maxdepth: 2
   :caption: Release notes:

   release-notes/release-notes-4.0.0.md
   release-notes/release-notes-4.2.0.md
   release-notes/release-notes-4.2.1.md
   release-notes/release-notes-4.3.0.md
   release-notes/release-notes-4.4.0.md
   release-notes/release-notes-4.5.0.md
   release-notes/release-notes-4.5.0-additional-testing-notes/modified-coldstaking-client-notes-4.5.0
   release-notes/release-notes-4.5.1.md
   release-notes/release-notes-4.5.2.md
   release-notes/release-notes-4.6.0.md
   release-notes/release-notes-4.7.0.md
   release-notes/release-notes-4.7.1.md
   release-notes/release-notes-4.7.2.md
   release-notes/release-notes-4.7.3.md
   release-notes/release-notes-5.0.0.md
   release-notes/release-notes-5.0.1.md
   release-notes/release-notes-6.0.md
