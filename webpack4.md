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
- Add a script for build in package.json, webpack is a executable file under node_modules/.bin folder
```
{
    scripts: {
        "build": "webpack"
    }
}
```
- Add scripts for environment builds
```
{
    scripts: {
        ...
        "build:dev": "yarn build -- --mode development",
        "build:prod": "yarn build -- --mode production"
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
        "debug:prod": "yarn debug -- --mode production"
    }
}
```
Open the url `chrome://inspect/#devices` on Chrome,
also you can click a link on Chrome to open dedicated DevTools for Node.
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
- Add modules and build them
```
touch src/message.js

// src/message.js
export default "Hello world";

// src/index.js
import msg from './message";
console.log(msg);

yarn build:dev
node dist/main.js
```
- Dead code elimination or tree shaking: It's the fact that Webpack is using statically the syntax to identify what am I using