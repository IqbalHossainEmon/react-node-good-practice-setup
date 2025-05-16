# This is a temporary solution :)
## Table of Contents

-   [Plugins](#plugins)
-   [Settings](#settings)
-   [Install Dev Dependencies](#install-dev-dependencies)
-   [Linting Configuration file manually](#linting-configuration-file-manually)

### Plugins

You need to install the below plugins:

-   ESLint by Dirk Baeumer
-   Prettier - Code formatter by Prettier

### Settings

Follow the below settings for VS Code -

1. Create a new folder called ".vscode" inside the project root folder
2. Create a new file called "settings.json" inside that folder.
3. Paste the below json in the newly created settings.json file and save the file.

```json
{
    /* config related to code formatting */
    "editor.defaultFormatter": "esbenp.prettier-vscode",
    "editor.formatOnSave": true,
    "[javascript]": {
        "editor.formatOnSave": false,
        "editor.defaultFormatter": null
    },
    "[javascriptreact]": {
        "editor.formatOnSave": false,
        "editor.defaultFormatter": null
    },
    "javascript.validate.enable": false, /* disable all built-in syntax checking */
    "editor.codeActionsOnSave": {
        "source.fixAll.eslint": true,
        "source.fixAll.tslint": true,
        "source.organizeImports": true
    },
    "eslint.alwaysShowStatus": true,
    /* emmet */
    "emmet.triggerExpansionOnTab": true,
    "emmet.includeLanguages": {
        "javascript": "javascriptreact"
    }
}
```
## Linting Setup

### Install Dev Dependencies
__React__

```
npm install prettier eslint-plugin-prettier eslint-config-prettier eslint-config-airbnb eslint-plugin-jsx-a11y eslint-plugin-import --save-dev --legacy-peer-deps
```
___
__Node__

```
npm init -y & npm i -D eslint-config-prettier eslint-plugin-prettier prettier
```
```
npm init @eslint/config
```




### Linting Configuration file manually

Change the `eslint.config.js` file in the project root with the below contents:

__React__
```javascript
import { FlatCompat } from '@eslint/eslintrc';
import js from '@eslint/js';
import prettierConfig from 'eslint-config-prettier';
import jsxA11y from 'eslint-plugin-jsx-a11y';
import prettierPlugin from 'eslint-plugin-prettier';
import react from 'eslint-plugin-react';
import reactHooks from 'eslint-plugin-react-hooks';
import reactRefresh from 'eslint-plugin-react-refresh';
import globals from 'globals';
import path from 'node:path';
import { fileURLToPath } from 'node:url';
import prettier from 'prettier';

const filename = fileURLToPath(import.meta.url);
const dirname = path.dirname(filename);
const compat = new FlatCompat({
	baseDirectory: dirname,
	recommendedConfig: js.configs.recommended,
	allConfig: js.configs.all,
});

export default [
	{ ignores: ['dist'] },
	...compat.extends('airbnb', 'airbnb/hooks'),
	{
		files: ['**/*.{js,jsx}'],
		languageOptions: {
			ecmaVersion: 'latest',
			globals: globals.browser,
			parserOptions: {
				ecmaVersion: 'latest',
				ecmaFeatures: { jsx: true },
				sourceType: 'module',
			},
		},
		settings: { react: { version: '18.3' } },
		plugins: {
			react,
			'react-hooks': reactHooks,
			'react-refresh': reactRefresh,
			'jsx-a11y': jsxA11y,
			prettier: prettierPlugin,
		},
		rules: {
			...js.configs.recommended.rules,
			...react.configs.recommended.rules,
			...react.configs['jsx-runtime'].rules,
			...reactHooks.configs.recommended.rules,
			...prettier.rules,
			...jsxA11y.configs.recommended.rules,
			...prettierConfig.rules,
			'prettier/prettier': [
				'error',
				{
					trailingComma: 'es5',
					singleQuote: true,
					jsxSingleQuote: true,
					printWidth: 100,
					tabWidth: 4,
					useTabs: true,
					semi: true,
					endOfLine: 'auto',
					arrowParens: 'avoid',
				},
			],
			'one-var': ['error', { initialized: 'never' }],
			'react/prop-types': 'off',
			'react/jsx-no-target-blank': 'off',
			'react-refresh/only-export-components': ['warn', { allowConstantExport: true }],
			'import/no-named-as-default': 'off',
			'import/no-named-as-default-member': 'off',
			'import/no-amd': 'off',
			'import/no-mutable-exports': 'off',
			'import/newline-after-import': 'off',
			'import/no-extraneous-dependencies': ['error', { devDependencies: true }],
		},
	},
];
```

[Bonus] If your snippets, auto imports and other vs code feature not working properly then create a `jsconfig.json` file in the root of your project and enter the below contents:

```json
{
	"compilerOptions": {
		"jsx": "react",
		"module": "esnext",
		"target": "es6",
		"moduleResolution": "node"
	},
	"exclude": ["node_modules", "build"],
	"include": ["src/**/*"]
}
```

__Node__
```json
import js from '@eslint/js';
import globals from 'globals';
import prettier from 'eslint-plugin-prettier';
import eslintConfigPrettier from 'eslint-config-prettier';
import { defineConfig } from 'eslint/config';

export default defineConfig([
	{
		files: ['**/*.{js,mjs,cjs}'],
		plugins: {
			js,
			prettier,
		},
		rules: {
			'no-console': 'off',
			indent: 'off',
			'linebreak-style': 'off',
			'no-nested-ternary': 'off',
			'no-underscore-dangle': 'off',
			'no-plusplus': 'off',
			'no-unused-vars': ['error', { argsIgnorePattern: '_' }],
			'prettier/prettier': [
				'error',
				{
					trailingComma: 'es5',
					singleQuote: true,
					printWidth: 140,
					tabWidth: 4,
					semi: true,
					useTabs: true,
					endOfLine: 'auto',
					arrowParens: 'avoid',
				},
			],
		},
		languageOptions: {
			ecmaVersion: 'latest',
			sourceType: 'module',
			globals: {
				...globals.node,
				...globals.es2023,
				...globals.jest,
				...globals.commonjs,
			},
		},
	},
	eslintConfigPrettier,
]);


```
