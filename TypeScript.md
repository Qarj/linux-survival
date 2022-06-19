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

## Inheritance

Can have `Parent / Base / Super` classes and `Child / Derived / Subclass` classes.

Example Person <- Student or Teacher

```ts
class Person {
    constructor(public firstName: string, public lastName: string) {}

    get fullName() {
        return `${this.firstName} ${this.lastName}`;
    }

    walk() {
        console.log(`${this.fullName} is walking`);
    }
}

class Student extends Person {
    constructor(public studentId: number, firstName: string, lastName: string) {
        super(firstName, lastName);
    }

    takeTest() {
        console.log(`${this.fullName} is taking a test`);
    }
}

let student = new Student(1, 'John', 'Doe');
student.walk();
student.takeTest();
```

## Method Overriding

```ts
class Person {
    constructor(public firstName: string, public lastName: string) {}

    get fullName() {
        return `${this.firstName} ${this.lastName}`;
    }

    walk() {
        console.log(`${this.fullName} is walking`);
    }
}

class Teacher extends Person {
    constructor(public teacherId: number, firstName: string, lastName: string) {
        super(firstName, lastName);
    }

    override get fullName() {
        return `Professor ${super.fullName}`;
    }

    teach() {
        console.log(`${this.fullName} is teaching`);
    }
}

let professor = new Teacher(1, 'Richard', 'Dawkins');
professor.teach();
```

## Polymorphism

Can handle multiple types of objects so long as they have the same parent class.

```ts
class Person {
    constructor(public firstName: string, public lastName: string) {}

    get fullName() {
        return `${this.firstName} ${this.lastName}`;
    }

    walk() {
        console.log(`${this.fullName} is walking`);
    }
}

class Student extends Person {
    constructor(public studentId: number, firstName: string, lastName: string) {
        super(firstName, lastName);
    }

    takeTest() {
        console.log(`${this.fullName} is taking a test`);
    }
}

class Teacher extends Person {
    constructor(public teacherId: number, firstName: string, lastName: string) {
        super(firstName, lastName);
    }

    override get fullName() {
        return `Professor ${super.fullName}`;
    }

    teach() {
        console.log(`${this.fullName} is teaching`);
    }
}

class Principal extends Person {
    override get fullName() {
        return `Principal ${super.fullName}`;
    }
}

function printNames(people: Person[]) {
    for (let person of people) {
        console.log(person.fullName);
    }
}

printNames([
    new Student(1, 'John', 'Doe'),
    new Student(2, 'Jane', 'Doe'),
    new Teacher(1000, 'Sean', 'Carroll'),
    new Principal('Sally', 'Smith'),
]);
```

## Protected vs Private Members

Protected members are members that can only be accessed by classes that are a subclass of the class that defines the member.

Use with caution. Cam run into coupling issues.

## Abstract Classes and Methods

Use when it does not make sense to create and instance of the parent class, for example a shape.

```ts
abstract class Shape {
    constructor(public colour: string) {}

    abstract render(): void;
}

class Circle extends Shape {
    constructor(public radius: number, colour: string) {
        super(colour);
    }

    override render(): void {
        console.log(`Render circle`);
    }
}

let circle = new Circle(5, 'red');
circle.render();
```

## Interfaces

Consier an abstract class

```ts
abstract class Calendar {
    constructor(public name: string) {}

    abstract addEvent(): void;
    abstract removeEvent(): void;
}
```

As an interface it looks like this

```ts
interface Calendar {
    name: string;
    addEvent(): void;
    removeEvent(): void;
}
```

Can implement it like an abstract class

```ts
interface Calendar {
    name: string;
    addEvent(): void;
    removeEvent(): void;
}

interface CloudCalendar extends Calendar {
    sync(): void;
}

class GoogleCalender implements Calendar {
    constructor(public name: string) {}
    addEvent(): void {
        throw new Error('Method not implemented.');
    }
    removeEvent(): void {
        throw new Error('Method not implemented.');
    }
}
```

It is also possible to implement a type

```ts
type Person = {
    name: string;
};

class Teacher implements Person {
    constructor(public name: string) {}
}
```

Can use one interface inside another

```ts
interface Address {
    street: string;
    city: string;
    postCode: number;
}

interface Employee {
    name: string;
    salary: number;
    address: Address;
}
```

## Generic Classes

Offer a way to create a class that can be used with multiple types

```ts
class KeyValuePair<T> {
    constructor(public key: T, public value: string) {}
}

let pair1 = new KeyValuePair<string>('hello', 'world');
let pair2 = new KeyValuePair<number>(1, 'world');
let pair3 = new KeyValuePair<boolean>(true, 'world');
```

Compiler can infer the type of the generic class

```ts
let pair4 = new KeyValuePair('hello', 'world');
```

