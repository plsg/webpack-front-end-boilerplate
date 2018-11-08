> __The Rockstar Front-end Boilerplate__  
> " Thunder of the Gods fueled with __npm__ "

___

<a name="top"></a>   

- [init](#init)
- [dependencies](#dependencies)
- [mkdir](#directories)
- [run scripts](#run)


<a name="init"></a>   
___    

<h1> Environment Information </h1>

<details>
<summary>
(click to open)
</summary>

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

</details>

```
localhost:3000
```
# webpack usage

## resources:  
> BEGINNER GUIDES, initial settings and config for Babel, React, SCSS==CSS, HTML, and more ...    
    https://medium.com/javascript-in-plain-english/its-time-for-you-to-learn-webpack-45d2b08ae754    
    https://hackernoon.com/a-tale-of-webpack-4-and-how-to-finally-configure-it-in-the-right-way-4e94c8e7e5c1  
    ~~https://www.valentinog.com/blog/webpack-tutorial/#webpack_4_extracting_CSS_to_a_file~~  
    ~~https://www.sitepoint.com/beginners-guide-webpack-module-bundling/~~   


## instructions:  

___  
  
### __Webpack + REACT boilerplate__   
<!-- <details> -->
<summary>
(click to open)
</summary>

1. create project
    ```   
    npm init -y
    mkdir src
    touch src/index.js
    mkdir src/components
    touch src/components/App.js 
    npm i react react-dom   
    ```   
2. webpack and babel
    ```
    npm i -D webpack webpack-cli webpack-dev-server html-webpack-plugin
    npm i -D babel-core babel-loader@7 babel-preset-env babel-preset-react 
    ```   
3. create `webpack.config.js`
    ```
    touch webpack.config.js
    ```
    > ```
    > const path = require('path')
    > const HTMLWebpackPlugin = require('html-webpack-plugin')
    >
    > module.exports = {
    >    entry: './src/index.js',
    >    output: {
    >        path: path.join(__dirname, '/dist'),
    >        filename: 'bundle.js'
    >    },
    >    module: {
    >        rules: [
    >            {
    >                test: /\.js$/,
    >                exclude: /node_modules/,
    >                use: {
    >                    loader: 'babel-loader'
    >                }
    >            }
    >        ]
    >    },
    >    plugins: [
    >        new HTMLWebpackPlugin({
    >            template: './src/index.html'
    >        })
    >    ]
    >}
    >```   
4. create scripts in `package.json`  
    >```
    >"scripts": {
    >    "start": "webpack-dev-server --mode development --open --hot",
    >    "build": "webpack --mode production"
    >}
    >```
5. create `.babelrc`
    ```
    touch .babelrc
    ```
    >```
    > {
    >    "presets": ["env", "react"]
    >}
    >```

</details>   

___  

### create a `package.json` file  
<details>
<summary>(click to open)</summary>

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

</details>  

<a name="dependencies"></a>   

#

### dependencies   
<details>
<summary>(click to open)</summary>

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
</details>

<a name="directories"></a>   

#

### Create source directories and files for __HTML__, __CSS__, and __JS__:  
<details>
<summary>(click to open)</summary>

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

</details>

# 

### sample `webpack.config.js`    
<details>
<summary>(click to open)</summary>  

```
// ./node_modules/.bin/webpack -v
// 4.22 .0
``` 
``` 
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

</details>

<a name="run"></a>   

#

### finding a script and running a script

<details>
<summary>(click to open)</summary>  
   
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

</details>


#   
- [back to top](#top)





