# [webpack builder for typescript](https://blog.logrocket.com/using-webpack-typescript/)


Using webpack with TypeScript
September 1, 2022  8 min read 

Typescript Webpack
Used in many modern projects, webpack is an amazing tool that optimizes application resources so that they work more efficiently and effectively on any device. webpack helps to compile and bundle modules into a single file, reducing HTTP requests and improving application performance as a result.

With webpack, TypeScript code is compiled into a JavaScript file that is browser-friendly. With webpack loaders, you can also convert SASS and LESS files into a single CSS bundle file.

In this article, we’ll learn how to use webpack to compile TypeScript to JavaScript, bundle source code into a single JavaScript file, and use a source map for debugging. We’ll also explore how to use webpack plugins.

To follow along with this tutorial, you’ll need the following:

npm
Node.js: If you already have Node.js installed, ensure it’s ≥v8.x.
Any code editor of your choice; I’ll use Visual Studio Code
Basic knowledge of TypeScript
Let’s get started!

Table of contents
webpack loaders
Setting up webpack and TypeScript
webpack configuration
TypeScript configuration
Package configuration
Creating HTML pages with HtmlWebpackPlugin
Bundling CSS With MiniCssExtractPlugin
Minifying CSS
Minifying JavaScript
Using Copywebpackplugin
Debugging with a source map
webpack loaders
By default, webpack only understands JavaScript files, treating every imported file as a module. webpack cannot compile or bundle non-JavaScript files, therefore, it uses a loader.

Loaders tell webpack how to compile and bundle static assets. They are used for compiling TypeScript modules into JavaScript, handling application styles, and even linting your code with ESLint.

A few webpack loaders include ts-loader, css-loader, style-loader, and more; we’ll discuss them later in this tutorial.

Setting up webpack and TypeScript
Let’s start by setting up our project. First, you should have TypeScript installed on your computer. To install TypeScript globally, use the command below:

npm install -g typescript
Installing TypeScript globally eliminates the need to install TypeScript each time you start a new project.

Next, we’ll install the webpack and ts-loader packages as dependencies in our project:

npm init -y
npm install -D webpack webpack-cli ts-loader webpack-dev-server>
webpack configuration
By default, webpack does not need a configuration file. It will assume that the entry point for your project is src/index.js and will output the minified and optimized result in dist/main.js during production.

If you want to use plugins or loaders, then you’ll need to use the webpack configuration file, allowing you to specify how webpack will work with your project, which files to compile, and where the output bundle file will be.

Let’s add the webpack configuration file to our project. From the project root folder, create a webpack.config.js file with the following configurations:

const path = require('path');

module.exports = {
  entry: './src/index.ts',
  module: {
    rules: [
      {
        test: /\.ts?$/,
        use: 'ts-loader',
        exclude: /node_modules/,
      },
    ],
  },
  resolve: {
    extensions: ['.tsx', '.ts', '.js'],
  },
  output: {
    filename: 'bundle.js',
    path: path.resolve(__dirname, 'dist'),
  },
  devServer: {
    static: path.join(__dirname, "dist"),
    compress: true,
    port: 4000,
  },
};
Let’s review some of the webpack configuration options. For one, the entry option is the starting point for the application, where webpack begins to build a dependency graph. webpack will proceed to other modules based on the entry file.


Over 200k developers use LogRocket to create better digital experiences
Learn more →
The output option tells webpack where to save bundle files and allows you to name the bundle file. Finally, the module option tells webpack how to process modules with specific rules using loaders.

TypeScript configuration
The TypeScript configuration file controls how TypeScript will be compiled to JavaScript and specifies the various compiler options required for transpiling TypeScript.

From the project root folder, create the tsconfig.json file and add the following configurations:

{
    "compilerOptions": {
        "noImplicitAny": true,
        "target": "ES5",
        "module": "ES2015"
    }
}
The target option is the version of JavaScript you want to transpile TypeScript to, while module is the format of the import statement used. You can set the module to CommonJS, ES6, or UMD since webpack will handle all module systems.