## Generic Functions

```ts
function wrapInArray<T>(value: T) {
    return [value];
}

let numbers = wrapInArray(1);
let strings = wrapInArray('hello');
```

Also works for methods.

## Generic Interfaces

```ts
interface Result<T> {
    data: T | null;
    error: string | null;
}

function fetch<T>(url: string): Result<T> {
    console.log(`Fetching ${url}`);
    return { data: null, error: null };
}

interface User {
    username: string;
}

interface Product {
    title: string;
}

let result = fetch<User>('url');
```

## Generic Constraints

Can constrain the type of a generic parameter

```ts
function echo<T extends number | string>(value: T): T {
    return value;
}

echo('1');
echo(1);
```

Must have a name property

```ts
function echo<T extends { name: string }>(value: T): T {
    return value;
}

echo({ name: 'test', value: 1 });
```

Combine with interface

```ts
interface Person {
    name: string;
}

function echo<T extends Person>(value: T): T {
    return value;
}

echo({ name: 'test', value: 1 });
```

Can use classes

```ts
class Person {
    constructor(public name: string) {}
}

class Customer extends Person {
    constructor(name: string) {
        super(name);
    }
}

function echo<T extends Person>(value: T): T {
    return value;
}

echo({ name: 'test', value: 1 });
echo(new Customer('test'));
echo(new Person('test'));
```

## Extending Generic Classes

```ts
interface Product {
    name: string;
    price: number;
}

class Store<T> {
    protected _objects: T[] = [];

    add(object: T) {
        this._objects.push(object);
    }
}

class CompressibleStore<T> extends Store<T> {
    compress() {}
}

let store = new CompressibleStore<Product>();
store.compress();

class SearchableStore<T extends { name: string }> extends Store<T> {
    find(name: string): T | undefined {
        return this._objects.find((obj) => obj.name === name);
    }
}

// Fix the generic type parameter
class ProductStore extends Store<Product> {
    filterByCategory(category: string) {
        return this._objects.filter((obj) => obj.name === category);
    }
}
```

## keyof operator

```ts
interface Product {
    name: string;
    price: number;
}

class Store<T> {
    protected _objects: T[] = [];

    add(object: T) {
        this._objects.push(object);
    }

    // T is Product
    // keyof T => name | price
    find(property: keyof T, value: unknown): T | undefined {
        return this._objects.find((object) => object[property] === value);
    }
}

class CompressibleStore<T> extends Store<T> {
    compress() {}
}

class SearchableStore<T extends { name: string }> extends Store<T> {
    search(name: string): T | undefined {
        return this._objects.find((obj) => obj.name === name);
    }
}

// Fix the generic type parameter
class ProductStore extends Store<Product> {
    filterByCategory(category: string) {
        return this._objects.filter((obj) => obj.name === category);
    }
}

let store = new Store<Product>();
store.add({ name: 'test', price: 1 });
store.add({ name: 'test2', price: 2 });
store.find('name', 'test');
// store.find('non-existing-property', 'test'); // correctly get compile error
```

## Type Mapping

Create a read only copy

```ts
interface Product {
    name: string;
    price: number;
}

type ReadOnlyProduct = {
    readonly [Property in keyof Product]: Product[Property];
};

let product: ReadOnlyProduct = {
    name: 'A',
    price: 1,
};
```

With generics

```ts
interface Product {
    name: string;
    price: number;
}

type ReadOnly<T> = {
    readonly [Property in keyof T]: T[Property];
};

let product: ReadOnly<Product> = {
    name: 'A',
    price: 1,
};
```

Create some type aliases

```ts
interface Product {
    name: string;
    price: number;
}

type ReadOnly<T> = {
    readonly [Property in keyof T]: T[Property];
};

type Optional<T> = {
    [Property in keyof T]?: T[Property];
};

type Nullable<T> = {
    [Property in keyof T]: T[Property] | null;
};

let product: ReadOnly<Product> = {
    name: 'A',
    price: 1,
};
```

Utility types are built into TypeScript

https://www.typescriptlang.org/docs/handbook/utility-types.html

-   Partial<T>
-   Required<T>
-   Readonly<T>
-   Record<K, Type>
-   Pick<T, K>
-   Omit<T, K>
-   Exclude<UnionType, ExcludedMembers>
-   Extract<Type, Union>
-   NonNullable<T>
-   Parameters<T>
-   ConstructorParameters<T>
-   ReturnType<T>
-   InstanceType<T>
-   ThisParameterType<T>
-   OmitThisParameter<T>
-   ThisType<T>

## Decorators

are experimental, need to enable in tsconfig.json

```json
    "experimentalDecorators": true /* Enable experimental support for TC39 stage 2 draft decorators. */,
```

