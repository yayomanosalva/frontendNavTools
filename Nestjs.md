# Nestjs CLI

==================== ---	Install new project & structure	--- ====================

- npm i -g @nestjs/cli
- nest new project-name
- cd project-name
- npm run start:dev

==================== ---	Configurando  Debugger  	--- ====================

crear carpeta .vscode y dentro archivo launch.json

##### launch.json

```json
{
  "version": "0.2.0",
  "configurations": [
    {
      "type": "node",
      "request": "launch",
      "name": "Debug Nest Framework",
      "args": ["${workspaceFolder}/src/main.ts"],
      "runtimeArgs": ["--nolazy", "-r", "ts-node/register"],
      "autoAttachChildProcesses": true,
      "sourceMaps": true,
      "cwd": "${workspaceRoot}",
      "protocol": "inspector"
    }
  ]
}
```



==================== ---	Módulo de configuración  	--- ====================

// injectar variables de entorno

```bash
npm i -D dotenv @types/dotenv
```

// create file .env –> no versionable –> add .gitignore 
PORT=5000

==================== --- Creando Módulo

```bash
nest g module config
nest g mo database
nest g mo modules/user	--> modules(folder) entidades principales
```

// src/config create file config.service.ts

##### config.service.ts

```ts
import * as fs from 'fs';
import { parse } from 'dotenv';

export class ConfigService {
  private readonly envConfig: { [key: string]: string };
  constructor() {
    const isDevelopmentEnv = process.env.NODE_ENV !== 'production';

    if (isDevelopmentEnv) {
      const envFilePath = __dirname + '/../../.env';
      const existsPath = fs.existsSync(envFilePath);

      if (!existsPath) {
        console.log('.env file does not exist');
        process.exit(0);
      }

      this.envConfig = parse(fs.readFileSync(envFilePath));
    } else {
      this.envConfig = {
        PORT: process.env.NODE_ENV,
      };
    }
  }

  get(key: string): string {
    return this.envConfig[key];
  }
}
```

##### config.module.ts				🡣🡣🡣🡣🡣🡣🡣🡣

```tsx
import { Module } from '@nestjs/common';
import { ConfigService } from './config.service';

@Module({
  providers: [
    {
      provide: ConfigService,
      useValue: new ConfigService(),
    },
  ],
  exports: [ConfigService],
})
export class ConfigModule {}

```

##### app.moduke.ts    			🡣🡣🡣🡣🡣🡣🡣🡣

```ts
import { Module } from '@nestjs/common';
import { AppController } from './app.controller';
import { AppService } from './app.service';
import { ConfigModule } from './config/config.module';
import { ConfigService } from './config/config.service';
import { Configuration } from './config/config.keys';
import { DatabaseModule } from './database/database.module';
import { UserModule } from './modules/user/user.module';
import { RoleModule } from './modules/role/role.module';

@Module({
  imports: [ConfigModule, DatabaseModule, UserModule, RoleModule],
  controllers: [AppController],
  providers: [AppService],
})
export class AppModule {
  static port: number | string;

  constructor(private readonly _ConfigService: ConfigService) {
    AppModule.port = this._ConfigService.get(Configuration.PORT);
  }
}
```

src/config/config.key.ts

##### config.key.ts

```ts
export enum Configuration {
  PORT = 'PORT',
  HOST = 'HOST',
  USERNAME = 'USERNAME',
  PASSWORD = 'PASSWORD',
  DATABASE = 'DATABASE',
}
```

configurar prefijo en main.ts

```ts
import { NestFactory } from '@nestjs/core';
import { AppModule } from './app.module';

async function bootstrap() {
  const app = await NestFactory.create(AppModule);
  app.setGlobalPrefix('api');
  //  /api/endpointName

    //importamos el puerto
  await app.listen(AppModule.port);
}
bootstrap();
```



==================== ---	Configurando  Base de Datos  - migraciones 	--- ====================

instalar docker y trabajaremos con postgres

```bash
docker run -d -p 5444:5432 --name my-postgres -e POSTGRES_PASSWORD postgres
```

