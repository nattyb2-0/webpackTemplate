# webpackTemplate
a template for webpack
In your directory, create a webpack.config.js file
copy and paste the following lines of code into the webpack.config.js file


'use strict'
const webpack           = require('webpack');
const path              = require('path');
const HtmlWebpackPlugin = require('html-webpack-plugin');
const ExtractTextPlugin = require('extract-text-webpack-plugin');

const BUILD_DIR         = path.resolve(__dirname, 'dist');
const APP_DIR           = path.resolve(__dirname, 'src');

module.exports = {
  entry: `${APP_DIR}/index.js`,
  output: {
    path: BUILD_DIR,
    filename: '/js/[name].js',
  },
  cache: true,
  debug: true,
  devtool: 'eval-source-map',
  stats: {
    colors: true,
    reasons: true
  },
  plugins: [
    new HtmlWebpackPlugin({
      title: '{your app name goes here}',
      xhtml: true,
      inject: false,
      template: require('html-webpack-template'),
      appMountId: 'root-container'
    }),
    new ExtractTextPlugin('/css/[name].css', {
      allChunks: true
    })
  ],

 module : {
    include: path.join(__dirname, 'src'),
    loaders: [
      {
        test: /\.css$/,
        loader: ExtractTextPlugin.extract('style-loader', 'css-loader')
      },
      {
        test: /\.svg$/,
        loader: 'file-loader?name=/img/[name].[hash:base64:5].[ext]'
      },
      {
        test: /\.gif$/,
        loader: 'file-loader?name=/img/[name].[hash:base64:5].[ext]'
      },
      {
        test: /\.jpg$/,
        loader: 'file-loader?name=/img/[name].[hash:base64:5].[ext]'
      },
      {
        test: /\.png$/,
        loader: 'file-loader?name=/img/[name].[hash:base64:5].[ext]'
      },
      {
        test: /\.(js|jsx)$/,
        loader: 'babel'
      },
      {
        test: /\.otf(\?v=\d+\.\d+\.\d+)?$/,
        loader: 'file-loader?name=/fonts/[name].[ext]'
      }
    ]
  }
};
****** make sure add your app name in the new HtmlWebpackPlugin object

run the webpack command in your terminal ----> $ webpack
