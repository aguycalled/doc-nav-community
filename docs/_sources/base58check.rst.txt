.. _base58check:

Base58Check
===========

An address is constructed using a Base58Check string, which is created from a version/application byte and payload as follows:

 - Take the :ref:`network-version-bytes` and :ref:`payloads` bytes, and concatenate them together (bytewise).
 - Take the first four bytes of SHA256(SHA256(results of step 1))
 - Concatenate the results of step 1 and the results of step 2 together (bytewise).
 - Treating the results of step 3 - a series of bytes - as a single big-endian bignumber, convert to base-58 using normal mathematical steps (bignumber division) and the base-58 alphabet described below. The result should be normalized to not have any leading base-58 zeroes (character '1').
 - The leading character '1', which has a value of zero in base58, is reserved for representing an entire leading zero byte, as when it is in a leading position, has no value as a base-58 symbol. There can be one or more leading '1's when necessary to represent one or more leading zero bytes. Count the number of leading zero bytes that were the result of step 3 (for old Bitcoin addresses, there will always be at least one for the version/application byte; for new addresses, there will never be any). Each leading zero byte shall be represented by its own character '1' in the final result.
 - Concatenate the 1's from step 5 with the results of step 4. This is the Base58Check result.
