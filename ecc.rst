#######################################################################
Key Exchange  + Encryption/Decryption using Elliptic Curve Cryptography
#######################################################################

Let's assume two parties X and Y, that need to communicate some data securely.
The first step taken is that X and Y agree on a curve ``C``, with a generator point ``G``.
 
.. note:: Note: The '*' operation is scalar multiplication, and '+' is field addition under the finite field in which the chosen curve lies. The '-' operation, is an inversion followed by point addition under the finite field in which the chosen curve lies.

The next step to be taken, is to exchange each other's pubkeys.

============
Key exchange
============

-------
X's POV
-------

* generate new random number (``x_privkey``)
* generate pubkey using privkey and ``G`` (``x_pubkey = G * x_privkey``)

-------
Y's POV
-------

* generate new random number (``y_privkey``)
* generate pubkey using privkey and ``G`` (``y_pubkey = G * y_privkey``)

Exchange these keys (x_pubkey and y_pubkey) publicly.

====================
Secure Communication
====================

Let's look at the case where X -> Y (i.e., X wants to transmit some data to Y)

-------
X's POV
-------

* Data ``D`` to be encrypted is converted into a cipher point, ``Cm`` on the curve ``C`` as follows:

.. code-block::
	Cm = {x_privkey * G, D + (x_privkey * y_pubkey)} ~~~> in the form (u, v)
	
Transmit this information publicly.

-------
Y's POV
-------

* Data ``Cm`` is recieved in the form (u, v), decrypted to obtain data D' as follows:

.. code-block::
	D' = v - y_privkey * (u)
	
D' is (should be) the same as D.
