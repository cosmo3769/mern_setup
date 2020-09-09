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
