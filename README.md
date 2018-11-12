# webpack-dev-server

*** Instructions for how to create a WEBPACK DEV SERVER ***

Create a directory for your project
```
$ mkdir webpack-demo
```


cd into your directory
```
$ cd webpack-demo
```


Create directories for your entry point, output, and config files for webpack
```
$ mkdir src dist config
```


Create files for webpack entry point, and output
```
$ touch src/index.js dist/index.html
```


Initialize npm with default values
```
$ npm init -y
```


Install Webpack
```
$ npm install -g webpack webpack-cli
```


*** Let's test our setup! *** \
**** Webpack 4 allows us to use Webpack without having a configuration file (by including flags) so lets test the current state of our setup before we add our config file ****

Add text to dist/index.html
```
test
```

Add an alert to src/index.js
```javascript
alert("test")
```


run webpack with mode flag to test current setup before we create the config file
```
$ webpack --mode=development
```
You should get something similar to this:
```
Hash: aa5b75cccf66cd9b1ffa
Version: webpack 4.25.1
Time: 555ms
Built at: 2018-11-11 23:02:24
  Asset       Size  Chunks             Chunk Names
main.js  930 bytes       0  [emitted]  main
Entrypoint main = main.js
[0] ./src/index.js 0 bytes {0} [built]
```

FYI the file dist/main.js automatically get created. This is a minified js file. We'll delete this soon. 

So far, so good. Now lets create a webpack config file 
```
touch config/webpack.dev.js
```

Time to populate the webpack config file. The Webpack file is just an object that takes a series of parameters. The three main parameters are ENTRY, MODE, & OUTPUT.

```javascript
module.exports = {
  entry: { },
  mode: " ",
  output: { }
}
```

An entry point indicates which module webpack should use to begin building out its internal dependency graph. The default value for entry is (but of course, this value can be customized)
```javascript
main: "./src/main.js"
```

Create main.js file in src
```
touch src/main.js
```

Next, we'll specify the mode. The mode can either be DEVELOPMENT or PRODUCTION
```
mode: "development"
```

Output is going to take a couple of parameters:
1. Filename: is what we'll call the file once webpack processes and outputs it
2. the path package

First we'll add the path parameter to our output:
```javascript
path: path.resolve(__dirname, "./dist")
```
Next we'll require path in our file
```javascript
const path = require("path");
```

Lastly, to finish our output section we'll add the filename parameter. The name specified in the brakcets is actually come from whatever we put in the entry section. Here, we named it main so our file name is actually [main]-bundle.js
```javascript
filename: "[name]-bundle.js"

Now that we've created a basic config file we can run it
```
webpack --config=config/webpack.dev.js
```

You should get something similar to this: 
```
Hash: 27ba9f37c27cef5eac7c
Version: webpack 4.25.1
Time: 129ms
Built at: 2018-11-12 00:00:19
         Asset      Size  Chunks             Chunk Names
main-bundle.js  3.76 KiB    main  [emitted]  main
Entrypoint main = main-bundle.js
[./src/main.js] 0 bytes {main} [built]
```

In dist/index.html we'll create some basic text:
<body>
  <h1>Hello, World</h1>
  <script src="main-bundle.js"></script>
</body>

And we'll create an alert in our main-bundle.js just for testing
```javascript
alert("Hello, wolrd)

Inside output in the config file we need to make our url root our publicPath
```javascript
publicPath: "/"

Next we need info for the devServer
```javascript
contentBase: "dist"
```

We want to save our dependencies locally
```
npm install -S webpack webpack-cli webpack-dev-server
```

Lets our run our webpack dev server locally
```
webpack-dev-server --config=config/webpack.dev.js
```

In the section that says running here we know what path our server is running at
