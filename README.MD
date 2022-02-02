# Rename Plugin

Rollup plugin to take modules from RollUp and rename their file name. Useful for when using `preserveModules`. The plugin will also parse
all modules code and rewrite imports/exports to match the new file name.

## Installation

```bash
npm i --save-dev rollup-plugin-rename
```

## Usage

```js
import rename from '@betit/rollup-plugin-rename';

// Rollup Configuration
export default {
    input: './src/index.js',
    preserveModules: true,
    /* ... */
    plugins: [
        // ...
        rename({
            include: ['**/*.ts', '**/*.vue'],
            map: (name) => name.replace('src/', 'source/'),
        })
    ],
},
```

## Options

```typescript
export interface IRenameExtensionsOptions {
    /**
     * Files to include for potential renames.
     * Also denotes files of which may import a renamed module in
     * order to update their imports.
     */
    include?: Array<string | RegExp> | string | RegExp | null;

    /**
     * Files to explicitly exclude
     */
    exclude?: Array<string | RegExp> | string | RegExp | null;

    /**
     * Generate source maps for the transformations.
     */
    sourceMap?: boolean;

    /**
     * Object describing the transformations to use.
     * IE. Input name => Output name.
     * Extensions should include the dot for both input and output.
     */
    map: (name: string) => string;


    /**
     * An acorn.Options object.
     * This option will extend the default:
     * `{ ecmaVersion: 6, sourceType: 'module' }`
     * Provide it if you do not transpile any es7+ features
     * @see https://github.com/acornjs/acorn/blob/master/acorn/src/options.js
     * @see https://github.com/acornjs/acorn/blob/9899904395d67776a78702fe5640ea4bc12b9ec6/acorn/dist/acorn.d.ts#L14
     */
    parserOptions?: acorn.Options;
}
```
