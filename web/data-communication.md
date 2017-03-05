# data communcation - client & server

## ajax (asynchronous JavaScript and XML)


## Long polling (modified ajax, Facebook)

client create ajax => server response => client get response, create another ajax => ...

## Server-Sent Event
MDN - [Using server-sent events](https://developer.mozilla.org/en-US/docs/Web/API/Server-sent_events/Using_server-sent_events)

### receiving events from server:
```javascript
// create a EventSource object
var evtSource = new EventSource("//api.example.com/ssedemo.php", { withCredentials: true } ); 

// listen to a message
evtSource.onmessage = function(e) {
  var newElement = document.createElement("li");
  
  newElement.innerHTML = "message: " + e.data;
  eventList.appendChild(newElement);
}

```

### sending message from server:
The header needs to use the MIME type `text/event-stream`.


## WebRTC (Real-time, peer to peer, Google)

## WebSocket (HTML5)

## Socket.IO
