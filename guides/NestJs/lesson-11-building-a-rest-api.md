---
title: Building a REST API
menu_order: 11
post_status: publish
post_excerpt: A step-by-step guide to building a modular and scalable REST API using NestJS with controllers, services, DTOs, and routing.
taxonomy:
  category:
    - nestjs
    - Practical Guide to NestJS
  post_tag:
    - nestjs
    - rest api
    - routing
    - crud
    - services
    - dto
---

<div class="toc" markdown="1">

## On this Page

- [What We're Building](#what-were-building)
- [Scaffold the Project](#scaffold-the-project)
- [Create a Feature Module](#create-a-feature-module)
- [Define DTOs for Request Validation](#define-dtos-for-request-validation)
- [Implement CRUD in the Service](#implement-crud-in-the-service)
- [Create REST Endpoints in the Controller](#create-rest-endpoints-in-the-controller)
- [Summary](#summary)

</div>

<div class="guru-main" markdown="1">

## What We're Building

We’ll build a **Posts API** with endpoints to:

- Create a post
- Get all posts
- Get a single post by ID
- Update a post
- Delete a post

We'll use:

- Controllers & Services
- DTOs for validation
- A basic in-memory array for data storage (for now)

---

## Scaffold the Project

If not already created:

```bash
nest new blog-api
cd blog-api
```

Generate the `posts` module:

```bash
nest g module posts
nest g controller posts
nest g service posts
```

---

## Create a Feature Module

Ensure `PostsModule` is imported in `AppModule`:

```ts
@Module({
  imports: [PostsModule],
})
export class AppModule {}
```

---

## Define DTOs for Request Validation

```ts
// posts/dto/create-post.dto.ts
export class CreatePostDto {
  title: string;
  content: string;
}
```

```ts
// posts/dto/update-post.dto.ts
export class UpdatePostDto {
  title?: string;
  content?: string;
}
```

---

## Implement CRUD in the Service

```ts
// posts/posts.service.ts
@Injectable()
export class PostsService {
  private posts = [];

  findAll() {
    return this.posts;
  }

  findOne(id: number) {
    return this.posts.find(p => p.id === id);
  }

  create(post: CreatePostDto) {
    const newPost = { id: Date.now(), ...post };
    this.posts.push(newPost);
    return newPost;
  }

  update(id: number, update: UpdatePostDto) {
    const index = this.posts.findIndex(p => p.id === id);
    if (index === -1) return null;
    this.posts[index] = { ...this.posts[index], ...update };
    return this.posts[index];
  }

  remove(id: number) {
    const index = this.posts.findIndex(p => p.id === id);
    if (index === -1) return null;
    const [removed] = this.posts.splice(index, 1);
    return removed;
  }
}
```

---

## Create REST Endpoints in the Controller

```ts
// posts/posts.controller.ts
@Controller('posts')
export class PostsController {
  constructor(private postsService: PostsService) {}

  @Get()
  findAll() {
    return this.postsService.findAll();
  }

  @Get(':id')
  findOne(@Param('id') id: string) {
    return this.postsService.findOne(Number(id));
  }

  @Post()
  create(@Body() dto: CreatePostDto) {
    return this.postsService.create(dto);
  }

  @Put(':id')
  update(@Param('id') id: string, @Body() dto: UpdatePostDto) {
    return this.postsService.update(Number(id), dto);
  }

  @Delete(':id')
  remove(@Param('id') id: string) {
    return this.postsService.remove(Number(id));
  }
}
```

Test it with Postman or curl:

```bash
curl http://localhost:3000/posts
```

---

## Summary

- We built a fully functional REST API using NestJS
- Used modular structure with controllers, services, and DTOs
- Created a CRUD feature with clean and testable code

> Next: **Lesson 12 – Building a GraphQL API**

</div>
