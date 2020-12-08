How to use NavCoin Core
=======================

The binaries
------------

 - ``navcoind``: A headless version of the node
 - ``navcoin-qt``: The graphical version of the node
 - ``navcoin-cli``: A RPC client to interact with the node

``navcoin-qt`` does not launch a RPC server by default. Interactions with the RPC server are possible using the ``Debug console`` which you can find in the menu ``Help -> Debug window``.

The data directory
------------------

Depending on your operating system, the data directory is located in:

 - Windows: ``C:\Users\YourUserName\Appdata\Roaming\Navcoin4``
 - Mac: ``~/Library/Application Support/navcoin4/``
 - Linux: ``~/.navcoin4/``

The structure of the data directory is separated in various folder and files:

 - ``blocks``: In this folder the raw blocks of the chain are stored.
 - ``chainstate``: The state view of the chain is stored here in a LevelDB database. This includes the UTXO set and diverse data related to the DAO.
 - ``wallet.dat``: The default name of the wallet database, using Berkeley DB 5.8.
 - ``navcoin.conf``: The configuration file. This file does not exist by default.
 - ``debug.log``: The debug log file.
 - ``error.log``: A filtered version of ``debug.log`` including only the errors.

.. _passing_options:

Passing launch options to the node
----------------------------------

Different :ref:`options` can be passed to the node on launch. There are two ways of doing this.

- By including them in the ``navcoin.conf`` file as pairs of keys and values::

   option1=value1
   option2=value2

- By passwing them as arguments to the binaries::

   ./navcoind -option1=value1 -option2=value2
   ./navcoin-qt -option1=value1 -option2=value2
