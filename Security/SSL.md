# SSL

## Definitions

SSL(Secure Sockets Layer) is the technology for encrypting and securing communication. It supports protocols such as HTTP, FTP, TELNET, SMTP, etc.  
TLS(Transport Layer Security) is the update version of SSL.

## How it works

![](https://www.entrust.com/-/media/entrust/resources/product-support/certificate-solutions/1258x489_how-ssl-certificates-work.jpg?la=en&hash=21C4AB8CF8CE8F9DAD70C19DC903DCB7)

1. Client Hello : Client connects to the server and send information like SSL version, encrypt settings
2. Server Hello : Server sends SSL Certificate + public key
3. Authentication and Pre-master Secret : Server certificate is authenticated by the client.
   If it is valid, client encrypts the pre-master secret (a symmetric session key) using server's public key and sends it to the server.
4. Decryption and Master Secret : Server uses its private key to decrypt the symmetric session key and sends an acknowledgement encrypted with master secret (session key).
5. Encryption with Session Key : All data will now be encrypted and transmitted with the session key.
