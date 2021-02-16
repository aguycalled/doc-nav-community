.. _options:

Options
=======

The following is a condensed list of options which can be passed to the daemon as explained in :ref:`passing_options`:


.. note::

   Default values are indicated in **bold**.

========================  ========================================================== ===========================
Key                       Description                                                Possible values
========================  ========================================================== ===========================
blsctmix                  Enables participation in xNAV aggregation sessions         **1**, 0
daemon                    Runs the node in the background                            1, **0**
dandelion                 Enables dandelion for transaction broadcast                **1**, 0
debug                     Enables debugging                                          all, or the debug category
excludevote               Marks staked blocks to be excluded from DAO quorums        1, **0**
port                      Sets the P2P listen port                
printtoconsole            Prints debug to console instead of debug.log
rpcuser                   Sets the RPC username 
rpcpassword               Sets the RPC password
rpcport                   Sets the RPC port
staking                   Enables or disables staking                                **1**, 0
testnet                   Switches between mainnet (0) or testnet (1)                1, **0**
torserver                 Launches a TOR server together with the daemon             **1**, 0
zapwallettxes             Wipes out the wallet transactions and rescans the chain    2, 1, **0**
========================  ========================================================== ===========================

