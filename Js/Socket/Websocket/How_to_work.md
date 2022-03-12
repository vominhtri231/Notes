# How to work with websocket

You could use either WebSocket or SockJS.
SockJs is a polyfill of WebSocket, which have fall-back comunication chandel in case websockets doesn't support.

```js
const sock = new WebSocket("ws://abc.com")
const sock = new SockJS("ws://abc.com")
```

## To emit message

```js
sock.send("message")
```

## To listen to event

```js
sock.addEventListener("message", message -> {
    // ...
})
```
