<!-- 此文件从 content/microservices/guards.md 自动生成，请勿直接修改此文件 -->
<!-- 生成时间: 2026-09-24T07:16:08.329Z -->
<!-- 源文件: content/microservices/guards.md -->

### Guards

Microservice guards work the same way as [regular HTTP application guards](/guards). The only difference is that they should throw `RpcException` instead of `HttpException`. When a guard returns `false`, Nest throws an `RpcException` with the `Forbidden resource` message.

> info **Hint** The `RpcException` class is exposed from the `@nestjs/microservices` package.

#### Binding guards

The following example uses a method-scoped guard. As with HTTP-based applications, you can also use controller-scoped guards (i.e., prefix the controller class with a `@UseGuards()` decorator).

```typescript
@UseGuards(AuthGuard)
@MessagePattern({ cmd: 'sum' })
accumulate(data: number[]): number {
  return (data || []).reduce((a, b) => a + b);
}

```

> info **Hint** Global guards registered on the main HTTP application don't apply to microservices connected to a [hybrid application](/faq/hybrid-application) unless you set the `inheritAppConfig` option. See [sharing configuration](/faq/hybrid-application#sharing-configuration).
