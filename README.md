# 🛠️ Node.js + Express + Mongoose + TypeScript Boilerplate

This is a boilerplate for setting up a Node.js server using Express, Mongoose, and TypeScript, with ESLint and Prettier configured.

---

## ✅ Step-by-Step Setup Guide

### 🟢 Step 1: Project Folder & VS Code

```bash
mkdir my-server
cd my-server
code .
```

### 🟢 Step 2: Initialize Node Project

```bash
npm init -y
```

### 🟢 Step 3: Install Core Dependencies

```bash
npm install express mongoose cors dotenv
```

### 🟢 Step 4: Install TypeScript

```bash
npm install --save-dev typescript
```

### 🟢 Step 5: Initialize TypeScript Configuration

```bash
npx tsc --init
```

Update `tsconfig.json`:

```json
{
  "rootDir": "./src",
  "outDir": "./dist",
  "include": ["src"],
  "exclude": ["node_modules"]
}
```

### 🟢 Step 6: Add Scripts to package.json

```json
"scripts": {
  "build": "tsc",
  "start:prod": "node ./dist/server.js",
  "start:dev": "ts-node-dev --respawn --transpile-only src/server.ts",
  "lint": "eslint src --ext .ts .",
  "lint:problem": "npx eslint src .",
  "lint:fix": "npx eslint src --fix",
  "prettier": "prettier --ignore-path .gitignore --write \"./src/**/*.+(js|ts|json)\"",
  "prettier:fix": "npx prettier --write src",
  "test": "echo \"Error: no test specified\" && exit 1"
}
```

### 🟢 Step 7: Install ts-node-dev

```bash
npm install --save-dev ts-node-dev
```

### 🟢 Step 8: Setup ESLint

```bash
npm install eslint @typescript-eslint/parser @typescript-eslint/eslint-plugin --save-dev
npx eslint --init
```

Create `eslint.config.mjs`:

```js
import globals from "globals";
import pluginJs from "@eslint/js";
import tseslint from "typescript-eslint";

/** @type {import('eslint').Linter.Config[]} */
export default [
  { files: ["**/*.{js,mjs,cjs,ts}"] },
  {
    languageOptions: {
      globals: {
        process: "readonly",
        ...globals.browser,
        ...globals.node
      }
    }
  },
  pluginJs.configs.recommended,
  ...tseslint.configs.recommended,
  {
    rules: {
      "no-unused-vars": "error",
      "prefer-const": ["error", { ignoreReadBeforeAssign: true }],
      "no-unused-expressions": "error",
      "no-console": "warn",
      "no-undef": "error",
    },

  },
  {
    ignores: [
      "node_modules/*",
      "dist/*",
    ]
  },
];
```

### 🟢 Step 9: Setup Prettier

```bash
npm install --save-dev prettier
```

Create `.prettierrc.json`:

```json
{
  "semi": true,
  "singleQuote": true
}
```

Create `.prettierignore`:

```
node_modules
dist
```

### 🟢 Step 10: Prevent ESLint & Prettier Conflict

```bash
npm install --save-dev eslint-config-prettier
```

### 🟢 Step 11: Install Type Definitions

```bash
npm install --save-dev @types/cors @types/express @types/node
```

---

## 🚀 Sample `src/server.ts`

```ts
import express, { Application, Request, Response } from 'express';
import cors from 'cors';
import dotenv from 'dotenv';

dotenv.config();

const app: Application = express();
const port = process.env.PORT || 5000;

app.use(cors());
app.use(express.json());

app.get('/', (req: Request, res: Response) => {
  res.send('Server is running!');
});

app.listen(port, () => {
  console.log(`Server is running on port ${port}`);
});
```

---

## 📜 License

MIT