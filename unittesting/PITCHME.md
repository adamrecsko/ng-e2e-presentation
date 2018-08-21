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

---

```TypeScript

@Injectable()
export class EngageLocalStorageService {
  constructor(private localStorageService:LocalStorageService) {

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

@[7]: Test getItem
@[4]: Dependency

---

```TypeScript
 describe('EngageLocalStorageService', ()=>{
     describe('getItem', ()=>{
         let service: EngageLocalStorageService;
         let storageMock: any;
         beforeEach( () => {
             storageMock = jasmine.createSpyObj('storageService', ['get']);
             service = new EngageLocalStorageService(storageMock);
         });
         it('should call the storageServices get method', ()=>{
             const res = service.getItem('something');
             expect(storageMock.get).toHaveBeenCalledWith('something');
         });
     });
 });
```
@[1]: Service Tests
@[2]: Method Tests
@[5-8]:Init
@[9-12]: Tests
---

# Service Test
(with TestBed)

@ul
  - What is TestBed?
  - TestBed creates a dynamically-constructed Angular test module
  - Emulates an Angular @NgModule.
@ulend

---

```TypeScript
@NgModule({
  providers: [
    LocalStorageService,
    EngageLocalStorageService,

  ],
  bootstrap: [AppComponent]
})
export class AppModule {
}

```

---

```TypeScript
beforeEach(() => {
  const storageMock = jasmine.
     createSpyObj('storageService', ['get']);
  TestBed.
  configureTestingModule(
      { providers: 
         [EngageLocalStorageService,
          { provide: LocalStorageService, useValue: storageMock }
         ]
      }
  );
});

it('should call the storageServices get method', ()=>{
   const service = TestBed.get(EngageLocalStorageService);
   expect(storageMock.get).toHaveBeenCalledWith('something');
});

```
@[4-10]: Init 
@[15-16]: Method Tests

---