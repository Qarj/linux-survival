# TypeScript

```sh
npm install -g typescript
tsc -v
.
Version 4.7.3
```

```sh
tsc index.ts
```

```sh
tsc --init
.
Created a new tsconfig.json with:
                                                                                                                     TS
  target: es2016
  module: commonjs
  strict: true
  esModuleInterop: true
  skipLibCheck: true
  forceConsistentCasingInFileNames: true


You can learn more at https://aka.ms/tsconfig
```

In tsconfig.json, you can remove target and hit `CTRL+SPACE` to see the available options

```sh
    "target": "ES2016",
```

Suggested config

```json
{
    "compilerOptions": {
        "target": "ES2016",
        "module": "commonjs",
        "rootDir": "./src",
        "outDir": "./dist",
        "removeComments": true,
        "noEmitOnError": true,
        "esModuleInterop": true,
        "forceConsistentCasingInFileNames": true,
        "strict": true,
        "skipLibCheck": true
    }
}
```

Once setup, it is possible to compile the code with just `tsc`.

## Debugger

Set debug points.

Click Run and Debug icon on LHS.

Create a launch.json file selecting node.js as the runtime.

Add a preLaunchTask as follows

```json
{
    // Use IntelliSense to learn about possible attributes.
    // Hover to view descriptions of existing attributes.
    // For more information, visit: https://go.microsoft.com/fwlink/?linkid=830387
    "version": "0.2.0",
    "configurations": [
        {
            "type": "pwa-node",
            "request": "launch",
            "name": "Launch Program",
            "skipFiles": ["<node_internals>/**"],
            "program": "${workspaceFolder}/src/index.ts",
            "preLaunchTask": "tsc: build - tsconfig.json",
            "outFiles": ["${workspaceFolder}/**/*.js"]
        }
    ]
}
```

Press `Launch Program` or `F5` to start debugging.

## Types

JavaScript

-   number
-   string
-   boolean
-   null
-   undefined
-   object

TypeScript

-   any
-   unknown
-   never
-   enum
-   tuple

```ts
let sales: number = 123_456_789;
let course: string = 'TypeScript';
let is_published: boolean = true;
```

TypeScript can infer the type of a variable

```ts
let sales = 123_456_789;
let course = 'TypeScript';
let is_published = true;
let someVar;
```

`someVar` is of type `any`

Can set TypeScript config option to false to infer types, not recommended

```json
"noImplicitAny": false /* Enable error reporting for expressions and declarations with an implied 'any' type. */,
```

then this will be possible

```ts
function render(document) {
    console.log(document);
}
```

tuple - array of fixed number of elements

```ts
let tuple: [number, string] = [1, 'hello'];
```

enum - enumeration

```ts
enum Size {
    Small = 1,
    Medium,
    Large,
} // PascalCase
let mySize = Size.Medium;
console.log(mySize);
```

If you assign to a constant, compiler will generate more optimised code

```ts
const enum Size {
    Small = 1,
    Medium,
    Large,
} // PascalCase
let mySize = Size.Medium;
console.log(mySize);
```

## Functions

```ts
function calculateTax(income: number, taxYear = 2022): number {
    if (taxYear < 2022) return income * 0.25;
    return income * 0.4;
}

calculateTax(100000);
```

3 suggested compiler options to enable

```json
"noUnusedLocals": true /* Enable error reporting when local variables aren't read. */,
"noUnusedParameters": true /* Raise an error when a function parameter isn't read. */,
// "exactOptionalPropertyTypes": true,               /* Interpret optional property types as written, rather than adding 'undefined'. */
"noImplicitReturns": true /* Enable error reporting for codepaths that do not explicitly return in a function. */,
```

## Objects

```ts
let employee: {
    readonly id: number;
    name: string;
    faxNumber?: string | null;
    retire: (date: Date) => void;
} = {
    id: 1,
    name: 'Max',
    retire: (date: Date) => {
        console.log(date);
    },
};
employee.name = 'Maximilian';
console.log(employee);
```

## Using a type alias

```ts
type Employee = {
    readonly id: number;
    name: string;
    faxNumber?: string | null;
    retire: (date: Date) => void;
};

let employee: Employee = {
    id: 1,
    name: 'Max',
    retire: (date: Date) => {
        console.log(date);
    },
};
```

## Union types

```ts
function kgToLbs(weight: number | string): number {
    if (typeof weight === 'number') return weight * 2.2046226218;
    return parseFloat(weight) * 2.2046226218;
}

console.log(kgToLbs(70));
console.log(kgToLbs('70kg'));
```

output

```txt
154.323583526
154.323583526
```

## Intersection types

```ts
type Draggable = {
    drag: () => void;
};

type Resizeable = {
    resize: () => void;
};

type UIWidget = Draggable & Resizeable;

let textBox: UIWidget = {
    drag: () => {},
    resize: () => {},
};
```

## Literal types

```ts
let quantity: 50 | 100 = 50;
quantity = 100;
```

or

```ts
type Amount = 50 | 100;
let amount: Amount = 50;
```

## Nullable Types

```ts
function greet(name: string | null) {
    if (name) console.log(name.toUpperCase());
    else console.log('Hola!');
}

greet(null);
```

## Optional chaining

```ts
type Customer = {
    birthday?: Date;
};

function getCustomer(id: number): Customer | null | undefined {
    return id === 0 ? null : { birthday: new Date() };
}

let customer = getCustomer(0);
console.log(customer?.birthday?.getFullYear());

let log: any = null;
log?.('Hello');
```

## Nullish Coalescing Operator (??)

```ts
let speed: number | null = null;
let ride = {
    speed: speed ?? 30,
};
```

Assign speed to 30 if it is null or undefined, but not 0.