Package configuration
Now, we need to add a webpack script that will run the webpack.config.js file for us.

To add the webpack script, open the package.json file and add the following scripts to the script option:

"develop": "webpack-dev-server --mode development",
"build" : "webpack --mode production"
The package.json file will now contain the following configuration settings:

{
    "name": "webpack-setup",
  "version": "1.0.0",
  "description": "",
  "main": "src/index.ts",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "develop": "webpack-dev-server --mode development",
    "build": "webpack --mode production"
  },
  "keywords": [],
  "author": "",
  "license": "ISC",
  "devDependencies": {
    "css-loader": "^6.7.1",
    "html-webpack-plugin": "^5.5.0",
    "mini-css-extract-plugin": "^2.6.1",
    "ts-loader": "^9.4.1",
    "webpack": "^5.74.0",
    "webpack-cli": "^4.10.0",
    "webpack-dev-server": "^4.11.1"
  }
}
Now, let’s create a simple TypeScript program that will subtract two numbers. Inside the src folder, create an index.ts file and add the following TypeScript code:

import { subtract } from "./app";

function init() {
    const form = document.querySelector("form");
    form?.addEventListener("submit", submitHandler);
  }

  function submitHandler(e: Event) {
    e.preventDefault();
    const num1 = document.querySelector("input[name='firstnumber']") as HTMLInputElement;
    const num2 = document.querySelector("input[name='secondnumber']") as HTMLInputElement;
    const result = subtract(Number(num1.value), Number(num2.value));
    const resultElement = document.querySelector("p");
    if (resultElement) {
      resultElement.textContent = result.toString();
    }
  }

  init();
Next, create another app.ts file and add the following code:

export function subtract(firstnumber: number, secondnumber: number): number {
  return firstnumber - secondnumber;
}
Running the develop script will start the app in development mode:

npm run develop 
Running the build script will run the app in production mode:

npm run build
After running the build command, webpack will transpile the two TypeScript files into JavaScript code and generate a bundle.js file inside the dist folder.

Creating HTML pages with HtmlWebpackPlugin
The HtmlWebpackPlugin allows webpack to generate a standard HTML page that will serve the generated bundle files.

When the filename of the bundle changes or is hashed, HTMLWebpackPlugin updates the filenames on the HTML page. First, to install HtmlWebpackPlugin, run the command below:

npm install html-webpack-plugin --save-dev
Next, we need to import and add HtmlWebpackPlugin to the webpack configuration plugin option as follows:

const HtmlWebpackPlugin = require("html-webpack-plugin");
const path = require('path');

module.exports = {
  entry: './src/index.ts',
  module: {
    rules: [
      {
        test: /\.ts?$/,
        use: 'ts-loader',
        exclude: /node_modules/,
      }
    ],
  },
  resolve: {
    extensions: ['.tsx', '.ts', '.js'],
  },
  output: {
    filename: 'bundle.js',
    path: path.resolve(__dirname, 'dist'),
  },

  plugins: [
    new HtmlWebpackPlugin({
        title: 'our project', 
        template: 'src/custom.html' }) 
   ],

  devServer: {
    static: path.join(__dirname, "dist"),
    compress: true,
    port: 4000,
  },
};
The template is a custom HTML file generated by HtmlWebpackPlugin to be injected into the HTML page. To create the custom HTML, inside the src folder, create a custom.html file and add the following HTML code:

<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8" />
  </head>
  <body>
    <div class="cal">
      <center>
     <form><br>
      <p>Result : <span id="display"></span></p>
      <input type="number" class="input" placeholder="Enter first number" name="firstnumber" value="1" min="1" min="9" /><br>
      <input type="number" class="input" placeholder="Enter second number" name="secondnumber" value="1" min="1" min="9" /><br><br>
      <button type="submit" class="button">Subtract</button>
    </form>
  </center>
  </div>
  </body>
