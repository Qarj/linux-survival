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

## Run tests in parallel and disable colours and much verbose output

package.json script

```json
    "test:int": "cross-env CI=true npm-run-all --parallel test:suite1 test:suite2; tar -czvf test_logs.tar.gz ./logs",
```

## Set report file names and reporters for unit tests

jest.config.js

```js
module.exports = {
    testEnvironment: 'jsdom',
    moduleNameMapper: { '^uuid$': 'uuid' }, // Force module uuid to resolve with the CJS entry point, because Jest does not support package.json.exports. See https://github.com/uuidjs/uuid/issues/451
    moduleDirectories: ['node_modules', 'src'],
    moduleFileExtensions: ['ts', 'tsx', 'js'],
    setupFilesAfterEnv: ['<rootDir>/setupTests.ts'],
    reporters: [
        'default',
        [
            'jest-junit',
            {
                outputDirectory: './test-reports',
                outputName: 'unit-test-report.xml',
            },
        ],
        [
            'jest-html-reporters',
            {
                publicPath: './test-reports',
                filename: 'unit-test-report.html',
                openReport: true,
            },
        ],
    ],
    testRegex: '__tests__/.*\\.spec\\.(ts|tsx|js)$',
    transform: {
        '^.+\\.(ts|tsx)$': 'ts-jest',
    },
    snapshotSerializers: ['@emotion/jest/serializer'],
    coveragePathIgnorePatterns: ['node_modules', 'src/config', 'src(/.*)?/(types|enums)', 'integration'],
    coverageDirectory: './coverage/',
    collectCoverageFrom: ['src/**/*.{ts,tsx}'],
    coverageThreshold: {
        global: {
            branches: 30,
            functions: 30,
            lines: 30,
            statements: 30,
        },
    },
    testPathIgnorePatterns: ['.*/__tests__/integration', 'node_modules'],
    testTimeout: 15000,
};
```

## Set report file names for integration tests with parallel workers

jest.config.int.js

```js
const baseJestConfig = require('./jest.config');

module.exports = () => {
    let suite = process.env.SUITE;

    if (suite === undefined) {
        suite = 'no_suite_specified';
    }

    const reportName = `${suite}_${sdk}`;

    return {
        ...baseJestConfig,
        reporters: [
            'default',
            [
                'jest-junit',
                {
                    outputDirectory: './test-reports',
                    outputName: `${reportName}.xml`,
                },
            ],
            [
                'jest-html-reporters',
                {
                    publicPath: './test-reports',
                    filename: `${reportName}.html`,
                    openReport: false,
                    inlineSource: true,
                },
            ],
        ],
        setupFilesAfterEnv: ['<rootDir>/jest.setup.tsx'],
        testEnvironment: 'node',
        testRegex: '__tests__/.*\\.int\\.(ts|tsx|js)$',
        transformIgnorePatterns: ['\\.pnp\\.[^\\/]+$'],
        testPathIgnorePatterns: ['node_modules'],
        testTimeout: 320000,
        maxWorkers: 5,
    };
};
```

## Example of a setupTests.ts

```ts
import '@testing-library/jest-dom'; // custom jest matchers like expect(...).toBeVisible()
import { cleanup } from '@testing-library/react';
import 'web-streams-polyfill/es2018';
afterEach(cleanup);
```
