mkdir src build
touch .gitignore
npm init --y
cd src && touch index.html

npm i react react-dom
npm i -D typescript @types/react @types/react-dom

touch tsconfig.json
tsc --init

cd src && touch app.tsx index.tsx

npm i -D @babel/core @babel/preset-env @babel/preset-react @babel/preset-typescript


touch .babelrc
add config

{
    "presets": [
        "@babel/preset-env",
        "@babel/preset-typescript",
        "@babel/preset-react"
    ]
}


npm i -D webpack webpack-cli webpack-dev-server html-webpack-plugin 


npm i -D babel-loader


mkdir webpack && cd webpack && touch webpack.config.js

add config

const path = require('path')
const HtmlWebpackPlugin = require('html-webpack-plugin')

module.exports = {
  entry: path.resolve(__dirname, '..', './src/index.tsx'),
  resolve: {
    extensions: ['.tsx', '.ts', '.js'],
  },
  module: {
    rules: [
      {
        test: /\.(ts|js)x?$/,
        exclude: /node_modules/,
        use: [
          {
            loader: 'babel-loader',
          },
        ],
      },
    //   {
    //     test: /\.css$/,
    //     use: ['style-loader', 'css-loader'],
    //   },
    //   {
    //     test: /\.(?:ico|gif|png|jpg|jpeg)$/i,
    //     type: 'asset/resource',
    //   },
    //   {
    //     test: /\.(woff(2)?|eot|ttf|otf|svg|)$/,
    //     type: 'asset/inline',
    //   },
    ],
  },
  output: {
    path: path.resolve(__dirname, '..', './build'),
    filename: 'bundle.js',
  },
  mode: 'development',
  plugins: [
    new HtmlWebpackPlugin({
      template: path.resolve(__dirname, '..', './src/index.html'),
    }),
  ],
  stats: 'errors-only',
}


