# Webpack-Babel-React

This package was created after watching the Webpack section of the "React - The Complete Guide (incl Hooks, React Router, Redux)" course on udemy.com. All the code there was very outdated and didn't work with fresh versions of webpack and babel. I made this project work with Webpack 4 and Babel 7, and later with Webpack 5.

Most of the commands and settings remained the same. Below I will describe how this project was created with the installation of packages and some explanations.

To begin with, since we use a react, you need to install it:

`npm install --save react react-dom react-router-dom`

After that we need to install the webpack, webpack-dev-server and webpack-cli. As of webpack v4, webpack is not expecting a configuration file, but often developers want to create a more custom webpack configuration based on their use-cases and needs. webpack CLI addresses these needs by providing a set of tools to improve the setup of custom webpack configuration.

`npm install --save-dev webpack webpack-dev-server webpack-cli`

In order for React to work, you need to install Babel with it. It will help in ES6 and JSX transpiling in ES5.

`npm install --save-dev @babel/core babel-loader @babel/preset-env @babel/preset-react` 

Next, we need to add loaders that will be responsible for loading and combining the source files.
style-loader: Inject CSS into the DOM
css-loader:  interprets @import and url() like import/require() and will resolve them
postcss-loader: Add vendor prefixes to CSS (in addition for that we use autoprefixer)
url-loader: A loader for webpack which transforms files into base64 URIs

`npm install --save-dev style-loader css-loader postcss-loader url-loader autoprefixer`

After we add the plugin that generate an HTML5 file for you and includes all your webpack bundles in the body using script tags

`npm install --save-dev html-webpack-plugin`

Also to use the functions of the language that are in the proposal stage, we need to install special libraries. Рreviously we used for this @babel/preset-stage-2 but it have been deprecated and we use @babel/plugin-proposal-class-properties for our needs. You can read about it here https://babeljs.io/blog/2018/07/27/removing-babels-stage-presets

`npm install --save-dev @babel/plugin-proposal-class-properties`

For minifying js in prodaction mode I used UglifyJsPlugin in Webpack 4. And in Webpack 5, I use TerserPlugin.

`npm install --save-dev terser-webpack-plugin` 

For these purposes, in the webpack 4 also have the function minimize. 
Just use in webpack.config.js

```
optimization: {
        minimize: true
    }
```

If you need support for older browsers then use core-js and regenerator. Previously used for this @babel/polyfill" but now it deprecated. It is used with https://babeljs.io/docs/en/next/babel-preset-env.html#usebuiltins
Just add once

```
import "core-js/stable";
import "regenerator-runtime/runtime";
```

to your main file and cofigure your @babel/preset-env

```
presets: [
   ["@babel/preset-env", {
       useBuiltIns: "usage",
       corejs: "3.2.0",
   }]
]
```

Warning: Using this feature will greatly increase the size of your files to support older browsers. I got rid of this feature in my project.