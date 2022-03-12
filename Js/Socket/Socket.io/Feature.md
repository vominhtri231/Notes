# Features

Some outstanding features of Socket.io:

## Multiplexing

The ability to send multiple signals via a single complex signal.  
The receiver recovers separate signals, called de-multiplexing.  
Socket io allows users to create multiple **namespaces**, which will be separate communication channel using the same connection.

## Room

Under each **namespace**, user can create **rooms**, which sockets can join and leave. User can broadcast to sockets in a room.

## Disconnect detection

Socket io has heartbeat mechanism, allow both server and client known the other not responding.

## Auto-reconnect

## Binary

Any serializable data can be sent, includes Blob, ArrayBuffer etc.
