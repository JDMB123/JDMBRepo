
## Remove Minification Warnings

In order to make the warning about using a minified copy of the development version of React go away, we have to make a couple changes to our config files.

Because we only want this process to happen in production, we are going to
update our `webpack.config.js` file to include the `UglifyJsPlugin` and use `DefinePlugin` to set `process.env.NODE_ENV` to `'production'` for use in our webpacked files.

By default, Heroku will run Node with `process.env.NODE_ENV == 'production'`. This allows us to include our plugins only under certain conditions.

```js
// webpack.config.js
var path = require("path");
var webpack = require("webpack");

var plugins = []; // if using any plugins for both dev and production
var devPlugins = []; // if using any plugins for development

var prodPlugins = [
  new webpack.DefinePlugin({
    'process.env': {
      'NODE_ENV': JSON.stringify('production')
    }
  }),
  new webpack.optimize.UglifyJsPlugin({
    compress: {
      warnings: true
    }
  })
];

plugins = plugins.concat(
  process.env.NODE_ENV === 'production' ? prodPlugins : devPlugins
)

// include plugins config
module.exports = {
  context: __dirname,
  entry: "./frontend/<name of entry file>",
  output: {
    path: path.resolve(__dirname, "app", "assets", "javascripts"),
    filename: "bundle.js"
  },
  plugins: plugins,
  module: {
    rules: [
      {
        test: /\.jsx?$/,
        exclude: /node_modules/,
        loader: 'babel-loader',
        query: {
          presets: ['@babel/react', '@babel/env']
        }
      }
    ]
  },
  devtool: 'source-map',
  resolve: {
    extensions: [".js", ".jsx", "*"]
  }
};
```
