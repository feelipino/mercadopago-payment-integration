# 🚀 **Development Environment Setup**

## **Project Overview**

MVP Payment System with Mercado Pago Integration using Node.js, TypeScript, NestJS, and React.

## 🛠️ **Base Environment Setup**

### **1. Node.js Verification**

Check if Node.js is installed by opening **Terminal** (or PowerShell):

```bash
node --version
npm --version
```

**If not installed:**

- Download LTS version from [nodejs.org](https://nodejs.org/)
- Follow standard installation wizard
- Restart terminal and test commands again

### **2. VSCode Configuration**

Install essential extensions for our stack:

**Required Extensions:**

- **TypeScript Importer** - Intelligent auto-import
- **ES7+ React/Redux/React-Native snippets** - React snippets
- **Prettier - Code formatter** - Consistent formatting
- **ESLint** - Code quality linting
- **Thunder Client** - API testing (Postman alternative)

## 📁 **Project Structure**

Create the base structure for our MVP:

```bash
# Create main directory
mkdir payment-mvp
cd payment-mvp

# Create folder structure
mkdir backend frontend shared docs
```

## 🎯 **Backend Setup (NestJS) - DETAILED EXPLANATION**

### **Why NestJS over pure Express?**

NestJS uses **decorators** and **dependency injection** (Angular concepts), making code more **organized** and **testable**. Think of Express as building a house brick by brick, while NestJS provides "pre-made blocks" that fit perfectly together.

### **Install NestJS CLI:**

```bash
npm i -g @nestjs/cli
```

**🔍 What this command does:**

- `npm i -g`: Installs **globally** on your system (not just in project)
- `@nestjs/cli`: Command-line tool that creates automatic structures
- **Why global?** So you can use `nest` command in any folder on your computer

### **Create backend project:**

```bash
cd backend
nest new . --strict
```

**🔍 Breaking down this command:**

- `cd backend`: Enter the backend folder we created
- `nest new .`: Creates new NestJS project **in current folder** (dot means "here")
- `--strict`: Activates **TypeScript strict mode** (more rigorous with types)

**🤔 What happens when you execute this:**

1. CLI asks which **package manager** to use (choose `npm`)
2. Downloads a **template** with standard NestJS structure
3. Automatically installs all basic dependencies
4. Creates files like `app.module.ts`, `main.ts`, etc.

### **Install specific dependencies:**

```bash
npm install @nestjs/config mercadopago
npm install --save-dev @types/node
```

**🔍 Understanding each dependency:**

**`@nestjs/config`:**

- **What it does:** Manages environment variables (.env) securely
- **Why we need it:** To store Mercado Pago tokens without exposing in code
- **How it works:** Transforms .env variables into typed TypeScript objects

**`mercadopago`:**

- **What it does:** Official Mercado Pago SDK for Node.js
- **Why official:** Has all features, maintained by the company itself
- **Advantage:** Abstracts all REST API complexity from MP

**`@types/node`:**

- **What it does:** TypeScript type definitions for Node.js
- **Why `--save-dev`:** Only needed during development, not in production
- **Example:** Without this, `process.env` wouldn't have autocomplete in VSCode

## 🎨 **Frontend Setup (React + TypeScript) - DETAILED EXPLANATION**

### **Why Vite instead of Create React App?**

**Vite** is **much faster** than CRA because:

- Uses **ESBuild** (written in Go) instead of Webpack
- **Instant hot reload** (changes appear in milliseconds)
- More optimized **production build**

### **Create React project:**

```bash
cd ../frontend
npm create vite@latest . -- --template react-ts
```

**🔍 Breaking down this command:**

- `cd ../frontend`: Go back one folder (`..`) and enter frontend
- `npm create vite@latest`: Uses latest Vite version
- `.`: Creates **in current folder** (frontend)
- `-- --template react-ts`: The `--` separates npm args from Vite args
- `react-ts`: Template that comes with React + TypeScript configured

**🤔 What happens internally:**

1. Downloads React + TypeScript template
2. Configures **Vite** as bundler
3. Installs basic dependencies (React, TypeScript, etc.)
4. Creates standard folder structure (`src/`, `public/`, etc.)

### **Install dependencies:**

```bash
# In frontend folder
npm install
npm install axios react-router-dom
npm install --save-dev @types/react @types/react-dom
```

**🔍 Understanding each dependency:**

**`npm install`:**

- **What it does:** Installs all dependencies from `package.json`
- **Why necessary:** Sets up React, TypeScript, Vite, etc.

**`axios`:**

- **What it does:** HTTP client for making requests to backend
- **Why not fetch?** Axios has interceptors, automatic timeout, better error handling
- **Usage example:** `axios.post('/api/payment', data)`

**`react-router-dom`:**

- **What it does:** Manages navigation between pages in React (SPA)
- **Why we need it:** To have routes like `/payment`, `/success`, `/error`
- **How it works:** Changes page content without browser reload

**`@types/react` and `@types/react-dom`:**

- **What they do:** TypeScript type definitions for React
- **Why `--save-dev`:** Only for development (autocomplete, type checking)
- **Example:** Without these, `useState` wouldn't have automatic typing

## ⚙️ **Environment Configuration (.env) - DETAILED EXPLANATION**

### **Create .env file:**

```bash
# In backend folder
echo '{}' > .env
```

**🔍 About the command:**

- **What it does:** Creates empty file with `.env` extension
- **Why .env:** Universal convention for environment variables

### **.env content explained line by line:**

```env
# Mercado Pago Configuration
MERCADOPAGO_ACCESS_TOKEN=your_access_token_here
MERCADOPAGO_PUBLIC_KEY=your_public_key_here

# Application Configuration
PORT=3001
NODE_ENV=development

# CORS
FRONTEND_URL=http://localhost:5173
```

**🔍 Understanding each variable:**

**`MERCADOPAGO_ACCESS_TOKEN`:**

- **What it is:** Private token to authenticate with MP API
- **Where to get:** Developer panel on Mercado Pago website
- **Security:** NEVER commit to Git (add to .gitignore)

**`MERCADOPAGO_PUBLIC_KEY`:**

- **What it is:** Public key for frontend (can be exposed)
- **Usage:** Initialize MP SDK in React
- **Difference:** Public key = frontend, Access token = backend

**`PORT=3001`:**

- **Why 3001:** Frontend uses 5173, backend needs different port
- **How it works:** `process.env.PORT` in NestJS code
- **Flexibility:** Can change without altering code

**`NODE_ENV=development`:**

- **What it does:** Tells Node we're in development
- **Impact:** Activates detailed logs, disables cache, etc.
- **Production:** Would be `NODE_ENV=production`

**`FRONTEND_URL=http://localhost:5173`:**

- **Purpose:** Configure CORS (Cross-Origin Resource Sharing)
- **CORS explained:** Browser blocks requests between different domains
- **Solution:** Backend explicitly authorizes frontend

## 🔧 **VSCode Configuration (Workspace) - DETAILED EXPLANATION**

### **Create workspace configuration:**

```bash
# In project root
mkdir .vscode
cd .vscode
echo '{}' > settings.json
```

**🔍 What happens:**

- `.vscode/`: Special folder that VSCode recognizes automatically
- `settings.json`: Project-specific configurations
- **Advantage:** Entire team will have same configurations

### **settings.json content explained:**

```json
{
    "typescript.preferences.importModuleSpecifier": "relative",
    "editor.formatOnSave": true,
    "editor.defaultFormatter": "esbenp.prettier-vscode",
    "editor.codeActionsOnSave": {
        "source.fixAll.eslint": true
    },
    "files.exclude": {
        "**/node_modules": true,
        "**/dist": true,
        "**/build": true
    }
}
```

**🔍 Each configuration explained:**

**`"typescript.preferences.importModuleSpecifier": "relative"`:**

- **What it does:** Imports use relative path (`./service`) instead of absolute
- **Example:** `import { PaymentService } from './payment.service'`
- **Why:** Clearer where each file is located

**`"editor.formatOnSave": true`:**

- **What it does:** Automatically formats code when saving (Ctrl+S)
- **Advantage:** Always consistent code, no style discussions
- **Works with:** Prettier (installed as extension)

**`"editor.defaultFormatter": "esbenp.prettier-vscode"`:**

- **What it does:** Sets Prettier as default formatter
- **Why:** Prettier is industry standard for formatting
- **Result:** Automatic indentation, spaces, line breaks

**`"source.fixAll.eslint": true`:**

- **What it does:** Automatically fixes ESLint issues on save
- **ESLint:** Tool that finds code problems
- **Example:** Removes unused variables, adds semicolons

**`"files.exclude"`:**

- **What it does:** Hides unnecessary folders from VSCode explorer
- **Why:** `node_modules` has thousands of files we don't edit
- **Performance:** VSCode runs faster without indexing these files



## 🚦 **Development Scripts**

### **Root package.json:**

Create `package.json` at root to manage both projects:

```bash
# At project root
echo '{}' > package.json
```
### **Add scripts to package.json:**

```json
{
  "name": "payment-mvp",
  "version": "1.0.0",
  "scripts": {
    "dev": "concurrently \"npm run dev:backend\" \"npm run dev:frontend\"",
    "dev:backend": "cd backend && npm run start:dev",
    "dev:frontend": "cd frontend && npm run dev",
    "install:all": "npm install && cd backend && npm install && cd ../frontend && npm install"
  },
  "devDependencies": {
    "concurrently": "^8.2.0"
  }
}

```

**Install concurrently:**

```bash
npm install
```

## ✅ **Environment Testing**

Test if everything is working:

```bash
# At project root
npm run dev
```

**You should see:**

- Backend running at `http://localhost:3001`
- Frontend running at `http://localhost:5173`
- Hot reload working on both