## SCSS

css → scss로 변경

```jsx
import './scss/main.scss';
```

**`🌐 webpack.config.js`**

```jsx
// 모듈 처리 방식을 설정
    module: {
        rules: [
        {
            test: /\.s?css$/,
            use: [
            // 순서 중요!
            'style-loader',
            'css-loader',
            'sass-loader'
            ]
        }
        ]
    },
```

**sass-loader**: SCSS(Sass) 파일을 로드

```
$ npm i -D sass-loader sass
```