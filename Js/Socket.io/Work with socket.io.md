### Remark:
Socket io is event base. Some pre-define event: connection, disconnect.
### To handle an event
```javascript
  socket.on('event', (obj) => {
  });
```
### To emit an event
```javascript
   // this will emit event for everyone
  socket.emit('event', {a:1, b:2});

  // this will emit event for everyone except sender
  socket.broadcast.emit('event', {a:1, b:2})
```