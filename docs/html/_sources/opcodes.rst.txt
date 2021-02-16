.. _opcodes:

Script Opcodes
==============

.. note::

   Besides the Opcodes included in the following table, NavCoin Core supports also every other Opcode present in Bitcoin Core 0.13.0

=============== ============ ==================================================================================================
Name            Value        Function
=============== ============ ==================================================================================================
OP_CFUND        0xc1         :ref:`script_dao`
OP_PROP         0xc2         :ref:`script_dao`
OP_PREQ         0xc3         :ref:`script_dao`
OP_YES          0xc4         :ref:`script_dao`
OP_NO           0xc5         :ref:`script_dao`
OP_ABSTAIN      0xc7         :ref:`script_dao`
OP_REMOVE       0xc8         :ref:`script_dao`
OP_DAO          0xc9         :ref:`script_dao`
OP_ANSWER       0xca         :ref:`script_dao`
OP_CONSULTATION 0xcb         :ref:`script_dao`
OP_COINSTAKE    0xc6         Pushes ``TRUE`` to the stack if the output spent in a coinstake transaction, ``FALSE`` otherwise.
OP_POOL         0xd0         Used to signal a block has been staked by NavPool
=============== ============ ==================================================================================================

