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
- Add a script for webpack in package.json, webpack is a executable file under node_modules/.bin folder
```
{
    scripts: {
        "webpack": "webpack"
    }
}
```
- Add scripts for different application modes
```
{
    scripts: {
        "webpack": "webpack",
        "dev": "yarn webpack -- --mode development",
        "prod": "yarn webpack -- --mode production"
    }
}
```
