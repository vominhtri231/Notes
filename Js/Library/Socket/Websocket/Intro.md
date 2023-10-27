# Websocket

The websocket is a protocol, starting with `ws:` which supported natively by various moderm browsers.

Currently, the protocol is initiated by HTTP request with a upgrade header to change the protocol to WS.
This requires client support for the websocket API and server support for the protocol update and websocket communication.

The biggest adventage of web socket over Socket.io is that it is light and you have absolute control.
However, this also means that you have to do everything on your own, including logging, rooms, namespaces, autoconnect, etc.