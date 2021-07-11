## babel

```
$ npm i -D @babel/core @babel/preset-env @babel/plugin-transform-runtime
```

**@babel/core**

: ES6 이상의 코드를 ES5 이하 버전으로 변환

**@babel/preset-env**

: Babel 지원 스펙을 지정

**@babel/plugin-transform-runtime**

: Async/Await 문법 지원

**`🥏.babelrc.js`**

```jsx
module.exports = {
  presets: ['@babel/preset-env'],
  plugins: [
    ['@babel/plugin-transform-runtime']
  ]
}
```

**`🌐 webpack.config.js`**

```jsx
// 모듈 처리 방식을 설정
    module: {
        rules: [
				...
        {
            test: /\.js$/,
            exclude: /node_modules/, // 제외할 경로
            use: [
            'babel-loader'
            ]
        }
        ]
    },
```

```
$ npm i -D babel-loader
```

**babel-loader**: JS 파일을 로드