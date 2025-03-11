# jseql

The `jseql` repo has been moved and rebranded to [protectjs](https://github.com/cipherstash/protectjs).

## Migrating to protectjs

The move to protectjs has been released as a major version bump as of [v5.0.0](https://github.com/cipherstash/protectjs/releases/tag/%40cipherstash%2Fprotect%405.0.0).

### Migrating from jseql to protectjs

Installing the new package is as simple as:

```bash
npm install @cipherstash/protect
# or
yarn add @cipherstash/protect
# or
pnpm add @cipherstash/protect
```

Then remove the `@cipherstash/jseql` package from your project.

#### Defining your schema

In an effort to be more declarative and type safe, the Protect.js client now requires a schema definition to be passed in when initializing the client.

Read more about defining your schema here: [Defining your schemas](https://github.com/cipherstash/protectjs/blob/main/docs/reference/schema.md).

The basic schema you will need when migrating from `jseql` to `protect` is:

**schema.ts**

```ts
import { csTable, csColumn } from "@cipherstash/protect";

export const tableNameInTypeScript = csTable("tableNameInDatabase", {
  columnNameInTypeScript: csColumn("columnNameInDatabase"),
});
```

#### Initializing the client

Initializing the `jseqlClient` is now done with the `protect` function:

Before:

```ts
import { eql } from '@cipherstash/jseql';

const jseqlClient = await eql();
```

After:

```ts
import { protect } from '@cipherstash/protect';
import { tableNameInTypeScript } from './schema';

// takes N number of csTables
const protectClient = await protect(tableNameInTypeScript, ...);
```

#### Crypto functions and returned values

The `encrypt` and `bulkEncrypt` functions have been updated to use the schemas to determine the columns and tables rather than defining these values as `strings`. 

All `encrypt`, `decrypt`, `bulkEncrypt` and `bulkDecrypt` functions now return a `Result` object with either a failure state or a data object for better error handling and more descriptive failure messages.

**Encrypt example**

Before:

```ts
const encryptedValue = await jseqlClient.encrypt(plaintext, {
  table: 'tableNameInDatabase',
  column: 'columnNameInDatabase',
});

// returned value is the encrypted value 
```

After:

```ts
const encryptedResult = await protectClient.encrypt(plaintext, {
  table: tableNameInTypeScript,
  column: tableNameInTypeScript.columnNameInTypeScript,
});

// returned a Result object with either a failure state of a data object
if (encryptedResult.failure) {
  // handle failure
}

// encrypted value is now in the data property
const encryptedValue = encryptedResult.data
```

Read more [here](https://github.com/cipherstash/protectjs/tree/main?tab=readme-ov-file#encrypting-data).

### @cipherstash/nextjs changes

The `@cipherstash/nextjs` package has been updated to use the new `protect` branding as of [v2.0.0](https://github.com/cipherstash/protectjs/releases/tag/%40cipherstash%2Fnextjs%402.0.0).

Before:

```ts
import { jseqlMiddleware } from '@cipherstash/nextjs'; 
import { jseqlClerkMiddleware } from '@cipherstash/nextjs/clerk';
```

After:

```ts
import { protectMiddleware } from '@cipherstash/nextjs';
import { protectClerkMiddleware } from '@cipherstash/nextjs/clerk';
```