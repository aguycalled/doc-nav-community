.. _standard_script:

Standard Scripts
================

Pay to Public Key Hash (P2PKH)
------------------------------

.. note::

   This script is the default for Legacy Public Addresses.

Script::

    OP_DUP OP_HASH160 <PKH> OP_EQUALVERIFY OP_CHECKSIG

.. _p2cs:

Pay To Cold Staking (P2CS)
--------------------------

.. note::

   This script is the default for Cold Staking v1 Addresses, which serve for delegating staking rights.

Outputs guarded by this script will be only spendable by the public key hash ``PKH_2`` and stakable by the public key hash ``PKH_1``. ``PKH_1`` will hold both staking and voting rights.

For an output to be considered staked, it must be spent in the coinstake transaction. `Read more <https://github.com/navcoin/npips/blob/master/npip-0002.mediawiki>`_.

Script::

    OP_COINSTAKE OP_IF
      OP_DUP OP_HASH160 <PKH_1> OP_EQUALVERIFY OP_CHECKSIG
    OP_ELSE
      OP_DUP OP_HASH160 <PKH_2> OP_EQUALVERIFY OP_CHECKSIG
    OP_ENDIF

.. _p2cs2:

Pay To Cold Staking v2 (P2CS2)
------------------------------

.. note::

   This script is the default for Cold Staking v2 Addresses, which serve for delegating staking and voting rights.

Outputs guarded by this script will be only spendable by the public key hash ``PKH_2`` and stakable by the public key hash ``PKH_1``. Voting rights are delegated to ``PKH_3``.

For an output to be considered staked, it must be spent in the coinstake transaction.

Script::

    <PKH_3>
    OP_DROP
    OP_COINSTAKE OP_IF
      OP_DUP OP_HASH160 <PKH_1> OP_EQUALVERIFY OP_CHECKSIG
    OP_ELSE
      OP_DUP OP_HASH160 <PKH_2> OP_EQUALVERIFY OP_CHECKSIG
    OP_ENDIF

Accumulation in the Community Fund
----------------------------------

Coins sent to this script will be effectively burned and removed from the spendable supply. The value of the output will be added to the available supply of the Community Fund.

Script::

    OP_RETURN OP_CFUND

Remeedable without conditions
-----------------------------

.. note::

   This script is the default for private BLSCT outputs, as they are still guarded by the spending key. Please don't use in other types of outputs, as they would be spendable by anyone!

Script::

   OP_1

.. _script_dao:

DAO Special Scripts
===================


Proposal Vote
-------------

Outputs with this script signal a vote ``VOTE`` for a proposal with hash ``PROPOSAL_HASH``. ``VOTE`` can be ``OP_YES``, ``OP_NO``. ``OP_ABSTAIN`` or ``OP_REMOVE``.

Script::

   OP_RETURN OP_CFUND OP_PROP <VOTE> <PROPOSAL_HASH>

Payment Request Vote
--------------------

Outputs with this script signal a vote ``VOTE`` for a payment request with hash ``PREQUESTL_HASH``. ``VOTE`` can be ``OP_YES``, ``OP_NO``. ``OP_ABSTAIN`` or ``OP_REMOVE``.

Script::

   OP_RETURN OP_CFUND OP_PREQ <VOTE> <PREQUEST_HASH>


Consultation Support
--------------------

Outputs with this script signal a support vote ``VOTE`` for a consultation with hash ``PROPOSAL_HASH``. ``VOTE`` can be ``OP_YES`` or ``OP_REMOVE``.

Script::

   OP_RETURN OP_DAO <VOTE> <CONSULTATION_HASH>

Consultation Vote
-----------------

Outputs with this script signal a vote ``VOTE_VALUE`` for a consultation with hash ``PROPOSAL_HASH``. ``VOTE`` can be ``OP_ABSTAIN``, ``OP_ANSWER`` or ``OP_REMOVE``. If ``VOTE`` is ``OP_ANSWER``, the answer for range consultations is specified as ``VOTE_VALUE``

Script::

   OP_RETURN OP_CONSULTATION <VOTE> <CONSULTATION_HASH> <VOTE_VALUE>
