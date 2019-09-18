# my-react-boilerplate

Build a react boilerplate from scratch using Webpack 4 and Babel

## Intro

The most common and popular way to build a react app is to use `creat-react-app`, but in this project I am going to build a react boilerplate from scratch.

## Folder Structure

- src
  - components
  - styles

```bash
mkdir react-boilerplate
cd react-boilerplate
mkdir -p src/components src/styles
```

## Initialize the Project

```bash
npm init
```

Now `package.json` will look like this below:

```json
//package.json
{
  "name": "react-boilerplate",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "keywords": [],
  "author": "",
  "license": "ISC"
}
```

## Installing Webpack

```bash
npm install webpack webpack-cli --save-dev
```

## Installing React

```bash
npm install react react-dom --save
```

## Installing Babel

```bash
npm install @babel/core babel-loader @babel/preset-env @babel/preset-react --save-dev
```

- babel-core: Transforms ES6 code to ES5
- babel-loader: Webpack helper to transpile code, given the the preset.
- babel-preset-env: Preset which helps babel to convert ES6, ES7 and ES8 code to ES5.
- babel-preset-react: Preset which Transforms JSX to JavaScript.

## Basic Files

Create 2 new files named `index.js` and `index.html`

- src
  - components
  - styles
  - index.js
  - index.html

```js
//index.js
console.log("hello");
```

```html
//index.html

<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <meta http-equiv="X-UA-Compatible" content="ie=edge" />
    <title>React Boilerplate</title>
  </head>

  <body>
    <div id="root"></div>
  </body>
</html>
```

## Entry and Output file

Create `webpack.config.js` in root directory of the project so that we can define rules for our loaders.

```js
// webpack.config.js

const path = require("path");

module.exports = {
  entry: "./src/index.js",
  output: {
    path: path.join(__dirname, "/dist"),
    filename: "index_bundle.js"
  }
};
```

In the above code, Webpack will bundle all of our JavaScript files into `index-bundle.js` file inside the `/dist` directory.

## Webpack Loaders

Loaders in `webpack.config.js` file are responsible for loading and bundling the source files.

```js
// webpack.config.js

const path = require("path");

module.exports = {
  entry: "./src/index.js",
  output: {
    path: path.join(__dirname, "/dist"),
    filename: "index_bundle.js"
  },
  module: {
    rules: [
      {
        test: /\.js$/,
        exclude: /node_modules/,
        use: {
          loader: "babel-loader"
        }
      },
      {
        test: /\.css$/,
        use: ["style-loader", "css-loader"]
      }
    ]
  }
};
```

- babel-loader: load our JSX/JavaScript files
- css-loader: load and bundle all of the CSS files into one file
- style-loader: add all of the styles inside the style tag of the document

#### Before using css-loader and style-loader, we should install them as a dev-dependency.

```bash
npm install css-loader style-loader --save-dev
```

### .babelrc:

Create .babelrc file inside root of the project directory with the following contents inside of it.

```json
{
  "presets": ["@babel/preset-env", "@babel/preset-react"]
}
```

This file will tell babel which presets to use for transpiling the code. Here we are using two presets:

- env: This preset is used to transpile the ES6/ES7/ES8 code to ES5.
- react: This preset is used to transpile JSX code to ES5.

## Compiling files using Webpack

Add these lines of code inside the script object of the `package.json` file as below:

```json
"start": "webpack --mode development --watch",
"build": "webpack --mode production"
```

So scripts will look like this below:

```json
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "start": "webpack --mode development --watch",
    "build": "webpack --mode production"
  },
```

`--watch` flag is to automatically compile all the source files in any changes

There are two modes in webpack 4:

- `--mode production` mode which produces optimized files ready for use in production
- `--mode development` mode which produces easy to read code and gives you best development experience.

Now you can compile the project using below command:

```bash
npm start
```

Then you will see how output part in `webpack.config.js` is working since `index_bundle.js` file created under the `/dist` directory which will contain transpiled ES5 code from `index.js` file.

### App.js

Create `/src/components/App.js`

```js
// App.js

import React, { Component } from "react";

import "../styles/App.css";

class App extends Component {
  render() {
    return (
      <div>
        <h1>My React App!</h1>
      </div>
    );
  }
}

export default App;
```

### App.css

Create `/src/styles/App.css`

```css
// App.css

h1 {
  color: #27aedb;
  text-align: center;
}
```

This CSS file is used to test whether the css-loader and style-loader are working correctly or not

Now we can modify our `index.js` file we created earlier in the `/src` directory

```js
// index.js
import React from "react";
import ReactDOM from "react-dom";
import App from "./components/App.js";

ReactDOM.render(<App />, document.getElementById("root"));
```

## Installing Html-webpack-plugin

So far we already have `index_bundle.js` in `/dist` directory, we also need HTML file. So let us install html-webpack-plugin, this plugin generates an HTML file, injects the script inside the HTML file and writes this file to `dist/index.html`.

Install the html-webpack-plugin as a dev-dependency:

```bash
npm install html-webpack-plugin --save-dev
```

This is a plugin, so that we add it inside the webpack.config.js file

```js
const path = require("path");
const HtmlWebpackPlugin = require("html-webpack-plugin");

module.exports = {
  entry: "./src/index.js",
  output: {
    path: path.join(__dirname, "/dist"),
    filename: "index-bundle.js"
  },
  module: {
    rules: [
      {
        test: /\.js$/,
        exclude: /node_modules/,
        use: ["babel-loader"]
      },
      {
        test: /\.css$/,
        use: ["style-loader", "css-loader"]
      }
    ]
  },
  plugins: [
    new HtmlWebpackPlugin({
      template: "./src/index.html"
    })
  ]
};
```

It uses `/src/index.html` file as a template and generates new file `/dist/index.html` with the script injected.

Almost finished! Let us compile the source files using webpack:

```bash
npm start
```

Open `/dist/index.html` in a web browser, you will see the text "My React App!"

## Installing Webpack-dev-server

To have webpack watch our changes and refresh webpage whenever any change is made to our components, we can install webpack-dev-server.

Install webpack-dev-server as a dev-dependency

```bash
npm install webpack-dev-server --save-dev
```

Then modify `package.json` start script like below:

```json
"start": "webpack-dev-server --mode development --open --hot"
```

`--open` and `--hot` represents that it will open and refresh the web page whenever any change is made to components.

## Final Todos

Final file structure:

- dist
- node_modules
- src
  - components
    - App.js
  - styles
    - App.css
  - index.html
  - index.js
- .babelrc
- .gitignore
- package.json
- package-lock.json
- webpack.config.js
- README.md

In `.gitignore`, we should add `dist/` and `node_modules/`

```md
node_modules/
dist/
```

Last thing is to run:

```
npm start
```

## Reference

https://medium.com/hackernoon/how-to-build-a-react-project-from-scratch-using-webpack-4-and-babel-56d4a26afd32
