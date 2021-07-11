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
**`🧩 package.json`**<br>

`"test": "echo \"Error: no test specified\" && exit 1"` -> 삭제
```json
"scripts": {
    "dev" : "webpack-dev-server --mode development",
    "bulid": "webpack --mode production"
  },
```
Parcel Bundler와 달리 구성파일을 제공해야함!<br>

**`🌐 webpack.config.js`**<br>
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


### [EJS 템플릿 사용하기](./docs/EJS.md)
### [Favicon 적용](./docs/Favicon.md)
### [CSS](./docs/css.md)   
### [SCSS](./docs/scss.md) 
### [Autoprefixer(PostCSS)](./docs/Autoprefixer.md) 
### [babel](./docs/babel.md) 

