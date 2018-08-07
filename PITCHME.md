# Testing with Protractor

---

## **Synchronous** vs **Asynchronous** execution in JS

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
Asynchronous example with Promise:

```TypeScript
  function  add(a:number):Promise<number>{
      return backendCall().then((b)=>{
          return a + b;
      }); 
  }
  
  // ... 
  const result = add(1);
  console.log(result); // Promise... 
  
  // ... 
  add(1).then((result)=>{
       console.log(result); // 2
  });
 
```

---
Asynchronous example with async:

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

## Async Test

```TypeScript

  it('should login', async () => {
    await login.loginUser(USERS.customerAdmin);
    await app.waitForHomeLoaded();
  });

```


---

## E2E

@ul
    - Don't e2e test what’s been unit tested
    - Make your tests **independent** at least at the file level
    - Do not add logic to your test
    - Don't mock unless you need to
    - Use Jasmine3
    - Make your tests independent from each other
    - Navigate to the page under test before each test
@ulend

---
## Do not add logic to your test, use Jasmine
https://jasmine.github.io/api/3.0/matchers.html

### Wrong test

```TypeScript
  it('I am bad', ()=>{
      if (items.length!==4){
          throw Error('Test is failing');
      }
      for (let i=0; i<items.length, i++) {
          if (items[i]<10){
              throw Error('Test is failing');
          }
      }
  });
```

---
### Good test
```TypeScript
  it('I am good', ()=>{
      expect(items).toEqual([10,10,10,10]);
  });
```

---


## Test suite
```TypeScript
import {Login} from './login.po';
import {App} from '../common/common.po';
import {USERS} from '../config';
describe('Login page', () => { 
    let login: Login;
    let app: App;
    beforeEach(async (done) => {
    });
    it('should not login if fake email given', async () => {
    });
});
```

@[1-3](Imports)
@[5](Test suite declaration)
@[6-8](Page objects declarations)
@[9-12](Test initialization, with navigate)
@[13-16](it blocks with expectations)

---

## Page Object Structure

```TypeScript

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

## Page Object reasons


@ul
 - Encapsulate information about the elements on the page under test
 - They can be reused across multiple tests
 - Decouple the test logic from implementation details
 - Avoid using expect() in page objects
@ulend

---

## Workshop

 - Branch: engage3/**e2e-workshop**
