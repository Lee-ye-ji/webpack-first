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

## Autoprefixer(PostCSS)

```
$ npm i -D postcss autoprefixer postcss-loader
```

→ 총 3개의 패키지

**postcss**

: Autoprefixer 등의 다양한 스타일 후처리기 패키지

**autoprefixer**

: 스타일에 자동으로 공급 업체 접두사(Vendor prefix)를 적용하는 PostCSS의 플러그인

**postcss-loader**

: PostCSS(Autoprefixer)로 스타일 파일을 처리

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
            'postcss-loader', // 추가
            'sass-loader'
            ]
        }
        ]
    },
```
    
**`🧩 package.json`**
```json
"browserslist": [
    "> 1%",
    "last 2 versions"
  ]
```

**`🎈.postcssrc.js`**

```jsx
module.exports = {
    plugins: [
        require('autoprefixer')
    ]
}
```

- module.exports를 통해서 할당된 내용을 밖으로 내보내기를 하고 node.js에서 동작됨
- 내부에  plugins옵션에 postcss의 플러그인으로 사용할 autoprefixer라는 패키지를 require함수를 통해서 가지고 와서 직접적으로 연결해주는 그런 코드를 작성함!
 
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
