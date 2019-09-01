# my-react-boilerplate 
build a react boilerplate from scratch using Webpack 4 and Babel 

## Intro 
the most commmon way to build a react app is to use `creat-react-app`, but in this project I am going to build a react bolierplate from scratch. 

## Folder Structure 

react-boilerplate  
____|--src  
________|--components  
________|--styles  
```
mkdir react-boilerplate
cd react-boilerplate
mkdir -p src/components src/styles
```

## Initialize the Project 
```
npm init
```
now package.json will look like this below:
```
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
```
npm install webpack webpack-cli --save-dev
```

## Installing React 
```
npm install react react-dom --save
```

## Installing Babel
```
npm install @babel/core babel-loader @babel/preset-env @babel/preset-react --save-dev 
``` 
- babel-core: Transforms ES6 code to ES5 
- babel-loader: Webpack helper to transpile code, given the the preset. 
- babel-preset-env: Preset which helps babel to convert ES6, ES7 and ES8 code to ES5. 
- babel-preset-react: Preset which Transforms JSX to JavaScript. 

## Basic Files 
create 2 new files named index.js and index.html 
react-boilerplate  
____|--src  
________|--components  
________|--styles  
________|--index.js  
________|--index.html  
```
//index.js
console.log("hello");
``` 
```
//index.html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>React Boilerplate</title>
</head>

<body>
    <div id="root">

    </div>
</body>

</html>
```

## Reference 
https://medium.com/hackernoon/how-to-build-a-react-project-from-scratch-using-webpack-4-and-babel-56d4a26afd32
