# Playwright
* Playwright is an open-source, cross-browser end-to-end testing and web automation framework,
  developed by Microsoft and launched in January 2020. 
### Why playwright?
  - open source
  - supports multiple languages: .net, java, python, javascript, typescript
  - cross platform support: windows, mac, linux
  - multiple browser support: chromium, webkit, firefox
  - can run from local or CI in headless or headed mode

### Top features
  - auto wait and retry
  - inbuilt codegen tool
  - reporting using traceviewer, powerful debugging using playwright inspector
  - parallel execution using multiple users, from muliple origin, on multiple tabs
  - isolated browser context
 
### Pre-requisites
 - Download nvm from official website: https://www.nvmnode.com/
  ```
  Run the .exe file as admin
  In terminal type : nvm install lts
  nvm use lts
  Check if it is installed correctly:
  nvm -v
  node -v
  npm -v
  ```
  - Download VS code from official website: https://code.visualstudio.com/download?_exp_download=fb315fc982
 ```
 Install the set up .exe
 Extensions on vscode: 
 a. Code Runner
 b. Playwright Test for VSCode
 ```
 - Download GIT from official website: https://gitforwindows.org/

### Install playwright
Open VSCode, create and open a folder in it. Install playwright in it.

latest version: https://playwright.dev/docs/release-notes

Install with command
```
npm init playwright@latest
```
OR

Install as a VS code extension
  
```
TypeScript or JavaScript (default: TypeScript)
Tests folder name (default: tests, or e2e if tests already exists)
Add a GitHub Actions workflow (recommended for CI)
Install Playwright browsers (default: yes)
```

### What is installed?
```
playwright.config.ts         # Test configuration
package.json
package-lock.json            # Or yarn.lock / pnpm-lock.yaml
tests/
  example.spec.ts            # Minimal example test
```

### How to run a test and generate the html report
```
npx playwright test
npx playwright show-report
```

### What are the extensions to install?
```
1. Playwright Test For VS Code : a triangle symbol will appear on the left side, you can click to run it the test
2. Playwright runner by Koushik : a triangle symbol will appear on top of a test with heading: Execute Playwright Test: This will show the command that is executed with test file name and line number
3. Playwright Snippets by Nitay Neeman : type pw- and commands will be auto generated.
4. Playwright Test Snippets by Mark Skelton
```

