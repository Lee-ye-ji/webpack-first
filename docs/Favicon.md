## Favicon 적용

[ICO Convert - Create Icons From PNG & JPG Images Online](https://icoconvert.com/)

png → Favicon 변경해주는 사이트를 이용해서 폴더에 담은 후 아래의 디렉토리 처럼 변경

![Untitled](https://user-images.githubusercontent.com/59958929/125202769-0b802100-e2b0-11eb-96df-bd5d69400723.png)

- statc 폴더 생성 후 favicon.ico
- images 폴더 생성 후 logo.png

**copy-webpack-plugin**

: 정적 파일(파비콘, 이미지 등)을 제품(dist) 폴더로 복사

```
$ npm i -D copy-webpack-plugin
```

**`🌐 webpack.config.js`**

```jsx
...
const CopyPlugin = require('copy-webpack-plugin');

// export
module.exports = {
   ...

    // 번들링 후 결과물의 처리 방식 등 다양한 플러그인들을 설정
    plugins: [
        ...
        new CopyPlugin({
        patterns: [
            { from: 'static' } // 여기서 static은 우리가 만들어 놓은 파일 이름!
        ]
        })
    ],

    ...
} 
```

그럼에도 파비콘이 chrome에 나오지 않는 경우 index.html <head></head>부분에 추가

```html
<link rel="icon" type="image/x-icon" href="favicon.ico?v=2"  />
```