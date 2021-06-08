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
        "build:dev": "yarn build -- --mode development",
        "build:prod": "yarn build -- --mode production",
    }
}
```
- Adding watch mode
```
{
    scripts: {
        ...
        "build:dev": "yarn build -- --mode development --watch",
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
        "debug:dev": "yarn debug -- --mode development",
        "debug:prod": "yarn debug -- --mode production",
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
- Create `webpack.config.js` file and add entry property to it. Entry tells webpack what(files) to load for the browser, compliments the output property.
```
module.exports = {
    entry: "./browser.main.ts",
}
```

- Add output property: output tells webpack where and how to distribute bundles (compilations), works with entry.
```
module.exports = {
    ...
    output: {
        path: "./dist",
        filename: "./bundle.js",
    }
}
```
- Add loaders and rules. A rule set tells webpack how to modify files before its added to dependency graph. Loaders are also javascript modules(functions) that takes the source file, and returns it in a [modified] state.
```
module.exports = {
    ...
    rules: [
        {test: /\.ts$/, use: 'ts-loader'},
        {test: /\.js$/, use: 'babel-loader'},
        {test: /\.css$/, use: 'css-loader'},
    ]
}
```
Enforce can be `pre` or `post`, tells webpack to run this rule before or after all other rules.
```
module.exports = {
    ...
    rules: [
        {test: /\.ts$/, use: 'ts-loader', enforce: "pre"},
        ...
    ]
}
```
