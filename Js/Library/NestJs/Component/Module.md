# NestJs Module

## Instroduction

Modules allows us to group services, controllers, etc, usually of a functionality, for better code organization.
For example we can have modules for logging, for data access or for caching. 
A module can expose its services and can depend on other modules.

Each NestJs project must have at least 1 module. 
It's known as the root module, which is used as the the starting point to resolve the structure and relationship of the application.

## Declaration

A module in NestJs is a class with the decorator `@Module`, with parameters:

* providers: which services to be initialized in this module
* exports: which services/modules to expose to other modules
* imports: which modules to import to this module
* controllers: which controllers defined in this module 

```typescript
import { Module } from '@nestjs/common';
import { AbcService } from './Abc.service';

@Module({
  imports: [],
  controllers: [],
  providers: [AbcService],
  exports: [AbcService],
})
export class AbcModule {
}
```

## Dynamic module

Dynamic module is a powerfull feature in NestJs, which allows us to create customizable modules.
They are created using static methods that return `DynamicModule`, noted that the configured parameters is removed from the class.

```typescript
import { DynamicModule, Module } from '@nestjs/common';
import { DefService } from './Def.service';
import { Config } from './config';
import { CONFIG_OPTIONS } from './consts'

@Module({})
export class DefModule {
  static forRoot(config: Config): DynamicModule {
    return {
      module: DefModule,
      providers: [
        {
          provide: CONFIG_OPTIONS,
          useValue: config
        },
        DefService
      ],
      exports: [Defervice],
    };
  }
}

@Injectable()
export class DefService {
  constructor(@Inject(CONFIG_OPTIONS) private readonly config: Config) {
    // initialize service using the given config
  }
}
```

## Using modules

To use a module, just import it in the wanted module.

```typescript
import { AbcModule } from 'abc-module'

@Module({
  imports: [
    AbcModule,
    DefModule.forRoot({config1: "configvalue1"})
  ]
})
export class AppModule {
}
```

## Global module

If a module is required in multiple places, for example, a cache module is required for feature 1,2 and 3 modules,
it would be required to be imported multiple time in each feature module.

This is because providers in each module is encapsulated inside module scope.
We can change that by declaring global scope modules, after that the module only need to be declared once in the root module.
Doing so via:

- `@Global` decoration
- global property when create module -> can have conditional global scope