</html>
You don’t have to include the script or link tags in the custom HTML; HtmlWebpackPlugin will take care of that by linking the bundle file URL with the generated page.

More great articles from LogRocket:
Don't miss a moment with The Replay, a curated newsletter from LogRocket
Learn how LogRocket's Galileo cuts through the noise to proactively resolve issues in your app
Use React's useEffect to optimize your application's performance
Switch between multiple versions of Node
Discover how to animate your React app with AnimXYZ
Explore Tauri, a new framework for building binaries
Compare NestJS vs. Express.js
Running the app in production mode will generate the index.html HTML page inside the dist folder.

Bundling CSS with MiniCSSExtractPlugin
css-loader tells webpack how to work with the CSS module. It interprets @import and URL() as import/require() and resolves them. css-loader enables webpack to compile all CSS files and convert them into JavaScript format.

Bundling CSS files with style-loader makes HTML page styles unresponsive until the Bundle.js is completely loaded. The style-loader injects CSS into the DOM, but the bundled JavaScript file has to load completely before the styles are injected. To solve this, we can use MiniCssExtractPlugin.

The MiniCssExtractPlugin extracts CSS files and bundles them into a single bundle.css file. This is useful for reducing the size of your CSS assets and avoiding unnecessary HTTP requests to load them.

We can install css-loader and MiniCssExtractPlugin by running the commands below in the terminal:

npm install css-loader --save-dev
npm install mini-css-extract-plugin --save-dev
Now, let’s add the css-loader and MiniCssExtractPlugin to the webpack.config.js file.

At the top of the webpack.config.js file, import the MiniCssExtractPlugin module using the code below:

const MiniCssExtractPlugin = require("mini-css-extract-plugin");
Then, we’ll add a new rule to the rules property as follows:

…
{
        test: /\.css$/,
        use: [MiniCssExtractPlugin.loader, "css-loader"]
}
…
When css-loader compiles all the CSS files into JavaScript, MiniCssExtractPlugin.loader loads the CSS into the CSS bundle file.

Next, we’ll add MiniCssExtractPlugin to the plugin option as follows:

plugins: [
    new HtmlWebpackPlugin({
        title: 'our project', // Load a custom template (lodash by default)
        template: 'src/custom.html' }),
    new MiniCssExtractPlugin({
      filename:"bundle.css"})
  ]
Now that we’ve configured css-loader and MiniCssExtractPlugin, let’s create a CSS file and import it into index.ts. Inside the src folder, create an index.css file and add the following CSS code:

form {
    background-color:pink;
    margin-top:100px;
    border-radius:40px;
}
.cal{
    width:550px;
    height:300px;
    margin-left:400px;
}

.button{
    border-radius:10px;
    margin-top:20px;
    margin-bottom:20px;
}
.input{
    border-radius:10px;
    margin-top:40px;
}
Inside index.ts, import the CSS style as follows:

import styles "./index.css"
Running npm run build will bundle the CSS and apply it to index.html. When you start the app in development mode and open http://localhost:4000 on the browser, it should look like the following image:

Bundled CSS Previewed Localhost
Minifying CSS
We can use the css-minimizer-webpack-plugin to reduce the size of CSS files by removing unused CSS rules and keeping only the necessary ones.

css-minimizer-webpack-plugin analyzes the compiled CSS file and finds any unused styles. This plugin will then remove these unused styles from your final CSS file, thereby reducing its size.

Run the installation command below to install css-minimizer-webpack-plugin:

npm install css-minimizer-webpack-plugin --save-dev
Let’s add css-minimizer-webpack-plugin to the webpack configuration. First, import the plugin as follows:

const CssMinimizerPlugin = require("css-minimizer-webpack-plugin");
Then, we’ll add a new optimization property to the webpack configuration as follows:

optimization: {
    minimizer: [
      new CssMinimizerPlugin()
    ],
  }
When we run the build command, bundle.css will be minified but bundle.js will not. The default bundle.js minimizer has been overridden with the minimizer option that we set. To solve this, we need to minify the JavaScript using TerserWebpackPlugin.

