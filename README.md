# vite-react-ts-tailwind-starter

Vite、React、Typescript、TailwindCSS開発環境セットアップの手順メモです。


## 🚀 Viteでプロジェクト作成

React、Typescriptを選択

```bash
npm create vite@latest
```


## 🎨 Tailwind CSS のインストール

```bash
npm install tailwindcss @tailwindcss/vite
```


## ⚙️ vite.config.tsの編集

```ts
import { defineConfig } from 'vite';
import react from '@vitejs/plugin-react';
import tailwindcss from '@tailwindcss/vite';

// https://vite.dev/config/
export default defineConfig({
  plugins: [react(), tailwindcss()],
});
```


## 🎨 index.cssの編集

```css
@import "tailwindcss";
```

- index.css から不要な記述を削除
- app.css を削除
- App.tsx を編集（不要な DOM を削除）
- assets フォルダを削除


## 🧰 開発補助パッケージをインストール

```bash
npm install -D vite-plugin-devtools-json prettier prettier-plugin-tailwindcss @ianvs/prettier-plugin-sort-imports eslint-plugin-react
```


## ⚙️ vite.config.tsにdevtoolsJsonを追記。

```ts
import { defineConfig } from 'vite';
import react from '@vitejs/plugin-react';
import tailwindcss from '@tailwindcss/vite';
import devtoolsJson from 'vite-plugin-devtools-json';

// https://vite.dev/config/
export default defineConfig({
  plugins: [react(), tailwindcss(), devtoolsJson()],
});
```


## ⚙️ prettier.config.jsを作成

```js
/** @type {import("prettier").Config} */
const config = {
  singleQuote: true,
  semi: true,
  printWidth: 100,
  tabWidth: 2,
  trailingComma: "all",
  plugins: [
    "@ianvs/prettier-plugin-sort-imports",
    "prettier-plugin-tailwindcss",
  ],
  importOrder: [
    "^@core/(.*)$",
    "",
    "^@server/(.*)$",
    "",
    "^@ui/(.*)$",
    "",
    "^[./]",
  ],
  importOrderParserPlugins: ["typescript", "jsx", "decorators-legacy"],
  importOrderTypeScriptVersion: "5.0.0",
  importOrderCaseSensitive: false,
};

export default config;
```


## ⚙️ eslint.config.jsを編集

```js
import js from "@eslint/js";
import globals from "globals";
import reactHooks from "eslint-plugin-react-hooks";
import reactPlugin from 'eslint-plugin-react';
import reactRefresh from "eslint-plugin-react-refresh";
import tseslint from "typescript-eslint";
import { defineConfig, globalIgnores } from "eslint/config";

export default defineConfig([
  globalIgnores(["dist"]),
  {
    files: ["**/*.{ts,tsx}"],
    extends: [
      js.configs.recommended,
      tseslint.configs.recommended,
      reactHooks.configs.flat.recommended,
      reactRefresh.configs.vite,
    ],
    languageOptions: {
      ecmaVersion: 2020,
      globals: globals.browser,
    },
    plugins: {
      react: reactPlugin,
    },
    rules: {
      "react-refresh/only-export-components": "off",
      "react/jsx-sort-props": [
        "warn",
        {
          ignoreCase: true,
          callbacksLast: true,
          shorthandFirst: false,
          shorthandLast: false,
          multiline: "ignore",
          noSortAlphabetically: true,
          reservedFirst: true,
        },
      ],
    },
  },
]);

```
 - reactPluginをインポート。


## ⚙️ .vscode/settings.jsonを作成

```js
{
  "editor.formatOnSave": true,
  "editor.defaultFormatter": "esbenp.prettier-vscode",
  "editor.codeActionsOnSave": {
    "source.fixAll.eslint": "always"
  },

  "files.associations": {
    "*.css": "tailwindcss"
  },
  "css.lint.unknownAtRules": "ignore",

  "javascript.suggestionActions.enabled": false,
  "typescript.suggestionActions.enabled": false
}
```
