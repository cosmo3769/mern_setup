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

**.babelrc**

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

###### Webpack

We will have to configure Webpack to **bundle both the client and server code and the client code separately for production**. All three fileswill have the following code structure, starting with imports, then the definition of the config object, and finally the export of the defined config object:

The config JSON object will differ with values specific to the client- or server-side code, and development versus production code. In the following sections, we will highlight the relevant properties in each configuration instance.

Alternatively, you can also generate Webpack configurations using the interactive portal **Generate Custom Webpack Configuration** at https://generatewebpackconfig.netlify.com/
or using the **Webpack-cli's init command** from the command line.

###### Client-side Webpack configuration for development

**webpack.config.client.js**

```
const path = require('path')
const webpack = require('webpack')
const CURRENT_WORKING_DIR = process.cwd()

const config = {
    name: "browser",
    mode: "development",
    devtool: 'eval-source-map',
    entry: [
        'webpack-hot-middleware/client?reload=true',
        path.join(CURRENT_WORKING_DIR, 'client/main.js')
    ],
    output: {
        path: path.join(CURRENT_WORKING_DIR , '/dist'),
        filename: 'bundle.js',
        publicPath: '/dist/'
    },
    module: {
        rules: [
            {
                test: /\.jsx?$/,
                exclude: /node_modules/,
                use: [
                    'babel-loader'
                ]
            }
        ]
    },  
    plugins: [
          new webpack.HotModuleReplacementPlugin(),
          new webpack.NoEmitOnErrorsPlugin()
    ],
    resolve: {
        alias: {
          'react-dom': '@hot-loader/react-dom'
        }
    }
}

module.exports = config
```

The highlighted keys and values in the **config** object will determine how Webpack bundles the code and where the bundled code will be placed:

###### Server-side Weback Configuration

**webpack.config.server.js**

###### Client-side Webpack Configuration for Development

**webpack.config.client.production.js**

###### nodemon

With the bundling configurations in place, we can add configuration for running these generated bundles automatically on code updates during development using Nodemon

This configuration will set up nodemon to watch for changes in the server files during development, then execute compile and build commands as necessary.

## Frontend views with React

In order to start developing a frontend, first create a root template file called **template.js** in the project folder, which will render the HTML with React components. 

When the server receives a request to the root URL, this HTML template will be rendered in the browser, and the div element with ID "root" will contain our React component.

**client --> main.js & HelloWorld.js**

The **main.js** file simply renders the top-level entry React component in the **div** element in the HTML document. In this case, the entry React component is the HelloWorld component imported from HelloWorld.js.

**HelloWorld.js** contains a basic **HelloWorld** React component, which is hot-exported to enable hot reloading with **react-hot-loader** during development.

To see the React component rendered in the browser when the server receives a request to the root URL, we need to use the Webpack and Babel setup to compile and bundle this code, and also add server-side code that responds to the root route request with the bundled code.

## Server with Express and Node

**server --> server.js & devBundle.js**

The **server.js** file will set up the server.

The **devBundle.js** file will help compile the React code using Webpack configurations while in development mode.

Here, we will implement the Node-Express app, which initiates client-side code bundling, starts the server, sets up the path to serve static assets to the client, and renders the
React view in a template when a GET request is made to the root route.

###### Express app

We will first add code to import the express module in order to initialize an Express app:

```
import express from 'express';
const app = express();
```

###### Bundling React app during development

We will initialize Webpack to compile the client-side code when the server is run. In devBundle.js, we will set up a compile method that takes the Express app and configures it to use the Webpack middleware to compile, bundle, and serve code, as well as enable hot reloading in development mode:

**devBundle.js**

```
import webpack from 'webpack'
import webpackMiddleware from 'webpack-dev-middleware'
import webpackHotMiddleware from 'webpack-hot-middleware'
import webpackConfig from './../webpack.config.client.js'

const compile = (app) => {
  if(process.env.NODE_ENV == "development"){
    const compiler = webpack(webpackConfig)
    const middleware = webpackMiddleware(compiler, {
      publicPath: webpackConfig.output.publicPath
    })
    app.use(middleware)
    app.use(webpackHotMiddleware(compiler))
  }
}

export default {
  compile
}
```

We will call this compile method in server.js by adding the following lines while in development mode

**server.js**

```
import devBundle from './devBundle';
devBundle.compile(app);
```

These two lines of code should be commented out when building the application code for production, this is only meant for development.

In development mode, when these lines are executed, Webpack will compile and bundle the React code to place it in **dist/bundle.js.**

###### Serving static files from the dist folder

Webpack will compile client-side code in both development and production mode, then place the bundled files in the dist folder. To make these static files available on requests from the client side, we will add the following code in server.js to serve static files from the dist folder:

**server.js**

```
import path from 'path';
const CURRENT_WORKING_DIR = process.cwd();
app.use('/dist', express.static(path.join(CURRENT_WORKING_DIR, 'dist')));
```

This will configure the Express app to return static files from the dist folder when the requested route starts with /dist.

###### Rendering templates at the root

When the server receives a request at the root URL /, we will render template.js in the browser. In server.js, add the following route-handling code to the Express app to receive GET requests at /:

**server.js**

```
import template from './../template'
app.get('/', (req, res) => {
  res.status(200).send(template())
})
```

Finally, configure the Express app to start a server that listens on the specified port for incoming requests:

**server.js**

```
let port = process.env.PORT || 3000
app.listen(port, function onStart(err) {
  if (err) {
    console.log(err)
  }
  console.info('Server started on port %s.', port)
})
```

With this code, when the server is running, it will be able to accept requests at the root route and render the React view with the "Hello World" text in the browser.

###### Connecting the server to the mongoDB

**server.js**

```
import { MongoClient } from 'mongodb'
// Database Connection URL
const url = process.env.MONGODB_URI || 'mongodb://localhost:27017/mernSimpleSetup'
// Use connect method to connect to the server
MongoClient.connect(url, { useNewUrlParser: true, useUnifiedTopology: true },(err, db)=>{
  console.log("Connected successfully to mongodb server")
  db.close()
})
```

MongoClient is the driver that connects to the running MongoDB instance using its URL. It allows us to implement the database related code in the backend. This completes our full-stack integration for this simple web application using the MERN setup, and finally, we can run this code to see this application working live.

###### Run scripts

**package.json**

```"scripts": {
    "development": "nodemon",
    "build": "webpack --config webpack.config.client.production.js && webpack --mode=production --config webpack.config.server.js",
    "start": "NODE_ENV=production node ./dist/server.generated.js"
  }
```

**npm run development** - This command will get Nodemon, Webpack, and the server started for development.

**npm build** - This will generate the client and server code bundles for production mode (before running this script, make sure to remove the devBundle.compile code from server.js).

**npm start** - This command will run the bundled code in production.
