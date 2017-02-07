## design patterns

### - constructor pattern

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

### - the module pattern

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


### the revealing module pattern

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

