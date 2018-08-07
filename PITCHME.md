# Testing with Protractor

---

## **Synchronous** vs **Asynchronous** execution in JS

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
Asynchronous example with Promise:

```JavaScript
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

```JavaScript
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
```JavaScript
  it('I am good', ()=>{
      expect(items).toEqual([10,10,10,10]);
  });
```

---


##  Test suite

```JavaScript
import {Login} from './login.po';
import {App} from '../common/common.po';
import {USERS} from '../config';

describe('Login page', () => {
  let login: Login;
  let app: App;


  beforeEach(async (done: () => void) => {
    login = new Login();
    app = new App();
    await login.navigateTo();
    done();
  });

  it('should login', async () => {
    await login.loginUser(USERS.customerAdmin);
    await app.waitForHomeLoaded();
  });

  it('should not login if fake email given', async () => {
    await login.loginUser({email: 'fakeemail@fff.ff', password: '123456'});
    expect(await login.getAlertMessage()).toContain('Incorrect email or password.');
  });
});
```

@[1-3]
@[5]
@[6-7]
@[10-15]
@[17-20]
@[22-25]

---

## Page Object Structure

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
