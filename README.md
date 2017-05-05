# react-webpack-template

## How to use this

* Clone the repo: git clone git@github.com:wendy81/react-webpack-template.git
* Install the dependencies: npm install
* Start webpack: npm start

### devtool
* devtool: 'source-map'

#### Add the plugins
* html-webpack-plugin
* CommonsChunkPlugin


#### webpack.config.js

	const webpack = require('webpack');
	const HtmlWebpackPlugin = require('html-webpack-plugin');
	
	// only load the resolve method of  the module 'path'
	const { resolve } = require('path');
	
	module.exports = {
	context: resolve(__dirname),
	entry: {
      app: './index.js',
      vendor: ['react', 'react-dom']
    },
    output: {
        filename: 'browser-bundle.js',
        path: 'docs'
    },
    devtool: 'source-map',
    module: {
        loaders: [
        {
          test: /\.js$/,
          loader: 'babel-loader',
          query: {
              presets: ['es2015', 'react']
          }
        }
        ]
    },
    plugins: [
        new HtmlWebpackPlugin({
            title: 'My App',
            template: __dirname + '/index.html'
        }),
        new webpack.optimize.CommonsChunkPlugin({
            name: 'vendor',
            filename: 'vendor.js'
        })
    ]
    };