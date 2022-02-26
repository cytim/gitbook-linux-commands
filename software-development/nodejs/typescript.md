# TypeScript

## Setup TypeScript, Eslint, Jest and Prettier

Refer to [here](https://dev.to/ornio/node-js-express-with-typescript-eslint-jest-prettier-and-husky-part-1-1lin).

## Narrowing

A variable can be declared to have multiple types. TypeScript will throw an error if the variable type might not fit an
operation.

```ts
function repeat(n: string | number) {
  return "x".repeat(n);
  // [Error]
  // Argument of type 'string | number' is not assignable to parameter of type 'number'.
}
```

To eliminate the error, we can "narrow" down the type before the operation.

```ts
function repeat(x: string | number) {
  if (typeof n === "number") {
    // TypeScript will understand that `n` is a number.
    return "x".repeat(n);
  }

  // TypeScript will understand that `n` is a string.
  return "x".repeat(Number(n));
}
```

Typescript supports the following narrowing guards:

- Truthiness
- Equality
- `typeof` operator
- `in` operator
- `instanceof` operator

Please refer to [the official documentation](https://www.typescriptlang.org/docs/handbook/2/narrowing.html) for the
details.

## Declaration Merging

> [Official Documentation](https://www.typescriptlang.org/docs/handbook/declaration-merging.html)

Declaration merging is an important technique to add custom fields to the
existing interfaces.

Assume you are working with the HTTP server. If you want to add the logger to
the `req` object as `req.log`, TypeScript will warn you that

> Property 'log' does not exist on type 'IncomingMessage'.

To achieve that, you have to declare your own `IncomingMessage` interface to
merge with the default `http.IncomingMessage` interface.

1.  Declare your custom interface - `./src/types/http/index.d.ts`

    ```typescript
    import { Logger } from "pino";

    declare module "http" {
      interface IncomingMessage {
        log: Logger;
      }
    }
    ```

    The folder path must be `/path/to/<MODULE>/index.d.ts` for [`ts-node` to
    work properly](https://github.com/TypeStrong/ts-node/pull/698).

2.  In `tsconfig.json`, update `compilerOptions.typeRoots` to include the
    custom "types" folder.

    ```javascript
    {
      // ...
      "compilerOptions": {
        // ...
        "typeRoots": ["./node_modules/@types", "./src/types"]
      }
    }
    ```

3.  Done. TypeScript will acknowledge that `req.log` is a `Logger` from now on.
