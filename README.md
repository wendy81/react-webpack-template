# react-webpack-template

This is a simple template for building React apps. Use this to get started, and if you find yourself needing additional features, see my [webpack-howto](https://github.com/petehunt/webpack-howto).

## How to use this

  * Clone the repo: `git clone https://github.com/petehunt/react-webpack-template my-new-project`
  * Install the dependencies: `cd my-new-project && npm install`
  * Start webpack: `npm start`
  * Add your code to `index.js` and open `index.html`
  
### add the HtmlWebpackPlugin and CommonsChunkPlugin
HtmlWebpackPlugin:  let the plugin generate an HTML file for you, supply your own template
CommonsChunkPlugin: consisting of common modules shared between multiple entry points. By separating common modules from bundles, the resulting chunked file can be loaded once initially, and stored in cache for later use.

const webpack = require('webpack');
const HtmlWebpackPlugin = require('html-webpack-plugin');
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
