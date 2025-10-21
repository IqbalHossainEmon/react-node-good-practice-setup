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
		"editor.defaultFormatter": "esbenp.prettier-vscode"
	},
	"[javascriptreact]": {
		"editor.formatOnSave": false,
		"editor.defaultFormatter": "esbenp.prettier-vscode"
	},
	"javascript.validate.enable": false /* disable all built-in syntax checking */,
	"editor.codeActionsOnSave": {
		"source.fixAll.eslint": "always",
		"source.fixAll.tslint": "always",
		"source.organizeImports": "never"
	},
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
import js from '@eslint/js';
import { defineConfig, globalIgnores } from 'eslint/config';
import prettierConfig from 'eslint-config-prettier';
import importPlugin from 'eslint-plugin-import';
import jsxA11y from 'eslint-plugin-jsx-a11y';
import prettierPlugin from 'eslint-plugin-prettier';
import react from 'eslint-plugin-react';
import reactHooks from 'eslint-plugin-react-hooks';
import reactRefresh from 'eslint-plugin-react-refresh';
import globals from 'globals';

export default defineConfig([
	globalIgnores(['dist', 'node_modules']),
	reactHooks.configs.flat['recommended-latest'],
	{
		files: ['**/*.{js,jsx}'],
		languageOptions: {
			ecmaVersion: 'latest',
			sourceType: 'module',
			globals: globals.browser,
			parserOptions: { ecmaFeatures: { jsx: true } },
		},
		settings: {
			'import/resolver': {
				node: {
					extensions: ['.mjs', '.js', '.jsx', '.json', '.cjs'],
					moduleDirectory: ['node_modules', 'src'],
				},
			},
			// optional: treat some packages as core so resolver won't try to resolve deep exports
			'import/core-modules': ['@vitejs/plugin-react', 'eslint/config'],
		},
		plugins: {
			react,
			'react-hooks': reactHooks,
			'react-refresh': reactRefresh,
			'jsx-a11y': jsxA11y,
			import: importPlugin,
			prettier: prettierPlugin,
		},

		rules: {
			...js.configs.recommended.rules,
			...react.configs.recommended.rules,
			...react.configs['jsx-runtime'].rules,
			...reactHooks.configs['recommended-latest'].rules,
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
			'react/button-has-type': 'error',
			'import/newline-after-import': 'off',
			'import/no-extraneous-dependencies': ['error', { devDependencies: true }],
			'react/jsx-props-no-spreading': 'off',
			'no-param-reassign': 'off',
			'no-plusplus': 'off',
			'no-nested-ternary': 'off',
			'consistent-return': 'off',
			'no-multi-assign': 'off',
			'no-case-declarations': 'off',
			// -----------------------
			// General JavaScript
			// -----------------------
			'no-unused-vars': [
				'error',
				{ vars: 'all', args: 'after-used', ignoreRestSiblings: true },
			],
			'no-console': ['warn', { allow: ['warn', 'error'] }],
			eqeqeq: ['error', 'always', { null: 'ignore' }],
			curly: ['error', 'all'],
			'no-var': 'error',
			'prefer-const': ['error', { destructuring: 'all' }],
			semi: ['error', 'always'],
			quotes: ['error', 'single', { avoidEscape: true, allowTemplateLiterals: true }],
			'comma-dangle': ['error', 'only-multiline'],
			'no-magic-numbers': [
				'warn',
				{
					ignore: [0, 1, -1],
					ignoreArrayIndexes: true,
					enforceConst: true,
					detectObjects: false,
				},
			],

			// -----------------------
			// React (eslint-plugin-react)
			// -----------------------
			'react/react-in-jsx-scope': 'off', // React 17+ automatic runtime
			'react/jsx-key': 'error', // keys in lists
			'react/jsx-no-duplicate-props': ['error', { ignoreCase: true }],
			'react/jsx-pascal-case': [
				'error',
				{ allowAllCaps: false, allowLeadingUnderscore: false },
			],
			'react/no-array-index-key': 'warn', // prefer stable keys
			'react/no-unknown-property': 'error', // e.g., use className not class

			// -----------------------
			// React Hooks
			// -----------------------
			'react-hooks/rules-of-hooks': 'error',
			'react-hooks/exhaustive-deps': ['error', { additionalHooks: '(useMyHook|useAnother)' }],

			// -----------------------
			// Accessibility (eslint-plugin-jsx-a11y)
			// -----------------------
			// Merge recommended rules (if you spread jsxA11y.configs.recommended.rules) and then:
			'jsx-a11y/alt-text': [
				'warn',
				{
					elements: ['img', 'object', 'area', "input[type='image']"],
					img: ['Image'],
					object: [],
					area: [],
				},
			],
			'jsx-a11y/anchor-is-valid': [
				'warn',
				{
					components: ['Link'],
					specialLink: ['to', 'hrefLeft', 'hrefRight'],
					aspects: ['noHref', 'invalidHref', 'preferButton'],
				},
			],
			'jsx-a11y/aria-props': 'error',
			'jsx-a11y/role-has-required-aria-props': 'error',
			'jsx-a11y/click-events-have-key-events': 'warn',
			'jsx-a11y/no-static-element-interactions': 'warn',
			'jsx-a11y/interactive-supports-focus': 'warn',
			'jsx-a11y/tabindex-no-positive': 'error',
			'jsx-a11y/label-has-associated-control': [
				'warn',
				{
					labelComponents: [],
					labelAttributes: [],
					controlComponents: ['Input', 'Select'],
					assert: 'either', // allow nesting or htmlFor
					depth: 3,
				},
			],
			'jsx-a11y/media-has-caption': 'warn',
			'jsx-a11y/heading-has-content': 'warn',

			// -----------------------
			// Imports (eslint-plugin-import)
			// -----------------------
			'import/no-unresolved': ['error', { commonjs: true, amd: true }],
			'import/named': 'error',
			'import/default': 'error',
			'import/namespace': 'error',
			'import/no-duplicates': 'error',
			'import/order': [
				'warn',
				{
					groups: ['builtin', 'external', 'internal', 'parent', 'sibling', 'index'],
					pathGroups: [{ pattern: 'react', group: 'builtin', position: 'before' }],
					pathGroupsExcludedImportTypes: ['react'],
					'newlines-between': 'always',
					alphabetize: { order: 'asc', caseInsensitive: true },
				},
			],

			// -----------------------
			// Best-practice / style helpers
			// -----------------------
			'no-else-return': 'warn',
			'no-lonely-if': 'warn',
			'default-case': 'warn',
			'valid-typeof': 'error',
		},
	},
]);

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
```javascript
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