## Class Decorators

```ts
function Component(constructor: Function) {
    console.log('Component decorator called');
    constructor.prototype.uniqueId = Date.now();
    constructor.prototype.insertInDOM = () => {
        console.log('Inserting component in DOM');
    };
}

@Component
class ProfileComponent {}
```

## Parameterised Decorators

Simple example

```ts
function Component(value: number) {
    return (constructor: Function) => {
        console.log('Component decorator called');
        constructor.prototype.options = value;
        constructor.prototype.uniqueId = Date.now();
        constructor.prototype.insertInDOM = () => {
            console.log('Inserting component in DOM');
        };
    };
}

@Component(1)
class ProfileComponent {}
```

Object example

```ts
type ComponentOptions = {
    selector: string;
};

function Component(options: ComponentOptions) {
    return (constructor: Function) => {
        console.log('Component decorator called');
        constructor.prototype.options = options;
        constructor.prototype.uniqueId = Date.now();
        constructor.prototype.insertInDOM = () => {
            console.log('Inserting component in DOM');
        };
    };
}

@Component({ selector: '#my-profile' })
class ProfileComponent {}
```

## Decorator Composition

```ts
type ComponentOptions = {
    selector: string;
};

function Component(options: ComponentOptions) {
    return (constructor: Function) => {
        console.log('Component decorator called');
        constructor.prototype.options = options;
        constructor.prototype.uniqueId = Date.now();
        constructor.prototype.insertInDOM = () => {
            console.log('Inserting component in DOM');
        };
    };
}

function Pipe(constructor: Function) {
    console.log('Pipe decorator called');
    constructor.prototype.pipe = true;
}

@Component({ selector: '#my-profile' })
@Pipe
class ProfileComponent {}
```

Will be called in the reverse order, output

```txt
Pipe decorator called
Component decorator called
```

## Method Decorators

Need to use function expression when redefining the method to access `this`

```ts
function Log(target: any, methodName: string, descriptor: PropertyDescriptor) {
    const original = descriptor.value as Function;
    descriptor.value = function (...args: any) {
        console.log('Before');
        original.call(this, ...args);
        console.log('After');
    };
}

class Person {
    @Log
    say(message: string) {
        console.log(`Person says ${message}`);
    }
}

let person = new Person();
person.say('Hello');
```

## Accessor Decorators

```ts
function Capitalize(target: any, methodName: string, descriptor: PropertyDescriptor) {
    const original = descriptor.get;
    descriptor.get = function () {
        const result = original!.call(this);
        return typeof result === 'string' ? result.toUpperCase() : result;
    };
    return descriptor;
}

class Person {
    constructor(public firstName: string, public lastName: string) {}

    @Capitalize
    get fullName() {
        return `${this.firstName} ${this.lastName}`;
    }
}

let person = new Person('john', 'doe');
console.log(person.fullName);
```

## Property Decorators

```ts
function MinLength(length: number) {
    return (target: any, propertyName: string) => {
        let value: string;

        const descriptor: PropertyDescriptor = {
            get() {
                return value;
            },
            set(newValue: string) {
                if (newValue.length < length) {
                    throw new Error(`${propertyName} must be at least ${length} characters long`);
                }
                value = newValue;
            },
        };

        Object.defineProperty(target, propertyName, descriptor);
    };
}

class User {
    @MinLength(4)
    password: string;

    constructor(password: string) {
        this.password = password;
    }
}

let user = new User('abc');
console.log(user.password);
```

Will throw error at runtime.

## Parameter Decorators

```ts
type WatchedParameter = {
    methodName: string;
    parameterIndex: number;
};

const watchedParameters: WatchedParameter[] = [];

function Watch(target: any, methodName: string, parameterIndex: number) {
    watchedParameters.push({
        methodName,
        parameterIndex,
    });
}

class Vehicle {
    move(@Watch speed: number) {}
}

console.log(watchedParameters);
```

## Modules

```ts
class Circle {
    constructor(public radius: number) {
        this.radius = radius;
    }
    get area() {
        return Math.PI * this.radius * this.radius;
    }
}

class Square {
    constructor(public length: number) {
        this.length = length;
    }
    get area() {
        return this.length * this.length;
    }
}

export { Circle, Square };
```

```ts
import { Circle } from './shapes';

let circle = new Circle(10);
console.log(circle.area);
```

## Default exports

```ts
export default class Store {}

export enum Format {
    Raw,
    Compressed,
}
```

```ts
import Store, { Format } from './storage';
```

## Wildcard Imports

```ts
import * as Shapes from './shapes';

let circle = new Shapes.Circle(10);
```

## Re-exporting

shapes/circle.ts

