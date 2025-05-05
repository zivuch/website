---
title: Testing in NestJS
menu_order: 10
post_status: publish
post_excerpt: Learn how to write unit and integration tests in NestJS using Jest and the built-in testing utilities provided by the framework.
taxonomy:
  category:
    - nestjs
    - Advanced Guide to NestJS
  post_tag:
    - nestjs
    - testing
    - jest
    - unit testing
    - e2e testing
    - mocks
---

<div class="toc" markdown="1">

## On this Page

- [Why Testing Matters in NestJS](#why-testing-matters-in-nestjs)
- [Testing Tools Included by Default](#testing-tools-included-by-default)
- [Writing Unit Tests for Services](#writing-unit-tests-for-services)
- [Testing Controllers](#testing-controllers)
- [Testing with Mocks](#testing-with-mocks)
- [End-to-End Testing](#end-to-end-testing)
- [Summary](#summary)

</div>

<div class="guru-main" markdown="1">

## Why Testing Matters in NestJS

NestJS is built with **testability** in mind.

Good tests:

- Prevent regressions
- Help you refactor safely
- Improve confidence in your app

Nest uses **Jest** by default, but you can use other test runners too.

---

## Testing Tools Included by Default

When you run:

```bash
nest new my-app
```

You get:

- Jest pre-configured
- `test/` folder with example e2e test
- `*.spec.ts` files ready to go

---

## Writing Unit Tests for Services

Example service:

```ts
@Injectable()
export class UsersService {
  findAll() {
    return ['Alice', 'Bob'];
  }
}
```

Unit test:

```ts
describe('UsersService', () => {
  let service: UsersService;

  beforeEach(() => {
    service = new UsersService();
  });

  it('should return all users', () => {
    expect(service.findAll()).toEqual(['Alice', 'Bob']);
  });
});
```

---

## Testing Controllers

For testing controllers, use `Test.createTestingModule`:

```ts
describe('UsersController', () => {
  let controller: UsersController;
  let service: UsersService;

  beforeEach(async () => {
    const module = await Test.createTestingModule({
      controllers: [UsersController],
      providers: [
        {
          provide: UsersService,
          useValue: {
            findAll: jest.fn().mockReturnValue(['Mocked']),
          },
        },
      ],
    }).compile();

    controller = module.get<UsersController>(UsersController);
    service = module.get<UsersService>(UsersService);
  });

  it('should return mocked users', () => {
    expect(controller.findAll()).toEqual(['Mocked']);
  });
});
```

---

## Testing with Mocks

Use `jest.fn()` to:

- Mock methods
- Spy on calls
- Assert behavior

Example:

```ts
const mockSend = jest.fn();
emailService.sendEmail = mockSend;

await emailService.sendEmail('test@example.com');
expect(mockSend).toHaveBeenCalledWith('test@example.com');
```

---

## End-to-End Testing

E2E tests live in `/test` and spin up the real app:

```ts
describe('AppController (e2e)', () => {
  let app: INestApplication;

  beforeAll(async () => {
    const moduleFixture = await Test.createTestingModule({
      imports: [AppModule],
    }).compile();

    app = moduleFixture.createNestApplication();
    await app.init();
  });

  it('/ (GET)', () => {
    return request(app.getHttpServer())
      .get('/')
      .expect(200)
      .expect('Hello World!');
  });
});
```

Use `supertest` to simulate HTTP requests.

---

## Summary

- NestJS is built to be test-friendly
- Use **unit tests** for services and business logic
- Use **integration tests** for controllers with mocks
- Use **e2e tests** to validate full app behavior via HTTP

> Next: **Lesson 11 – Building a REST API** (start of the Practical Guide)

</div>
