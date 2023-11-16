# tsup-template

Create a JavaScript package that fully supports ESM and CJS - [example](https://arethetypeswrong.github.io/?p=new-request%400.0.2)

## Quick Start

1. Click the `Use this template` button
2. Clone the newly created repository
3. `npm i` — install the dependencies
4. [Set package data](#set-package-data) in `package.json`
5. Write library code in `/src/index.ts`
6. `npm version` — [bump package version](https://docs.npmjs.com/cli/v10/commands/npm-version)
7. `npm run publish` — clean / build / publish

## Set Package Data

Reference the [npm Docs](https://docs.npmjs.com/cli/v10/configuring-npm/package-json) for the full list

```jsonc
// package.json
{
  // ..
  "name": "name",
  "description": "description",
  "keywords": ["keyword"],
  "author": "author",
  "license": "license",
  "repository": {
    "type": "git",
    "url": "git+https://github.com/username/project-name.git"
  },
  "bugs": {
    "url": "https://github.com/username/project-name/issues"
  },
  "homepage": "https://github.com/username/project-name#readme"
}
```

## Subpath Exports

Modules can be exported from files other than `src/index.ts`

```jsonc
// package.json
// Requires Node.js >=12
{
  // ..
  "tsup": {
    // Add a new entry point
    "entry": ["src/index.ts", "src/nested/index.ts"]
  },
  "exports": {
    ".": {
      "import": "./dist/index.js",
      "require": "./dist/index.cjs"
    },
    // Add subpath export as relative paths
    "./nested": {
      "import": "./dist/nested/index.js",
      "require": "./dist/nested/index.cjs"
    }
  }
}
```
