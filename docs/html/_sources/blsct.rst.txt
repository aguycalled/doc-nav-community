.. _blsct:

BLSCT Cryptography
==================

This section will describe the cryptography behind BLSCT, the novel protocol which we used to build NavCoin's new private token xNAV.

For a wallet to create and receive BLSCT transactions, it needs to own a set of BLS keys. Let :math:`KDF(k, p)` be a key derivation function where ``k`` is a BLS private key and ``p`` a derivation path, and ``m`` the wallet's master secret key. We use ``G1`` from the pairing-friendly elliptic curve BLS12-381 and let ``g`` be a ``G1`` generator. Let ``H`` be a secure hash function whose output is of 256-bit length and ``HG1`` a hash function whose output is mapped as a ``G1`` element.

The first steps are to calculate:

   - A master blinding key: :math:`bmk = KDF(m, 130'/1')`
   - A master view key: :math:`vmk = KDF(m, 130'/0'/0')`
   - A master spend key: :math:`smk = KDF(m, 130'/0'/1')`

A wallet can then generate the needed keys to construct an arbitrary number of addresses where coins can be received. Wallets generate their ``SAi``-th address :math:`SAi = (0,1,2,...)` in their ``Ai``-th account :math:`Ai = (0,1,2,...)` as a pair of public keys ``(C, D)`` where:

.. math::

   m &= H("SubAddress"||vmk||Ai||SAi)
   \\
   M &= m*g
   \\
   D &= g*smk + M
   \\
   C &= vmk*D

Wallets must store ``D`` in the wallet's database registered to the index ``(Ai, SAi)`` as an integer pair. Addresses are a :ref:`base58check` representation of the keys ``(C, D)`` using ``73`` and ``33`` as mainnet :ref:`network-version-bytes`. When a wallet wants to send funds to an address, it must:

   - Decode and extract ``(C, D)`` from the address.
   - Maintain an incremental counter of blinding addresses ``Bi``.
   - Generate an ephemeral private key :math:`e = KDF(bmk, Bi++)`
   - Calculate the ephemeral public key :math:`E = e*g`
   - Generate the output's public key :math:`R = e*D`
   - Generate the spending key :math:`P = H(e*C)*g+D`
   - Generate a shared secret :math:`S = e*C`

The wallet must construct a per-output range-proof ``bp`` to prove that the hidden amount ``v`` is positive and within the allowed range. It is allowed to attach an encrypted message ``memo`` limited to 54 bytes only viewable by the transaction's recipient. Some of the scalars used in the proof creation are calculated from the shared secret ``S``. 

.. math::

   alpha &= H(S||1) + (v | (memo[:23]<<64))
   \\
   rho &= H(S||2)
   \\
   tau1 &= H(S||3) + (memo[23:54])
   \\
   tau2 &= H(S||4)
   \\
   gamma &= H(S||10)

The commitment's secret key gamma will sign the message ``BLSCTBALANCE`` to create a signature ``BPSO``, which will serve to prove later that the transaction creates no new coins. Constructing the signature using the basic scheme and a constant message is secure against a rogue public-key attack combined with a valid Bulletproofs range-proof. An attacker can not create it without knowledge of the secret key gamma.

.. math::

   BPSO = BasicSchemeSign(gamma, "BLSCTBALANCE")

The output's ephemeral key ``e`` will sign the output's hash to create a signature ``BSO`` using the augmented scheme.

.. math::

   BSO = AugSchemeSign(e, H(tx_out)) 

The range proof ``bp`` and the public keys ``E``, ``R``, and ``P`` will be attached to a transaction's output when it targets a private address. Transactions that include a BLSCT output have their version bit ``10`` set to ``1``. Both public and BLSCT outputs can combine in the same transaction.

When a client sees this output, he will determine whether it belongs to him or not by performing the following checks:

   - Calculate :math:`D' = P - H(vmk*R)*g` and check if its wallet's database has it registered to an index ``(Ai', SAi')``.
   - Calculate :math:`S' = vmk * R`
   - Derive ``alpha``, ``rho``, ``tau1`` and ``tau2`` and ``gamma'`` from ``S'``.
   - Verify if the range proof ``bp`` is valid.
   - Calculate :math:`ex = (mu - rho*x) - alpha` and :math:`ex2 = ((taux - tau2*x^2 - gamma*z^2) * x^{-1}) - tau1`
   - Extract the amount as :math:`v' = ex \& 0xFFFFFFFFFFFFFFFF`
   - Extract the encrypted message as :math:`memo' = ex2 || ex >> 64`
   - Check if the range-proof value's commitment equals to :math:`gamma'*g + v'*HG1(g||"bulletproof"||0)`

When the client wants to spend this output, it must set the spending transaction's version bit ``11`` to ``1``. It can calculate the output's private spending key as :math:`p = H(vmk*R) + smk + H("SubAddress"||vmk||Ai'||SAi')`. The private key ``p`` will sign the transaction input hash using the augmented scheme to produce the signature ``BSI``.

.. math::

   BSI = AugSchemeSign(p, H(tx_in))

The extracted commitment's secret key ``gamma'`` will sign the message ``BLSCTBALANCE`` to create a signature ``BPSI``.

.. math::

   BPSI = BasicSchemeSign(gamma', "BLSCTBALANCE")

The wallet will store the aggregation of all of the transaction's ``BSI`` s and ``BSO`` s in its BLS transaction signature field as ``BS``. The transaction's BLS balance signature will result from aggregating all the ``BPSI`` s and ``BPSO`` s signatures as ``BPS``.

Every transaction must include an output with a transparent amount whose script is the provably unspendable ``OP_RETURN`` representing the sender's fee. Transactions are not allowed to combine public and private inputs. 

A validator can determine if a transaction is correct:

   - By verifying that ``BPS`` is a valid signature by defining ``pkBal`` as, for each transaction's input ``prevOut``, the sum of :math:`prevOut.bp.v` if it is private or :math:`prevOut.amount*HG1(g||"bulletproof"||0)` if it is public, minus the sum of, for each transaction's output ``out``, :math:`out.bp.v` if it is private or :math:`out.amount*HG1(g||"bulletproof"||0)` if it is public, and using ``pkBal`` as the signer's public key and ``BLSCTBALANCE`` as the message of the basic scheme,
   - by verifying that ``BS`` is a valid signature using the augmented scheme with ``P, H(tx_in)`` for each transaction's input as inputs to the verify signature function, and ``E, H(tx_out)`` from each transaction's output,
   - and by verifying that for each output, its range proof ``bp`` is validated correctly.
