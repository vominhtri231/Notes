# Java security

## Keystore vs truststore

Keystore holds key of your application which can later use to prove integrity of the messages.
They can be private keys, certificates with public keys or just secret keys.

Truststore is for saving sites that you trust.

If you as a server want clients to talk to you via HTTPS, you must have a keystore. 
When a request is sent from a client to a you, you will sent the certificate from your keystore to them.
The client will verify it using certificates in its truststore.
If the certificate or **Certificate Authorities** are not in the truststore, the connection will fail.

## Certificate Authority (CA)

A digital certificate guarantee the ownership of a public key by the common name (CN) in the certificate.
A certificate can be used to verify the other certificates and form a "chain of trust".
SSL certificates sometimes are referred to as "public keys" or "end entity" certificate since they are in the bottom of the "chain".

![](./img/chain_of_trust.jpg)

A certificate authority is the one that issues the digital certificates.
It can act as a 3rd party that can guarantee a certificate is really what it said.
