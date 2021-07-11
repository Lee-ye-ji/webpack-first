## CSS

**1) index.html에 링크 추가 하는 방법**

```html
<link rel="stylesheet" href="./css/main.css">
```

static 폴더에 css 폴더를 생성해주어도 됨!

**2) css 폴더를 root경로에 빼놓는 방법**

```jsx
import './css/main.css';
```

webpack은 main.js부터 읽기 때문에 css 파일을 읽을 수 있는 구조

but, css를 해석할 수 있는 패키지를 설치해야함!

```
$ npm i -D css-loader style-loader
```

**css-loader**

: 자바스크립트 안에 CSS를 해석하고, 모든 의존성을 해결/ CSS 파일을 로드

**style-loader**

: 로드된 스타일(CSS)을 <style>로 <head>에 삽입

**`🌐 webpack.config.js`**

```jsx
// 모듈 처리 방식을 설정
    module: {
        rules: [
        {
            test: /\.css$/, // 정규표현식
            use: [
            // 순서 중요!
            'style-loader',
            'css-loader',
            // 먼저 해석되는 로더 : css-loader
            // main.js에서 import를 통해서 css파일을 가지고 옴
            // 자바스크립트 파일에서는 css파일을 해석할 수 없기 때문에
            // css-loader : 자바스크립트에서 css파일을 해석하는 용도
            // style-loader : HTML 부분의 style부분에다가 해석된 내용을 삽입해주는 역할
            ]
        }
    },
```