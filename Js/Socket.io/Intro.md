# Intro
- Socket.io provides bi-direction connection, build on top on Engine.io
- It first establishes long-polling connection then try to upgrade to better transport like WebSocket if it is possible.
  This is to make sure it works even in the presence of proxies, load balancer, firewall, etc. which may prevent WebSocket transport.
- Not an implementation of WebSocket, even thought using WebSocket under the hook. 
  It has a completely different set of [protocol](https://github.com/socketio/socket.io-protocol). 