```ts
export class Circle {
    constructor(public radius: number) {
        this.radius = radius;
    }
    get area() {
        return Math.PI * this.radius * this.radius;
    }
}
```

shapes/square.ts

```ts
export class Square {
    constructor(public length: number) {
        this.length = length;
    }
    get area() {
        return this.length * this.length;
    }
}
```

shapes/index.ts

```ts
export { Circle } from './Circle';
export { Square } from './Square';
```

./index.ts

```ts
import { Circle, Square } from './shapes';
```

## Using JavaScript in TypeScript

enable config

```json
        "module": "commonjs" /* Specify what module code is generated. */,
        "allowJs": true /* Allow JavaScript files to be a part of your program. Use the 'checkJS' option to get errors from these files. */,
```

commonjs is more compatible with modules.

## Type Checking JS Code

config option

```json
        "checkJs": true /* Enable error reporting in type-checked JavaScript files. */,
```

Can disable type checking

```js
// @ts-nocheck
export function calculateTax(amount) {
    return amount * 0.08;
}
```

## Use JSDoc to provide type information in js files

```js
/**
 * Calculate income tax.
 * @param {number} amount - Net salary after expenses
 * @returns {number}
 */
export function calculateTax(amount) {
    return amount * 0.08;
}
```

## Creating Declaration Files

tax.d.ts created for tax.js

```ts
export declare function calculateTax(income: number): number;
```

## Using Definitely Typed Declaration Files

There are declaration files for popular libraries.

```sh
npm i lodash
npm i --save-dev @types/lodash
```

Some libraries have TypeScript definitions.

## Using React with TypeScript

https://reactjs.org/docs/static-type-checking.html#adding-typescript-to-a-project

https://react-typescript-cheatsheet.netlify.app/docs/basic/setup/

```sh
npx create-react-app reminders-app --template typescript
.
Need to install the following packages:
  create-react-app
Ok to proceed? (y) y
npm WARN deprecated tar@2.2.2: This version of tar is no longer supported, and will not receive security updates. Please upgrade asap.

Creating a new React app in reminders-app.

Installing packages. This might take a couple of minutes.
Installing react, react-dom, and react-scripts with cra-template-typescript...


added 1383 packages in 53s

192 packages are looking for funding
  run `npm fund` for details

Installing template dependencies using npm...
npm WARN deprecated source-map-resolve@0.6.0: See https://github.com/lydell/source-map-resolve#deprecated

added 39 packages, and changed 1 package in 3s

192 packages are looking for funding
  run `npm fund` for details

We detected TypeScript in your project (src/App.test.tsx) and created a tsconfig.json file for you.

Your tsconfig.json has been populated with default values.

Removing template package using npm...


removed 1 package, and audited 1422 packages in 2s

192 packages are looking for funding
  run `npm fund` for details

6 high severity vulnerabilities

To address all issues (including breaking changes), run:
  npm audit fix --force

Run `npm audit` for details.

Success! Created reminders-app at reminders-app
Inside that directory, you can run several commands:

  npm start
    Starts the development server.

  npm run build
    Bundles the app into static files for production.

  npm test
    Starts the test runner.

  npm run eject
    Removes this tool and copies build dependencies, configuration files
    and scripts into the app directory. If you do this, you can’t go back!

We suggest that you begin by typing:

  cd reminders-app
  npm start

Happy hacking!
```

## Adding Bootstrap

```sh
npm i bootstrap
```

Add to index.tsx

```ts
import 'bootstrap/dist/css/bootstrap.css';
```

## Creating a Component - Title

install extension `Reactjs code snippets`

`rsf` react stateless function

## Calling the Backend

jsonplaceholder.typicode.com

## Emet abbreviation

```sh
label+input.form-control+button.btn.btn-primary.rounded-pill;
```

becomes

```tsx
    <label htmlFor=""></label>
    <input type="text" className="form-control" />
    <button className="btn btn-primary rounded-pill"></button>
```

Should work on tab, might need to invoke suggestions.

## Node, Express and TypeScript

```sh
mkdir reminders-api
cd reminders-api
npm init -y
npm i --save-dev ts-node
```

set script

```json
  "scripts": {
    "start": "ts-node index.ts"
  },
```

Run from command line

```sh
npx ts-node index.ts
```

Install ts-node globally to drop the npx.

## Set up Express project

```sh
npm i express
npm i --save-dev typescript @types/node @types/express
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

```sh
npm i --save-dev nodemon
```

```json
  "scripts": {
    "start": "nodemon index.ts"
  },
```

## Very simple express app

```ts
import express from 'express';
const app = express();
const port = 8000;

app.get('/', (req, res) => {
    res.send('Hello World!');
});

app.listen(port, () => console.log(`Server started, port ${port}`));
```

## Status

By convention, when creating a new object the return code status should be 201.
