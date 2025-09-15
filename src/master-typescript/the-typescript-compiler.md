# The TypeScript Compiler

## Init and Compile

First, we can hit the init command to create the `tsconfig.json` file. Then we can compile the files on watch mode.

```bash
tsc --init

# compile only the selected file
tsc index.ts -w

# all the .ts files will be compiled by default
tsc -w
```

## Configurations

- files: Specifies an allowlist of files to include in the program
- include: Specifies an array of filenames or patterns to include in the program
- exclude: Specifies an array of filenames or patterns that should be skipped when resolving include.
- (Priority: files > exclude > include)
- outDir: If specified, .js (as well as .d.ts, .js.map, etc.) files will be emitted into this directory. The directory structure of the original source files is preserved.
- target: governs the JavaScript version of output that TypeScript compiles into.
- lib: specify the libs that TS can access the types

```ts
{
  "compilerOptions": {
    "outDir": "dist",
    "target": "es5",
    "lib": [
      "DOM",
      "es2021
    ]
  },
  "files": ["mustRun.test.ts", "shouldRun.test.ts"],
  "include": ["src/**/*.?(ts|tsx)"],
  "exclude": ["src/**/*.test.ts"]
```
