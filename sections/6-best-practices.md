# **Best Practices**

This section will cover best practices for writing TypeScript codThese practices are not mandatory, but they can help
you write cleaner, more maintainable code.

## **Table of Contents**

1. [Enforce Strict Typing](#enforce-strict-typing)
2. [Use Type Aliases and Interfaces Wisely](#use-type-aliases-and-interfaces-wisely)
3. [Avoid Excessive Use of `any`](#avoid-excessive-use-of-any)
4. [Use Readonly and Immutable Types](#use-readonly-and-immutable-types)
5. [Leverage Utility Types](#leverage-utility-types)
6. [Narrow Types Explicitly](#narrow-types-explicitly)
7. [Use `unknown` Over `any`](#use-unknown-over-any)
8. [Avoid Namespace Pollution](#avoid-namespace-pollution)
9. [Document Types and Functions](#document-types-and-functions)
10. [Keep `tsconfig.json` Clean](#keep-tsconfigjson-clean)
11. [Optimize `any` to `never` in Utility Scenarios](#optimize-any-to-never-in-utility-scenarios)
12. [Utilize ESLint and Prettier](#utilize-eslint-and-prettier)
13. [Ensure Backward Compatibility](#ensure-backward-compatibility)

## **Enforce Strict Typing**

-   Always enable the `strict` mode in your `tsconfig.json` file.
-   Use specific types instead of `any` to reduce ambiguity and catch potential errors during development.
-   Enable `noImplicitAny`, `strictNullChecks`, `strictFunctionTypes`, and `strictPropertyInitialization` to enforce
    stricter type checking.

### Suggested reading

-   [`strict` flag documentation](https://www.typescriptlang.org/tsconfig/#strict)

## **Use Type Aliases and Interfaces Wisely**

-   Use **interfaces** when defining objects with fixed structures, extending or implementing other interfaces.
-   Use **type aliases** for unions, intersections, or when defining more complex structures like utility types.

### Suggested reading

-   **From this guide**:

    -   [Type Aliases](./3-the-basics.md#type-aliases)
    -   [Interfaces](./3-the-basics.md#interfaces)
    -   [Type Aliases vs Interfaces](./3-the-basics.md#type-aliases-vs-interfaces)

-   **Official documentation**:

    -   [Type Aliases](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html#type-aliases)
    -   [Interfaces](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html#interfaces)
    -   [Type Aliases vs Interfaces](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html#differences-between-type-aliases-and-interfaces)

## **Avoid Excessive Use of `any`**

-   Replace `any` with stricter alternatives like `unknown` or a more specific type to maintain type safety.
-   Use `any` only when migrating legacy code or when the type is truly unknown.
-   Use `noImplicitAny` to catch implicit `any` types in your codebase.

### Suggested reading

-   **From this guide**:

    -   [Special Types](./3-the-basics.md#special-types)

-   **Official documentation**:

    -   [`any` documentation](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html#any)
    -   [`noImplicitAny` flag documentation](https://www.typescriptlang.org/tsconfig#noImplicitAny)
    -   [`unknown` documentation](https://www.typescriptlang.org/docs/handbook/release-notes/typescript-3-0.html#new-unknown-top-type)

## **Use Readonly and Immutable Types**

-   Use `readonly` for properties that shouldn't change after initialization.
-   Use `ReadonlyArray` and `Readonly` utility types to create read-only versions of arrays and objects.
-   Consider libraries like **Immutable.js** if working with data that requires immutability. As mentioned in the guide,
    it's important to keep in mind that using third-party libraries or runtime solutions can have performance
    implications.

### Suggested reading

-   **From this guide**:

    -   [Readonly](./4-utility-types.md#readonly)
    -   [ReadonlyArray](./4-utility-types.md#readonlyarray)

-   **Official documentation**:

    -   [`readonly` documentation](https://www.typescriptlang.org/docs/handbook/2/objects.html#readonly-properties)
    -   [`ReadonlyArray` documentation](https://www.typescriptlang.org/docs/handbook/utility-types.html#readonlytype)
    -   [`Readonly` documentation](https://www.typescriptlang.org/docs/handbook/utility-types.html#readonlytype)

## **Leverage Utility Types**

-   Use built-in utility types like `Partial`, `Pick`, `Omit`, and `Record` to handle common transformations.
-   Create custom utility types when needed to make your code reusable.

### Suggested reading

-   **From this guide**:

    -   [Utility Types](./4-utility-types.md)

-   **Official documentation**:

    -   [Utility Types](https://www.typescriptlang.org/docs/handbook/utility-types.html)

## **Narrow Types Explicitly**

-   Use type guards (e.g., `typeof`, `instanceof`) to safely narrow types.
-   Write custom type guard functions for more complex scenarios.

### Suggested reading

-   **From this guide**:

    -   [Type Narrowing](./5-advanced-topics.md#type-narrowing)

-   **Official documentation**:

    -   [Type Narrowing](https://www.typescriptlang.org/docs/handbook/2/narrowing.html)

## **Use `unknown` Over `any`**

-   When accepting unknown data (e.g., from external APIs), use `unknown` instead of `any` to enforce type checks before
    usage.
-   Use type assertions or type guards to narrow down the type when using `unknown`.

### Suggested reading

-   **From this guide**:

    -   [Special Types](./3-the-basics.md#special-types)

-   **Official documentation**:

    -   [`unknown` documentation](https://www.typescriptlang.org/docs/handbook/release-notes/typescript-3-0.html#new-unknown-top-type)

## **Avoid Namespace Pollution**

-   Prefer ES6 modules over `namespace` to keep your code clean and modular.
-   Use `namespace` only when working with global objects or legacy code.

### Suggested reading

-   **From this guide**:

    -   [Modules](./5-advanced-topics.md#modules)
    -   [Namespaces](./5-advanced-topics.md#namespaces)

-   **Official documentation**:

    -   [Modules](https://www.typescriptlang.org/docs/handbook/2/modules.html)
    -   [Namespaces](https://www.typescriptlang.org/docs/handbook/namespaces.html)

## **Document Types and Functions**

-   Add `JSDoc` comments to clarify complex types, interfaces, or generics.
-   Use tools like `tsdoc` for consistent documentation.
-   Document function parameters, return types, and side effects to improve code readability.

### Useful links

-   [JSDoc](https://jsdoc.app/)
-   [TSDoc](https://tsdoc.org/)

## **Keep `tsconfig.json` Clean**

-   Organize your `tsconfig.json` file by enabling only necessary settings.
-   Separate configurations for `base` and `app-specific` use cases when managing multiple projects.
-   For large or complex projects, consider using a `tsconfig.base.json` file to share common settings across multiple
    projects.

### Suggested reading

-   **Official documentation**:

    -   [`tsconfig.json` reference](https://www.typescriptlang.org/tsconfig)

## **Optimize `any` to `never` in Utility Scenarios**

-   Use `never` in places where a value should never exist.
-   Use `never` as a return type for functions that never return.

### Suggested reading

-   **From this guide**:

    -   [Special Types](./3-the-basics.md#special-types)

-   **Official documentation**:

    -   [`never` documentation](https://www.typescriptlang.org/docs/handbook/2/functions.html#never)

## **Ensure Backward Compatibility**

-   When creating libraries or frameworks, provide backward-compatible typings using overloads or helper types.

### Suggested reading

-   **From this guide**:

    -   [Overloading](./5-advanced-topics.md#overloading)

-   **Official documentation**:

    -   [Overloads](https://www.typescriptlang.org/docs/handbook/2/functions.html#function-overloads)

## **Utilize ESLint and Prettier**

-   Use a linter (e.g., **ESLint**) and code formatter (**Prettier**) with TypeScript plugins to enforce coding
    standards.

### Useful links

-   [ESLint](https://eslint.org/)
-   [Prettier](https://prettier.io/)
