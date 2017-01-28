---
layout: post
title: Importing types into *.d.ts files with global definitions
---

tldr: Use [global augmentation](https://www.typescriptlang.org/docs/handbook/declaration-merging.html#global-augmentation) and a tripple slash directive
```typescript
// index.d.ts
import { Robot } from "robot"

declare global {
  // Globally defined interfaces here.
}

// index.js
/// <reference path="index.d.ts" />
```

In the last couple of months I've started using visual studio code as my go to text editor. One of the greatest features
of vscode is its built in "intellisense" which gives you lots of usefull type information (string, number, etc) as you're
coding. This is especially useful for typescript projects but works great in javascript projects using jsdoc. Well recently I ran into
a tricky problem with intelisense. I wanted typing hints for a javascript project that happened to rely on a typescript
code base. Usually when I want good intellisense support for a javascript file I'll just write a .d.ts file with all of
my declarations and it will apply to the global javascript scope (I know, I know, globals are bad. But bear with me,
you'll see why). But in this case I wanted to import a type from a typescript project. As it turns out import statements
change the .d.ts file from a global definition to a module definition. Since this .d.ts only contained interfaces (which
dont exist in javascript) there was no way to import it into my javascript file. The .d.ts file had to affect the global
scope and it needed to import a type. This was somewhat of a catch 22. Luckily, after much anguish, I found an obscure
reference to a solution at the very bottom of the decleration merging section of the typescript handbook. [global augmentation.](https://www.typescriptlang.org/docs/handbook/declaration-merging.html#global-augmentation)

After that discovery the implementation was trivial:
```typescript
// index.d.ts
import { Robot } from "robot"

declare global {
  declare interface MovementFunc {
    (robot: Robot): Promise<any>
  }
}
```
```javascript
// index.js
/// <reference path="index.d.ts" /> // You must use a triple slash directive for the .d.ts file to work

/**
 * Convince the robot to do your motion
 * @param {MovementFunc} motion - motion to do
 **/
function doWork(motion) {
  // Internals
}
```

vscode version 1.8