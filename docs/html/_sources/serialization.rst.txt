.. _serialization:

Serialization
=============


.. _header_s:

Block Header
------------

================ ===================== ======================  ====================
Field            Type                  Length                  Present
================ ===================== ======================  ====================
nVersion         signed int            4 bytes                 Always
hashPrevBlock    uint256               32 bytes                Always
hashMerkleRoot   uint256               32 bytes                Always
nTime            unsigned int          4 bytes                 Always
nBits            unsigned int          4 bytes                 Always
nNonce           unsigned int          4 bytes                 Always
================ ===================== ======================  ====================

Block
-----

================ ===================== ======================  ====================
Field            Type                  Length                  Present
================ ===================== ======================  ====================
blockHeader      :ref:`header_s`       70 bytes                Always
vTx              :ref:`tx_s` vector    Variable                Always
vchBlockSig      unsigned char vector  Variable                Always
================ ===================== ======================  ====================

.. _bp_s:

Bulletproof Range Proof
-----------------------

================ ===================== ======================  ======================
Field            Type                  Length                  Present
================ ===================== ======================  ======================
V_size           Compact size          Variable                Always
V                :ref:`g1_s` vector      V_size                  If V_size > 0
L_size           Compact size          Variable                Always
L                :ref:`g1_s` vector      L_size                  If L_size > 0
R_size           Compact size          Variable                Always
R                :ref:`g1_s` vector      R_size                  If R_size > 0
A                :ref:`g1_s`             48 bytes                Always
S                :ref:`g1_s`             48 bytes                Always
T1               :ref:`g1_s`             48 bytes                Always
T2               :ref:`g1_s`             48 bytes                Always
taux             :ref:`sca_s`                32 bytes                Always
mu               :ref:`sca_s`                32 bytes                Always
a                :ref:`sca_s`                32 bytes                Always
b                :ref:`sca_s`                32 bytes                Always
t                :ref:`sca_s`                32 bytes                Always
================ ===================== ======================  ======================


.. _tx_s:

Transaction
-----------

================ ====================== ======================  ======================
Field            Type                   Length                  Present
================ ====================== ======================  ======================
nVersion         signed int             4 bytes                 Always
nTime            unsigned int           4 bytes                 Always
vin              :ref:`tx_in_s` vector  Variable                Always
flags            unsigned char          1 byte                  If vin.size() == 0
vin              :ref:`tx_in_s` vector  Variable                If vin.size() == 0
vout             :ref:`tx_out_s` vector Variable                If vin.size() == 0
vout             :ref:`tx_out_s` vector Variable                If vin.size() > 0
wit              :ref:`tx_wit_s` vector Variable                If flags&1
nLockTime        unsinged int           4 bytes                 Always
strDZeel         string                 Variable                If nVersion >= 2
vchBalanceSig    unsigned char vector   96 bytes                If nVersion & 0x30
vchTxSig         unsigned char vector   96 bytes                If nVersion & 0x10
================ ====================== ======================  ======================

.. _tx_in_s:

Transaction Input
-----------------

================ ====================== ======================  ======================
Field            Type                   Length                  Present
================ ====================== ======================  ======================
prevout          :ref:`outpoint_s`      36 bytes                Always
scriptSig        unsigned char vector   Variable                Always
nSequence        unsigned int           4 bytes                 Always
================ ====================== ======================  ======================

.. _tx_out_s:

Transaction Output
------------------

================ ====================== ======================  =========================
Field            Type                   Length                  Present
================ ====================== ======================  =========================
nValue           unsigned int           8 bytes                 Always
nValue           unsinged int           8 bytes                 If nValue == ~(uint64_t)0
ephemeralKey     unsigned char vector   48 bytes                If nValue == ~(uint64_t)0
outputKey        unsigned char vector   48 bytes                If nValue == ~(uint64_t)0
spendingKey      unsigned char vector   48 bytes                If nValue == ~(uint64_t)0
bp               :ref:`bp_s`                                    If nValue == ~(uint64_t)0
scriptPubKey     unsigned char vector   Variable                Always
================ ====================== ======================  =========================

.. _sca_s:

Scalar
------

================ ====================== ======================  ======================
Field            Type                   Length                  Present
================ ====================== ======================  ======================
data             unsigned char vector   32                      Always
================ ====================== ======================  ======================

.. _g1_s:

G1Element
---------

================ ====================== ======================  ======================
Field            Type                   Length                  Present
================ ====================== ======================  ======================
data             unsigned char vector   48                      Always
================ ====================== ======================  ======================


.. _outpoint_s:

OutPoint
--------

================ ====================== ======================  ======================
Field            Type                   Length                  Present
================ ====================== ======================  ======================
hash             uint256                32                      Always
n                unsigned int           4                       Always
================ ====================== ======================  ======================

.. _tx_wit_s:

TxWitness
---------

================ =============================== ======================  ======================
Field            Type                            Length                  Present
================ =============================== ======================  ======================
stack            vector of unsigned char vectors Variable                Always
================ =============================== ======================  ======================
