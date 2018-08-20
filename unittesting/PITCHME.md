# Tests in Angular6

---



@ul
  - Service Tests (UnitTest)
  - Component Tests:
    - Component Class Tests
    - Component DOM Tests
@ulend



---

# UnitTest

   - Make your tests **independent**
   - Do not add **logic** to your test
   - **Mock** dependencies
   - Use **Spies** and Stubs
   - Use Jasmine3
   - Don't test **private** methods


---

# Service Tests

```TypeScript
@Injectable()
export class EngageLocalStorageService {
  constructor(private localStorageService) {

  }
  public getItem(key): any {
    return this.localStorageService.get(key);
  }
  public setItem(key, value) {
    this.localStorageService.set(key, value);
  }
  public removeItem(key) {
    this.localStorageService.remove(key);
  }

}
```

@[3]: Dependency
---
# Service Tests
```TypeScript
 describe('EngageLocalStorageService', ()=>{
     describe('getItem', ()=>{

     });
 });
```
