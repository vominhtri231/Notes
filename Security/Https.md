# HTTPS

## Why we need HTTPS

* Secure privacy of message, prevent them from being eavesdropped by attackers

* Ensure integrity of messages, prevent them from being modified

* Guarantee messages from the actual wanting server using the certificate issued by legitimate CA.

## Keys

The keys are used to encrypt and decrypt the messages and should be kept secure. Since symmetric keys are hard to share, in HTTPS asymmetric keys are used.

Asymmetric key pair include private key and public key. Once for encrypt the messages, once for decrypt the messages.

How key pair is exchanged:

* Client hello
  The client would also list of available SSL/TLS versions and encryption algorithms (AKA cipher suite) on client side.

* Server hello
  The server would choose the best possible SSL/TLS version and encryption algorithm, then reply with my certificate and public key.

* Client key exchange
  The client would check the server's certificate to make sure it is legit. A generated `pre-master-key` will be encrypted using server's public key and send to server.

* Change cipher spec
  The server would decrypt the `pre-master-key` using the server's private. Since the  `pre-master-key` is encrypted using asymmetric key, so nobody could spy on it. The key is used to generate the same `share secret` for client and server that will be used as a symmetric key.]

* Client and server send test messages with the shared message, after that, all messages will be secured.

## CA - Certificate authority

A certificate authority is a third-party organization which can:

1. Issue certificates

2. Confirm identity of the certificate owner

3. Prove proof that the certificate is valid

Some of the well known CA: Symantec, Comodo, Let's Encrypt, etc. They are trusted to be accepted to the root store which is a database of trusted CAs. Apple, Windows or Mozilla run their own root store and installed it in user's devices.
