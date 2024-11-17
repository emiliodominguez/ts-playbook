# **Getting Started**

Before you start learning TypeScript, you need to set up your development environment. This section will guide you
through the installation, configuration, and editor setup to get you up and running with TypeScript.

## **Installation**

To get started with TypeScript and follow along with this playbook, you need to have Node.js installed on your machine.
You can download and install Node.js from the [official website](https://nodejs.org/).

Once you have Node.js installed, you can install TypeScript globally or locally using your preferred package manager. In
this guide, we will use `npm` to install TypeScript.

To install TypeScript globally, you can run the following command in your terminal:

```bash
npm install -g typescript
```

You can verify the installation by checking the version of TypeScript installed on your machine:

```bash
tsc --version
```

This will display the version of TypeScript installed. If you see the version number, TypeScript is successfully
installed on your machine, and you are ready to start learning.

## **Project Setup**

To create a new TypeScript project, you need to initialize a new Node.js project using npm. Open your terminal and run
the following command to create a new directory for your project:

```bash
mkdir my-ts-project
cd my-ts-project
```

Next, run the following command to initialize a new Node.js project:

```bash
npm init -y
```

This will create a `package.json` file in your project directory. Now, you can either use the previously globally
installed TypeScript dependency or install it locally in your project. The recommended approach is to install TypeScript
locally in your project to ensure that the project dependencies are isolated and consistent across different
environments.

Run the following command to install TypeScript locally:

```bash
npm install -D typescript
```

This will add TypeScript as a development dependency in your project. You can now create a new TypeScript file (e.g.,
`src/index.ts`) in your project directory and start writing TypeScript code.

## **Configuration**

TypeScript uses a `tsconfig.json` file to configure the TypeScript compiler options for your project. You can initialize
a new `tsconfig.json` file using the following instructions.

If you have installed TypeScript globally, you can run:

```bash
tsc --init
```

Otherwise, if you have installed TypeScript locally in your project, you can run:

```bash
npx tsc --init
```

If, for some reason, you want to create the `tsconfig.json` file manually, you can create it in the root of your project
directory and add the necessary compiler options.

If you created the configuration file using the CLI tool, you'll notice that it was created with a set of default
compiler options with comments explaining each option. You can customize these options based on your project
requirements. Here is an example of a basic `tsconfig.json` file:

```json
{
    "compilerOptions": {
        "target": "ESNext",
        "module": "commonjs",
        "esModuleInterop": true,
        "forceConsistentCasingInFileNames": true,
        "strict": true,
        "skipLibCheck": true
    },
    "exclude": ["node_modules"]
}
```

For a complete list of compiler options, you can refer to the
[official documentation](https://www.typescriptlang.org/tsconfig).

Now, let's add some scripts to the `package.json` file to compile TypeScript files using the TypeScript compiler. Open
the `package.json` file and add the following scripts:

```json
{
    // ...
    "scripts": {
        "tsc:build": "tsc",
        "tsc:watch": "tsc -w"
    }
    // ...
}
```

These scripts will allow you to compile TypeScript files using the TypeScript compiler. The `tsc:build` script compiles
the TypeScript files once, while the `tsc:watch` script watches for changes in the files and recompiles them
automatically.

Now, if you haven't already, let's create a simple TypeScript file (`src/index.ts`) with the following code:

```typescript
const message: string = "Hello, TypeScript!";
console.log(message);
```

You can compile the TypeScript file using the following command:

```bash
npm run tsc:build
```

This will compile the TypeScript file and generate a JavaScript file (`src/index.js`) in the same directory. You can run
the JavaScript file using Node.js to see the output:

```bash
node src/index.js
```

If you want to watch for changes in the TypeScript files and recompile them automatically, you can run the following
command:

```bash
npm run tsc:watch
```

This will watch for changes in the TypeScript files and recompile them whenever you save the file.

Additionally, you can add some more scripts to the `package.json` file to run the compiled JavaScript files using
Node.js. Let's update the `package.json` file with the following scripts:

```json
{
    // ...
    "scripts": {
        "start": "node src/index.js",
        "dev": "node --watch src/index.js",
        "tsc:build": "tsc",
        "tsc:watch": "tsc -w"
    }
    // ...
}
```

Now you can open two terminal windows and run the following commands in each terminal:

```bash
npm run tsc:watch
```

```bash
npm run dev
```

Try making some changes to the TypeScript file and see the changes reflected in the output.

This will work for now to follow along with the playbook and keeping it simple. As we move forward, we will explore more
advanced, scalable and efficient ways to set up your TypeScript projects.

## **Editor Setup**

To enhance your development experience with TypeScript, you can use an editor that provides TypeScript support, such as
Visual Studio Code. Visual Studio Code is a popular code editor that offers built-in support for TypeScript, including
syntax highlighting, code completion, and error checking. It also provides integration with the TypeScript compiler and
debugging tools. You can download Visual Studio Code from the [official website](https://code.visualstudio.com/).

### **Useful Extensions**

Visual Studio Code has a rich ecosystem of extensions that can enhance your TypeScript development experience. Here are
some useful extensions for working with TypeScript:

-   [ESLint](https://marketplace.visualstudio.com/items?itemName=dbaeumer.vscode-eslint): Integrates ESLint into Visual
    Studio Code for linting your TypeScript code.
-   [Prettier](https://marketplace.visualstudio.com/items?itemName=esbenp.prettier-vscode): Code formatter that supports
    TypeScript and helps maintain consistent code style.
-   [Jest](https://marketplace.visualstudio.com/items?itemName=Orta.vscode-jest): Provides integration with Jest for
    testing your TypeScript code.
-   [Path Intellisense](https://marketplace.visualstudio.com/items?itemName=christian-kohler.path-intellisense):
    Autocompletes filenames in your TypeScript code.
-   [Total TypeScript](https://marketplace.visualstudio.com/items?itemName=mattpocock.ts-error-translator): Provides
    TypeScript language features and tools. Additionaly it can translate TypeScript errors to plain English and provide
    concise explanations about TypeScript features with examples and links to the official documentation. In my personal
    experience this is a must-have extension for TypeScript developers.

You can install these extensions from the Visual Studio Code marketplace to improve your TypeScript development
workflow.
