Webpack is a module bundler. A module bundler lets you write any module format, compiles them for the browser. On top of that, Webpack can support
- code splitting
- static async bundling, where you can create separately bundles at build time

Three ways that you can use Webpack:
- the webpack.config.js file, it is a commonJS module
- Webpack CLI
- Node API: [Neutrino](https://github.com/neutrinojs/neutrino) and joy


* * *


- Install Node.js and yarn
```
npm install --global yarn
```
- Create your project folder, install webpack as a dev dependency
```
yarn init
mkdir src
touch src/index.js
yarn add -D webpack webpack-cli
```
- Add a script for build in package.json, there is a executable file named webpack under node_modules/.bin folder
```
{
    scripts: {
        "build": "webpack",
    }
}
```
- Add scripts for environment builds
```
{
    scripts: {
        ...
        "build:dev": "yarn build --mode development",
        "build:prod": "yarn build --mode production",
    }
}
```
- Adding watch mode
```
{
    scripts: {
        ...
        "build:dev": "yarn build --mode development --watch",
        ...
    }
}
```
- Setting up Debugging
```
{
    scripts: {
        ...
        "debug": "node --inspect --inspect-brk ./node_modules/webpack/bin/webpack.js",
        "debug:dev": "yarn debug --mode development",
        "debug:prod": "yarn debug --mode production",
    }
}
```
Open the url `chrome://inspect/#devices` on Chrome,
also you can click a link on Chrome to open dedicated DevTools for Node.
- Add modules and build them
```
touch src/message.js
vim src/message.js
export default "Hello";
```
```
vim src/index.js
import msg from "./message";
console.log(msg);
```
```
yarn build:prod
node dist/main.js
```
- Dead code elimination or tree shaking
- Create a `webpack.config.js` file and add entry property to it. Entry tells webpack what(files) to load for the browser, compliments the output property.
```
module.exports = () => ({
    entry: "./src/index.js",
});
```
- Add output property: output tells webpack where and how to distribute bundles (compilations), works with entry.
```
module.exports = () => ({
    ...
    output: {
        filename: "bundle.js",
    }
});
```
- Add loaders and rules. A rule set tells webpack how to modify files before its added to dependency graph. Loaders are also javascript modules(functions) that takes the source file, and returns it in a [modified] state. A loader tells webpack how to interpret and translate files, transformed on a per-file basis before adding to the dependency graph.
```
yarn add -D babel-loader @babel/core
```
```
module.exports = () => ({
    ...
    module: {
        rules: [
            {test: /\.js$/, use: 'babel-loader'},
        ]
    }
})
```
Enforce can be `pre` or `post`, tells webpack to run this rule before or after all other rules.
```
module.exports = () => ({
    ...
    module: {
        rules: [
            {test: /\.ts$/, use: 'ts-loader', enforce: "pre"},
        ]
    }
})
```
Chaining loaders always execute from right to left
```
yarn add -D style-loader css-loader less less-loader
touch src/styles.less
```
```
vim src/index.js
import msg from "./message";
import './styles.less';
console.log(msg);
```
``` 
module.exports = () => ({
    ...
    module: {
        rules: [
            ...
            {test: /\.less$/, use: ['style-loader', 'css-loader', 'less-loader']}
        ]
    }
})
```
- A plugin for webpack, it is an object with an apply property in the prototype chain, to allow you to hook into the entire compilation lifecycle of events. Plugins adds additional functionality to compilations(optimized bundled modules). More powerful w/more access to CompilerAPI. webpack has a variety of built in plugins. 
```
yarn add -D html-webpack-plugin
```
```
const webpack = require("webpack");
const HtmlWebpackPlugin = require("html-webpack-plugin");
module.export = () => ({
    ...
    plugins: [new HtmlWebpackPlugin(), new webpack.ProgressPlugin()]
})
```
- Setting up a local development server
```
```