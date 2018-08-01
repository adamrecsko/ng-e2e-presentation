# Testing Angular6

---

## Preface

- TypeScript
- Asynchronous vs Synchronous execution in JavaScript

---

## TypeScript
 
@ul

  - Use Types all the time (avoid ```any```)
  - What is Type Inference
  - Helps refactoring
  - Maintain consistency

@ulend

---
## Synchronous vs Asynchronous execution in JavaScript

---
Synchronous example:

```JavaScript 

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

```JavaScript
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
- Jasmine
- Structure
- PageObject (The Interface of the Page)
- Directives (describe/it/before/after..)
- No Side effect


---

## Protractor

- E2E runner (top of the test pyramid)
- Works with selenium and **browserstack**
- Shipped with angular6


## Jasmine

---gist=adamrecsko/36bf9e6502691c24c3f106d5d36190f2?lang=JavaStrip

---

## Structure
Directory structure:
  ```
     e2e/
        ./common  -- common logic goes there, e.g.: customer creation, smtp connection. etc...
        ./page1   -- multiple user steps like: user invite, registration related to that page
        ./page2
        ./flow1   -- multiple user steps related to that user flow.
                  -- the subfolders representing the scope of the e2e test
        ....
      
  ```
  
---  
File structure
   flow1/flow1.e2e-spec.ts  -- the prefix is used by the test runner to find the scenarios
   flow1/page
  
  
---

## End
