# **The Basics**

OK, let's start with the basics of TypeScript. In this section, we will cover variables, data types, functions, classes,
interfaces, and more. These fundamental concepts will help you understand the core features of TypeScript and how to use
them in your code.

## **Variables**

In TypeScript, as in JavaScript, you can declare variables using the `let`, `const`, or `var` keywords. Each of these
keywords has different scoping rules and behaviors. Considering this isn't a JavaScript conceptual guide, I'll just give
you a brief overview of each keyword:

-   `let`: Declares a block-scoped variable that can be reassigned. Refer to
    [TypeScript Docs](https://www.typescriptlang.org/docs/handbook/variable-declarations.html#let-declarations) and
    [MDN Web Docs](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/let) for more
    information.
-   `const`: Declares a block-scoped variable that cannot be reassigned. Refer to
    [TypeScript Docs](https://www.typescriptlang.org/docs/handbook/variable-declarations.html#const-declarations) and
    [MDN Web Docs](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/const) for more
    information.
-   `var`: Declares a variable with function scope or global scope. It is not recommended to use `var` in modern
    TypeScript code. Refer to
    [TypeScript Docs](https://www.typescriptlang.org/docs/handbook/variable-declarations.html#var-declarations) and
    [MDN Web Docs](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/var) for more
    information.

As mentioned before and as per TypeScript documentation, it is recommended to use `let` and `const` for variable
declarations instead of `var` to avoid common pitfalls and ensure better code quality.

Here is an example of declaring variables in TypeScript:

```typescript
let person: string = "John Doe"
const age: number = 30
var isActive: boolean = true
```

In this example, we declare three variables: `person` of type `string`, `age` of type `number`, and `isActive` of type
`boolean`. The variables are assigned initial values of `"John Doe"`, `30`, and `true`, respectively.

Now, let's see how these behave in TypeScript. If you try to reassign a value to a `const` variable, TypeScript will
throw an error:

```typescript
const age: number = 30

age = 40 // Error: Cannot assign to 'age' because it is a constant.
```

Similarly, if you try to access a variable before it is declared or use a different type than the one declared,
TypeScript will throw an error:

```typescript
console.log(person) // Error: Block-scoped variable 'person' used before its declaration.

let person: string = "John Doe"

person = 30 // Error: Type 'number' is not assignable to type 'string'.
```

Now, let's see some common pitfalls when using `var` in TypeScript, which can lead to unexpected behavior:

```typescript
if (true) {
    var x: number = 10
}

console.log(x) // Output: 10

for (var i = 0; i < 5; i++) {
    setTimeout(() => {
        console.log(i) // Output: 5 5 5 5 5
    }, 1000)
}

console.log(i) // Output: 5
```

Although these aren't issues per se, but rather expected behavior in JavaScript, it is important to know when to use
each keyword and the differences and implications of using them in your code. For more information on variable
declarations in TypeScript, you can refer to the
[official documentation](https://www.typescriptlang.org/docs/handbook/variable-declarations.html).

---

## **Data Types**

TypeScript provides several built-in data types to help you define the shape of your data and ensure type safety. Below
is an overview of the most commonly used types:

### **Primitive Types**

-   **`number`**: Represents numeric values, including integers and floating-point numbers.
-   **`string`**: Represents textual data, enclosed in single or double quotes.
-   **`boolean`**: Represents a logical value, either `true` or `false`.

> **Note**: From
> [TypeScript Docs](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html#the-primitives-string-number-and-boolean):
> The type names `String`, `Number`, and `Boolean` (starting with capital letters) are legal, but refer to special
> built-in types that rarely appear in your code. Always use lowercase `string`, `number`, or `boolean` for types.

-   **`bigint`**: Represents arbitrary-precision integers.
    [Learn more](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html#bigint).
-   **`object`**: Represents a collection of key-value pairs.
    [Learn more](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html#object-types).

### **Array and Tuple Types**

-   **`Array`**: Represents a list of elements of the same type.
    [Learn more](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html#arrays).
    -   **Tuple Types**: Represents an array with a fixed number of elements where each element may be of a different
        type. [Learn more](https://www.typescriptlang.org/docs/handbook/2/objects.html#tuple-types).

### **Enums**

-   **`Enum`**: Represents a set of named constants.
    [Learn more](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html#enums).

### **Function Types**

-   **`Function`**: Represents a function that takes a specific set of arguments and returns a specific type.
    [Learn more](https://www.typescriptlang.org/docs/handbook/2/functions.html#function).

### **Special Types**

-   **`any`**: Represents any type, bypassing type checking.
    [Learn more](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html#any).
-   **`unknown`**: A safer counterpart to `any`, requiring type assertion or checking before being used.
    [Learn more](https://www.typescriptlang.org/docs/handbook/2/functions.html#unknown).
-   **`void`**: Represents the absence of a return value (commonly used with functions that don't return anything).
    [Learn more](https://www.typescriptlang.org/docs/handbook/2/functions.html#void).
-   **`null`**: Represents a null value.
    [Learn more](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html#null-and-undefined).
-   **`undefined`**: Represents an undefined value.
    [Learn more](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html#null-and-undefined).
-   **`never`**: Represents a value that never occurs (used for functions that never return or throw errors).
    [Learn more](https://www.typescriptlang.org/docs/handbook/2/functions.html#never).

---

## **Functions**

Functions in TypeScript are similar to JavaScript functions but with added type annotations for parameters and return
values.

Here's an example of a simple function in TypeScript:

```typescript
function greet(name: string): string {
    return `Hello, ${name}!`
}

console.log(greet("John")) // Output: Hello, John!
```

In this example, the `greet` function takes a `name` parameter of type `string` and returns a string greeting. The type
of the return value is explicitly defined as `string`.

> **Exercise**: Try changing the parameter type or return value type to see how TypeScript enforces type safety in
> functions.

Learn more about functions in TypeScript by reading the following resources from the official documentation:

-   [Functions](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html#functions)
-   [More on Functions](https://www.typescriptlang.org/docs/handbook/2/functions.html)

---

## **Classes**

Classes in TypeScript allow you to create blueprints for objects with properties and methods. They provide a way to
model real-world entities and encapsulate data and behavior.

Here's an example of a simple class in TypeScript:

```typescript
class Person {
    private name: string

    constructor(name: string) {
        this.name = name
    }

    greet(): string {
        return `Hello, my name is ${this.name}.`
    }
}

const john = new Person("John")

console.log(john.greet()) // Output: Hello, my name is John.
```

In this example, the `Person` class has a private property `name`, a constructor that initializes the `name` property,
and a `greet` method that returns a greeting message.

> **Curious Fact**: TypeScript supports public, private, and protected access modifiers for class members, providing
> greater control compared to JavaScript, where everything is public by default unless explicitly marked as private
> using the # syntax. .

To learn more about classes in TypeScript, refer to the
[official documentation](https://www.typescriptlang.org/docs/handbook/2/classes.html).

---

## **Interfaces**

Interfaces in TypeScript define the structure of objects, specifying the properties and methods they must have. They
help in enforcing a consistent shape across different parts of your code.

Here's an example of an interface in TypeScript:

```typescript
interface Person {
    name: string
    age: number
    greet(): string
}

const john: Person = {
    name: "John",
    age: 30,
    greet() {
        return `Hello, my name is ${this.name} and I'm ${this.age} years old.`
    }
}

console.log(john.greet()) // Output: Hello, my name is John and I'm 30 years old.
```

In this example, the `Person` interface defines the structure of a person object with `name` and `age` properties and a
`greet` method. The `john` object implements this interface, ensuring it has the required properties and methods.

Anonther usage of interfaces is to define the shape of classes, ensuring that a class implements specific properties and
methods.

Here's an example of using an interface with a class:

```typescript
interface Animal {
    name: string
    makeSound(): void
}

class Dog implements Animal {
    name: string

    constructor(name: string) {
        this.name = name
    }

    makeSound(): void {
        console.log("Woof!")
    }
}

const dog = new Dog("Buddy")
dog.makeSound() // Output: Woof!
```

In this example, the `Animal` interface defines the structure of an animal object with a `name` property and a
`makeSound` method. The `Dog` class implements this interface, ensuring it has the required properties and methods.

To learn more about interfaces in TypeScript, refer to the
[official documentation](https://www.typescriptlang.org/docs/handbook/2/objects.html).

---

## **Intersection Types**

Intersection types in TypeScript allow you to combine multiple types into a single type. This enables you to create new
types by merging existing ones.

Here's an example of using intersection types:

```typescript
interface Person {
    name: string
}

interface Employee {
    company: string
}

type EmployeePerson = Person & Employee

const employee: EmployeePerson = {
    name: "John Doe",
    company: "Acme Inc."
}

console.log(employee) // Output: { name: 'John Doe', company: 'Acme Inc.' }
```

In this example, the `EmployeePerson` type is an intersection of the `Person` and `Employee` interfaces, combining their
properties into a single type. The `employee` object implements this type, containing properties from both interfaces.

To learn more about intersection types in TypeScript, refer to the
[official documentation](https://www.typescriptlang.org/docs/handbook/2/objects.html#intersection-types).

---

## **Union Types**

Union types in TypeScript allow you to specify that a value can be one of several types. This provides flexibility in
how you define variables and function parameters.

Here's an example of using union types:

```typescript
type ID = string | number

function printID(id: ID): void {
    console.log(`ID: ${id}`)
}

printID("ABC123") // Output: ID: ABC123
printID(456) // Output: ID: 456
```

In this example, the `ID` type is a union of `string` and `number`, allowing the `printID` function to accept values of
either type. This flexibility helps in handling different scenarios where a value can have multiple types.

To learn more about union types in TypeScript, refer to the
[official documentation](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html#union-types).

---

## **Generics**

Generics in TypeScript allow you to create reusable components that work with a variety of data types. They provide a
way to define functions, classes, and interfaces without specifying the exact type they will work with. This flexibility
makes your code more adaptable and reusable.

Here's an example of using generics:

```typescript
function identity<T>(arg: T): T {
    return arg
}

const result1 = identity<string>("Hello, generics!")
console.log(result1) // Output: Hello, generics!

const result2 = identity<number>(42)
console.log(result2) // Output: 42
```

In this example, the `identity` function uses a generic type `T` to accept and return values of any type. By specifying
the type when calling the function, you can ensure type safety while maintaining flexibility. This is especially useful
when working with collections, algorithms, and other scenarios where the exact type is not known in advance.

Here's a more advanced example of using generics with interfaces:

```typescript
interface Box<T> {
    value: T
}

const box1: Box<string> = { value: "Hello, generics!" }
const box2: Box<number> = { value: 42 }

console.log(box1.value) // Output: Hello, generics!
console.log(box2.value) // Output: 42
```

In this example, the `Box` interface uses a generic type `T` to define a box that can hold values of any type. This
allows you to create instances of `Box` with different value types while maintaining type safety. Generics are a
powerful feature of TypeScript that can greatly enhance the flexibility and reusability of your code.

To learn more about generics in TypeScript, refer to the
[official documentation](https://www.typescriptlang.org/docs/handbook/2/generics.html).
