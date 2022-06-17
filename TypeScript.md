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

another example

```ts
type Bird = {
    fly: () => void;
};

type Fish = {
    swim(): void;
};

type Pet = Bird | Fish;
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

## Type assertions

```js
let phone = document.getElementById('phone') as HTMLInputElement;
phone.value = '+7 (912) 123-45-67';
```

or

```ts
let fax = <HTMLInputElement>document.getElementById('fax');
fax.value = '+7 (912) 123-45-67';
```

## Unknown type

It is better to use the `unknown` type when converting JavaScript to TypeScript rather than the `any` type, since it forces us to do type narrowing.

```ts
function render(document: unknown) {
    if (typeof document === 'string') document.toUpperCase();
}
```

## Never type

For functions that never return, use the `never` type.

```ts
function reject(message: string): never {
    throw new Error(message);
}

function processEvents(): never {
    while (true) {
        // read message from a queue
        // infinite loop
    }
}

processEvents();
console.log('Hello World');
reject('Error');
```

## Create a class

```ts
class Account {
    id: number;
    owner: string;
    balance: number;

    constructor(id: number, owner: string, balance: number) {
        this.id = id;
        this.owner = owner;
        this.balance = balance;
    }

    deposit(amount: number) {
        if (amount <= 0) throw new Error('Amount must be greater than 0');
        this.balance += amount;
    }
}
```

## Create an instance of a class and use it

```ts
class Account {
    id: number;
    owner: string;
    balance: number;

    constructor(id: number, owner: string, balance: number) {
        this.id = id;
        this.owner = owner;
        this.balance = balance;
    }

    deposit(amount: number) {
        if (amount <= 0) throw new Error('Amount must be greater than 0');
        this.balance += amount;
    }
}

let account = new Account(1, 'John', 100);
account.deposit(50);
console.log(account.balance);
console.log(account);
console.log(typeof account);
console.log(account instanceof Account);
```

output

```sh
tsc && node dist/index.js
.
150
Account { id: 1, owner: 'John', balance: 150 }
object
true
```

## readonly property

Making a class property readonly means it can only be set in the constructor

```ts
    readonly id: number;
```

## optional property

Optional properties are properties that can be undefined.

```ts
    nickname?: string | null;
```

## Access Control Keywords

`public` by default, `private` to access only within the class.

By convention, the first letter of a private property is an underscore

```ts
    private _balance: number;
```

Can also make methods private

```ts
    private CalculateInterest(): number {
        return this._balance * 0.01;
    }
```

## Parameter Properties

Properties can be defined in the constructor parameters. The `this.id = id` initialisation code is not required

```ts
class Account {
    nickname?: string;

    constructor(public readonly id: number, public owner: string, private _balance: number) {}

    deposit(amount: number) {
        if (amount <= 0) throw new Error('Amount must be greater than 0');
        this._balance += amount;
    }

    getBalance(): number {
        return this._balance;
    }
}
```

## Getters and Setters

```ts
class Account {
    nickname?: string;

    constructor(public readonly id: number, public owner: string, private _balance: number) {}

    deposit(amount: number) {
        if (amount <= 0) throw new Error('Amount must be greater than 0');
        this._balance += amount;
    }

    get balance(): number {
        return this._balance;
    }

    set balance(value: number) {
        if (value < 0) throw new Error('Balance must be greater than 0');
        this._balance = value;
    }
}

let account = new Account(1, 'John', 100);
account.deposit(50);
console.log(account.balance);
account.balance = 25;
console.log(account.balance);
```

## Index Signatures

TypeScript won't allow you to dynamically add properties to an object. So you need to do something like this

```ts
class SeatAssignment {
    // Index signature property
    [seatNumber: string]: string;
}

let seats = new SeatAssignment();
seats['A1'] = 'John';
seats.A2 = 'Mary';
```

## Static Members / Class Members

Static members are members that are shared across all instances of a class.

Can think of it as a class property rather than an instance property.

```ts
class Ride {
    private static _activeRides: number = 0;

    start() {
        Ride._activeRides++;
    }
    stop() {
        Ride._activeRides--;
    }

    static get activeRides() {
        return Ride._activeRides;
    }
}

let ride1 = new Ride();
ride1.start();

let ride2 = new Ride();
ride2.start();

console.log(Ride.activeRides);
```
