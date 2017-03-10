# design patterns

- [constructor pattern](#constructor-pattern)
- [the module pattern](#the-module-pattern)
- [the revealing module pattern](#the-revealing-module-pattern)
- [the observer pattern](#the-observer-pattern)
- [publish / subscribe pattern](#publish--subscribe-pattern)
- [factory pattern](#factory-pattern)
- [singleton pattern](#singleton-pattern)
- [facade pattern](#facade-pattern)

The notes are taken from Addy Osmani's book, [learning javascript design patterns](https://addyosmani.com/resources/essentialjsdesignpatterns/book/)

## constructor pattern

```javascript
function Car( model, year, miles ) {
 
  this.model = model;
  this.year = year;
  this.miles = miles;
 
  this.toString = function () {
    return this.model + " has done " + this.miles + " miles";
  };
}
 
// Usage:
 
// We can create new instances of the car
var civic = new Car( "Honda Civic", 2009, 20000 );
var mondeo = new Car( "Ford Mondeo", 2010, 5000 );
 
// and then open our browser console to view the
// output of the toString() method being called on
// these objects
console.log( civic.toString() );
console.log( mondeo.toString() );
```
There are some problems with this pattern: 

1. one is that it makes inheritance difficult,
2. and the other is that functions such as `toString()` are redefined for each of the new objects created using the Car constructor. This isn't very optimal as the function should ideally be shared between all of the instances of the Car type.

To avoid this issue, we can use `prototype`:

```javascript
function Car( model, year, miles ) {
 
  this.model = model;
  this.year = year;
  this.miles = miles;
}

Car.prototype.toString = function () {
    return this.model + " has done " + this.miles + " miles";
};

```

## the module pattern

The Module pattern encapsulates "privacy", state and organization using `closures`.

It should be noted that there isn't really an explicitly true sense of "privacy" inside JavaScript because unlike some traditional languages, it doesn't have access modifiers. Variables can't technically be declared as being public nor private and so we use function scope to simulate this concept.

Module pattern, variables or methods declared are only available inside the module itself thanks to closure. Variables or methods defined within the returning object however are available to everyone.

codepen demo - [#interviewPrep - js - module pattern](http://codepen.io/chenzhe142/pen/ZLMWXe?editors=1011)

```javascript
var testModule = (function () {
 
  var counter = 0;
 
  return {
 
    incrementCounter: function () {
      return counter++;
    },
 
    resetCounter: function () {
      console.log( "counter value prior to reset: " + counter );
      counter = 0;
    }
  };
 
})();

// output: 0
console.log(testModule.incrementCounter());

// output: 1
console.log(testModule.incrementCounter());

// output: 2
console.log(testModule.incrementCounter());
```

The counter variable `counter` is actually fully shielded from our global scope so it acts just like a private variable would - its existence is limited to within the module's closure so that the only code able to access its scope are our two functions.

When working with the Module pattern, we may find it useful to define a simple template that we use for getting started with it. Here's one that covers namespacing, public and private variables:

```javascript
var myNamespace = (function () {
 
  var myPrivateVar, myPrivateMethod;
 
  // A private counter variable
  myPrivateVar = 0;
 
  // A private function which logs any arguments
  myPrivateMethod = function( foo ) {
      console.log( foo );
  };
 
  return {
 
    // A public variable
    myPublicVar: "foo",
 
    // A public function utilizing privates
    myPublicFunction: function( bar ) {
 
      // Increment our private counter
      myPrivateVar++;
 
      // Call our private method using bar
      myPrivateMethod( bar );
 
    }
  };
 
})();
```

#### Advantages

We've seen why the Constructor pattern can be useful, but why is the Module pattern a good choice? For starters, it's a lot cleaner for developers coming from an object-oriented background than the idea of true encapsulation, at least from a JavaScript perspective.

Secondly, it supports private data - so, in the Module pattern, public parts of our code are able to touch the private parts, however the outside world is unable to touch the class's private parts (no laughing! Oh, and thanks to David Engfer for the joke).

#### Disadvantages

The disadvantages of the Module pattern are that as we access both public and private members differently, when we wish to change visibility, we actually have to make changes to each place the member was used.

We also can't access private members in methods that are added to the object at a later point. That said, in many cases the Module pattern is still quite useful and when used correctly, certainly has the potential to improve the structure of our application.

Other disadvantages include the inability to create automated unit tests for private members and additional complexity when bugs require hot fixes. It's simply not possible to patch privates. Instead, one must override all public methods which interact with the buggy privates. Developers can't easily extend privates either, so it's worth remembering privates are not as flexible as they may initially appear.


## the revealing module pattern

The result of his efforts was an updated pattern where we would simply define all of our functions and variables in the private scope and return an anonymous object with pointers to the private functionality we wished to reveal as public.

```javascript
var myRevealingModule = (function () {
 
        var privateVar = "Ben Cherry",
            publicVar = "Hey there!";
 
        function privateFunction() {
            console.log( "Name:" + privateVar );
        }
 
        function publicSetName( strName ) {
            privateVar = strName;
        }
 
        function publicGetName() {
            privateFunction();
        }
 
 
        // Reveal public pointers to
        // private functions and properties
 
        return {
            setName: publicSetName,
            greeting: publicVar,
            getName: publicGetName
        };
 
    })();
 
myRevealingModule.setName( "Paul Kinlan" );
```


## the observer pattern

The Observer is a design pattern where an object (known as a subject) maintains a list of objects depending on it (observers), automatically notifying them of any changes to state.

## publish / subscribe pattern

Basic idea: `hashMap: {eventName: [..callback]}`

```javascript
var pubsub = {};
 
(function(myObject) {
 
    // Storage for topics that can be broadcast
    // or listened to
    var topics = {};
 
    // An topic identifier
    var subUid = -1;
 
    // Publish or broadcast events of interest
    // with a specific topic name and arguments
    // such as the data to pass along
    myObject.publish = function( topic, args ) {
 
        if ( !topics[topic] ) {
            return false;
        }
 
        var subscribers = topics[topic],
            len = subscribers ? subscribers.length : 0;
 
        while (len--) {
            subscribers[len].func( topic, args );
        }
 
        return this;
    };
 
    // Subscribe to events of interest
    // with a specific topic name and a
    // callback function, to be executed
    // when the topic/event is observed
    myObject.subscribe = function( topic, func ) {
 
        if (!topics[topic]) {
            topics[topic] = [];
        }
 
        var token = ( ++subUid ).toString();
        topics[topic].push({
            token: token,
            func: func
        });
        return token;
    };
 
    // Unsubscribe from a specific
    // topic, based on a tokenized reference
    // to the subscription
    myObject.unsubscribe = function( token ) {
        for ( var m in topics ) {
            if ( topics[m] ) {
                for ( var i = 0, j = topics[m].length; i < j; i++ ) {
                    if ( topics[m][i].token === token ) {
                        topics[m].splice( i, 1 );
                        return token;
                    }
                }
            }
        }
        return this;
    };
}( pubsub ));
```

#### Example: user interface notification

Next, let's imagine we have a web application responsible for displaying real-time stock information.

The application might have a grid for displaying the stock stats and a counter for displaying the last point of update. When the data model changes, the application will need to update the grid and counter. In this scenario, our subject (which will be publishing topics/notifications) is the data model and our subscribers are the grid and counter.

When our subscribers receive notification that the model itself has changed, they can update themselves accordingly.

In our implementation, our subscriber will listen to the topic "newDataAvailable" to find out if new stock information is available. If a new notification is published to this topic, it will trigger gridUpdate to add a new row to our grid containing this information. It will also update a last updated counter to log the last time data was added

```javascript
// Return the current local time to be used in our UI later
getCurrentTime = function (){
 
   var date = new Date(),
         m = date.getMonth() + 1,
         d = date.getDate(),
         y = date.getFullYear(),
         t = date.toLocaleTimeString().toLowerCase();
 
        return (m + "/" + d + "/" + y + " " + t);
};
 
// Add a new row of data to our fictional grid component
function addGridRow( data ) {
 
   // ui.grid.addRow( data );
   console.log( "updated grid component with:" + data );
 
}
 
// Update our fictional grid to show the time it was last
// updated
function updateCounter( data ) {
 
   // ui.grid.updateLastChanged( getCurrentTime() );
   console.log( "data last updated at: " + getCurrentTime() + " with " + data);
 
}
 
// Update the grid using the data passed to our subscribers
gridUpdate = function( topic, data ){
 
  if ( data !== undefined ) {
     addGridRow( data );
     updateCounter( data );
   }
 
};
 
// Create a subscription to the newDataAvailable topic
var subscriber = pubsub.subscribe( "newDataAvailable", gridUpdate );
 
// The following represents updates to our data layer. This could be
// powered by ajax requests which broadcast that new data is available
// to the rest of the application.
 
// Publish changes to the gridUpdated topic representing new entries
pubsub.publish( "newDataAvailable", {
  summary: "Apple made $5 billion",
  identifier: "APPL",
  stockPrice: 570.91
});
 
pubsub.publish( "newDataAvailable", {
  summary: "Microsoft made $20 million",
  identifier: "MSFT",
  stockPrice: 30.85
});
```


Further readings:

- [David Walsh - Pub / Sub Javascript object](https://davidwalsh.name/pubsub-javascript)

## factory pattern
It provides a generic interface for creating objects, where we can specify the type of factory object we wish to create.
```javascript
var Limo = function(){
 this.carType = 'limo';
};

var Suv = function() {
 this.carType = 'suv';
};

var CarFactory = function(carType) {
 if (carType === 'limo') {
  return new Limo();
 } else if (carType === 'suv') {
  return new Suv();
 }
};

```

## singleton pattern
It restricts instantiation of a class to a single object.
- If instance does not exist, create one
- If exists, return that instance

## facade pattern
It provides a convenient higher-level interface to a larger body of code, hiding its true underlying complexity. Whenever we use jQuery's `$(el).css()` or `$(el).animate()` methods, we are using a Facade.

### performance issue is hidden behind when using Facade as well. One example: `getElementById` vs `$(#someId)`
