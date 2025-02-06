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

const protectClient = await protect();
```

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