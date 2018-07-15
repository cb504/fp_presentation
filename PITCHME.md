# Functional Programming: 

## The good, the bad, and the ugly.

Hezi Ben-Michael

---

# Overview

* Part 1: Pure functions
	* what and why
	* Walkthrough demo
* Part 2: Review of all the rest
	* Higher order functions
	* Recursion
	* Currying
	* Composition
	* Functors
	* Monads

---


# FP is all about Pure Functions


1. Is not affected by its environment. It is stateless

2.  Does not have side affects

* Why is this good?

---

# Walkthrough 

```javascript
getEventsBookableInNextHalfHour(events);
bookEvents(events);

function getEventsBookableInNextHalfHour(events) {
    // code
}
```

---

# Walkthrough 

```javascript
getEventsBookableInNextHalfHour(events);
bookEvents(events);

function getEventsBookableInNextHalfHour(events) {
    let now = Date.now();
}
```

---

# Walkthrough 

```javascript
getEventsBookableInNextHalfHour(events, Date.now());
bookEvents(events);

function getEventsBookableInNextHalfHour(events, datetime) {
    // code
}
```

---

# Walkthrough 

```javascript
let bookableEvents = getEventsBookableInNextHalfHour(events,
                                        Date.now());
bookEvents(bookableEvents);

function getEventsBookableInNextHalfHour(events, datetime) {
    // code
}
```

---

# Walkthrough – "Discover-ability Problem"


```javascript
let bookableEvents = getEventsBookableInNextHalfHour(events);
bookEvents(bookableEvents);

function getEventsBookableInNextHalfHour(events, datetime) {
    // code
}
```

---

# Walkthrough – "Discover-ability Problem"


```javascript
let bookableEvents = events.getEventsBookableInNextHalfHour();
bookEvents(bookableEvents);
//events.getEventsBookableInNextHalfHour().bookEvents();

static function getEventsBookableInNextHalfHour(this events: list[:event], datetime) {
    // code
}
```

---

# Part 1: highlights

* Pure Functions are pure logic/algorithm
* The "safe" place in your code
* OOP + Fluent API/Interface
* Use JS .filter(), .map(), .reduce()

---

# Part 2: All the rest

## Programming Languages

* Procedural: C
* OO: Java(~), Smalltalk
* __FP: Haskell, Scala, Erlang__
* Multi-paradigm: Javascript, C++, C#

---

# Review of all the rest 

* Higher order functions
* Recursion
* Currying
* Composition
* Functors
* Monads

---

# Higher order functions

```javascript
let f = foo() {};
```

* Module exports rely on this feature.

---

# Recursion
```javascript
let numbers = [1, 2, 3, 4];
let sum = add(0, numbers);

function add(accumulator, numbers) {
    accumulator = numbers[0];
    if (numbers.length == 1) return accumulator;
    add(accumulator, numbers.pop());
}
```

---

# Recursion, alternative is Loop

```javascript
let numbers = [1, 2, 3, 4];
let sum = add(0, numbers);

function add(numbers) {
    accumulator = 0;
    for(let number in numbers) accumulator += number;
    return accumulator;
}
```

---

# Currying

* Motive: allow function to have state
* Mathematics Motive: function should have only 1 input parameter

```javascript
// base service
let lcsClient = httpClient("lcs"); 

// average
let numbers = [1, 2, 3, 4];
let avg = divide(add(0, numbers), numbers.length);
// using currying, improve readability
let divideByLength = divideBy(numbers.length);
let avg = divideByLength(add(0, numbers));
```

---

# Currying, alterntives are OOP and fluent-api

```javascript
// base service - OOP
let lcsClient = new HttpClient("lcs"); 

// average – fluent API
let avg = numbers.sum().divideBy(numbers.length);
// 	real code
let avg = numbers.reduce(0, (a, b) => a + b) / numbers.length;
```

---

# Composition

```javascript
// -- Challenge 4 -------------------------
// Your challenge: implement a function to
// compute the average values in a list using
// only fork, _.divide, _.sum, and _.size.

var fork = _.curry(function(lastly, f, g, x) {
  return lastly(f(x), g(x));
});



// As you can see, the fork function is a
// pipeline like compose, except it duplicates
// its value, sends it to two functions, then
// sends the results to a combining function.

var avg = fork(_.divide, _.sum, _.size); // change this
assertEqual(3, avg([1,2,3,4,5]));
```

---

# Composition

* Fluent API is often better (more maintainable)
* But, when you can’t because the language doesn’t support fluent api?

* Try and use .filter(), .map(), .reduce()   everyone will thank you later
* Keep all your utility functions related to a specific type in one OBVIOUS place. 
Your composed function are in the same file as the composite.
* Make sure at least 1-2 other people understand your code. If it is too difficult, explicit composition is better/safer (if a bit ugly):

```javascript
let avg = divide(sum(numbers), numbers.length);
```

---

# Functors

* Stuff that is mappable

---

# Monads

* Wrapping procedural code in function.

* In JS, rely multi-paradigm

---

# Review of all the rest 

FP Idiom | Critique
---------|-----------
Higher order functions | (ok)
Recursion | "Loops are your friends"
Currying | OOP
Composition | Fluent-API
Functors | ????
Monads | "Because procedural is a naughty word"

---

# Final Thoughts

* Procedural -> FP -> FP -> Procedural
* Leverage multi-paradigm (OOP, procedural) 
* FP creates safe places in your code, code that is very testable
* Use .filter(), .map(), .reduce()
* Discover-ability, Fluent API

Have a great day
