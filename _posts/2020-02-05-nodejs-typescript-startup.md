---
title: "Node + TypeScript Startup"
categories:
  - Blog
tags:
  - NodeJs,TypeScript
---
**Node + TypeScript starter**

**Prequisites**

- Node + npm installed

**Goals**

In this guide, I'll walk you through the process of creating a basic TypeScript application and compling it. It's   actually really easy!

>[View the source](https://github.com/chendu/node-ts-starter-all/tree/main/node-ts-starter)

**Initial Setup**

```shell
mkdir node-ts-starter
cd node-ts-starter
```

Next, setup `project.json` and add dependencies

**Setup Node.js package.json**

Using `-y`flag when create `package.json` will approve all the defaults.

```shell
npm init -y
```

**Add TypeScript as a dev dependency**

```shell
npm install typescript --save-dev
```

> This command to revert back to default npm registry
>
> ```shell
> npm config set registry https://registry.npmjs.org/
> ```

**Install ambient Node.js types for TypeScript**

TypeScript has Implicit, Explicit, and *Ambient* types. Ambient types are types that get added to the global execution scope. Since using Node, it would be good if we could get type safety and auto-compiletion on the Node apis like `file`,`path`,`process`, etc. That is what installing the [DefinitelyTyped](https://github.com/DefinitelyTyped/DefinitelyTyped) type definition for Node will do.

```shell
npm install --save-dev @types/node
```

**Create a `tsconfig.json`**

The `tsconfig.json`is where we define the TypeScript compiler options. We can create a tsconfig with serveral options set.

```shell
npx tsc --init --rootDir src --outDir build \
--esModuleInterop --resolveJsonModule --lib es6 \
--module commonjs --allowJs true --noImplicitAny true
```

> - `rootDir` : Where TypeScript looks for our code.
> - `outDir` : Where TypeScript puts our compiled code.
> - `esModuleInterop` : If we're using `commonjs` as our module system (for Node apps, you should be), then we need this to be set to `true`.
> - `resolveJsonModule` : If use JSON in project, this option allows TypeScript o use it.
> - `lib` : This option adds ambient types to project, allowing us to rely on features from different Ecmascript versions, testing library, and even the browser DOM api. We'd like to utilize some `es6` language featurtes. This all get gets compiled down to `es5`.
> - `allowJs` : If you're converting and old JavaScript project to TypeScript one, this option will alow you to include `.js` files among `.ts` ones.
> - `noImplicitAny` : In TypeScript files, don't allow a type to be unexplicitly specified. Every type need to either have a specific type or be explicitly declared `any`. No implicit `any`s.
> - Others - for more details compier options can refer to below comments in generated json file.

At this point, you should have a `tsconfig.json` looks like this:

```
{
  "compilerOptions": {
    /* Visit https://aka.ms/tsconfig.json to read more about this file */

    /* Basic Options */
    // "incremental": true,                   /* Enable incremental compilation */
    "target": "es5",                          /* Specify ECMAScript target version: 'ES3' (default), 'ES5', 'ES2015', 'ES2016', 'ES2017', 'ES2018', 'ES2019', 'ES2020', or 'ESNEXT'. */
    "module": "commonjs",                     /* Specify module code generation: 'none', 'commonjs', 'amd', 'system', 'umd', 'es2015', 'es2020', or 'ESNext'. */
    "lib": ["es6"],                           /* Specify library files to be included in the compilation. */
    "allowJs": true,                          /* Allow javascript files to be compiled. */
    // "checkJs": true,                       /* Report errors in .js files. */
    // "jsx": "preserve",                     /* Specify JSX code generation: 'preserve', 'react-native', or 'react'. */
    // "declaration": true,                   /* Generates corresponding '.d.ts' file. */
    // "declarationMap": true,                /* Generates a sourcemap for each corresponding '.d.ts' file. */
    // "sourceMap": true,                     /* Generates corresponding '.map' file. */
    // "outFile": "./",                       /* Concatenate and emit output to single file. */
    "outDir": "build",                        /* Redirect output structure to the directory. */
    "rootDir": "src",                         /* Specify the root directory of input files. Use to control the output directory structure with --outDir. */
    // "composite": true,                     /* Enable project compilation */
    // "tsBuildInfoFile": "./",               /* Specify file to store incremental compilation information */
    // "removeComments": true,                /* Do not emit comments to output. */
    // "noEmit": true,                        /* Do not emit outputs. */
    // "importHelpers": true,                 /* Import emit helpers from 'tslib'. */
    // "downlevelIteration": true,            /* Provide full support for iterables in 'for-of', spread, and destructuring when targeting 'ES5' or 'ES3'. */
    // "isolatedModules": true,               /* Transpile each file as a separate module (similar to 'ts.transpileModule'). */

    /* Strict Type-Checking Options */
    "strict": true,                           /* Enable all strict type-checking options. */
    "noImplicitAny": true,                    /* Raise error on expressions and declarations with an implied 'any' type. */
    // "strictNullChecks": true,              /* Enable strict null checks. */
    // "strictFunctionTypes": true,           /* Enable strict checking of function types. */
    // "strictBindCallApply": true,           /* Enable strict 'bind', 'call', and 'apply' methods on functions. */
    // "strictPropertyInitialization": true,  /* Enable strict checking of property initialization in classes. */
    // "noImplicitThis": true,                /* Raise error on 'this' expressions with an implied 'any' type. */
    // "alwaysStrict": true,                  /* Parse in strict mode and emit "use strict" for each source file. */

    /* Additional Checks */
    // "noUnusedLocals": true,                /* Report errors on unused locals. */
    // "noUnusedParameters": true,            /* Report errors on unused parameters. */
    // "noImplicitReturns": true,             /* Report error when not all code paths in function return a value. */
    // "noFallthroughCasesInSwitch": true,    /* Report errors for fallthrough cases in switch statement. */
    // "noUncheckedIndexedAccess": true,      /* Include 'undefined' in index signature results */

    /* Module Resolution Options */
    // "moduleResolution": "node",            /* Specify module resolution strategy: 'node' (Node.js) or 'classic' (TypeScript pre-1.6). */
    // "baseUrl": "./",                       /* Base directory to resolve non-absolute module names. */
    // "paths": {},                           /* A series of entries which re-map imports to lookup locations relative to the 'baseUrl'. */
    // "rootDirs": [],                        /* List of root folders whose combined content represents the structure of the project at runtime. */
    // "typeRoots": [],                       /* List of folders to include type definitions from. */
    // "types": [],                           /* Type declaration files to be included in compilation. */
    // "allowSyntheticDefaultImports": true,  /* Allow default imports from modules with no default export. This does not affect code emit, just typechecking. */
    "esModuleInterop": true,                  /* Enables emit interoperability between CommonJS and ES Modules via creation of namespace objects for all imports. Implies 'allowSyntheticDefaultImports'. */
    // "preserveSymlinks": true,              /* Do not resolve the real path of symlinks. */
    // "allowUmdGlobalAccess": true,          /* Allow accessing UMD globals from modules. */

    /* Source Map Options */
    // "sourceRoot": "",                      /* Specify the location where debugger should locate TypeScript files instead of source locations. */
    // "mapRoot": "",                         /* Specify the location where debugger should locate map files instead of generated locations. */
    // "inlineSourceMap": true,               /* Emit a single file with source maps instead of having a separate file. */
    // "inlineSources": true,                 /* Emit the source alongside the sourcemaps within a single file; requires '--inlineSourceMap' or '--sourceMap' to be set. */

    /* Experimental Options */
    // "experimentalDecorators": true,        /* Enables experimental support for ES7 decorators. */
    // "emitDecoratorMetadata": true,         /* Enables experimental support for emitting type metadata for decorators. */

    /* Advanced Options */
    "resolveJsonModule": true,                /* Include modules imported with '.json' extension */
    "skipLibCheck": true,                     /* Skip type checking of declaration files. */
    "forceConsistentCasingInFileNames": true  /* Disallow inconsistently-cased references to the same file. */
  }
}

```

We're set to run our first TypeScript file.

**Create `src` folder and create the first TypeScirpt file**

```shell
mkdir src
touch src/index.ts
```

And write some code.

```typescript
console.log('Hello World!');
```

**Compiling TypeScript**

To compile the code, need to run `tsc` command using `npx`, which is the Node package executer. `tsc` will read the `tsconfig.json` in current directory, and apply the configuration against the TypeScript compiler to generate the compiled JavaScript code.

```shell
npx tsc
```

**Compiled code**

Check out `build/index.js`, we've compiled our first TypeScript file.

```javascript
"use strict";
console.log('Hello World!');
```

---

**Useful configurations & scripts**

**Code reloading as dev dependency**

Code reloading is a nice for local development. In order to do this, we'll need to rely on a couple more packages: `ts-node`(refer to [ts-node](https://www.npmjs.com/package/ts-node)) for running TypeScript code directly without having to wait for it be compiled, and `nodemon` (refer to [nodemon](https://www.npmjs.com/package/nodemon)), to watch for changes to local code and automatically restart when a file is changed.

> Aboud ts-node
>
> > TypeScript execution and REPL for node.js, with source map support. **Works with `typescript@>=2.7`**.
> >
> > ```shell
> > # Execute a script as `node` + `tsc`.
> > ts-node script.ts
> > # Starts a TypeScript REPL.
> > ts-node
> > ```
>
> About nodemon
>
> > nodemon is a tool that helps develop node.js based applications by automatically restarting the node application when file changes in the directory are detected.
> >
> > nodemon does **not** require *any* additional changes to your code or method of development. nodemon is a replacement wrapper for `node`. To use `nodemon`, replace the word `node` on the command line when executing your script.

```shell
npm install --save-dev ts-node nodemon
```

Add a `nodemon.json` configuration file.

```shell
touch nodemon.json
```

Add below content

```
{
	"watch": ["src, /* by default nodemon monitors the current working directory, use this to add specific paths*/
	"ext": ".ts,.js", /* specify extentions watch list */
	"ignore": [], /* ignoring files */
	"exec": "ts-node ./src/index.ts" /* execute some scripts*/
}
```

And then to run this project, all we have to do is run `nodemon`. Let's add a script for that:

```json
"start:dev": "nodemon",
```

By running `nom run start:dev`, `nodemon` will start out app using command `ts-node ./src/index.ts`, watching for changes to `.ts` and `.js` files from within `/src`.

**Creating productions builds**

In order to clen and compile the project for production, we can add a `build` script.

Install `rimraf`(refer to [rimraf](https://www.npmjs.com/package/rimraf), a cross-platform tool that acts like the `rm -rf` command (just obliterates whatever you tell it to).

```shell
npm install --save-dev rimraf
```

And then, add this to your `package.json`. scripts part.

```
"scripts": {
  "build": "rimraf ./build && tsc",
  ...
}
```

Noow, when we run `npm run build`, `rimraf` will remove our old `build` folder before the TypeScript compiler emits new code to `dist` folder.

**Production startup script**

In order to start the app in production, all we need to do is run the `build` command first, and then execute the compiled JavsScript at `build/index.js`.

The startup script looks like this.

```
"scripts": {
  "start": "npm run build && node build/index.js",
  ...
}
```

I told you it was simple!

---

 **Scripts overview**

```shell
npm run start:dev
```

Starts the application in development using `nodemon` and final run `ts-node ./src/index.ts` command to do cold reloading.

```shell
npm run build
```

Build the app at `build`, lceaning the folder first.

```shell
np9m run start
```

Starts the app in production by first building the project with `npm run build`, and then executing the compiled JavaScript at `build/index.js`.

**Linting**

Linting is another thing you'll mostly likely want to do. If you'are interested in that, reading the next post, [How to use ESLint with Typescript]().

