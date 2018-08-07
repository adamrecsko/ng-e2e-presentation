# Testing with Protractor

---

## **Sync** vs **Async** 

@ul
    - Everything is async in protractor
    - What is sync and what is async?
@ulend

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

@[6]
@[2]
@[3]
@[7]

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

@[8]
@[2]
@[9]
@[12]
@[3]
@[13]
---
## What is a Promise?
```TypeScript
   interface Promise {
     then(onResolve, onReject):Promise;
     catch(onReject):Promise;
   }
   
   let i = 1;
   const prom = new Promise((resolve, reject)=>{
      i=i+1; // this is ugly, side effect!! avoid it all cost!!
      resolve();
   });
   console.log(i); // ????
```

@[1-4](Promise interface)
@[6-11](What is on the console?)
---

Asynchronous example with async (ES7):

```TypeScript
  function async add(a:number):Promise<number>{
      const b = await backendCall(); // 1
      return a + b;
  }
  
  // ... 
  const result = add(1);
  console.log(result); // Promise... 
  
  // ... 
  const result = await add(1);
  console.log(result); // 2
```

@[1](async function)
@[2](await for something, it is like the then block)
@[3](work with the async result data)
@[7-8](still returns a promise)
@[11-12](but you can await)
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
## Do not add logic to your test
https://jasmine.github.io/api/3.0/matchers.html

### Wrong test

```TypeScript
  it('should contain only 4 10 values', ()=>{
      if (items.length!==4){
          throw Error('Test is failing');
      }
      for (let i=0; i<items.length, i++) {
          if (items[i]!==10){
              throw Error('Test is failing');
          }
      }
  });
```

@[2-4](Test if the items length not equal 4)
@[5-9](Test if every item in the items array is 10)

---
### Good test
```TypeScript
  it('should contain only 4 10 values', ()=>{
      expect(items).toEqual([10,10,10,10]);
  });
```
@[2](Use Jasmine)
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
@[4](Test suite declaration)
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

}

export class App {

  isHomeLoaded() {
    return PageLocators.getObjByTagName('tm-home').isPresent();
  }

  async waitForHomeLoaded(waitSec = 3000) {
    await browser.wait(() => this.isHomeLoaded(), waitSec, `Home screen should loaded within ${waitSec}s`);
  }
}

```

@[1](It is a simple class nothing fancy)
@[3-5](Navigate to his page, use the browser module)
@[7-9](Methods to manipulate or query the DOM strucutre)

@[13](Common App Page object)
@[20](Wait for something to load, async world)

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
