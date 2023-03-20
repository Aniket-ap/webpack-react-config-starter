# Webpack/Babel setup for React project with tailwind css

[Medium article](https://dev.to/ivadyhabimana/how-to-create-a-react-app-without-using-create-react-app-a-step-by-step-guide-30nl)

#### Create a Node project

```
    npm init -y
```

#### Install Babel dependencies

```
npm install --save-dev @babel/core babel-loader @babel/cli @babel/preset-env @babel/preset-react

```

#### Install Webpack dependencies

```
npm install --save-dev webpack webpack-cli webpack-dev-server
```

#### Install HtmlWebpackPlugin

```
npm install --save-dev html-webpack-plugin
```

#### Install React dependencies

```
npm install react react-dom
```

#### Add React files

> public/index.html

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>React App</title>
</head>
<body>
    <div id="root"></div>
</body>
</html>
```

> src/App.js

```
import React from "react";

const App = () =>{
    return (
        <h1>
            Hello world! I am using React
        </h1>
    )
}

export default App
```

> index.js

```
import React from 'react'
import  { createRoot }  from 'react-dom/client';
import App from './src/App.js'

const container = document.getElementById('root');
const root = createRoot(container);
root.render(<App/>);
```

#### configure Babel

- In the root folder create a file named .babelrc

```
{
    "presets": ["@babel/preset-env","@babel/preset-react"]
}
```

#### configure Webpack

- Create a file named webpack.config.js

```
    const HtmlWebpackPlugin = require('html-webpack-plugin');
const path = require('path');

module.exports = {
  entry: './index.js',
  mode: 'development',
  output: {
    path: path.resolve(__dirname, './dist'),
    filename: 'index_bundle.js',
  },
  target: 'web',
  devServer: {
    port: '5000',
    static: {
      directory: path.join(__dirname, 'public')
},
    open: true,
    hot: true,
    liveReload: true,
  },
  resolve: {
    extensions: ['.js', '.jsx', '.json'],
  },
  module: {
    rules: [
      {
        test: /\.(js|jsx)$/,
        exclude: /node_modules/,
        use: 'babel-loader',
      },
    ],
  },
  plugins: [
    new HtmlWebpackPlugin({
      template: path.join(__dirname, 'public', 'index.html')
    })
  ]
};
```

#### add scripts in package.json

```
"scripts": {
    "start": "webpack-dev-server .",
    "build": "webpack ."
  }
```