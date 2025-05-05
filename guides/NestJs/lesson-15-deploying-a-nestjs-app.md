---
title: Deploying a NestJS App
menu_order: 15
post_status: publish
post_excerpt: Learn how to prepare and deploy your NestJS app to production using platforms like Heroku, Render, Vercel, or a custom server.
taxonomy:
  category:
    - nestjs
    - Practical Guide to NestJS
  post_tag:
    - nestjs
    - deployment
    - production
    - vercel
    - heroku
    - docker
---

<div class="toc" markdown="1">

## On this Page

- [Preparing for Deployment](#preparing-for-deployment)
- [Build and Serve the App](#build-and-serve-the-app)
- [Environment Variables](#environment-variables)
- [Deployment Options](#deployment-options)
- [Dockerizing a NestJS App](#dockerizing-a-nestjs-app)
- [Useful Production Tips](#useful-production-tips)
- [Summary](#summary)

</div>

<div class="guru-main" markdown="1">

## Preparing for Deployment

Before deploying, make sure to:

✅ Use `production` environment variables  
✅ Disable `synchronize: true` if using TypeORM  
✅ Enable validation and global pipes  
✅ Add proper logging

In `main.ts`:

```ts
app.useGlobalPipes(new ValidationPipe({ whitelist: true }));
```

---

## Build and Serve the App

Build the project:

```bash
npm run build
```

Nest will compile your TypeScript files to JavaScript in the `/dist` directory.

Then run it with:

```bash
node dist/main.js
```

Or use a process manager like `pm2` in production:

```bash
pm2 start dist/main.js
```

---

## Environment Variables

Store sensitive config like DB credentials and JWT secrets in a `.env` file and load with `@nestjs/config`.

```bash
npm install @nestjs/config
```

```ts
ConfigModule.forRoot({
  isGlobal: true,
  envFilePath: '.env',
});
```

Access variables via `process.env.DB_HOST`.

---

## Deployment Options

### 🔹 Heroku

1. Install Heroku CLI
2. Add a `Procfile`:

```
web: npm run start:prod
```

3. Push to Heroku:

```bash
git push heroku main
```

### 🔹 Render

1. Connect GitHub repo
2. Use `npm run build && npm run start:prod` as build & start command
3. Add `.env` variables via dashboard

### 🔹 Vercel

Use [vercel-serverless](https://vercel.com/docs/serverless-functions/introduction) functions if you export Nest as a handler (with Express adapter).

For full server Nest apps, prefer Render or Railway instead.

---

## Dockerizing a NestJS App

```Dockerfile
# Dockerfile
FROM node:18-alpine
WORKDIR /app
COPY package*.json ./
RUN npm install --production
COPY . .
RUN npm run build
CMD ["node", "dist/main"]
```

Build & run:

```bash
docker build -t nest-app .
docker run -p 3000:3000 nest-app
```

---

## Useful Production Tips

- Set `NODE_ENV=production`
- Use `.env` for secrets and disable auto schema sync
- Add HTTPS and CORS if needed
- Use `helmet`, rate-limiting, and security guards
- Monitor with services like Sentry, Datadog, or LogRocket

---

## Summary

- Build your app with `npm run build` and serve with `node dist/main.js`
- Store secrets in `.env` and load them with `@nestjs/config`
- Deploy to Heroku, Render, Docker, or any cloud service with Node.js support
- Optimize with security, validation, and observability in production

> 🎉 Congrats! You’ve completed the Practical Guide to NestJS.

</div>
