## SCSS

css β scssλ‘ λ³κ²½

```jsx
import './scss/main.scss';
```

**`π webpack.config.js`**

```jsx
// λͺ¨λ μ²λ¦¬ λ°©μμ μ€μ 
    module: {
        rules: [
        {
            test: /\.s?css$/,
            use: [
            // μμ μ€μ!
            'style-loader',
            'css-loader',
            'sass-loader'
            ]
        }
        ]
    },
```

**sass-loader**: SCSS(Sass) νμΌμ λ‘λ

```
$ npm i -D sass-loader sass
```