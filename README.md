# mern_setup

In this we will know about the modules: 

## Babel modules 

This is needed to convert ES6 and JSX to suitable JavaScript for all browsers. The modules needed to get Babel working are as follows:

###### For transpiling JavaScript files with Webpack

**@babel/core**

**babel-loader**

###### To provide support for React, and the latest JavaScript feature

**@babel/preset-env** 

**@babel/preset-react** 

## Webpack modules 

This will help bundle the compiled JavaScript, both for the client-side and the server-side code. Modules needed to get Webpack working are as follows:

**webpack**

**webpack-cli** to run Webpack commands

**webpack-node-externals** to ignore external Node.js module files when bundling in Webpack.

**webpack-dev-middleware** to serve the files emitted from Webpack over a connected server during the development of the code.

**webpack-hot-middleware** to add hot module reloading into an existing server by connecting a browser client to a Webpack server and receiving updates as code changes during development.

**nodemon** to watch server-side changes during development, so the server can be reloaded to put changes into effect.

**react-hot-loader** for faster development on the client side. Every time a file changes in the React frontend, react-hot-loader enables the browser app to update without re-bundling the whole frontend code.

**@hot-loader/react-dom** to enable hot-reloading support for React hooks. It essentially replaces the react-dom package of the same version, but with additional patches to support hot reloading.

***Although react-hot-loader is meant to help the development flow, it is safe to install this module as a regular dependency rather than a devDependency. It automatically ensures
that hot reloading is disabled in production and the footprint is minimal.***

## Workflow

| mern-simplesetup/

 | -- client/
 
  | --- HelloWorld.js
  
  | --- main.js
  
 | -- server/
 
  | --- devBundle.js
  
  | --- server.js
  
 | -- .babelrc
 
 | -- nodemon.json
 
 | -- package.json
 
 | -- template.js
 
 | -- webpack.config.client.js
 
 | -- webpack.config.client.production.js
 
 | -- webpack.config.server.js
 
 ## Setup
 
 **npm init-y**
 
 **npm install @hot-loader/react-dom express mongodb react react-dom react-hot-loader --save**
 
 **npm install @babel/core @babel/preset-env @babel/preset-react babel-loader nodemon webpack webpack-cli webpack-dev-middleware webpack-hot-middleware webpack-node-externals --save-dev**
 
 **package.json**
 
 ```
 {
  "name": "mern_setup",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "repository": {
    "type": "git",
    "url": "git+https://github.com/piyush-cosmo/mern_setup.git"
  },
  "keywords": [],
  "author": "",
  "license": "ISC",
  "bugs": {
    "url": "https://github.com/piyush-cosmo/mern_setup/issues"
  },
  "homepage": "https://github.com/piyush-cosmo/mern_setup#readme",
  "dependencies": {
    "@hot-loader/react-dom": "^16.13.0",
    "express": "^4.17.1",
    "mongodb": "^3.6.1",
    "react": "^16.13.1",
    "react-dom": "^16.13.1",
    "react-hot-loader": "^4.12.21"
  },
  "devDependencies": {
    "@babel/core": "^7.11.6",
    "@babel/preset-env": "^7.11.5",
    "@babel/preset-react": "^7.10.4",
    "babel-loader": "^8.1.0",
    "nodemon": "^2.0.4",
    "webpack": "^4.44.1",
    "webpack-cli": "^3.3.12",
    "webpack-dev-middleware": "^3.7.2",
    "webpack-hot-middleware": "^2.25.0",
    "webpack-node-externals": "^2.5.2"
  }
}
```

## Configuring Babel, Webpack, and Nodemon

Before we start coding up the web application, we need to configure **Babel, Webpack, and Nodemon** to **compile, bundle, and auto-reload the changes in the code during development**

###### Babel

```
{
    "presets": [
      ["@babel/preset-env",
        {
          "targets": {
            "node": "current"
          }
        }
      ],
      "@babel/preset-react"
    ],
    "plugins": [
      "react-hot-loader/babel"
    ]
}
```

In this configuration, we specify that we need **Babel** to transpile the latest JavaScript syntax with support for code in a Node.js environment and also React/JSX code. The 
**react-hot-loader/babel plugin** is required by the **react-hotloader module** to compile React components.
