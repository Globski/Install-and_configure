# Install and Configure - React (CRA and Vite)

## Description

This guide walks you through the complete process of installing and setting up a React application using two approaches:

1. **Create React App (CRA)** – a traditional setup method (now deprecated).
2. **Vite** – a modern and faster build tool recommended for new projects.

We will also cover the installation of **Node.js**, which is a required dependency for working with React.

---

## Table of Contents

1. [Install Node.js](#install-nodejs)
   - [Windows](#windows)
   - [macOS](#macos)
   - [Linux / WSL](#linux--wsl)
2. [Verify Installation](#verify-installation)
3. [Install React Using CRA (Deprecated)](#install-react-using-cra-deprecated)
4. [Install React Using Vite (Recommended)](#install-react-using-vite-recommended)
5. [Project Structure Explanation](#project-structure-explanation)
6. [Conclusion](#conclusion)

---

## Install Node.js

### 📌 Windows

1. Visit the official [Node.js downloads page](https://nodejs.org/).
2. Download the **LTS** version (recommended).
3. Run the installer and accept the default settings.
4. During setup, make sure to check the box that says:
   > "Automatically install the necessary tools."

Once complete, restart your command prompt or terminal.

---

### 🍏 macOS

1. Install **Homebrew** if not already installed:

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
````

2. Then install Node.js:

```bash
brew install node
```

---

### 🐧 Linux / WSL (Ubuntu)

1. Update and install Node.js and npm:

```bash
sudo apt update
sudo apt install nodejs npm -y
```

2. (Optional) Use Node Version Manager (nvm) for better control:

```bash
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.5/install.sh | bash
source ~/.bashrc
nvm install --lts
```

---

## Verify Installation

After installation, confirm Node.js and npm versions:

```bash
node -v
npm -v
```

You should see something like:

```
v18.17.1
9.6.7
```

If the versions appear, Node.js and npm are installed successfully.

---

## Install React Using CRA (Deprecated)

> ⚠️ CRA is deprecated and should only be used for legacy or learning projects.

### Step 1: Create a Project Folder

```bash
cd ~/Documents
mkdir my-react-cra
cd my-react-cra
```

### Step 2: Use CRA to Scaffold React App

```bash
npx create-react-app my-cra-app
```

This may take a few minutes.

### Step 3: Open in VS Code

```bash
cd my-cra-app
code .
```

### Step 4: Start Development Server

```bash
npm start
```

Your browser should open at `http://localhost:3000`.

---

## Install React Using Vite (Recommended)

### Step 1: Navigate to Project Folder

```bash
cd ~/Documents
mkdir my-react-vite
cd my-react-vite
code .
```

### Step 2: Scaffold App with Vite

```bash
npm create vite@latest my-vite-app
```

* Select `React` for the framework.
* Select `JavaScript` as the language.

### Step 3: Enter Project Folder

```bash
cd my-vite-app
```

### Step 4: Install Dependencies

```bash
npm install
```

### Step 5: Run the Development Server

```bash
npm run dev
```

Your terminal will show a URL like:

```
Local: http://localhost:5173/
```

Hold `Ctrl` (or `Cmd` on mac) and click the link to open it in your browser.

---

## Project Structure Explanation

When you open your project in VS Code, you'll see:

```
my-vite-app/
├── node_modules/       # Installed npm packages
├── public/             # Static files (e.g. images, favicon)
├── src/                # React components and files
│   ├── App.jsx
│   └── main.jsx
├── package.json        # Project dependencies and scripts
├── package-lock.json   # Locked dependency versions
├── index.html          # Main HTML file
└── vite.config.js      # Vite-specific configuration
```

### Notable Files

* `node_modules/`: All npm dependencies
* `src/`: Contains main React code
* `vite.config.js`: Optional config file for advanced Vite usage
* `package.json`: Defines project metadata, dependencies, and scripts

---

## Conclusion

React is one of the most powerful libraries for building front-end applications. With tools like **Vite**, development is faster and easier.

If your project is displaying in the browser successfully, congratulations — you've completed the setup!

**Happy Coding!**

---

