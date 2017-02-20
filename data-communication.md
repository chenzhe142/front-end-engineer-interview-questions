# data communcation - client & server

## ajax (asynchronous JavaScript and XML)


## Long polling (modified ajax, Facebook)


## Server-Sent Event
MDN - [Using server-sent events](https://developer.mozilla.org/en-US/docs/Web/API/Server-sent_events/Using_server-sent_events)

### receiving events from server:
```javascript
var evtSource = new EventSource("ssedemo.php");
```

### sending message from server:
The header needs to use the MIME type `text/event-stream`.
