# **TS**Playbook

![TypeScript](https://img.shields.io/badge/TypeScript-007ACC?style=for-the-badge&logo=typescript&logoColor=white)

**TS**Playbook is an open-source guide to help developers learn TypeScript. With clear explanations, practical examples,
and exercises, it covers everything from basics to advanced topics. Improve your TypeScript skills and write more
reliable code with this hands-on guide.

## How to Use This Guide

This guide is designed to be read in order, starting with the introduction and moving through each section. Each section
builds on the previous one, so it's important to follow the order to get the most out of it. You can also use the table
of contents to jump to a specific section if you're looking for something specific. The guide has been separated into
multiple sections to make it easier to navigate and understand.

## Table of Contents

1. [Introduction](./sections/1-introduction.md)
2. [Getting Started](./sections/2-getting-started.md)
    - [Installation](./sections/2-getting-started.md#installation)
    - [Project Setup](./sections/2-getting-started.md#project-setup)
    - [Configuration](./sections/2-getting-started.md#configuration)
    - [Editor Setup](./sections/2-getting-started.md#editor-setup)
        - [Useful Extensions](./sections/2-getting-started.md#useful-extensions)
3. [The Basics](./sections/3-the-basics.md)
    - [Variables](./sections/3-the-basics.md#variables)
    - [Data Types](./sections/3-the-basics.md#data-types)
        - [Primitive Types](./sections/3-the-basics.md#primitive-types)
        - [Array and Tuple Types](./sections/3-the-basics.md#array-and-tuple-types)
        - [Enums](./sections/3-the-basics.md#enums)
        - [Function Types](./sections/3-the-basics.md#function-types)
        - [Special Types](./sections/3-the-basics.md#special-types)
    - [Functions](./sections/3-the-basics.md#functions)
    - [Classes](./sections/3-the-basics.md#classes)
    - [Interfaces](./sections/3-the-basics.md#interfaces)
    - [Type Aliases](./sections/3-the-basics.md#type-aliases)
        - [Type Aliases vs Interfaces](./sections/3-the-basics.md#type-aliases-vs-interfaces)
    - [Intersection Types](./sections/3-the-basics.md#intersection-types)
    - [Union Types](./sections/3-the-basics.md#union-types)
    - [Generics](./sections/3-the-basics.md#generics)
4. [Utility Types](./sections/4-utility-types.md)
    - [Partial](./sections/4-utility-types.md#partial)
    - [Required](./sections/4-utility-types.md#required)
    - [Readonly](./sections/4-utility-types.md#readonly)
    - [ReadonlyArray](./sections/4-utility-types.md#readonlyarray)
    - [Record](./sections/4-utility-types.md#record)
    - [Pick](./sections/4-utility-types.md#pick)
    - [Omit](./sections/4-utility-types.md#omit)
    - [Exclude](./sections/4-utility-types.md#exclude)
    - [Extract](./sections/4-utility-types.md#extract)
    - [NonNullable](./sections/4-utility-types.md#nonnullable)
    - [ReturnType](./sections/4-utility-types.md#returntype)
    - [InstanceType](./sections/4-utility-types.md#instancetype)
    - [NoInfer](./sections/4-utility-types.md#noinfer)
    - [Awaited](./sections/4-utility-types.md#awaited)
    - [ThisType](./sections/4-utility-types.md#thistype)
    - [ThisParameterType](./sections/4-utility-types.md#thisparametertype)
    - [OmitThisParameter](./sections/4-utility-types.md#omitthisparameter)
    - [Parameters](./sections/4-utility-types.md#parameters)
    - [ConstructorParameters](./sections/4-utility-types.md#constructorparameters)
    - [KeyOf](./sections/4-utility-types.md#keyof)
    - [ValuesType](./sections/4-utility-types.md#valuestype)
    - [String Manipulation Types](./sections/4-utility-types.md#string-manipulation-types)
        - [Capitalized](./sections/4-utility-types.md#capitalized)
        - [Lowercase](./sections/4-utility-types.md#lowercase)
        - [Uppercase](./sections/4-utility-types.md#uppercase)
        - [Uncapitalize](./sections/4-utility-types.md#uncapitalize)
5. [Advanced Topics](./sections/5-advanced-topics.md#advanced-topics)
    - [Mapped Types](./sections/5-advanced-topics.md#mapped-types)
    - [Conditional Types](./sections/5-advanced-topics.md#conditional-types)
    - [Template Literal Types](./sections/5-advanced-topics.md#template-literal-types)
    - [Recursive Types](./sections/5-advanced-topics.md#recursive-types)
    - [Type Inference](./sections/5-advanced-topics.md#type-inference)
    - [Type Narrowing](./sections/5-advanced-topics.md#type-narrowing)
        - [Type Casting](./sections/5-advanced-topics.md#type-casting)
            - [Casting Objects](./sections/5-advanced-topics.md#casting-objects)
        - [Type Guards](./sections/5-advanced-topics.md#type-guards)
        - [Type Predicates](./sections/5-advanced-topics.md#type-predicates)
        - [The `in` Operator](./sections/5-advanced-topics.md#the-in-operator)
    - [Type Reflection](./sections/5-advanced-topics.md#type-reflection)
    - [Type Compatibility](./sections/5-advanced-topics.md#type-compatibility)
    - [Overloading](./sections/5-advanced-topics.md#overloading)
    - [Mixins](./sections/5-advanced-topics.md#mixins)
    - [Decorators](./sections/5-advanced-topics.md#decorators)
    - [Modules](./sections/5-advanced-topics.md#modules)
    - [Namespaces](./sections/5-advanced-topics.md#namespaces)
6. [Best Practices](./sections/6-best-practices.md)
    - [Enforce Strict Typing](./sections/6-best-practices.md#enforce-strict-typing)
    - [Use Type Aliases and Interfaces Wisely](./sections/6-best-practices.md#use-type-aliases-and-interfaces-wisely)
    - [Avoid Excessive Use of `any`](./sections/6-best-practices.md#avoid-excessive-use-of-any)
    - [Use Readonly and Immutable Types](./sections/6-best-practices.md#use-readonly-and-immutable-types)
    - [Leverage Utility Types](./sections/6-best-practices.md#leverage-utility-types)
    - [Narrow Types Explicitly](./sections/6-best-practices.md#narrow-types-explicitly)
    - [Use `unknown` Over `any`](./sections/6-best-practices.md#use-unknown-over-any)
    - [Avoid Namespace Pollution](./sections/6-best-practices.md#avoid-namespace-pollution)
    - [Document Types and Functions](./sections/6-best-practices.md#document-types-and-functions)
    - [Keep `tsconfig.json` Clean](./sections/6-best-practices.md#keep-tsconfigjson-clean)
    - [Optimize `any` to `never` in Utility Scenarios](./sections/6-best-practices.md#optimize-any-to-never-in-utility-scenarios)
    - [Utilize ESLint and Prettier](./sections/6-best-practices.md#utilize-eslint-and-prettier)
    - [Ensure Backward Compatibility](./sections/6-best-practices.md#ensure-backward-compatibility)
7. [Advanced setup](./sections/7-advanced-setup.md)
8. [Conclusion](./sections/8-conclusion.md)
9. [Resources](./sections/9-resources.md)
10. [Contributing](#contributing)
11. [Code of Conduct](#code-of-conduct)
12. [License](#license)

---

## Contributing

Contributions are welcome! Please read the [contribution guidelines](./CONTRIBUTING.md) to get started.

## Code of Conduct

Please read our [code of conduct](./CODE_OF_CONDUCT.md) to understand our community standards.

## License

This project is licensed under the MIT License - see the [LICENSE](./LICENSE) file for details.
