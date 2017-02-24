---
layout: post
title: VSCode&#58; Imports in *.d.ts files for javascript projects
---

Use [global augmentation](https://www.typescriptlang.org/docs/handbook/declaration-merging.html#global-augmentation) and a triple slash directive

```typescript
// index.d.ts
import { Robot } from "robot"

declare global {
  // Globally defined interfaces here.
}

// index.js
/// <reference path="index.d.ts" />
```
