# NestJs provider

Providers are important in NestJs, because they are used to created relations between components.
They can also be injected as dependency.

## @Injectable

Any services, repos, helpers, etc can be treated as providers by adding `@Injectable` decoration.

```typescript
@Injectable()
export class MyService {
}
```

Under the hook, NestJs will attach metadata to the class and mark it as managed by the IoC container.
Once an instance of the class is created, based on the metadata, the instance will be configured.
With the metadata, the given class is now the **provider** to its instances. 
The provider can be registered on module level.

## Custom provider

Instead of using `@Injectable`, metadata can be passed directly. This can be helpful in various senerios.

```typescript
@Module({
  providers: [
    {
        provide: ConfigService,
        useClass:
            process.env.NODE_ENV === 'development'
            ? DevelopmentConfigService
            : ProductionConfigService
    }, {
        provide: 'foobar',
        useFactory: (dependency1, dependency2) => {...},
        inject: [dependency1, dependency2]
    }
  ]
})
export class AppModule {}
```

When declare a custom provider, it required:

- Provider key field - `provider`
    Can be any type, however, usually class or constant would be used.
- Value field.
    Can be `useClass`, `useValue`, `useExisting` or `useFactory`
