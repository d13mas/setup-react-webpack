# React Webpack Setup

In your Terminal:
1. Create a new folder for your project 
    ```
    mkdir myproject
    ```
2. Initialize the NPM project. This will create the package.json file in a standard mode.
    ```
    npm init -y
    ```
3. Install dependencies
    ```
    npm i react react-dom
    # this will update your package.json file including the new dependencies
    ```
4. Install development dependencies (not needed for production environments)
    ```
    npm i -D @babel/core @babel/preset-env @babel/preset-react babel-loader file-loader css-loader sass-loader sass webpack webpack-cli style-loader webpack-dev-server
    # this also updates your package.json file
    ```
5. Create a file ".babelrc" in the project's root folder with this content:
    ```
    {
        "presets": ["@babel/preset-env", "@babel/preset-react"]
    }
    ```
6. Create another file "webpack.config.js" in the project's root folder with this content:
    ```
    const path = require('path');
    const MiniCssExtractPlugin = require('mini-css-extract-plugin');

    module.exports = {
        output: {
            path: path.join(__dirname, '/dist'),
            filename: 'index.bundle.js',
        },
        devServer: {
            port: 3010,
            static: true,
        },
        module: {
            rules: [
                {
                    test: /\.(js|jsx)$/,
                    exclude: /node_modules/,
                    use: {
                        loader: 'babel-loader'
                    }
                },
                {
                    test: /\.scss$/,
                    use: [
                        MiniCssExtractPlugin.loader,
                        'css-loader',
                        'sass-loader'
                    ]
                }
            ]
        },
        plugins: [new MiniCssExtractPlugin()],
    }
    ```
7. Create a 'src' folder and download the files on this repo inside that folder.
8. In your package.json file add the following 2 scripts:
    ```
    "serve": "webpack serve --mode development", //
    "build": "webpack --mode production"
    ```
9. Run ```npm run serve``` for checking on development. Every change you do on your files will be autloaded to your browser.
10. Run ```npm run build``` will create the 'dist' folder with the production ready files to upload to your server.