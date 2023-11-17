Shows that linting does not happen.

Do the normal `npm i`, then try an `npm run lint`:

```
╭─ken@Kens-MBP.localdomain ~/Projects/Tutorials/bad-linty-linty  ‹main*›
╰─➤  npm run lint                                                                                                               2 ↵

> bad-linty-linty@0.0.1 lint
> eslint
```

OK, that's nice, but it didn't actually do anything. I know this because `cypress.config.ts` does not lint out of the box.

Try it, though, and you will get:

```
╭─ken@Kens-MBP.localdomain ~/Projects/Tutorials/bad-linty-linty  ‹main*›
╰─➤  npm run lint cypress.config.ts                                                                                             2 ↵

> bad-linty-linty@0.0.1 lint
> eslint cypress.config.ts


Oops! Something went wrong! :(

ESLint: 8.53.0

Error [ERR_REQUIRE_ESM]: require() of ES Module /Users/ken/Projects/Tutorials/bad-linty-linty/.eslintrc.js from /Users/ken/Projects/Tutorials/bad-linty-linty/node_modules/@eslint/eslintrc/dist/eslintrc.cjs not supported.
.eslintrc.js is treated as an ES module file as it is a .js file whose nearest parent package.json contains "type": "module" which declares all .js files in that package scope as ES modules.
Instead rename .eslintrc.js to end in .cjs, change the requiring code to use dynamic import() which is available in all CommonJS modules, or change "type": "module" to "type": "commonjs" in /Users/ken/Projects/Tutorials/bad-linty-linty/package.json to treat all .js files as CommonJS (using .mjs for all ES modules instead).
```

That is easy enough to fix:

```
╭─ken@Kens-MBP.localdomain ~/Projects/Tutorials/bad-linty-linty  ‹main*›
╰─➤  mv .eslintrc.js .eslintrc.cjs
╭─ken@Kens-MBP.localdomain ~/Projects/Tutorials/bad-linty-linty  ‹main*›
╰─➤  npm run lint cypress.config.ts

> bad-linty-linty@0.0.1 lint
> eslint cypress.config.ts

=============

WARNING: You are currently running a version of TypeScript which is not officially supported by @typescript-eslint/typescript-estree.

You may find that it works just fine, or you may not.

SUPPORTED TYPESCRIPT VERSIONS: >=3.3.1 <5.2.0

YOUR TYPESCRIPT VERSION: 5.2.2

Please only submit bug reports when using the officially supported version.

=============

/Users/ken/Projects/Tutorials/bad-linty-linty/cypress.config.ts
  10:21  warning  'on' is defined but never used      @typescript-eslint/no-unused-vars
  10:25  warning  'config' is defined but never used  @typescript-eslint/no-unused-vars

✖ 2 problems (0 errors, 2 warnings)
```

What is needed is:

- do the above `mv`
- add a `.eslintignore` file
- fix the `package.json` to do an `eslint .` for the lint command

You can see these mods in place by doing `git checkout good-linty-linty` and then running `npm run lint`


