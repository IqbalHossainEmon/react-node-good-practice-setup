## Table of Contents

-   [Plugins](#plugins)
-   [Settings](#settings)
-   [Set Line Breaks](#set-line-breaks)
-   [Linting Setup](#linting-setup)
-   [Install Dev Dependencies](#install-dev-dependencies)
-   [Create Linting Configuration file manually](#create-linting-configuration-file-manually)

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
    // config related to code formatting
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
    "javascript.validate.enable": false, //disable all built-in syntax checking
    "editor.codeActionsOnSave": {
        "source.fixAll.eslint": true,
        "source.fixAll.tslint": true,
        "source.organizeImports": true
    },
    "eslint.alwaysShowStatus": true,
    // emmet
    "emmet.triggerExpansionOnTab": true,
    "emmet.includeLanguages": {
        "javascript": "javascriptreact"
    }
}
```

### Set Line Breaks

Make sure in your VS Code Editor, "LF" is selected as line feed instead of CRLF (Carriage return and line feed). To do that, just click LF/CRLF in bottom right corner of editor, click it and change it to "LF". If you dont do that, you will get errors in my setup.

## Linting Setup

### Install Dev Dependencies
__React__

```
npm i -D eslint-config-prettier eslint-plugin-prettier prettier @babel/eslint-parser @babel/preset-react
```
```
npm init @eslint/config
```
___
__Node__

```
npm i -D eslint-config-prettier eslint-plugin-prettier prettier
```
```
npm init @eslint/config
```




### Create Linting Configuration file manually

Create a `.eslintrc` file in the project root and enter the below contents:

__React__
```json
{
  "extends": [
    "airbnb",
    "airbnb/hooks",
    "eslint:recommended",
    "prettier",
    "plugin:jsx-a11y/recommended",
    "plugin:react/recommended"
  ],
  "parser": "@babel/eslint-parser",
  "parserOptions": {
    "ecmaVersion": "latest",
    "sourceType": "module",
    "requireConfigFile": false,
    "babelOptions": {
      "presets": ["@babel/preset-react"]
    }
  },
  "env": {
    "browser": true,
    "node": true,
    "es2023": true,
    "jest": true
  },
  "rules": {
    "react/jsx-props-no-spreading": 0,
    "react/react-in-jsx-scope": 0,
    "react-hooks/rules-of-hooks": "error",
    "no-console": 0,
    "react/state-in-constructor": 0,
    "indent": 0,
    "linebreak-style": 0,
    "react/prop-types": 0,
    "jsx-a11y/click-events-have-key-events": 0,
    "no-param-reassign": 0,
    "no-nested-ternary": 0,
    "prettier/prettier": [
      "error",
      {
        "trailingComma": "es5",
        "singleQuote": true,
        "printWidth": 100,
        "tabWidth": 2,
        "semi": true,
        "endOfLine": "auto"
      }
    ]
  },
  "plugins": ["prettier", "react", "react-hooks"]
}
```

__Node__
```json
{
  "extends": ["airbnb-base", "eslint:recommended", "prettier"],
  "parserOptions": {
    "ecmaVersion": "latest"
  },
  "env": {
    "node": true,
    "es2023": true,
    "jest": true,
    "commonjs": true
  },
  "rules": {
    "no-console": 0,
    "indent": 0,
    "linebreak-style": 0,
    "no-nested-ternary": 0,
    "prettier/prettier": [
      "error",
      {
        "trailingComma": "es5",
        "singleQuote": true,
        "printWidth": 100,
        "tabWidth": 2,
        "semi": true,
        "endOfLine": "auto"
      }
    ]
  },
  "plugins": ["prettier"]
}

```
