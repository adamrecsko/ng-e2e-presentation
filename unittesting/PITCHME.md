# Tests in Angular6

---


@ul
  - Service Tests
  - Component Tests:
    - Component Class Tests
    - Component DOM Tests
@ulend



---


# Service Tests

```TypeScript
@Injectable()
export class EngageLocalStorageService {
  constructor(private localStorageService: LocalStorageService) {
  }
  getItem(key): any {
    return this.localStorageService.get(key);
  }
  setItem(key, value) {
    this.localStorageService.set(key, value);
  }
  removeItem(key) {
    this.localStorageService.remove(key);
  }
  clear() {
    this.localStorageService.clearAll();
  }
}

```

@[3]: Dependency

---
