<div align="center">
    <h2>
      ⚙ <img src="./public/logo192.png" width="40x"/>
      REACT &nbsp; D E P L O Y 
      <img src="./public/logo192.png" width="40x"/> ⚙
    </h2>
    <a href="https://andredavedovicz.github.io/react-deploy/" target="_blank">🔗 Working in GitHub Pages</a>
    <h3>How add a React project(deploy) to GitHub Pages? </h3>
    <h3>Whenever you push to GitHub, it will deploy automatically!</h3>
    <h4>Vite: <a href="https://github.com/andredavedovicz/vite-deploy" target="_blank">If you want to deploy a vite app see this repository!</a></h4>
    
</div>



<br>

### Follow the steps below on how to deploy a React app:

#### 01. Create a React app
##### For Creating React Without Typescript:
```npm
npx create-react-app [REPO_NAME]
```
##### For Creating React With Typescript:
```npm
npx create-react-app [REPO_NAME] --template typescript
```
--------------------------------------------
Open the folder
```npm
cd [REPO_NAME]
```
Open in VsCode
```npm
code .
```
#### 01.1 (OPTIONAL) For those who are going to use TypeScript, follow these steps:
##### Step A: Create [tsconfig.json] file, inside the main folder, paste the code below inside the file:
```json
  {
    "compilerOptions": 
    {
      "target": "es5",
      "lib": [
        "dom",
        "dom.iterable",
        "esnext"
      ],
      "allowJs": true,
      "skipLibCheck": true,
      "esModuleInterop": true,
      "allowSyntheticDefaultImports": true,
      "strict": true,
      "forceConsistentCasingInFileNames": true,
      "noFallthroughCasesInSwitch": true,
      "module": "esnext",
      "moduleResolution": "node",
      "resolveJsonModule": true,
      "isolatedModules": true,
      "noEmit": true,
      "jsx": "react-jsx"
    },
    "include": [
      "src"
    ]
  }
```
##### Step A Continued (OPTIONAL), Create a file called [index.d.ts] inside the ./src folder, this file serves to declare file extension modules, copy the example below to declare .png files
```ts
  declare module '*.png';
```

##### Step B (OPTIONAL): Install styled-components dependency:
```nom
npm i styled-components
```
```nom
npm i @types/styled-components -D
```


#### 02. Create a new repository on GitHub and initialize GIT
start and create git
```git
git init
```
add all files staging area
```git
git add . 
```
add comment commit
```git
git commit -m "first commit" 
```
branch name 
```git
git branch -M main 
```
call remote repository
```git
git remote add origin https://github.com/[USER]/[REPO_NAME] 
```
push to remote repository on branch 'main'
```git
git push -u origin main
```


#### 03. Setup homepage on package.json
```js
"homepage": "https://[USER].github.io/[REPO_NAME]/"
```

#### 04. Create ./.github/workflows/deploy.yml and add the code bellow
##### On your file create: 
# ![aa](https://user-images.githubusercontent.com/88905492/217887391-1cf07688-37bd-434b-8294-503ec65dca6f.png)

##### Paste the code below: 

```yml
name: Build & deploy

on:
  push:
    branches:
      - main
  pull_request:
    branches:
      - main

jobs:
  build:
    name: Build
    runs-on: ubuntu-latest
    
    steps:
    - name: Checkout code
      uses: actions/checkout@v3
    
    - name: Install Node.js
      uses: actions/setup-node@v1
      with:
        node-version: 16.x
    
    - name: Install NPM packages
      run: npm ci
    
    - name: Build project
      run: npm run build
    
    - name: Run tests
      run: npm run test

    - name: Upload production-ready build files
      uses: actions/upload-artifact@v2
      with:
        name: production-files
        path: ./build
  
  deploy:
    name: Deploy
    needs: build
    runs-on: ubuntu-latest
    if: github.ref == 'refs/heads/main'
    
    steps:
    - name: Download artifact
      uses: actions/download-artifact@v2
      with:
        name: production-files
        path: ./build

    - name: Deploy to gh-pages
      uses: peaceiris/actions-gh-pages@v3
      with:
        github_token: ${{ secrets.GITHUB_TOKEN }}
        publish_dir: ./build
```

#### 05. Push
```git
git add . 
```
```git
git commit -m "add: deploy workflow" 
```
```git
git push
```

#### 06. Active workflow
```js
Settings -> Actions -> General -> Workflow permissions -> Read and Write permissions 
Settings -> Pages -> gh-pages -> save
Obs.: Wait a few minutes,if gh-pages it's not showing something is wrong! (the better way is doing again)
Actions -> failed deploy -> re-run-job failed jobs 

```

#### BONUS: For code changes
```git
git add . 
```
```git
git commit -m "fix: some bug" 
```
```git
git push
```

<h3>Remember: Whenever you push to GitHub, it will deploy automatically</h3>