```bash
docker run -p 5431:5432 --name NEST-POSTGRES -e POSTGRES_PASSWORD=123456 -d postgres
```

##### .env  –> no versionable –> add .gitignore 

```makefile
PORT=5000
HOST=localhost
USERNAME=postgres
PASSWORD=123456
DATABASE=bookstore
```

inyectamos dependencias.

```bash
npm i @nestjs/typeorm typeorm pg
```

create module database

```bash
nest g mo database
```

create file  src/database/database.service.ts

##### database.service.ts

```ts
import { TypeOrmModule } from '@nestjs/typeorm';
import { ConfigModule } from '../config/config.module';
import { ConfigService } from '../config/config.service';
import { ConnectionOptions } from 'typeorm';
import { Configuration } from '../config/config.keys';

export const databaseProviders = [
  TypeOrmModule.forRootAsync({
    imports: [ConfigModule],
    inject: [ConfigService],
    async useFactory(config: ConfigService) {
      return {
        ssl: true,
        type: 'postgres' as 'postgres',
        host: config.get(Configuration.HOST),
        username: config.get(Configuration.USERNAME),
        password: config.get(Configuration.PASSWORD),
        entities: [__dirname + '/../**/*.entity{.ts,.js}'],
        migrations: [__dirname + '/migrations/*{.ts,.js}'],
      } as ConnectionOptions;
    },
  }),
];
```

##### config.key.ts

```ts
export enum Configuration {
  PORT = 'PORT',
  HOST = 'HOST',
  USERNAME = 'USERNAME',
  PASSWORD = 'PASSWORD',
  DATABASE = 'DATABASE',
}
```

database.module.ts

```ts
import { Module } from '@nestjs/common';
import { databaseProviders } from './database.service';

@Module({
  imports: [...databaseProviders],
  exports: [...databaseProviders],
})
export class DatabaseModule {}
```



==================== ---	Creando entidad usuarios 	--- ====================

```bash
nest g mo modules/user
```

create file src/modules/user/user.entity.ts

##### user.entity.ts

```ts
import {
  BaseEntity,
  Entity,
  PrimaryGeneratedColumn,
  Column,
  OneToOne,
  JoinColumn,
  ManyToMany,
  JoinTable,
} from 'typeorm';
import { UserDatils } from './user.details.entity';
import { Role } from '../role/role.entity';

@Entity('users')
export class User extends BaseEntity {
  @PrimaryGeneratedColumn('increment')
  id: number;

  @Column({ type: 'varchar', unique: true, length: 45, nullable: false })
  username: string;

  @Column({ type: 'varchar', nullable: false })
  email: string;

  @Column({ type: 'varchar', nullable: false })
  password: string;

  @OneToOne(type => UserDatils, { cascade: true, nullable: false, eager: true })
  details: UserDatils;
  @JoinColumn({ name: 'detail_id' })
  @ManyToMany(
    type => Role,
    role => role.users,
  )
  @JoinTable({ name: 'user_roles' })
  roles: Role[];

  @Column({ type: 'varchar', default: 'ACTIVE', length: 8 })
  status: string;

  @Column({ type: 'timestamp', name: 'created_at' })
  createdAt: Date;

  @Column({ type: 'timestamp', name: 'updated_at' })
  updatedAt: Date;
}
```

create file repositorio  src/modules/user/user.repository.ts

##### user.repository.ts

```ts
import { Repository, EntityRepository } from 'typeorm';
import { User } from './user.entity';

@EntityRepository(User)
export class UserRepository extends Repository<User> {}
```

##### user.module.ts

```ts
import { Module } from '@nestjs/common';
import { TypeOrmModule } from '@nestjs/typeorm';
import { UserRepository } from './user.repository';
import { UserService } from './user.service';
import { SharedModule } from 'src/shared/shared.module';

@Module({
  imports: [TypeOrmModule.forFeature([UserRepository]), SharedModule],
  providers: [UserService],
})
export class UserModule {}
```

