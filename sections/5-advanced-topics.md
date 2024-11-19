# **Advanced Topics**

In this section, we'll cover some advanced topics in TypeScript that can help you write more expressive and powerful
code. Let's dive in!

## **Table of Contents**

1.  [Mapped Types](#mapped-types)
2.  [Conditional Types](#conditional-types)
3.  [Template Literal Types](#template-literal-types)
4.  [Recursive Types](#recursive-types)
5.  [Type Inference](#type-inference)
6.  [Type Narrowing](#type-narrowing)
    -   [Type Guards](#type-guards)
    -   [Type Predicates](#type-predicates)
    -   [Type Casting](#type-casting)
        -   [Casting Objects](#casting-objects)
7.  [Type Reflection](#type-reflection)
8.  [Type Compatibility](#type-compatibility)
9.  [Type Aliases](#type-aliases)
    -   [Type Aliases vs Interfaces](#type-aliases-vs-interfaces)
10. [Decorators](#decorators)
11. [Modules](#modules)
12. [Namespaces](#namespaces)

## **Mapped Types**

Mapped types allow you to create new types by transforming the properties of an existing type. You can use mapped types
to create new types that are based on the properties of another type, with the ability to modify or filter out certain
properties.

```typescript
type Person = {
    name: string;
    age: number;
    city: string;
};

type ReadonlyPerson = {
    readonly [K in keyof Person]: Person[K];
};

const person: ReadonlyPerson = {
    name: "Alice",
    age: 30,
    city: "New York"
};

// Error: Cannot assign to 'name' because it is a read-only property
person.name = "Bob";
```

Another use case for mapped types is to create new types based on the keys of an existing type. This can be useful for
creating new types that are subsets of an existing type, or for transforming the keys of an existing type.

```typescript
type Status = "active" | "inactive" | "pending";

type StatusMap = {
    [K in Status]: boolean;
};

const statusMap: StatusMap = {
    active: true,
    inactive: false,
    pending: true
};

// Error: Property 'deleted' is missing in type 'StatusMap'
statusMap.deleted = false;
```

## **Conditional Types**

Conditional types allow you to create types that depend on a condition. You can use conditional types to create types
that are based on the values of other types, with the ability to branch based on a condition.

```typescript
type IsString<T> = T extends string ? "yes" : "no";

type A = IsString<string>; // "yes"

type B = IsString<number>; // "no"
```

Conditional types can be used to create more complex type transformations, such as filtering out certain types from a
union.

```typescript
type Filter<T, U> = T extends U ? T : never;

type C = Filter<string | number | boolean, string>; // string
```

These examples may be a little simplistic or abstract, so here's a more real-life example of how conditional types can
be used:

```typescript
// API request types
type RequestType = "getUser" | "getPosts";

// API response types
interface UserResponse {
    id: number;
    name: string;
}

interface PostsResponse {
    id: number;
    title: string;
    content: string;
}

// Map request type to its response type
type ApiResponse<T extends RequestType> = T extends "getUser"
    ? UserResponse
    : T extends "getPosts"
      ? PostsResponse
      : never;

// Example function to fetch data from the API
function fetchApi<T extends RequestType>(request: T): ApiResponse<T> {
    switch (request) {
        case "getUser":
            return {
                id: 1,
                name: "Alice"
            } as ApiResponse<T>;
        case "getPosts":
            return {
                id: 1,
                title: "Hello World",
                content: "Welcome to my blog!"
            } as ApiResponse<T>;
        default:
            throw new Error("Unsupported request type");
    }
}

// Usage examples
const user = fetchApi("getUser");
// user is inferred as UserResponse
console.log(user.name); // Alice

const post = fetchApi("getPosts");
// post is inferred as PostsResponse
console.log(post.title); // Hello World
```

Ok, this may look a bit complex, so let's break it down:

-   We define a `RequestType` type that represents the different types of API requests we can make.
-   We define `UserResponse` and `PostsResponse` interfaces that represent the response data for the `getUser` and
    `getPosts` requests, respectively.
-   We define a `ApiResponse` type that maps each request type to its corresponding response type using conditional
    types. Let's break down the condition for further understanding:
    -   If the request type is `"getUser"`, the response type is `UserResponse`.
    -   If the request type is `"getPosts"`, the response type is `PostsResponse`.
    -   If the request type is neither `"getUser"` nor `"getPosts"`, the response type is `never` (which means it's an
        invalid request type - it should **_never_** happen).
-   We define a `fetchApi` function that takes a request type as an argument and returns the corresponding response
    type. The function uses a switch statement to handle different request types and return the appropriate response
    data. (May not be the best way to handle this, but it's just an example)
-   We use the `fetchApi` function to fetch data from the API for the `"getUser"` and `"getPosts"` requests. The return
    type of the function is inferred based on the request type, so we get the correct response data for each request.

As you can see, conditional types can be very powerful and allow you to create complex type transformations based on the
values of other types.

## **Template Literal Types**

Template literal types allow you to create new types by concatenating string literals. You can use template literal
types to create new types that are based on the values of other types, with the ability to concatenate or transform
string literals.

```typescript
type Greeting = "Hello, " | "Hi, ";

type Name = "Alice" | "Bob";

type Greet<T extends Name> = `${Greeting}${T}`;

type A = Greet<"Alice">; // "Hello, Alice"

type B = Greet<"Bob">; // "Hi, Bob"
```

A more practical example of template literal types is to create types that represent CSS class names. You can use
template literal types to create types that are based on the values of other types, with the ability to concatenate or
transform string literals. This might be useful when working with CSS-in-JS libraries or other scenarios where you need
to generate class names dynamically.

```typescript
type ClassName = "button" | "link" | "input";

type Size = "small" | "medium" | "large";

type Color = "primary" | "secondary" | "tertiary";

type ButtonClass<T extends Size, U extends Color> = `${T}-${U} ${ClassName}`;

type A = ButtonClass<"small", "primary">; // "small-primary button"

type B = ButtonClass<"medium", "secondary">; // "medium-secondary button"
```

## **Recursive Types**

Recursive types allow you to create types that refer to themselves. You can use recursive types to create types that are
based on their own structure, with the ability to nest or reference themselves.

```typescript
type TreeNode<T> = {
    value: T;
    left?: TreeNode<T>;
    right?: TreeNode<T>;
};

const tree: TreeNode<number> = {
    value: 1,
    left: {
        value: 2,
        left: {
            value: 4
        },
        right: {
            value: 5
        }
    },
    right: {
        value: 3,
        left: {
            value: 6
        },
        right: {
            value: 7
        }
    }
};
```

For a more realistic usage of this, imagine you're building a discussion forum or social media platform where comments
can have replies, forming a tree-like structure. Recursive types can model this nested comment system by allowing
comments to have replies that are also comments, and so on.

```typescript
interface UserComment {
    id: number;
    text: string;
    replies?: UserComment[];
}

const comment: UserComment = {
    id: 1,
    text: "This is a really useful guide!",
    replies: [
        {
            id: 2,
            text: "I agree!"
        },
        {
            id: 3,
            text: "Me too!",
            replies: [
                {
                    id: 4,
                    text: "Great job!"
                }
            ]
        }
    ]
};
```

Recursive types can be very useful for modeling hierarchical data structures like trees, graphs, or nested objects.

## **Type Inference**

Type inference is the ability of the TypeScript compiler to automatically determine the type of a value based on its
usage in the code. You can use type inference to let TypeScript infer the type of a value without explicitly specifying
it.

```typescript
let x = 10; // x is inferred as number
let y = "hello"; // y is inferred as string
let z = [1, 2, 3]; // z is inferred as number[]
```

We've already seen examples of type inference throughout this guide, where TypeScript infers the type of a variable
based on its value or usage. Type inference can be very useful for writing concise and readable code, as you don't have
to explicitly specify the type of every variable. However, there are cases where you may want to explicitly specify the
type of a variable to provide additional type safety or clarity.

```typescript
let x: number = 10; // x is explicitly typed as number
let y: string = "hello"; // y is explicitly typed as string
let z: number[] = [1, 2, 3]; // z is explicitly typed as number[]
```

Explicitly specifying the type of a variable can be useful when you want to provide additional type safety, document the
code, or make the code more readable. It's up to you to decide when to use type inference and when to explicitly specify
types based on your preferences and the requirements of your project.

## **Type Narrowing**

Type narrowing is the process of refining a value's type in TypeScript based on control flow. When you perform checks
(such as `typeof` or `instanceof`), TypeScript narrows the type of the value accordingly.

For example, when working with union types, TypeScript can infer which type a value will have inside a specific block of
code based on the check.

```typescript
type Animal =
    | {
          type: "dog";
          bark: () => void;
      }
    | {
          type: "cat";
          meow: () => void;
      };

function makeSound(animal: Animal) {
    if (animal.type === "dog") {
        animal.bark(); // animal is narrowed to { type: "dog"; bark: () => void }
    } else {
        animal.meow(); // animal is narrowed to { type: "cat"; meow: () => void }
    }
}
```

In the above example, TypeScript narrows the type of `animal` based on the `type` property, so you can safely call
either `bark` or `meow`.

### **Type Guards**

Type guards are a way to check the type of a value at runtime and narrow its type in a conditional block. You can use
type guards to perform type checks on values and narrow their types based on the results of the checks.

```typescript
function isString(value: any): value is string {
    return typeof value === "string";
}

function example(value: any) {
    if (isString(value)) {
        // value is narrowed to string
        console.log(value.toUpperCase());
    } else {
        // value is not a string
        console.log("Not a string");
    }
}
```

Type guards are very useful for working with values of uncertain or unknown types, such as when you're dealing with
union types or values from dynamic sources. By using type guards, you can narrow the type of a value and take advantage
of TypeScript's type checking and autocompletion features.

### **Type Predicates**

Type predicates are a special type of type guard in TypeScript. They allow you to narrow the type of a value in a way
that the compiler understands. This is particularly useful when you're checking types in conditional expressions and
want TypeScript to understand what type the value will be after the check.

A **type predicate** is a function whose return type is a special form of `value is Type`. This tells TypeScript that,
inside the conditional block where the predicate is true, the value can be treated as the given type.

```typescript
function isString(value: any): value is string {
    return typeof value === "string";
}

function isNumber(value: any): value is number {
    return typeof value === "number";
}

function isObject(value: any): value is object {
    return typeof value === "object" && value !== null;
}

function example(value: any) {
    if (isString(value)) {
        // value is narrowed to string
        console.log(value.toUpperCase());
    } else if (isNumber(value)) {
        // value is narrowed to number
        console.log(value.toFixed(2));
    } else if (isObject(value)) {
        // value is narrowed to object
        console.log(Object.keys(value));
    } else {
        // value is not a string, number, or object
        console.log("Unknown type");
    }
}
```

Type predicates provide more precise type narrowing in your functions and help with runtime checks.

### **Type Casting**

Type casting allows you to tell TypeScript to treat a value as a certain type. This is useful when you know more about
the value's type than TypeScript can infer. There are two ways to perform type casting:

-   `as` syntax (preferred)

```typescript
let value: any = "Hello, World!";
let stringLength: number = (value as string).length;
```

-   Angle-bracket syntax

```typescript
let value: any = "Hello, World!";
let stringLength: number = (<string>value).length;
```

While both methods work, the `as` syntax is generally preferred because it’s more explicit and avoids conflicts with,
for example, JSX in React.

#### **Casting Objects**

You can also cast objects when you know the object conforms to a certain type, but TypeScript cannot automatically infer
it.

```typescript
interface Person {
    name: string;
    age: number;
}

const data: any = { name: "Alice", age: 30 };
const person = data as Person; // Now `person` is treated as type `Person`
```

> **Note:** While type casting can be useful, it bypasses TypeScript’s safety checks, so it's best used sparingly and
> only when you are confident about the value’s type.

## **Type Reflection**

Type reflection is the ability to inspect and manipulate types at runtime. TypeScript doesn't have built-in support for
type reflection, but you can achieve similar functionality using conditional types and mapped types. By using
conditional types and mapped types, you can create types that represent the structure of other types and use them to
perform type reflection.

Here's an example of how you can use conditional types and mapped types to perform type reflection in TypeScript:

```typescript
type Person = {
    name: string;
    age: number;
    city: string;
};

type Reflect<T> = {
    [K in keyof T]: T[K];
};

type ReflectedPerson = Reflect<Person>;

const person: ReflectedPerson = {
    name: "Alice",
    age: 30,
    city: "New York"
};

// Log the keys and values of the person object
for (const key in person) {
    console.log(`${key}: ${person[key]}`);
}
```

To breakdown the example:

-   We define a `Person` type that represents the structure of a person object.
-   We define a `Reflect` type that uses a mapped type to create a new type that reflects the structure of another type.
-   We create a `ReflectedPerson` type by applying the `Reflect` type to the `Person` type.
-   We create a `person` object that conforms to the `ReflectedPerson` type.
-   We use a `for...in` loop to iterate over the keys of the `person` object and log the keys and values to the console.

> **Note:** Libraries like [`reflect-metadata`](https://www.npmjs.com/package/reflect-metadata) provide more advanced
> type reflection capabilities in TypeScript. These are particularly useful for working with complex types, performing
> advanced type transformations or working with dependency injection frameworks.

## **Type Compatibility**

Type compatibility determines whether one type can be assigned to another type. TypeScript uses structural typing,
meaning that types are compatible if they have the same shape. This allows you to assign objects with the same structure
to each other, even if they were defined with different types.

```typescript
interface Point2D {
    x: number;
    y: number;
}

interface Point3D {
    x: number;
    y: number;
    z: number;
}

let point2D: Point2D = { x: 1, y: 2 };
let point3D: Point3D = { x: 1, y: 2, z: 3 };

point2D = point3D; // OK
point3D = point2D; // Error: Property 'z' is missing in type 'Point2D' but required in type 'Point3D'
```

In the example above, `Point2D` and `Point3D` have the same structure, so you can assign a `Point3D` object to a
`Point2D` variable, but not vice versa. This is because `Point3D` has an additional property `z` that `Point2D` doesn't
have. TypeScript checks the shape of the types to determine compatibility, rather than relying on explicit type
annotations.

## **Type Aliases**

Type aliases allow you to create custom names for types in TypeScript. You can use type aliases to define complex types
or to give more descriptive names to existing types.

```typescript
type ID = number;

type User = {
    id: ID;
    name: string;
};

const user: User = {
    id: 1,
    name: "Alice"
};
```

In the example above, we define a `ID` type alias for `number` and a `User` type alias for an object with `id` and
`name` properties. Type aliases can make your code more readable and maintainable by giving meaningful names to types.
They can also help reduce duplication by defining common types in one place.

### **Type Aliases vs Interfaces**

Type aliases and interfaces are similar in many ways, but there are some key differences between them:

-   **Type aliases** are more flexible than interfaces. You can use type aliases to define union types, intersection
    types, tuple types, and more complex types that interfaces cannot express.
-   **Interfaces** are more suitable for defining object shapes. If you need to define an object with specific
    properties, methods, or signatures, interfaces are the way to go. Interfaces can also be extended and implemented,
    which is not possible with type aliases.

In general, use type aliases when you need to define complex types or give meaningful names to existing types, and use
interfaces when you need to define object shapes with specific properties and methods. You can also use a combination of
type aliases and interfaces to achieve the desired level of expressiveness and flexibility in your code.

## **Decorators**

Decorators are a feature of TypeScript that allow you to add metadata to classes, methods, properties, or parameters.
You can use decorators to modify the behavior of classes or class members at design time.

```typescript
function log(target: Object, propertyKey: string): void {
    console.log(`Method ${propertyKey} was called from ${target.constructor.name} class`);
}

class Example {
    @log
    sayHello() {
        console.log("Hello, World!");
    }
}

const example = new Example();
example.sayHello();

class Example {
    @log
    sayHello() {
        console.log("Hello, World!");
    }
}

const example = new Example();
example.sayHello();
// Method sayHello was called from Example class
// Hello, World!
```

In the example above, we define a `log` decorator that logs a message when a method is called. We apply the `log`
decorator to the `sayHello` method of the `Example` class. When we create an instance of the `Example` class and call
the `sayHello` method, the decorator logs a message to the console. Decorators can be a powerful tool for adding
cross-cutting concerns, such as logging, caching, or validation, to your classes and methods.

Additionally you can customize the behavior of a decorator by passing arguments to it:

```typescript
type LogLevel = "INFO" | "WARN" | "ERROR" | "DEBUG";

function log(logLevel: LogLevel = "INFO"): MethodDecorator {
    return function (target, propertyKey, descriptor) {
        console.log(`[${logLevel}] - Method ${propertyKey.toString()} was called`);
        console.log(`[${logLevel}] - Target: ${target.constructor.name}`);
        console.log(`[${logLevel}] - Descriptor: ${JSON.stringify(descriptor, null, 4)}`);
    };
}

class Example {
    @log()
    sayHello() {
        console.log("Hello, World!");
    }
}

const example = new Example();
example.sayHello();
// [INFO] - Method sayHello was called
// [INFO] - Target: Example
// [INFO] - Descriptor: {
//     "writable": true,
//     "enumerable": false,
//     "configurable": true
// }
// Hello, World!
```

This way, you can create more flexible decorators that can be customized based on the arguments passed to them.

> **Important note**: At the time of writing this guide, decorators are an experimental feature in TypeScript and may
> change in future versions of the language. You can enable decorators by setting the `experimentalDecorators` compiler
> option to `true` in your `tsconfig.json` file.

## **Modules**

Modules are a way to organize code in TypeScript. You can use modules to split your code into separate files and reuse
it across different parts of your application. TypeScript supports several module formats, including CommonJS, AMD, UMD,
and ES6 modules.

Here's an example of how you can define and export a module in TypeScript:

```typescript
// math.ts
export function add(a: number, b: number): number {
    return a + b;
}

export function subtract(a: number, b: number): number {
    return a - b;
}

// app.ts
import { add, subtract } from "./math";

console.log(add(1, 2)); // 3
console.log(subtract(5, 3)); // 2
```

In the example above, we define a `math` module that exports two functions, `add` and `subtract`. We then import these
functions in the `app` module using the `import` statement. This allows us to use the functions defined in the `math`
module in the `app` module. Modules are a way to organize and reuse code in TypeScript, making it easier to manage large
codebases and collaborate with other developers.

## **Namespaces**

Namespaces are a way to organize code in TypeScript by grouping related code under a common name. You can use namespaces
to create logical groupings of code and avoid naming conflicts between different parts of your application. Namespaces
are similar to modules, but they are more suitable for organizing code within a single file or a small set of related
files. Here's an example of how you can define and use a namespace in TypeScript:

```typescript
// shapes.ts
namespace Shapes {
    export interface Point {
        x: number;
        y: number;
    }

    export function distance(a: Point, b: Point): number {
        const dx = a.x - b.x;
        const dy = a.y - b.y;
        return Math.sqrt(dx * dx + dy * dy);
    }
}

// app.ts
const pointA: Shapes.Point = { x: 0, y: 0 };
const pointB: Shapes.Point = { x: 3, y: 4 };

console.log(Shapes.distance(pointA, pointB)); // 5
```

In the example above, we define a `Shapes` namespace that contains an interface `Point` and a function `distance`. We
then use the `Shapes` namespace to access the `Point` interface and the `distance` function in the `app` module.
Namespaces are a way to organize related code in TypeScript and avoid naming conflicts between different parts of your
application.

> **Note**: Namespaces are a legacy feature in TypeScript, and modules are the preferred way to organize code in modern
> TypeScript applications. Although many third-party libraries still use namespaces, it's recommended to use modules for
> new projects to take advantage of the latest features and best practices in TypeScript.
