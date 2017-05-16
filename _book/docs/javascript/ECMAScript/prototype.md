## prototype
prototype is an **object**, to which the search for a particular property can be delegated to.

```
var Name = function() {
  var name = 'what';
  
  // getName() is assigned to function Name's property. Thus the function can be invoked by f.getName().
  // it's called instance method
  this.getName = function() {
    return name;
  };
}
```

In javascript, the object's prototype is an internal property that's not directly accessible.

A function's prototype has a constructor property that references back to the function.

Every function, when created, gets a new prototype object. When we use a function as a constructor, the constructed object's prototype is set to the function's prototype.

**Within the constructor function, the `this` keyword refers to the newly created object.**

```javascript
var name = new Name();

```

## inheritance
Creating a prototype chain:
```javascript
// 1. we replace SubClass's prototype by SuperClass's instance. We lost connection to the SubClass's constructor.
SubClass.prototype = new SuperClass();

// 2. use object property configuration to extend SubClass from SuperClass:
Object.defineProperty(SubClass.prototype, 'constructor', {
  enumerable: false,
  value: SubClass,
  writable: true
});

// example:
Worker.prototype = new Person();
```

## `instanceof`
`instanceof` is to check whether an object is a part of a class hierarchy. It works by checking whether the current prototype of the SubClass's instance is in the prototype chain of SubClass.

## `class` in ES6
```javascript
class Person {
  constructor(name) {
    this.name = name;
  }
  dance() {
    return true;
  }
}

class Worker extends Person {
  constructor(name, skill) {
    // manually call the base class constructor
    super(name);
    this.skill = skill;
  }
}
```

## `getter` and `setter`
Getter and setter methods can be defined in two ways:
- by specifying them within object literals or within ES6 class definitions

```javascript
const names = {
    nameList: ['andy', 'amy', 'adam'],
    get firstName() {
        return this.nameList[0];
    },
    set firstName(value) {
        this.nameList[0] = value;
    }
}

names.firstName; //output: 'andy'
```

- by using the built-in `Object.defineProperty` method
```javascript
var Company = function() {
    let _ceo = 'someone';

    Object.defineProperty(this, 'ceo', {
        get: () => {
            return _ceo;
        },
        set: (value) => {
          // validate value
          if (typeof value !== 'string') {
                throw new TypeError('ceo\'s name should be string!');
            }
            _ceo = value;
        }
    });
}

var newCompany = new Company();

// access get() method
console.log(newCompany.ceo); // output: 'someone'

// access set() method
newCompany.ceo = 'me';

// access get() method
console.log(newCompany.ceo); // output: 'me'
```

### usage
- data validation

```javascript
set: (value) => {
  // validate value
  if (typeof value !== 'string') {
    throw new TypeError('ceo\'s name should be string!');
  }
  _ceo = value;
}
```

- define computed properties
```javascript
var manager = {
    firstName: 'blake',
    lastName: 'weiss',
    get fullName() {
        return this.firstName + ' ' + this.lastName;
    }
}

console.log(manager.fullName);
```
