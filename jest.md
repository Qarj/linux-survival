# Jest

## Set to Jest 26

```sh
npm i -D jest@26 ts-jest@26
npm i -D @types/jest@26
```

## Run tests in a specific folder

```sh
npm run test -- --testRegex "src/__tests__/*.ts"
```

## TextDecoder is not defined

Put at top of test file

```ts
import { TextEncoder, TextDecoder } from 'util';
Object.assign(global, { TextDecoder, TextEncoder });
```

In theory it should work in jest.setup.tsx but it didn't for me.
