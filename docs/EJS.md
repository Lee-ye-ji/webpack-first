## EJS 템플릿 사용하기

**html-webpack-plugin**

: 최초 실행될 HTML 파일(템플릿)을 연결

```
$ npm i -D html-webpack-plugin
```

**`🌐 webpack.config.js`** 에 다시 작성
```jsx
...
const HtmlPlugin = require('html-webpack-plugin');

// export
module.exports = {
   ...

    // 번들링 후 결과물의 처리 방식 등 다양한 플러그인들을 설정
    plugins: [
        new HtmlPlugin({
        template: './index.html',
        })
    ]
}
```
그 후 

```
$ npm run dev
```

을 통해 실행해보면 

**`http://[::]:8080/`** 같은 서버가 나올 수 있음

그러므로 plugins 뒤에 **devServer** 설정해 줌!

```jsx
// 개발 서버 옵션
    devServer: {
        host: 'localhost',
    }
```