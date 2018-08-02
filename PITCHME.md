# Testing with Protractor

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

## Async Test

```JavaScript

  it('should login', async () => {
    await login.loginUser(USERS.customerAdmin);
    await app.waitForHomeLoaded();
  });

```


---

## E2E

@ul
    - Don't e2e test what’s been unit tested
    - Make your tests independent at least at the file level
    - Do not add logic to your test
    - Don't mock unless you need to
    - Use Jasmine2
    - Make your tests independent from each other
    - Navigate to the page under test before each test
@ulend

---

## Page Object

```JavaScript

export class Login {

  navigateTo() {
    return browser.get(loginPage);
  }

  getEmailField() {
    return PageLocators.getObjByFormCtrlName('email');
  }
  ...
}

```

---

## Page Object


@ul
 - Encapsulate information about the elements on the page under test
 - They can be reused across multiple tests
 - Decouple the test logic from implementation details
 - Avoid using expect() in page objects
@ulend

---

## Workshop
