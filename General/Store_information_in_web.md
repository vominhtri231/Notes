## Session  
* Session is saved on server side as well as client.   
a) When session is saved on server side, server will create a file to hold session info => Data will be available to all pages of the side but replication is needed. (AKA server-side session)
b) When session is saved on client side , it will be saved as a cookie. (AKA client-side session)
*  When user close browser, server will keep the session for a predetermined time before deleting it.  
## Cookie  
* Cookie is saved on client side as a file.
* Has a lot of attributes like life-time, same site, http only, etc.
* Everytime browser send a request, cookie will be sent along.