# Utility Types

Utility types are a set of predefined generic types that can be used to manipulate and transform other types. They are a
powerful feature of TypeScript that can help you write more concise and expressive code. Here are some of the most
commonly used utility types:

## Partial

The [`Partial`](https://www.typescriptlang.org/docs/handbook/utility-types.html#partialtype) utility type can be used to
make all properties of a type optional. This can be useful when you want to create a new type that is a partial version
of an existing type.

```typescript
interface User {
    name: string;
    age: number;
}

// This will throw an error because the 'age' property is missing
// Error: Property 'age' is missing in type '{ name: string; }' but required in type 'User'
const user: User = {
    name: "Alice"
};

// This will not throw an error because all properties are optional
const partialUser: Partial<User> = {
    name: "Alice"
};
```

In this example, the `PartialUser` type is a partial version of the `User` type, with all properties made optional. This
allows you to create objects that only have some of the properties of the original type.

## Required

The [`Required`](https://www.typescriptlang.org/docs/handbook/utility-types.html#requiredtype) utility type can be used
to make all properties of a type required. This can be useful when you want to create a new type that requires all
properties of an existing type.

```typescript
interface User {
    name?: string;
    age?: number;
}

// This will throw an error because the 'name' property is missing
// Error: Type '{}' is missing the following properties from type 'Required<User>': name, age
const user: Required<User> = {};

// This will not throw an error because all properties that are required are present
const requiredUser: Required<User> = {
    name: "Alice",
    age: 30
};
```

In this example, the `RequiredUser` type is a required version of the `User` type, with all properties made required.
This allows you to create objects that have all the properties of the original type.

## Readonly

The [`Readonly`](https://www.typescriptlang.org/docs/handbook/utility-types.html#readonlytype) utility type can be used
to make all properties of a type read-only. This can be useful when you want to ensure that an object's properties
cannot be modified after they have been set.

```typescript
interface Point {
    x: number;
    y: number;
}

const point: Readonly<Point> = {
    x: 10,
    y: 20
};

// This will throw an error because the 'x' property is read-only
// Error: Cannot assign to 'x' because it is a read-only property
point.x = 5;
```

In this example, the `Point` type is made read-only using the `Readonly` utility type. This ensures that the `x` and `y`
properties cannot be modified after the `point` object is created.

> **Important Note**: The `Readonly` utility, as any other TypeScript utility, is a build-time feature and does not
> affect the runtime behavior of your code. If you need to ensure inmutability you can rely in JavaScript features like
> [`Object.freeze`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/freeze),
> [`Object.seal`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/seal) or
> libraries like [`Immutable.js`](https://immutable-js.github.io/immutable-js/). This will generate runtime overhead, so
> you'll need to evaluate your specific use case to decide which approach is best for you.

Here's an example of how `Readonly` could be overridden:

```typescript
interface Point {
    x: number;
    y: number;
}

const point: Readonly<Point> = {
    x: 10,
    y: 20
};

(point as any).x = 5; // No error
```

> **Note:** This is often considered a bad practice because it defeats the purpose of using `Readonly` (or any type for
> that matter).

## ReadonlyArray

The
[`ReadonlyArray`](https://www.typescriptlang.org/docs/handbook/release-notes/typescript-3-4.html#a-new-syntax-for-readonlyarray)
utility type can be used to make an array read-only. This can be useful when you want to ensure that an array's elements
cannot be modified after they have been set.

```typescript
const numbers: ReadonlyArray<number> = [1, 2, 3];

// This will throw an error because the array is read-only
// Error: Index signature in type 'readonly number[]' only permits reading
numbers[0] = 4;
```

In this example, the `numbers` array is made read-only using the `ReadonlyArray` utility type. This ensures that the
array elements cannot be modified after the array is created.

> **Important Note**: As mentioned in the previous note, `ReadonlyArray` is a build-time feature and does not affect the
> runtime behavior of your code. If you need to ensure immutability, you can use JavaScript features like
> [`Object.freeze`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/freeze) or
> libraries like [`Immutable.js`](https://immutable-js.github.io/immutable-js/). You can also use TypeScript's
> `ReadonlyArray` in combination with
> [`Object.freeze`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/freeze) to
> achieve a similar effect. However, keep in mind that this will generate runtime overhead, so you'll need to evaluate
> your specific use case to decide which approach is best for you.

## Record

The [`Record`](https://www.typescriptlang.org/docs/handbook/utility-types.html#recordkeys-type) utility type can be used
to create a new type with a set of properties of a given type. This can be useful when you want to define an object with
a specific set of properties and their corresponding types.

```typescript
type Point = Record<"x" | "y", number>;

const point: Point = {
    x: 10,
    y: 20
};
```

In this example, the `Point` type is defined using the `Record` utility type, which creates a new type with the `x` and
`y` properties of type `number`. This allows you to create objects with those specific properties and types.

An alternative way to achieve the same result is by using **mapped types**, which we'll cover in upcoming sections.

```typescript
type Point = { [Key in "x" | "y"]: number };

const point: Point = {
    x: 10,
    y: 20
};
```

## Pick

The [`Pick`](https://www.typescriptlang.org/docs/handbook/utility-types.html#picktype-keys) utility type can be used to
create a new type by picking a set of properties from an existing type. This can be useful when you want to create a new
type that only has a subset of the properties of another type.

```typescript
interface User {
    name: string;
    age: number;
    email: string;
}

type UserWithoutEmail = Pick<User, "name" | "age">;

const user: UserWithoutEmail = {
    name: "Alice",
    age: 30
};
```

In this example, the `UserWithoutEmail` type is created using the `Pick` utility type, which picks the `name` and `age`
properties from the `User` type. This allows you to create objects that only have those properties.

## Omit

The [`Omit`](https://www.typescriptlang.org/docs/handbook/utility-types.html#omittype-keys) utility type can be used to
create a new type by omitting a set of properties from an existing type. This can be useful when you want to create a
new type that excludes certain properties from another type.

```typescript
interface User {
    name: string;
    age: number;
    email: string;
}

type UserWithoutEmail = Omit<User, "email">;

const user: UserWithoutEmail = {
    name: "Alice",
    age: 30
};
```

In this example, the `UserWithoutEmail` type is created using the `Omit` utility type, which omits the `email` property
from the `User` type. This allows you to create objects that do not have that property.

## Exclude

The [`Exclude`](https://www.typescriptlang.org/docs/handbook/utility-types.html#excludeuniontype-excludedmembers)
utility type can be used to create a new type by excluding a set of types from another type. This can be useful when you
want to create a new type that excludes certain types from another type.

```typescript
type States = "active" | "inactive" | "pending";

type ActiveState = Exclude<States, "inactive" | "pending">; // "active"
```

In this example, the `ActiveState` type is created using the `Exclude` utility type, which excludes the `"inactive"` and
`"pending"` types from the `States` type. This allows you to create a new type that only includes the `"active"` type.

## Extract

The [`Extract`](https://www.typescriptlang.org/docs/handbook/utility-types.html#extracttype-union) utility type can be
used to create a new type by extracting a set of types from another type. This can be useful when you want to create a
new type that only includes certain types from another type.

```typescript
type States = "active" | "inactive" | "pending";

type ActiveState = Extract<States, "active">; // "active"
```

In this example, the `ActiveState` type is created using the `Extract` utility type, which extracts the `"active"` type
from the `States` type. This allows you to create a new type that only includes the `"active"` type.

## NonNullable

The [`NonNullable`](https://www.typescriptlang.org/docs/handbook/utility-types.html#nonnullabletype) utility type can be
used to create a new type by removing `null` and `undefined` from another type. This can be useful when you want to
create a new type that does not allow `null` or `undefined` values.

```typescript
type User = {
    name: string;
    age: number | null;
    email: string | undefined;
};

// We're using NonNullable to create a new type that doesn't allow null or undefined values
type ValidUserAge = NonNullable<User["age"]>;
type ValidUserEmail = NonNullable<User["email"]>;

// This function will only accept valid user ages and emails
function createUserProfile(age: ValidUserAge, email: ValidUserEmail) {
    console.log(`User profile created with age: ${age} and email: ${email}`);
}

// Valid case: Age and email are properly defined.
createUserProfile(25, "user@example.com");

// The following examples will throw errors:

// Error: Argument of type 'null' is not assignable to parameter of type 'number'.
createUserProfile(null, "user@example.com");

// Error: Argument of type 'undefined' is not assignable to parameter of type 'string'.
createUserProfile(30, undefined);
```

In this example, while slightly verbose, the `ValidUserAge` and `ValidUserEmail` types are created using the
`NonNullable` utility type, which removes `null` and `undefined` from the User type. This ensures that the
`createUserProfile` function only accepts valid values for the age and email properties, enforcing type safety.

## ReturnType

The [`ReturnType`](https://www.typescriptlang.org/docs/handbook/utility-types.html#returntypetype) utility type can be
used to get the return type of a function type. This can be useful when you want to extract the return type of a
function and use it in other parts of your code.

```typescript
function greet(name: string): string {
    return `Hello, ${name}!`;
}

type GreetReturnType = ReturnType<typeof greet>;

const message: GreetReturnType = greet("Alice");

console.log(message); // Output: Hello, Alice!
```

In this example, the `GreetReturnType` type is created using the `ReturnType` utility type, which extracts the return
type of the `greet` function.

## InstanceType

The [`InstanceType`](https://www.typescriptlang.org/docs/handbook/utility-types.html#instancetypetype) utility type can
be used to get the instance type of a constructor function type. This can be useful when you want to extract the
instance type of a class and use it in other parts of your code.

```typescript
class User {
    name: string;

    constructor(name: string) {
        this.name = name;
    }
}

type UserInstanceType = InstanceType<typeof User>;

const user: UserInstanceType = new User("Alice");

console.log(user.name); // Output: Alice
```

In this example, the `UserInstanceType` type is created using the `InstanceType` utility type, which extracts the
instance type of the `User` class. This allows you to create instances of the `User` class and access its properties.

## NoInfer

The [`NoInfer`](https://www.typescriptlang.org/docs/handbook/utility-types.html#noinfertype) utility type is used to
prevent TypeScript from automatically inferring a type in specific contexts. By wrapping a type parameter with
`NoInfer`, you can ensure that a specific type is used exactly as declared, overriding TypeScript's default behavior of
type inference.

> **Note:** This is particularly useful when working with generics where you want to provide explicit control over the
> types being used, such as ensuring type constraints are adhered to or preventing undesired type inference.

```typescript
type NoInfer<T> = [T][T extends any ? 0 : never]; // Prevents inference by introducing a dependency

function transformData<T>(data: T, transformFn: (item: NoInfer<T>) => T): T[] {
    return [transformFn(data)];
}

// Example: Ensuring explicit types
const data = { id: 1, name: "Alice" };

// TypeScript will enforce that `item` must explicitly match the `data` type
const result = transformData(data, (item) => {
    // Without NoInfer, this could infer the type loosely
    return { ...item, name: item.name.toUpperCase() };
});

console.log(result); // Output: [{ id: 1, name: "ALICE" }]

// Example: Preventing misuse
// The following will result in a type error, as `item` must exactly match `T` (the `data` type).
transformData(data, (item) => ({ id: item.id, age: 30 }));
```

In this example, the `NoInfer` utility type is used to prevent TypeScript from inferring the type of `item` in the
context of the `transformData` function. This ensures that the `item` parameter must exactly match the `data` type
provided, enforcing type safety and preventing unwanted type inference.

> **How TypeScript Type Inference Works:** TypeScript attempts to infer the most specific type for a value or parameter
> based on its usage. In generic contexts, this behavior is automatic and can sometimes lead to unexpected results.
> `NoInfer` acts as a safeguard to prevent TypeScript from inferring a type, requiring explicit specification instead.

## Awaited

The [`Awaited`](https://www.typescriptlang.org/docs/handbook/utility-types.html#awaitedtype) utility type can be used to
get the resolved type of a `Promise` or other asynchronous type. This can be useful when you want to extract the
resolved value of a promise and use it in other parts of your code.

```typescript
// This function simulates fetching a user from an API
async function fetchUser(): Promise<{ id: number; name: string; email: string }> {
    return {
        id: 1,
        name: "Alice",
        email: "alice@example.com"
    };
}

// We're using Awaited to get the resolved type of the fetchUser function
type User = Awaited<ReturnType<typeof fetchUser>>;

// This function transforms user data into a string
function transformUserData(user: User): string {
    return `User Info: ${user.name} (${user.email})`;
}

// This function demonstrates using Awaited to handle asynchronous data
async function app(): Promise<void> {
    const user = await fetchUser(); // The User type is inferred
    const userInfo = transformUserData(user);

    console.log(userInfo); // Output: User Info: Alice (alice@example.com)
}

app();
```

In this example, the `User` type is created using the `Awaited` utility type, which extracts the resolved type of the
`Promise` returned by the `fetchUser` function. This allows you to work with the resolved value of the promise as a
regular type. The `app` function demonstrates how to use `Awaited` to handle asynchronous data in a type-safe manner.

## ThisType

The [`ThisType`](https://www.typescriptlang.org/docs/handbook/utility-types.html#thistypetype) utility type can be used
to specify the type of `this` in an object literal. This can be useful when you want to provide type information for the
`this` context in methods of an object, especially when the `this` context is more complex or created dynamically.

### Example 1: Using `ThisType` with an object literal

In a simple scenario, when you directly define an object and its methods, you can use `ThisType` to explicitly define
the type of `this` within those methods.

```typescript
interface User {
    name: string;
    greet(): string;
}

const user = {
    name: "Alice",
    greet() {
        return `Hello, ${this.name}!`;
    }
} as User & ThisType<User>;

console.log(user.greet()); // Output: Hello, Alice!
```

> **Note:**
>
> -   In this case, `ThisType<User>` ensures that inside the `greet` method, `this` is treated as a `User` object, even
>     though TypeScript could infer it from the object.
> -   If we didn't use `ThisType<User>`, TypeScript would still infer the type of `this` because the object and method
>     are defined together, but using `ThisType` makes the type explicit.

### Example 2: `ThisType` in a factory function

`ThisType` becomes more valuable when creating objects dynamically using a factory function, where the `this` context
needs to be explicitly defined in the methods of the returned object.

```typescript
interface User {
    name: string;
    greet(): string;
}

// Factory function that creates a user
function createUser(): ThisType<User> & User {
    return {
        name: "Alice",
        greet() {
            // 'this' will be correctly typed as User
            return `Hello, ${this.name}!`;
        }
    };
}

const user = createUser();
console.log(user.greet()); // Output: Hello, Alice!
```

> **Note:** In this example, the `createUser` function returns an object with a `greet` method. The `ThisType<User>`
> ensures that within the `greet` method, `this` refers to a `User` type, which is critical because `this` is not
> automatically inferred when methods are defined inside a function.

### So, to summarize

-   Use `ThisType` when you need to explicitly specify the type of `this` within an object or method.
-   It is especially useful in dynamic object creation (e.g., factory functions) or when defining methods outside a
    class or object literal.
-   While `ThisType` is not always necessary in simple cases where `this` can be inferred, it provides clarity and
    correctness in more complex patterns.

## ThisParameterType

The [`ThisParameterType`](https://www.typescriptlang.org/docs/handbook/utility-types.html#thisparametertype) utility
type can be used to extract the type of the `this` parameter in a function type. This can be useful when you want to
work with the type of the `this` parameter in a function and use it in other parts of your code.

```typescript
function greet(this: { name: string }, message: string): string {
    return `${this.name} says: ${message}`;
}

type GreetThisType = ThisParameterType<typeof greet>;

const user: GreetThisType = { name: "Alice" };
const message = greet.call(user, "Hello, TypeScript!");

console.log(message); // Output: Alice says: Hello, TypeScript!
```

In this example, the `GreetThisType` type is created using the `ThisParameterType` utility type, which extracts the type
of the `this` parameter in the `greet` function.

## OmitThisParameter

The [`OmitThisParameter`](https://www.typescriptlang.org/docs/handbook/utility-types.html#omitthisparametertype) utility
type can be used to remove the `this` parameter from a function type. This can be useful when you want to create a new
function type that does not have a `this` parameter.

```typescript
function greet(this: { name: string }, message: string): string {
    return `${this.name} says: ${message}`;
}

type GreetFunction = OmitThisParameter<typeof greet>;

const message = greet.call({ name: "Alice" }, "Hello, TypeScript!");

console.log(message); // Output: Alice says: Hello, TypeScript!
```

In this example, the `GreetFunction` type is created using the `OmitThisParameter` utility type, which removes the
`this` parameter from the `greet` function type. This allows you to work with the function type without the `this`
parameter.

## Parameters

The [`Parameters`](https://www.typescriptlang.org/docs/handbook/utility-types.html#parameterstype) utility type can be
used to get the parameter types of a function type as a tuple. This can be useful when you want to extract the parameter
types of a function and use them in other parts of your code.

```typescript
function greet(name: string, age: number): string {
    return `Hello, ${name}! You are ${age} years old.`;
}

type GreetParams = Parameters<typeof greet>;

const params: GreetParams = ["Alice", 30];
const message = greet(...params);

console.log(message); // Output: Hello, Alice! You are 30 years old.
```

In this example, the `GreetParams` type is created using the `Parameters` utility type, which extracts the parameter
types of the `greet` function as a tuple.

## ConstructorParameters

The [`ConstructorParameters`](https://www.typescriptlang.org/docs/handbook/utility-types.html#constructorparameterstype)
utility type can be used to get the parameter types of a constructor function type as a tuple. This can be useful when
you want to extract the parameter types of a class constructor and use them in other parts of your code.

```typescript
class User {
    constructor(name: string, age: number) {
        console.log(`User created: ${name}, ${age}`);
    }
}

type UserConstructorParams = ConstructorParameters<typeof User>;

const params: UserConstructorParams = ["Alice", 30];
const user = new User(...params); // Output: User created: Alice, 30
```

In this example, the `UserConstructorParams` type is created using the `ConstructorParameters` utility type, which
extracts the parameter types of the `User` class constructor as a tuple.

## KeyOf

The [`KeyOf`](https://www.typescriptlang.org/docs/handbook/2/keyof-types.html) utility type can be used to get the keys
of a type as a union type. This can be useful when you want to extract the keys of an object type and use them in other
parts of your code.

```typescript
interface User {
    id: number;
    name: string;
    email: string;
}

type UserKeys = keyof User;

const keys: UserKeys = "name";
console.log(keys); // Output: name
```

In this example, the `UserKeys` type is created using the `keyof` operator, which extracts the keys of the `User`
interface as a union type.

## ValuesType

The `ValuesType` utility type can be used to get the values of a type as a union type. This can be useful when you want
to extract the values of an object type and use them in other parts of your code.

```typescript
interface User {
    id: number;
    name: string;
    email: string;
}

type UserValues = ValuesType<User>;

const values: UserValues = 1;
console.log(values); // Output: 1
```

In this example, the `UserValues` type is created using the `ValuesType` utility type, which extracts the values of the
`User` interface as a union type.

## String Manipulation Types

TypeScript provides a set of utility types for manipulating string literals. These types can be useful when you want to
transform or manipulate string literals in your code.

### Capitalized

The `Capitalized` utility type can be used to transform the first character of a string literal to uppercase. This can
be useful when you want to ensure that a string starts with an uppercase letter.

```typescript
type CapitalizedString = Capitalized<"hello">; // "Hello"
```

In this example, the `CapitalizedString` type is created using the `Capitalized` utility type, which transforms the
string literal `"hello"` to `"Hello"`.

### Lowercase

The `Lowercase` utility type can be used to transform a string literal to lowercase. This can be useful when you want to
ensure that a string is in lowercase.

```typescript
type LowercaseString = Lowercase<"Hello">; // "hello"
```

In this example, the `LowercaseString` type is created using the `Lowercase` utility type, which transforms the string
literal `"Hello"` to `"hello"`.

### Uppercase

The `Uppercase` utility type can be used to transform a string literal to uppercase. This can be useful when you want to
ensure that a string is in uppercase.

```typescript
type UppercaseString = Uppercase<"hello">; // "HELLO"
```

In this example, the `UppercaseString` type is created using the `Uppercase` utility type, which transforms the string
literal `"hello"` to `"HELLO"`.

### Uncapitalize

The `Uncapitalize` utility type can be used to transform the first character of a string literal to lowercase. This can
be useful when you want to ensure that a string starts with a lowercase letter.

```typescript
type UncapitalizeString = Uncapitalize<"Hello">; // "hello"
```

In this example, the `UncapitalizeString` type is created using the `Uncapitalize` utility type, which transforms the
string literal `"Hello"` to `"hello"`.
