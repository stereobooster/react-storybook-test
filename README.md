This project was bootstrapped with [Create React App](https://github.com/facebook/create-react-app).

From [manual](https://github.com/storybooks/storybook/blob/master/MIGRATION.md#create-react-app)

> create-react-app@2 should be compatible as is, since it uses babel 7.

### Attempt 1

```
npx storybook
yarn storybook

ERR! Error: Cannot find module 'babel-loader/package.json' from 'react-storybook-test'
ERR!     at module.exports (react-storybook-test/node_modules/resolve/lib/sync.js:43:15)
ERR!     at isBabelLoader8 (react-storybook-test/node_modules/@storybook/core/dist/server/loadCustomBabelConfig.js:68:52)
ERR!     at _default (react-storybook-test/node_modules/@storybook/core/dist/server/loadCustomBabelConfig.js:88:10)
ERR!     at Object.babel (react-storybook-test/node_modules/@storybook/core/dist/server/core-preset-dev.js:36:45)
ERR!     at accumulationPromise.then.newConfig (react-storybook-test/node_modules/@storybook/core/dist/server/presets.js:73:72)
ERR!     at process._tickCallback (internal/process/next_tick.js:68:7)
ERR!  { Error: Cannot find module 'babel-loader/package.json' from 'react-storybook-test'
ERR!     at module.exports (react-storybook-test/node_modules/resolve/lib/sync.js:43:15)
ERR!     at isBabelLoader8 (react-storybook-test/node_modules/@storybook/core/dist/server/loadCustomBabelConfig.js:68:52)
ERR!     at _default (react-storybook-test/node_modules/@storybook/core/dist/server/loadCustomBabelConfig.js:88:10)
ERR!     at Object.babel (react-storybook-test/node_modules/@storybook/core/dist/server/core-preset-dev.js:36:45)
ERR!     at accumulationPromise.then.newConfig (react-storybook-test/node_modules/@storybook/core/dist/server/presets.js:73:72)
ERR!     at process._tickCallback (internal/process/next_tick.js:68:7)
ERR!   stack:
ERR!    'Error: Cannot find module \'babel-loader/package.json\' from \'react-storybook-test\'\n    at module.exports (react-storybook-test/node_modules/resolve/lib/sync.js:43:15)\n    at isBabelLoader8 (react-storybook-test/node_modules/@storybook/core/dist/server/loadCustomBabelConfig.js:68:52)\n    at _default (react-storybook-test/node_modules/@storybook/core/dist/server/loadCustomBabelConfig.js:88:10)\n    at Object.babel (react-storybook-test/node_modules/@storybook/core/dist/server/core-preset-dev.js:36:45)\n    at accumulationPromise.then.newConfig (react-storybook-test/node_modules/@storybook/core/dist/server/presets.js:73:72)\n    at process._tickCallback (internal/process/next_tick.js:68:7)',
ERR!   code: 'MODULE_NOT_FOUND' }
✨  Done in 2.96s.
```

Broken :(

```
yarn add babel-loader@8
yarn storybook
```

Works :)

### Attempt 2

Add dynamic import `import("./locales/en.js");`

```
yarn storybook

ERROR in ./src/App.js
Module build failed (from ./node_modules/babel-loader/lib/index.js):
SyntaxError: /Users/slavik/my/react-storybook-test/src/App.js: Support for the experimental syntax 'dynamicImport' isn't currently enabled (5:1):
```

Broken :(

```
yarn add @babel/plugin-syntax-dynamic-import
```

Add `.storybook/.babelrc`

```json
{
  "presets": ["@babel/preset-env", "@babel/preset-react"],
  "plugins": ["@babel/plugin-syntax-dynamic-import"]
}
```

Works :)
