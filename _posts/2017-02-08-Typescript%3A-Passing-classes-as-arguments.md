---
layout: post
title: Typescript&#58 Passing classes as arguments
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

Now consumer can take any class with the name Apple as an argument.
