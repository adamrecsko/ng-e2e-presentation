
# Testing Angular6

---




## Preface

- TypeScript
- Asynchronous vs Synchronous execution in JavaScript

---

## TypeScript
 
@ul
  - Type Inference
  - Helps refactor
  - Maintain consistency
  - Use Types all the time (avoid ```any```)
@ulend

---
## Synchronous vs Asynchronous execution in JavaScript

---
Synchronous example:


```TypeScript 
  function add(a:number):number{
     const b = 1;
     return a + b;
  }
  // ... 
  const result = add(1);
  console.log(result); // 2
  
```
---
Asynchronous example:

```TypeScript
  function async add(a:number):Promise<number>{
      const b = await backendCall(); // 1
      return await a + b;
  }
  
  // ... 
  const result = add(1);
  console.log(result); // Promise... 
  
  // ... 
  const result = await add(1);
  console.log(result); // 2
  
  
```

---



## E2E

- Protractor
- Structure
- Directives (describe/it/before/after..)
- No Side effect
- PageObject (The Interface of the Page)

---

## Protractor

- E2E runner (top of the test pyramid)
- Works with selenium and **browserstack**
- Shipped with angular6


---

## End
