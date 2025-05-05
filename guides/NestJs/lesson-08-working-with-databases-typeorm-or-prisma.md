---
title: Working with Databases (TypeORM or Prisma)
menu_order: 8
post_status: publish
post_excerpt: Learn how to connect NestJS to a database using TypeORM or Prisma, define models, and write clean, scalable queries.
taxonomy:
  category:
    - nestjs
    - Advanced Guide to NestJS
  post_tag:
    - nestjs
    - database
    - typeorm
    - prisma
    - postgres
    - mongodb
---

<div class="toc" markdown="1">

## On this Page

- [Choosing Between TypeORM and Prisma](#choosing-between-typeorm-and-prisma)
- [Setting Up TypeORM](#setting-up-typeorm)
- [Defining Entities and Repositories](#defining-entities-and-repositories)
- [Setting Up Prisma](#setting-up-prisma)
- [Defining Models and Using the Prisma Client](#defining-models-and-using-the-prisma-client)
- [Database Module Best Practices](#database-module-best-practices)
- [Summary](#summary)

</div>

<div class="guru-main" markdown="1">

## Choosing Between TypeORM and Prisma

NestJS supports both **TypeORM** and **Prisma**. Choose based on:

| Feature              | TypeORM                    | Prisma                      |
|----------------------|----------------------------|-----------------------------|
| Decorators           | ✅ Built-in                 | ❌ Uses schema.prisma file  |
| Type Safety          | ⚠️ Partial                 | ✅ Excellent                 |
| Migration Support    | ✅ Yes                      | ✅ Yes                       |
| Performance          | ⚠️ Slower                   | ✅ Fast + optimized queries  |
| Ecosystem Fit        | ✅ Native to NestJS         | ✅ Works well with NestJS    |

---

## Setting Up TypeORM

Install:

```bash
npm install @nestjs/typeorm typeorm pg
```

Configure in `AppModule`:

```ts
import { TypeOrmModule } from '@nestjs/typeorm';

@Module({
  imports: [
    TypeOrmModule.forRoot({
      type: 'postgres',
      host: 'localhost',
      port: 5432,
      username: 'postgres',
      password: '',
      database: 'test',
      autoLoadEntities: true,
      synchronize: true, // 🚫 disable in prod
    }),
  ],
})
export class AppModule {}
```

---

## Defining Entities and Repositories

```ts
@Entity()
export class User {
  @PrimaryGeneratedColumn()
  id: number;

  @Column()
  name: string;

  @Column({ unique: true })
  email: string;
}
```

Use with `TypeOrmModule.forFeature`:

```ts
@Module({
  imports: [TypeOrmModule.forFeature([User])],
  providers: [UsersService],
  controllers: [UsersController],
})
export class UsersModule {}
```

Inject repository:

```ts
@Injectable()
export class UsersService {
  constructor(
    @InjectRepository(User) private repo: Repository<User>
  ) {}

  async findAll() {
    return this.repo.find();
  }
}
```

---

## Setting Up Prisma

Install:

```bash
npm install prisma --save-dev
npm install @prisma/client
npx prisma init
```

Edit `prisma/schema.prisma`:

```prisma
model User {
  id    Int    @id @default(autoincrement())
  name  String
  email String @unique
}
```

Generate client:

```bash
npx prisma generate
```

Create module:

```ts
import { PrismaClient } from '@prisma/client';

@Injectable()
export class PrismaService extends PrismaClient {
  constructor() {
    super();
  }
}
```

Use in services:

```ts
@Injectable()
export class UsersService {
  constructor(private prisma: PrismaService) {}

  async findAll() {
    return this.prisma.user.findMany();
  }
}
```

---

## Database Module Best Practices

- Wrap database logic in services
- Keep ORM-specific logic isolated from your controllers
- Use `@Transactional()` or Prisma middleware for atomic ops
- Use `.env` for DB config (never hardcode credentials)

---

## Summary

- NestJS supports **TypeORM** (decorator-based) and **Prisma** (schema-first)
- Both integrate cleanly with DI and modules
- Use feature modules and repository patterns to stay organized
- Prefer Prisma for large-scale apps and advanced type safety

> Next: **Lesson 9 – Authentication with Passport and JWT**

</div>
