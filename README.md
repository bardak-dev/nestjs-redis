## Description

NestJs 的 redis 模块，使用 ioredis

## Basic usage

```typescript
import { Module } from '@nestjs/common';
import { RedisModule } from './redis.module';

@Module({
  imports: [RedisModule.forRoot({
    host: '127.0.0.1',
    port: 6379,
    password: '123456',
  })]
})
export class AppModule {
  
}
```

## Connection Decorators

```typescript
import { Module } from '@nestjs/common';
import { RedisModule } from './redis.module';

@Module({
  imports: [RedisModule.forRoot([
    {
      host: '127.0.0.1',
      port: 6379,
      password: '123456',
    },
    {
      name: 'test',
      host: '127.0.0.1',
      port: 6379,
      password: '123456',
     }
  ])]
})
export class AppModule {
  
}
```

```typescript
import {Injectable, Module } from '@nestjs/common';
import { InjectRedisClient } from './index';

@Injectable()
export class TestService {
  constructor(
    @InjectRedisClient('test') private redisClient: Redis.Redis,
    @InjectRedisClient('0') private redisClient0: Redis.Redis,
  ) {}
  
  getClient() {
    return this.redisClient;
  }
  
  getClient0() {
    return this.redisClient0;
  }
}
```
