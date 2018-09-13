
![alt text](https://i2.wp.com/lumox.xyz/wp-content/uploads/2018/07/es6-webpack-react-babel.png?fit=1213%2C231&ssl=1 "Logo webpack-babel")
#  Webpack 4 & typescript

![alt text](webpack-4.png "Logo webpack-4")

#### Installing TypeScript (Via yarn)

```sh
 yarn global add typescript
```

#### Installing Webpack (Via yarn)

```sh
 yarn global add webpack
 yarn add webpack --dev
 yarn add webpack-cli --dev
```

#### Create new directory

```sh
mkdir proyect proyect/src  proyect/src/app proyect/src/app/components && cd proyect && touch src/index.js && touch server.js && touch tsconfig.json && touch webpack.config.js && touch src/app/App.ts && touch src/app/components/hello.tsx
```

```sh
tree
tree -I node_modules
proyect/
├─ dist/
|-src/
  |-index.js
  |-app/
    |-components/
      |-Hello.tsx
    |-App.tsx
    |-index.html
|-package.json
|-package-lock.json
|-server.js
|-tsconfig.json
|-webpack.config.js
```

#### yarn init
```sh
yarn init
```

#### Edit package.json

```javascript
...
"scripts": {
    "dev": "webpack --mode development",
    "build": "webpack --mode production"
    },
...
```

#### overriding the defaults entry/output
```javascript
...
"scripts": {
  "dev": "webpack --mode development ./foo/src/js/index.js --output ./foo/main.js",
  "build": "webpack --mode production ./foo/src/js/index.js --output ./foo/main.js"
},
...
```

### transpiling Javascript ES6 with Babel
![alt text](webpack-babel.png "Logo webpack-babel")

babel-core
babel-loader
babel-preset-env for compiling Javascript ES6 code down to ES5

```sh
 yarn add babel-core babel-loader babel-preset-env --dev
```

#### .babelrc file only

```javascript
 {
    "presets": [
        "env"
    ]
}
```

#### webpack.config.js babel-loader

```javascript
module.exports = {
    module: {
        rules: [{
            test: /\.js$/,
            exclude: /node_modules/,
            use: {
                loader: "babel-loader"
            }
        }]
    }
};
```

#### ./src/index.js and write some ES6

```javascript
const arr = [1, 2, 3];
const iAmJavascriptES6 = () => console.log(`I'm a silly entry point`);
window.iAmJavascriptES6 = iAmJavascriptES6;
```

#### setting up webpack 4 with React
![alt text](react.png "Logo Title Text 1")

##### Install React with:
```sh
 yarn add react react-dom --dev
```

##### Next up add babel-preset-react:

```sh
 yarn add babel-preset-react --dev
```

#### .babelrc file with react

```javascript
{
  "presets": ["env", "react"]
}
```

#### webpack.config.js with jsx

```javascript
module.exports = {
  module: {
    rules: [
      {
        test: /\.(js|jsx)$/,
        exclude: /node_modules/,
        use: {
          loader: "babel-loader"
        }
      }
    ]
  }
};
```

#### componnent react
##### ./src/App.js:
```javascript
import React from "react";
import ReactDOM from "react-dom";
const App = () => {
  return (
    <div>
      <p>React here!</p>
    </div>
  );
};
export default App;
ReactDOM.render(<App />, document.getElementById("app"));
```

##### ./src/index.js:
```javascript
import App from "./App";
```
and run the build again.

#### html-webpack-plugin and html-loader

```sh
 yarn add --dev html-webpack-plugin html-loader
```

```javascript
const HtmlWebPackPlugin = require("html-webpack-plugin");
module.exports = {
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
        test: /\.html$/,
        use: [
          {
            loader: "html-loader",
            options: { minimize: true }
          }
        ]
      }
    ]
  },
  plugins: [
    new HtmlWebPackPlugin({
      template: "./src/index.html",
      filename: "./index.html"
    })
  ]
};
```

##### ./src/index.html:
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="utf-8">
    <title>webpack 4 quickstart</title>
</head>
<body>
    <div id="app">
    </div>
</body>
</html>
```

```sh
 $ yarn run build
```

#### extracting CSS to a file

```sh
 yarn add --dev mini-css-extract-plugin css-loader
```

#### ./src/main.css

```CSS
body {
    line-height: 2;
}
```

```javascript
const HtmlWebPackPlugin = require("html-webpack-plugin");
const MiniCssExtractPlugin = require("mini-css-extract-plugin");

module.exports = {
  module: {
    rules: [
      {
        test: /\.(js|jsx)$/,
        exclude: /node_modules/,
        use: {
          loader: "babel-loader"
        }
      },
      {
        test: /\.html$/,
        use: [
          {
            loader: "html-loader",
            options: { minimize: true }
          }
        ]
      },
      {
        test: /\.css$/,
        use: [MiniCssExtractPlugin.loader, "css-loader"]
      }
    ]
  },
  plugins: [
    new HtmlWebPackPlugin({
      template: "./src/index.html",
      filename: "./index.html"
    }),
    new MiniCssExtractPlugin({
      filename: "[name].css",
      chunkFilename: "[id].css"
    })
  ]
};
```

#### ./src/index.js
```javascript
import style from "./main.css";
```

```sh
 $ yarn run build
```

#### the webpack dev server

```sh
 yarn add --dev webpack-dev-server
```

```javascript
"scripts": {
        "start": "webpack-dev-server --mode development --open",
        "dev": "webpack --mode development",
        "build": "webpack --mode production"
    },
```

##### Ahora, ejecutando:

```sh
 yarn run start
```
////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////

### Plugins development dependencies

Explicación de los plugins instalados como dependencia de desarollo

| Plugin                | README                                                                    |
| --------------------- | ------------------------------------------------------------------------- |
| apollo-server-express | integracion de graphql con express                                        |
| graphql-tools         | herramientas de graphql                                                   |
| mongoose              | mongodb                                                                   |
| babel-cli             | babel-node "npm run dev"                                                  |
| babel-core            | plugin basico                                                             |
| babel-loader          | transpila babel con webpack                                               |
| babel-preset-env      | http://babeljs.io/docs/en/env/                                            |
| babel-preset-react    | https://babeljs.io/docs/en/babel-preset-react                             |
| .babelrc              | configura el entorno dev "npm run dev" https://babeljs.io/docs/en/babelrc |
