# tsup-template

Create a JavaScript package that properly supports ESM:

> [!NOTE]
> Although v20 is in maintenance mode (…) an exception was made to backport `require(esm)` due to its importance and impact on the ecosystem. — [Node v20.19.0 (LTS)](https://nodejs.org/en/blog/release/v20.19.0)

## Quick Start

1. [Use this template] to create a new repository.
2. Clone the repository and install dependencies.
3. Write library code in the `/src/index.ts` file.
4. [Set package data](#set-package-data) in the `package.json` file.

[Use this template]: https://github.com/new?template_name=tsup-template&template_owner=hyunbinseo

```shell
npm version patch # [<newversion> | major | minor | patch | premajor | ... ]
npm publish # the package is newly built and linted before it gets published.
```

## Set Package Data

Reference the [npm Docs](https://docs.npmjs.com/cli/v10/configuring-npm/package-json) for the full list

```jsonc
// package.json
{
  "name": "name",
  "description": "description",
  // ...
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
      "types": "./dist/index.d.ts",
      "default": "./dist/index.js"
    },
    // Add subpath export as relative paths
    "./nested": {
      "types": "./dist/nested/index.d.ts",
      "default": "./dist/nested/index.js"
    }
  }
}
```

## Set Lifecycle Scripts

Automate package versioning tasks. Reference the [npm documentation].

[npm documentation]: https://docs.npmjs.com/cli/v10/commands/npm-version#description

```jsonc
{
  "scripts": {
    // `npm version` order of execution:

    // 1. Check to make sure the git working directory is clean.

    // 2. Run the `preversion` script.
    "preversion": "npm test", // These scripts have access to the old `version` in package.json.

    // 3. Bump `version` in `package.json` as requested.

    // 4. Run the `version` script.
    "version": "npm run build && git add -A dist", // These scripts have access to the new `version` in package.json

    // 5. Commit and tag.

    // 6. Run the `postversion` script.
    "postversion": "git push && git push --tags" // Use it to clean up the file system or automatically push the commit and/or tag.
  }
}
```
