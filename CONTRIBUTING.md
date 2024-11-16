# Contributing to **TS**Playbook

Thank you for considering contributing to **TSPlaybook**! Your support helps improve this resource for developers. This
guide outlines how to get started and contribute effectively.

---

## Table of Contents

1.  [Code of Conduct](#code-of-conduct)
2.  [Getting Started](#getting-started)
3.  [How to Contribute](#how-to-contribute)
    -   [Reporting Issues](#reporting-issues)
    -   [Submitting Improvements](#submitting-improvements)
    -   [Adding Examples or Exercises](#adding-examples-or-exercises)
    -   [Fixing Bugs](#fixing-bugs)
4.  [Style Guide](#style-guide)
5.  [Pull Request Process](#pull-request-process)

---

## Code of Conduct

By contributing, you agree to adhere to the project's [Code of Conduct](./CODE_OF_CONDUCT.md). Please ensure your
interactions remain respectful and collaborative.

---

## Getting Started

1.  Fork the repository by clicking the **Fork** button at the top right of the page.

2.  Clone your fork to your local machine:

```bash
git clone https://github.com/emiliodominguez/ts-playbook.git
```

3. Install the project dependencies:

```bash
cd ts-playbook
npm install
```

---

## How to Contribute

### Reporting Issues

If you encounter a bug, typo, or unclear section, create an issue with the following details:

-   A clear and descriptive title.
-   Steps to reproduce the issue (if applicable).
-   Suggestions for improvement (optional).

### Submitting Improvements

If you think a section can be clarified, expanded, or corrected:

1.  Propose changes in an issue first to avoid overlapping efforts.
2.  Provide a detailed explanation of the improvement.

### Adding Examples or Exercises

Want to make the guide more interactive?

-   Create concise examples that highlight TypeScript concepts.
-   Propose fun and engaging exercises that help reinforce learning.
-   Ensure examples follow the [Style Guide](#style-guide).

### Fixing Bugs

Found a bug in the code examples or documentation?

1.  Check for an open issue. If none exist, create one.
2.  Submit a pull request with the fix and a short explanation of the problem and resolution.

---

## Style Guide

To maintain consistency, adhere to these rules:

1.  **Code Formatting**:

    -   Use 4 spaces for indentation.
    -   Use double quotes for strings.
    -   Use camelCase for variable and function names.
    -   Use PascalCase for class names.
    -   Use `function` keyword for function declarations.
    -   Use `const` or `let` for variable declarations.

2.  **Writing Style**:

    -   Be clear and concise.
    -   Use proper markdown syntax.
    -   Avoid overly technical jargon; aim for accessibility.

3.  **Code Examples**:

    -   Use TypeScript syntax exclusively.
    -   Include comments where necessary.

---

## Pull Request Process

1.  Ensure your branch is up-to-date with the `main` branch:

```bash
git checkout main
git pull upstream main
```

2.  Create a new branch for your changes:

```bash
git checkout -b feature/my-new-feature
```

3.  Make your changes and test them locally.
4.  Commit your changes:

```bash
git commit -m "Brief description of changes"
```

5.  Push your branch to your fork:

```bash
git push origin feature/my-new-feature
```

6.  Open a pull request on the main repository, linking to any related issues.

---

Thank you for helping improve **TSPlaybook**! Together, we can make this the best resource for learning TypeScript. 🌟
