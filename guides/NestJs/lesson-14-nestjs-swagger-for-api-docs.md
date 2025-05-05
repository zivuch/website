---
title: NestJS + Swagger for API Docs
menu_order: 14
post_status: publish
post_excerpt: Automatically generate interactive API documentation for your NestJS app using the built-in Swagger module.
taxonomy:
  category:
    - nestjs
    - Practical Guide to NestJS
  post_tag:
    - nestjs
    - swagger
    - api docs
    - openapi
    - documentation
---

<div class="toc" markdown="1">

## On this Page

- [Why Use Swagger with NestJS?](#why-use-swagger-with-nestjs)
- [Installing Swagger Module](#installing-swagger-module)
- [Setting Up Swagger in main.ts](#setting-up-swagger-in-main.ts)
- [Using Decorators for Auto-Docs](#using-decorators-for-auto-docs)
- [Customizing Swagger Options](#customizing-swagger-options)
- [Protecting or Versioning the Docs](#protecting-or-versioning-the-docs)
- [Summary](#summary)

</div>

<div class="guru-main" markdown="1">

## Why Use Swagger with NestJS?

NestJS integrates seamlessly with **Swagger** (OpenAPI spec) to:

- Auto-generate API documentation
- Provide an interactive UI for testing endpoints
- Document request/response DTOs, headers, and status codes
- Make APIs easier to understand and share

---

## Installing Swagger Module

Install the official NestJS Swagger package:

```bash
npm install --save @nestjs/swagger swagger-ui-express
```

---

## Setting Up Swagger in `main.ts`

```ts
import { SwaggerModule, DocumentBuilder } from '@nestjs/swagger';

async function bootstrap() {
  const app = await NestFactory.create(AppModule);

  const config = new DocumentBuilder()
    .setTitle('Blog API')
    .setDescription('API docs for the blog platform')
    .setVersion('1.0')
    .addBearerAuth()
    .build();

  const document = SwaggerModule.createDocument(app, config);
  SwaggerModule.setup('docs', app, document);

  await app.listen(3000);
}
bootstrap();
```

Open [http://localhost:3000/docs](http://localhost:3000/docs) to see it in action.

---

## Using Decorators for Auto-Docs

Decorate your DTOs and endpoints to make Swagger smarter:

```ts
import { ApiProperty } from '@nestjs/swagger';

export class CreatePostDto {
  @ApiProperty({ example: 'NestJS Guide' })
  title: string;

  @ApiProperty({ example: 'A full tutorial on NestJS.' })
  content: string;
}
```

In controllers:

```ts
@ApiTags('posts')
@Controller('posts')
export class PostsController {
  @Post()
  @ApiCreatedResponse({ description: 'The post has been created.' })
  create(@Body() dto: CreatePostDto) {
    return this.postsService.create(dto);
  }
}
```

Other useful decorators:

- `@ApiQuery()`
- `@ApiParam()`
- `@ApiBody()`
- `@ApiResponse()`

---

## Customizing Swagger Options

You can:

- Add logo, contact info, servers
- Enable Bearer token auth
- Group endpoints by tags

```ts
.setContact('Support', '', 'support@example.com')
.setExternalDoc('Postman Collection', '/docs/postman')
.addServer('http://localhost:3000')
```

---

## Protecting or Versioning the Docs

To version your API docs:

```ts
SwaggerModule.setup('docs/v1', app, document);
```

To protect with a password, wrap the `/docs` route in a middleware or guard.

---

## Summary

- NestJS + Swagger = beautiful, live-updating API docs
- Use decorators like `@ApiProperty()` and `@ApiResponse()` for rich documentation
- Customize and protect your docs to suit your needs

> Next: **Lesson 15 – Deploying a NestJS App**

</div>
