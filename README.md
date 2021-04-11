# 목적 

frontend 개발에 필요한 설정들을 하.나.씩. 추가해보기


# 순서
## 1. index.html / index.js 작성 

- 기본 문법 사용 
- 다만, index.js에는 backtick(`)을 사용(ES6문법)하여 IE에서는 동작하지 않도록 생성함

## 2. Babel 설치 

- Babel? 
    - transpiler (코드 변환기)
    - 현재 작업할 내용에서는 ES6 문법으로 작성된 코드를 ES5 문법 코드로 변환해주는 작업 
- 참고 URL : https://babeljs.io/docs/en/usage 

### 2-1. Install packages

- 참고 : npm init 없이 진행해 보았다. 

```shell
npm install --save-dev @babel/core @babel/cli @babel/preset-env
npm install --save @babel/polyfill
```

위 명령어를 실행하면 아래와 같은 일이 발생한다. 
- /node_modules 폴더가 생성됨
- package-lock.json 파일이 생성됨


## 3. 설치한 Babel 이용하여 ES6 문법으로 작성된 JS를 ES5 문법으로 변환 

### 3-1. babel.config.json 설정없이 먼저 실행해보기 
`실행병령어 변경할파일또는폴더(index.js) -out-dir 목적지폴더(lib)`

```shell
./node_modules/.bin/babel index.js --out-dir lib 
```

또는 (npm 5.2.0 버전 이상이라면 아래 명령어도 사용가능)

```shell
npx babel index.js -d lib
```

위 명령어를 실행하면 아래와 같은 일이 발생한다. 
- /lib 폴더가 생성되었고, 하위에 index.js 파일이 만들어졌다. 
- 하지만 내용은 ES6문법 그대로 보인다. (변환되지 않음)

### 3-2. babel.config.json 설정 

- `babel.config.json` 파일을 프로젝트 root에 생성 후 아래 내용을 작성 (참조URL에 있는 내용 복사한 것임)

```json
{
  "presets": [
    [
      "@babel/env",
      {
        "targets": {
          "edge": "17",
          "firefox": "60",
          "chrome": "67",
          "safari": "11.1"
        },
        "useBuiltIns": "usage",
        "corejs": "3.6.5"
      }
    ]
  ]
}
```

다시 명령어 실행해보기 
```shell
npx babel index.js -d lib
```

위 명령어를 실행하면 아래와 같은 일이 발생한다. 
- /lib/index.js 파일을 확인하면 ES5 문법으로 변경된 것을 확인할 수 있다.


index.html에서 index.js 파일 위치 지정 변경
```html
<script src="lib/index.js"></script> <!-- index.js 를 -> lib/index.js 로 변경 -->
```

* 크롬, IE 모두에서 정상 동작하는 것을 확인 할 수 있다. 