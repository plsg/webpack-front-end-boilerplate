> __The Rockstar Front-end Boilerplate__  
> Thunder of the Gods fueled with __npm__ 

```
/src/
    styles.scss
    index.html
    app.js

/dist/
    bundle.js
    index.html
    main.css
```
> NOTE: `/src/js/app.js` is the entry point   

___

- [init](#init)
- [dependencies](#dependencies)
- [mkdir](#directories)
- [run scripts](#run)




<a name="init"></a>   
___    

# Environment Information
```
aha-sparx-01.ahundredanswers.com
192.168.50.61
```

# webpack usage

## resources:  
- > BEGINNER GUIDES, initial settings and config for Babel, React, SCSS==CSS, HTML, and more ...    
    https://hackernoon.com/a-tale-of-webpack-4-and-how-to-finally-configure-it-in-the-right-way-4e94c8e7e5c1  
    ~~https://www.valentinog.com/blog/webpack-tutorial/#webpack_4_extracting_CSS_to_a_file~~  
    ~~https://www.sitepoint.com/beginners-guide-webpack-module-bundling/~~   


## instructions:  
1. create a `package.json` file  
    - If no file exists:
        ```
        npm init
        ```
    - If file already exists:
        ```
        npm install
        ```
    - Alternatively 
        - create a package.json with default settings  
            ```
            npm init -y
            ```
        - install webpack 
            ```
            npm install --save-dev webpack webpack-cli
            ```  

    <a name="dependencies"></a>   
    #
1. dependencies   
    1. install development dependencies   
        ```
        npm install --save-dev  html-webpack-plugin html-loader file-loader  style-loader css-loader postcss-loader autoprefixer  sass-loader node-sass  optimize-css-assets-webpack-plugin mini-css-extract-plugin  babel-loader @babel/core @babel/preset-env  uglifyjs-webpack-plugin  webpack webpack-cli
        ```   
        >- Read documentation for details on loading and extracting css    
        >   https://webpack.js.org/loaders/sass-loader   
        > - solution for `url(...)` path using a variable is mentioned at the following url:   
        >   https://webpack.js.org/loaders/sass-loader/#problems-with-url-    

    2. install production dependencies   
        ```
        npm install --save bootstrap jquery
        ```  

    <a name="directories"></a>   
    #
1. Create source directories and files for __HTML__, __CSS__, and __JS__:  
    ```
    mkdir -p src/js/inc src/css/inc src/html/inc && touch src/js/app.js src/css/styles.scss src/index.html .babelrc webpack.config.js 
    ```
    - first lines in `app.js`   
        ```
        import '../css/styles.scss'
        import '../img/logo.png'

        var $ = require('jquery');
        ``` 

    - first lines in `styles.scss`  
        ```
        @import "../../node_modules/bootstrap/scss/bootstrap-reboot.scss";
        ``` 

    - use `HTML partials`   
        ```
        ${require('./inc/component.html')}
        ```

    - place this inside the `.babelrc` file (file-relative configuration)  
        ```
        {
            "presets": ["@babel/preset-env"]
        }
        ```  

    - sample `webpack.config.js`    
        ```
        // ./node_modules/.bin/webpack - v
        // 4.22 .0

        const path = require('path');
        const HtmlWebPackPlugin = require("html-webpack-plugin");
        const MiniCssExtractPlugin = require("mini-css-extract-plugin");

        module.exports = {
            entry: './src/js/app.js',
            output: {
                filename: 'bundle.js',
                path: path.resolve(__dirname, 'dist')
            },
            module: {
                rules: [{
                        test: /\.js$/,
                        exclude: /node_modules/,
                        use: {
                            loader: 'babel-loader',
                        }
                    },
                    {
                        test: /\.html$/,
                        use: [{
                            loader: "html-loader",
                            options: {
                                minimize: false,
                                interpolate: true
                            }
                        }]
                    },
                    {
                        // test: /\.css$/,
                        test: /\.scss$/,
                        use: [
                            // "style-loader",
                            MiniCssExtractPlugin.loader,
                            "css-loader",
                            "sass-loader"
                        ]
                    },
                    {
                        test: /\.(png|jpg|gif)$/,
                        use: [{
                            loader: 'file-loader',
                            options: {
                                name: '[name].[ext]',
                                outputPath: 'images/'
                            }
                        }]
                    }
                ]
            },
            plugins: [
                new MiniCssExtractPlugin({
                    filename: '[name].css',
                    // chunkFilename: "[id].css"
                }),
                new HtmlWebPackPlugin({
                    template: "./src/html/index.html",
                    filename: "index.html"
                })
            ]
        }
        ```  
    <a name="run"></a>   
    #
1. finding a script and running a script
    - see the list of scripts
        ```
        npm run
        ```
    - run a script
        ```
        npm run develop
        ```
    - or select from list using `ntl` (installed globally)    
        https://www.npmjs.com/package/ntl  
        ```
        npm install -g ntl
        ```
        ```
        ntl
        ```

