# webpack-first
![logo](https://user-images.githubusercontent.com/59958929/125202104-14bbbe80-e2ad-11eb-8427-d8730b0b37de.png)
- 매우 꼼꼼한 구성
- 중 / 대형 프로젝트에 적합

### 참고자료(출처)
[Webpack - 1 - 시작하기 / EJS / SASS(SCSS)](https://heropy.blog/2017/10/18/webpack_1_start_ejs_sass/)

## Webpack을 시작해보자!
폴더를 만든 후 
```
$ npm init -y
$ npm i -D 
```
***`🧩 package.json`***<br>

`"test": "echo \"Error: no test specified\" && exit 1"` -> 삭제
```json
"scripts": {
    "dev" : "webpack-dev-server --mode development",
    "bulid": "webpack --mode production"
  },
```
Parcel Bundler와 달리 구성파일을 제공해야함!<br>

***`🌐 webpack.config.js`***<br>
브라우저에서 동작하는 것이 아니라 node.js환경에서 동작함
```jsx
// import
const path = require('path');
// node.js 환경에서 사용할 수 있는 path라는 전역모듈을 가지고 와서 path라는 변수에다가 할당함

// export
module.exports = {
    // 파일을 읽어들이기 시작하는 진입점 설정
    entry: './js/main.js',
    
    // 결과물(번들)을 반환하는 설정
    output: {
        // path: 'dist', // path는 node.js에서 제공하는 절대경로를 필요로 함(상대경로로 하면 안됨!)
        path : path.resolve(__dirname, 'dist'), // __dirname : 전역변수 // dist라는 폴더에다가 반환하겠다는 의미
        // resolve는 첫번째 인수와 두번째 인수를 합쳐주는 역할을 함
        // __dirname : 현재 파일이 있는 그 경로를 지칭함 dist라는 경로를 합쳐서 path에다가 제공함
        // dist라는 폴더에다가 main.js라는 파일이름으로 entry에서 진입점으로 사용한 main.js에 연결된 내용들을 번들로 만들어서 합쳐서 내어줌
        filename: 'main.js' 
    },
}
```

그 후 터미널에 npm run bulid를 입력해주면 dist라는 폴더가 생긴 뒤 main.js가 생겨남!
```jsx
// path: NodeJS에서 파일 및 디렉토리 경로 작업을 위한 전역 모듈
const path = require('path')
const HtmlPlugin = require('html-webpack-plugin')
const CopyPlugin = require('copy-webpack-plugin')

module.exports = {
  // 파일을 읽어들이기 시작하는 진입점 설정
  entry: './js/main.js',

  // 결과물(번들)을 반환하는 설정
  output: {
    // 주석은 기본값!, `__dirname`은 현재 파일의 위치를 알려주는 NodeJS 전역 변수
    // path: path.resolve(__dirname, 'dist'),
    // filename: 'main.js',
    clean: true
  },
}
```

### EJS 템플릿 사용하기

**html-webpack-plugin: 최초 실행될 HTML 파일(템플릿)을 연결**

```
**$** npm i -D html-webpack-plugin
```

🌐**`webpack.config.js`**에 다시 작성
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

### Favicon 적용

[ICO Convert - Create Icons From PNG & JPG Images Online](https://icoconvert.com/)

png → Favicon 변경해주는 사이트를 이용해서 폴더에 담은 후 아래의 디렉토리 처럼 변경

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/67c1b93a-2f6e-452a-8118-61ef1b4a8b95/Untitled.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/67c1b93a-2f6e-452a-8118-61ef1b4a8b95/Untitled.png)

- statc 폴더 생성 후 favicon.ico
- images 폴더 생성 후 logo.png

**copy-webpack-plugin: 정적 파일(파비콘, 이미지 등)을 제품(dist) 폴더로 복사**

```
npm i -D copy-webpack-plugin
```

**`webpack.config.js`**

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
