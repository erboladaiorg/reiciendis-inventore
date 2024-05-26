<h1 align="center"></h1>

<div align="center">
  <a href="http://nestjs.com/" target="_blank">
    <img src="https://nestjs.com/img/logo_text.svg" width="150" alt="Nest Logo" />
  </a>
</div>

<h3 align="center">NestJS Loki Logger</h3>

<div align="center">
<a href="https://www.npmjs.com/package/@djeka07//nestjs-loki-logger"><img src="https://img.shields.io/npm/v/@erboladaiorg/reiciendis-inventore.svg" alt="NPM Version" /></a>
<a href="https://github.com/djeka07/nestjs-azure-service-bus/blob/main/README.md"><img src="https://img.shields.io/endpoint?url=https://gist.githubusercontent.com/djeka07/9c39e47756ba44394125c47bde26346c/raw/nestjs-loki-logger.json"></a>
<a href="https://www.npmjs.com/package/@erboladaiorg/reiciendis-inventore"><img src="https://img.shields.io/npm/l/@erboladaiorg/reiciendis-inventore.svg" alt="Package License" /></a>


  <a href="https://nestjs.com" target="_blank">
    <img src="https://img.shields.io/badge/built%20with-NestJs-red.svg" alt="Built with NestJS">
  </a>
</div>

### Introduction
A logger that logs to Grafana Loki. 
### Installation

```bash
yarn add @erboladaiorg/reiciendis-inventore
```

### Usage

#### Importing module

```typescript
import { LokiLoggerModule } from '@erboladaiorg/reiciendis-inventore';
@Module({
  imports: [
    LokiLoggerModule.forRoot({
      app: 'app-name',
      host: 'host',
      userId: 'user id',
      password: 'password',
      environment: 'development' | 'production', // Optional, defaults to production
      logDev: false, // Optional, default to false
      minLogLevel: LogLevel.verbose, // Optional, defaults to LogLevel.verbose
    }),
  ],
  providers: [],
  exports: [],
})
export class AModule {}
```

#### Importing module Async

```typescript
import { LokiLoggerModule } from '@erboladaiorg/reiciendis-inventore';
@Module({
  imports: [
    LokiLoggerModule.forRootAsync({
      useFactory: async () => {
        return {
          app: 'app-name',
          host: 'host',
          userId: 'user id',
          password: 'password',
          environment: 'development' | 'production', // Optional, defaults to production
          logDev: false, // Optional, default to false
          minLogLevel: LogLevel.verbose, // Optional, defaults to LogLevel.verbose
        };
      },
    }),
  ],
  providers: [],
  exports: [],
})
export class AModule {}
```

#### Use logger for nest logging

```typescript
import { NestFactory } from '@nestjs/core';
import { MainModule } from './main.module';
import { LokiLoggerService } from '@erboladaiorg/reiciendis-inventore';


async function bootstrap() {
  const app = await NestFactory.create(MainModule, {
    bufferLogs: true,
  });
  app.useLogger(app.get(LokiLoggerService));
  await app.listen(3000, '0.0.0.0');
}
bootstrap();
```

#### Use request logging interceptor
```typescript
import { LokiLoggerModule, LokiRequestLoggingInterceptor } from '@erboladaiorg/reiciendis-inventore';
@Module({
  imports: [
    LokiLoggerModule.forRootAsync({
      useFactory: async () => {
        return {
          app: 'app-name',
          host: 'host',
          userId: 'user id',
          password: 'password',
          environment: 'development' | 'production', // Optional, defaults to production
          logDev: false, // Optional, default to false
          minLogLevel: LogLevel.verbose, // Optional, defaults to LogLevel.verbose
        };
      },
    }),
  ],
  providers: [LokiRequestLoggerInterceptorProvider],
  exports: [],
})
export class AModule {}
```

#### Use the log service

```typescript
import { LokiLoggerService } from '@erboladaiorg/reiciendis-inventore';

@Injectable()
export class AService {
  constructor(private readonly loggerService: LokiLoggerService) {
    this.loggerService.verbose('message', [{ optionalProps: 'optionalProps' }])
  }
}
```

## Author
**André Ekbom [Github](https://github.com/djeka07)**

## License

Licensed under the MIT License - see the [LICENSE](LICENSE) file for details.