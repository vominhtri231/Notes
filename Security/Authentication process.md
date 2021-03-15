### Basic model
![](https://miro.medium.com/max/1050/1*Uz3bHpisBBCeZAqX46BiKg.png)
Because the Http is stateless, server would required username/password everytime for authentication/authorization.
### Server side session (SSS)
![](https://miro.medium.com/max/1050/1*KOBd8XFcwhexNe_dZ7DEBw.png)
* Server now save authenticate/authorize data in server session, that would prevent unnecessary authentication.
* However this also cause a problem when the system got scaled(which later required the session synchronization) and also security problem.
### Json web token (JWT)
![](https://miro.medium.com/max/1050/1*1efaAnWzyZzI15utuJ-xEg.png)
* JWT is a token format. Each token is self-contained, containning sufficent data for checking its validity as well as user information.
* JWT contains 3 parts: `header.payload.signature` (each part is encodes in base 64)
    1. header: contain key id and the algorithm which later used in signature
    2. payload: the information + the issurer
    3. signature = encrypte `header.payload` by the given algorithm and a private key.
* To validate JWT, we first get public key from issurer by key id, use that to decrypt the signature and compaire with the header and payload  
  => This switchs the rolls of public and private keys from the asymetric algorithm. 