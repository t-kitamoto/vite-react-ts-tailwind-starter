# 🛠 vite-react-ts-tailwind-starter

Vite、React、Typescript、TailwindCSS開発環境セットアップの手順メモです。


## 🚀 Viteでプロジェクト作成。

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


## 🧰 prettier-plugin-tailwindcss / @trivago/prettier-plugin-sort-imports / vite-plugin-devtools-jsonをインストール

```bash
npm install -D vite-plugin-devtools-json prettier prettier-plugin-tailwindcss @trivago/prettier-plugin-sort-imports
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


## 🧹 .prettierrcを作成

```json
{
  "plugins": [
    "@trivago/prettier-plugin-sort-imports",
    "prettier-plugin-tailwindcss"
  ],
  "importOrder": ["^react$", "<THIRD_PARTY_MODULES>", "^@/(.*)$", "^[./]"],
  "importOrderSeparation": true,
  "importOrderSortSpecifiers": true
}
```

## 🧪 .vscode/settings.jsonを作成

必要な項目追加。

```json
{
  "css.lint.unknownAtRules": "ignore"
}
```


![画面イメージ](https://github.com/t-kitamoto/vite-react-ts-tailwind-starter/blob/main/public/image.png)
