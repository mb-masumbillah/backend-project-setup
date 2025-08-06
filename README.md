# ✅ Step-by-Step Guide to Setup Node.js + Express + Mongoose + TypeScript Server

এই প্রোজেক্টটি Node.js + Express + Mongoose + TypeScript ব্যবহার করে একটি সার্ভার তৈরি করার পুরো প্রক্রিয়া কভার করে।

---

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

### 🟢 Step 4: Install TypeScript (dev dependency)

```bash
npm install --save-dev typescript
```

### 🟢 Step 5: Initialize TypeScript Configuration

```bash
tsc --init
```

তারপর `tsconfig.json` ফাইলে নিচের পরিবর্তন করুন:

```json
{
  "rootDir": "./src",
  "outDir": "./dist",
  "include": ["src"],
  "exclude": ["node_modules"]
}
```

### 🟢 Step 6: Add Build Script to package.json

```json
"scripts": {
  "build": "tsc"
}
```

### 🟢 Step 7: Install ts-node-dev for Development

```bash
npm install --save-dev ts-node-dev
```

`package.json` এ স্ক্রিপ্ট যুক্ত করুন:

```json
"scripts": {
  "dev": "ts-node-dev --respawn --transpile-only src/server.ts",
  "dev:prod": "node ./dist/server.js"
}
```

### 🟢 Step 8: Setup ESLint

```bash
npm install eslint @typescript-eslint/parser @typescript-eslint/eslint-plugin --save-dev
npx eslint --init
```

`eslint.config.mjs` ফাইলে যুক্ত করুন:

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

`package.json` এ lint স্ক্রিপ্ট যুক্ত করুন:

```json
"scripts": {
  "lint": "eslint src --ext .ts .",
  "lint:problem": "npx eslint src .",
  "lint:fix": "npx eslint src --fix"
}
```

### 🟢 Step 9: ESLint setup test command

```bash
npx eslint .
```

### 🟢 Step 9: Setup Prettier

```bash
npm install --save-dev prettier
```

`.prettierrc.json` ফাইল তৈরি করুন:

```json
{
  "semi": true,
  "singleQuote": true
}
```

`.prettierignore` ফাইল তৈরি করুন:

```
node_modules
dist
```

`package.json` এ Prettier স্ক্রিপ্ট যুক্ত করুন:

```json
"scripts": {
  "prettier": "prettier --ignore-path .gitignore --write \"./src/**/*.+(js|ts|json)\"",
  "prettier:fix": "npx prettier --write src"
}
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

### ✅ Bonus: Sample `src/server.ts`

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

সফলভাবে আপনি এখন একটি টাইপস্ক্রিপ্ট বেসড এক্সপ্রেস সার্ভার তৈরি করে ফেলেছেন 🎉
