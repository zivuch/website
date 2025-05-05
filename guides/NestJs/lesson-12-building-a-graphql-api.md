---
title: Building a GraphQL API
menu_order: 12
post_status: publish
post_excerpt: Learn how to build a GraphQL API in NestJS using decorators, resolvers, and schema-first or code-first approaches.
taxonomy:
  category:
    - nestjs
    - Practical Guide to NestJS
  post_tag:
    - nestjs
    - graphql
    - api
    - schema
    - resolver
    - code-first
---

<div class="toc" markdown="1">

## On this Page

- [Why Use GraphQL with NestJS?](#why-use-graphql-with-nestjs)
- [Installing GraphQL Dependencies](#installing-graphql-dependencies)
- [Setting Up the GraphQL Module](#setting-up-the-graphql-module)
- [Defining a GraphQL Object Type](#defining-a-graphql-object-type)
- [Creating a Resolver](#creating-a-resolver)
- [Querying the API with Playground](#querying-the-api-with-playground)
- [Summary](#summary)

</div>

<div class="guru-main" markdown="1">

## Why Use GraphQL with NestJS?

GraphQL is a modern alternative to REST that allows clients to:

- Ask for exactly the data they need
- Combine multiple resources in one query
- Get strong typing and introspection for free

NestJS integrates tightly with GraphQL via a **code-first** or **schema-first** approach.

---

## Installing GraphQL Dependencies

```bash
npm install @nestjs/graphql @nestjs/apollo graphql apollo-server-express
```

---

## Setting Up the GraphQL Module

In your `AppModule`:

```ts
import { GraphQLModule } from '@nestjs/graphql';

@Module({
  imports: [
    GraphQLModule.forRoot({
      autoSchemaFile: true, // generates schema.gql
      playground: true,
    }),
  ],
})
export class AppModule {}
```

This sets up **code-first** GraphQL with schema auto-generation.

---

## Defining a GraphQL Object Type

```ts
import { ObjectType, Field, Int } from '@nestjs/graphql';

@ObjectType()
export class Post {
  @Field(() => Int)
  id: number;

  @Field()
  title: string;

  @Field()
  content: string;
}
```

---

## Creating a Resolver

```ts
import { Resolver, Query, Mutation, Args, Int } from '@nestjs/graphql';

@Resolver(() => Post)
export class PostsResolver {
  private posts: Post[] = [];

  @Query(() => [Post])
  getPosts() {
    return this.posts;
  }

  @Mutation(() => Post)
  createPost(
    @Args('title') title: string,
    @Args('content') content: string,
  ): Post {
    const newPost = { id: Date.now(), title, content };
    this.posts.push(newPost);
    return newPost;
  }

  @Query(() => Post, { nullable: true })
  getPost(@Args('id', { type: () => Int }) id: number) {
    return this.posts.find(p => p.id === id);
  }
}
```

---

## Querying the API with Playground

Start the server and go to:

```
http://localhost:3000/graphql
```

Example query:

```graphql
query {
  getPosts {
    id
    title
    content
  }
}
```

Example mutation:

```graphql
mutation {
  createPost(title: "Nest GraphQL", content: "Works great!") {
    id
    title
  }
}
```

---

## Summary

- NestJS supports GraphQL via code-first or schema-first approach
- You define object types and resolvers using decorators
- GraphQL playground makes development and testing simple
- Use GraphQL for flexible, client-driven APIs

> Next: **Lesson 13 – File Uploads and Validation**

</div>
