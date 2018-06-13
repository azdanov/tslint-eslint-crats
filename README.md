# TSLint + ESLint + Prettier + Create React App - Typescript

Using all the tools, all at once.

## Prettier + TSLint

To use prettier with TSLint you will need [`tslint-config-prettier`](https://github.com/alexjoverm/tslint-config-prettier) which disables all the conflicting rules and optionally [`tslint-plugin-prettier`](https://github.com/ikatyang/tslint-plugin-prettier) which will highlight differences as TSLint issues.

Example configuration:

### [tslint.json](https://github.com/azdanov/tslint-eslint-crats/blob/master/tslint.json)

```json
{
  "rulesDirectory": ["tslint-plugin-prettier"],
  "extends": [
    "tslint:recommended",
    "tslint-config-airbnb",
    "tslint-react",
    "tslint-config-prettier"
  ],
  "linterOptions": {
    "exclude": ["config/**/*.js", "node_modules/**/*.ts"]
  },
  "rules": {
    "prettier": true
  }
}
```

### [.prettierrc](https://github.com/azdanov/tslint-eslint-crats/blob/master/.prettierrc)

```json
{
  "printWidth": 89,
  "tabWidth": 2,
  "useTabs": false,
  "semi": true,
  "singleQuote": true,
  "trailingComma": "all",
  "bracketSpacing": true,
  "jsxBracketSameLine": false
}
```

## ESLint + TSLint

Why? ESLint ecosystem is rich, with lots of different plugins and config files, whereas TSLint tend to lag behind in some areas.

To remedy this nuisance there is an [`eslint-typescript-parser`](https://github.com/eslint/typescript-eslint-parser) which tries to bridge the differences between javascript and typescript. It still has some rough corners, but can provide consistent assistance with certain plugins.

Example configuration:

### [.eslintrc](https://github.com/azdanov/tslint-eslint-crats/blob/master/.eslintrc)

```json
{
  "extends": [
    "airbnb",
    "prettier",
    "prettier/react",
    "plugin:prettier/recommended",
    "plugin:jest/recommended",
    "plugin:unicorn/recommended"
  ],
  "plugins": ["prettier", "jest", "unicorn"],
  "parserOptions": {
    "sourceType": "module",
    "ecmaFeatures": {
      "jsx": true
    }
  },
  "env": {
    "es6": true,
    "browser": true,
    "jest": true
  },
  "rules": {
    "prettier/prettier": [
      "error",
      {
        "singleQuote": true,
        "trailingComma": "all"
      }
    ],
    "jsx-a11y/anchor-is-valid": [
      "error",
      {
        "components": ["Link"],
        "specialLink": ["to"],
        "aspects": ["noHref", "invalidHref", "preferButton"]
      }
    ],
    "react/jsx-filename-extension": "off",
    "unicorn/filename-case": "off",
    "import/extensions": { "ts": "never", "tsx": "never" },
    "no-use-before-define": "warn",
    "no-param-reassign": "warn"
  },
  "settings": {
    "import/resolver": {
      "node": {
        "extensions": [".js", ".jsx", ".ts", ".tsx"]
      }
    }
  },
  "overrides": [
    {
      "files": ["**/*.ts", "**/*.tsx"],
      "parser": "typescript-eslint-parser",
      "rules": {
        "no-undef": "off"
      }
    }
  ]
}
```
