# Introduction

`import-js` is a vim plugin that simplifies your CommonJS project by
automatically resolving variables in a `require` statement. Use it by placing
the cursor on a variable, then hit `<leader>j` to import it at the top of the
file.

## Example

Let's say that you have a project with the following setup:

```
.
|-- index.html
|-- components
|     |-- button.js
|     |-- icon.js
|-- vendor
|     |--
|-- pages
|     |-- index.js
```

Now, you open pages/index.js to edit in Vim. It currently looks like this:

```js
document.createElement(new Button({ text: 'Save' }).toDOMElement());
```

At this point, `Button` is undefined, we need to import it. You begin by
placing your cursor on "Button". Then hit `<leader>j`. The Vim buffer changes to the following:

```js
var Button = require('components/button');
document.createElement(new Button({ text: 'Save' }).toDOMElement());
```

There, you just saved yourself having to type ~40 characters!

## Things to note

- Only files ending in .js\* are considered when importing
- All imports are expressed on one line each, starting with `var`
- As part of resolving an import, all imports will be sorted

## Configuration

Drop a file called `.importjs` in the root folder of your project to configure
import-js. This file is a YAML file, and has the following configuration
options.

### `lookup_paths`

Configure where import-js should look to resolve imports. If you are using
Webpack, these should match the `modulesDirectories` configuration. Example:

```yaml
lookup_paths:
  - 'app/assets/javascripts'
  - 'vendor/bower_components'
```

Happy hacking!