Minifying JavaScript
In the current version of webpack at the time of writing, v5.74.0 and later, you don’t have to install the TerserWebpackPlugin since it’s included out of the box. First, we have to import TerserWebpackPlugin:

const TerserPlugin = require("terser-webpack-plugin");
Then, add TerserPlugin to the minimizer option as follows:

optimization: {
    minimizer: [
      new CssMinimizerPlugin(),
     new TerserPlugin()
    ],
  }
If you run the build script and look at the bundle files in the dist folder, you’ll see that both JavaScript and CSS are minified.

Using Copywebpackplugin
We can configure webpack to copy application assets from the development folder into the build folder dist using CopyWebpackPlugin. This plugin can copy files like images, videos, and other assets into the dist folder.

Install CopyWebpackPlugin using the command below:

npm install copy-webpack-plugin --save-dev
Now, let’s add CopyWebpackPlugin to the webpack configuration. Import the plugin as follows:

const CopyPlugin = require("copy-webpack-plugin");
Next, we’ll add CopyWebpackPlugin to the plugin option. The from property is the folder that we’ll copy from, and the to property is the folder in dist directory to copy all files to:

...
plugins: [
new HtmlWebpackPlugin({
        title: 'our project', // Load a custom template (lodash by default)
        template: 'src/custom.html' }),
    new MiniCssExtractPlugin({
      filename:"bundle.css"}),
    new CopyPlugin({
      patterns: [
        { from: "src/img", to: "img" }
      ]
    }),
  ]

...
Create a new img folder and add images in it. Once the build command is run, the images will be copied to dist/img.

Debugging with a source map
When we build to the bundle by compiling TypeScript files into JavaScript files, we might need to debug and test the bundle file using our browser’s DevTool.

When you’re debugging your code on a browser’s DevTool, you’ll notice that only the bundle files appear. Whenever there is an error in our TypeScript code, it’ll only be indicated in the bundle file, making it hard to trace errors back to TypeScript for correction. However, with a source map, we can easily debug TypeScript using our DevTool:

Typescript Debug Devtool
Source maps display the original source file, making it easy for us to debug TypeScript and fix bundles and minified JavaScript code.

Source map .map files contain details of both the original source files and the bundle files. DevTools uses this file to map the original source file with the bundle file.

To generate .map files for the bundle files, we need to configure both webpack and TypeScript. In the TypeScript configuration file, add sourceMap to the compiler option and set its value to true:

{
    "compilerOptions": {
        "noImplicitAny": true,
        "target": "ES5",
        "module": "ES2015",
        "sourceMap": true
    }
}
Next, we’ll add the devtool property to the webpack configuration and set it to true, telling webpack to generate an appropriate source map for each bundle file:

module.exports = {
  devtool: 'source-map',
   ...
}
When you run the build command, you’ll be able to debug the original source code directly:

Debug Source Code Build Tool
Conclusion
As TypeScript’s popularity continues to grow, webpack has become an important option for developers looking to optimize their projects. With webpack plugins, we can optimize TypeScript application resources.

In this tutorial, we walked through the step-by-step process of setting up webpack with TypeScript. We also learned how to optimize TypeScript applications using webpack plugins, and we explored debugging our TypeScript code with a source map.

LogRocket: Full visibility into your web and mobile apps
LogRocket Dashboard Free Trial Banner
LogRocket is a frontend application monitoring solution that lets you replay problems as if they happened in your own browser. Instead of guessing why errors happen, or asking users for screenshots and log dumps, LogRocket lets you replay the session to quickly understand what went wrong. It works perfectly with any app, regardless of framework, and has plugins to log additional context from Redux, Vuex, and @ngrx/store.

In addition to logging Redux actions and state, LogRocket records console logs, JavaScript errors, stacktraces, network requests/responses with headers + bodies, browser metadata, and custom logs. It also instruments the DOM to record the HTML and CSS on the page, recreating pixel-perfect videos of even the most complex single-page and mobile apps.
