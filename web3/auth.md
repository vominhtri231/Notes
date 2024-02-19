# Web3 auth

There are 3 factors of authentication

## Identity

In normal web2 application, users would need a unique username or email to identify themself. This identity would associate with all application-specific data. Each application, user would need new identify for it.

For web3, users are identified using their wallet address instead, allow them to be used across applications.

## Proof-of-identity

In web2, in order to login to an application, user would need to send the password associated with their username. This required user to remember passwords, security questions or using password manager.

With web3, proving identities are done via digital signatures. By simply signing a message and send it to the server,  you can prove that you own a wallet. This works because the message can only be singed using the private key that the wallet's owner holds.

## Authority

In modern application, to remember a user we would prefer to use JWT tokens rather than require user to login constantly or save user session.

For web2 applications, this means we need to use a third-party service like auth0 for managing private keys or handle them by ourself.

For web3 applications, for issuing and verifying JWT, we can use the user's wallet. This enable **self-custodied** authentication flow, which means users fully hold and mange their assets and private keys. 
