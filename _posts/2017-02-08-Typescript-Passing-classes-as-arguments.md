---
layout: post
title: Typescript&#58; Passing classes as arguments
---

In typescript is is very common to pass an instance of a class type as an argument. For example:

```typescript
class Apple { /** ...etc */ }

function consumer(apple: Apple) { /** ...etc */ }

consumer(apple: new Apple());
```

But what if you wanted to pass the class itself as an argument rather than an instance of the class?
The answer is luckily very simple.

You place `typeof` in front of the parameter type:

```typescript
class Apple { /** ...etc */ }



function consumer(Apple: typeof Apple) { // apple is now Apple
  /** ...etc */
}

consumer(Apple: Apple); 
```

Now `consumer` can take any class with the name Apple as an argument.

## Classes that implement an interface as an argument

If you care more about the implementation of the class then the class name itself the above example isn't much use. Semantically what you need is a constructor function as an argument.

That looks something like this.

```typescript
interface Apple { /** ...etc */ } // You want your function to take a class that implements this interface

class GoldenDelicious implements Apple { /** ...etc */ } // Here is an example of one of those classes

function consumer(Apple: new () => Apple) { // Consumer takes a class that implements apple
 const apple = new Apple();
}

consumer(Apple: GoldenDelicious) // We did it (ﾉ◕ヮ◕)ﾉ*:･ﾟ✧
```
