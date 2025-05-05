---
title: Authentication with Passport and JWT
menu_order: 9
post_status: publish
post_excerpt: Learn how to secure your NestJS app using Passport strategies and JWT tokens for authentication and protected routes.
taxonomy:
  category:
    - nestjs
    - Advanced Guide to NestJS
  post_tag:
    - nestjs
    - passport
    - jwt
    - authentication
    - guards
    - login
---

<div class="toc" markdown="1">

## On this Page

- [Why Use Passport and JWT?](#why-use-passport-and-jwt)
- [Installing Required Packages](#installing-required-packages)
- [Setting Up AuthModule](#setting-up-authmodule)
- [Creating JWT Strategy and Guard](#creating-jwt-strategy-and-guard)
- [Login Endpoint and Token Generation](#login-endpoint-and-token-generation)
- [Protecting Routes with AuthGuard](#protecting-routes-with-authguard)
- [Summary](#summary)

</div>

<div class="guru-main" markdown="1">

## Why Use Passport and JWT?

Passport is the most widely used authentication library in the Node.js ecosystem.

- NestJS offers tight integration with Passport
- JWT is a stateless, scalable way to authenticate users via access tokens
- Combine both to protect routes and implement login securely

---

## Installing Required Packages

Install Passport and JWT dependencies:

```bash
npm install @nestjs/passport passport passport-jwt
npm install @nestjs/jwt jsonwebtoken
```

---

## Setting Up AuthModule

Create the Auth module and service:

```bash
nest g module auth
nest g service auth
nest g controller auth
```

Import `JwtModule`:

```ts
import { JwtModule } from '@nestjs/jwt';

@Module({
  imports: [
    JwtModule.register({
      secret: process.env.JWT_SECRET || 'supersecret',
      signOptions: { expiresIn: '1h' },
    }),
  ],
  providers: [AuthService],
  exports: [AuthService],
})
export class AuthModule {}
```

---

## Creating JWT Strategy and Guard

Create a strategy:

```ts
@Injectable()
export class JwtStrategy extends PassportStrategy(Strategy) {
  constructor() {
    super({
      jwtFromRequest: ExtractJwt.fromAuthHeaderAsBearerToken(),
      secretOrKey: process.env.JWT_SECRET || 'supersecret',
    });
  }

  async validate(payload: any) {
    return { userId: payload.sub, email: payload.email };
  }
}
```

And an auth guard:

```ts
@Injectable()
export class JwtAuthGuard extends AuthGuard('jwt') {}
```

Register them in `AuthModule` providers.

---

## Login Endpoint and Token Generation

In your `AuthService`:

```ts
@Injectable()
export class AuthService {
  constructor(private jwtService: JwtService) {}

  async login(user: any) {
    const payload = { email: user.email, sub: user.id };
    return {
      access_token: this.jwtService.sign(payload),
    };
  }
}
```

And controller:

```ts
@Post('login')
async login(@Body() loginDto: LoginDto) {
  const user = await this.usersService.validateUser(loginDto);
  return this.authService.login(user);
}
```

---

## Protecting Routes with AuthGuard

Use the guard to protect any route:

```ts
@UseGuards(JwtAuthGuard)
@Get('me')
getProfile(@Request() req) {
  return req.user;
}
```

Nest will automatically:
- Check the bearer token
- Validate it using the strategy
- Inject the payload into `req.user`

---

## Summary

- Passport + JWT is a powerful combo for NestJS auth
- Use `@nestjs/passport` and `@nestjs/jwt` for smooth integration
- Secure routes with guards, and use strategies to extract and verify tokens
- This pattern works for any API needing sessionless user authentication

> Next: **Lesson 10 – Testing in NestJS**

</div>
