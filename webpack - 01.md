# 웹팩

- 자바스크립트 코드가 많아짐에 따라 관리의 한계, 코드 스코프 침범, 변수 충돌 위험성
  - 모듈을 IIFE스타일로 변경해주는 과정, 하나의 파일로 묶음(bundled)로 비용감소



## 웹팩의 장점

- 다른 module bundle에 비해 perfomance가 우수
- Code Split:chunk(코드 혹은 모듈을 묶는 하나의 단위) 단위로 의존성 트리를 동기적, 비동기적으로 분활
- Loader가 존재하여 다른 리소스를 순수 Javascript로 변환하고 모든 리소스에 대한 모듈을 구성한다.
  - babel을 사용하여 ES6와 같이 브라우저에서 지원되지 않는 script code를 변환하여 사용할 수 있다
- 3rd-party library에 대해 모듈로 통합하는 기능을 제공
- Module bundler의 대부분의 기능을 사용자가 커스터마이징하여 사용할 수 있다
- 다양한 플러그인을 제공



## 웹팩의 단점

- Spring 환경에서는 whtch로 변경을 감지해도 바로바로 리소스 업데이트되지 않는 점
- document문서가 빠르게 파악하고 사용하게끔 심플하게 구성 되지 못한점



## 사용이유

Browsify, Gruntm Gulp 등의 도구들과 차이

- webpack은 모든 리소스(javascript, css, img, fonts, etc)에 대한 dependency graph를 생성하여 빌드시켜주는 도구
- webpack은 require()를 사용하여 리소스들간의 의존성 관계를 형성시켜주며 어떤 javascript를 bundling할 것인지 결정해준다.
- 크고 복잡하며 다양한 리소스들이 들어있는 프로젝트에는webpack을 사용하는것이 최상의 선택일 것이다.
- 질문에 대한 답으로 Grunt, Gulp는 오로지 리소스들에 대한 틀로 사용되며 dependency graph에 대한 개념이 없다
- Browsify는 비슷한 도구이지만 속도면에서 webpack이 더 우월하다.



## 웹팩의 주요 4가지

- 엔트리
- 아웃풋
- 로더
- 플러그인



## 엔트리 - bundling하고 싶은 파일들을 선언

####자바스크립트가 로딩하는 모듈이 많아 질수록 의존성 그래프의 시작점을 웹팩에서는 엔트리(entry)라고 한다.

웹팩은 엔트리를 통해서 필요한 모듈을 로딩하고 하나의 파일로 묶는다.

~~~javascript
module.exports = {
    entry: {
        main: './src/main.js'
    }
    // entry 시작점 경로 지정
}

// './src/main.js' - 자바스크립트의 시작점
~~~



## 아웃풋 - bundling되고 만들어질 파일에 대한 정보 명시

#### 엔트리에 설정한 자바스크립트 파일을 시작으로 의존되어 있는 모든 모듈을 하나로 묶는다. 번들된 결과물을 처리할 위치는 output에 기록한다.

webpack.config.js

~~~javascript
module.exports = {
    output: {
        filename: 'bundle.js',
        path: './dist'
    }
}
~~~

dist 폴더의 bundle.js 파일로 결과를 저장할것이며 html파일에 번들링된 이 파일을 로딩하게끔 한다. 

index.html

~~~html
<body>
    <script src="./dist/bundle.js"></script>
</body>
~~~

엔트리에 설정한 자바스크립트는 Utils.js 모듈을 사용한다.

src/main.js

~~~javascript
import Utils from './Utils'
Utils.log('Hello webpack')
~~~

Utils.js는 코드는 다음과 같다

Src/Utils.js

~~~javascript
export default class Utils {
    static log(msg) { console.log('[LOG]' + msg)}
}
~~~

웹팩은 터미널에서 ***webpack*** 커맨드로 빌드할 수 있다.



## 로더 - bundling을 진행하며 실행되는 함수역활을 맡는다

####웹팩은 모든 파일을 모듈로 관리하고 이것은 js파일 뿐만 아니라 이미지,폰트,스타일시트도 전부 모듈로 관리한다. 그러나 웹팩은 자바스크립트만 안다. 비 자바스크립트 파일은 웹팩이 이해하게끔 변경해야하는데 로더가 그런 역활을 한다.



로더는 ***test*** 와 ***use*** 키로 구성된 객체로 설정할 수 있다.

- test에 로딩할 파일을 지정하고
- use에 적용할 호더를 설정한다.



####babel-loader

가장 간단한 예가 바벨이다. ES6에서 ES5로 변환할 때 바벨을 사용하는데 test 에 ES6로 작성한 자바스크립트 파일을 지정하고, use에 이를 변환할 바벨 로더를 설정한다.

Web pack.config.js

~~~javascript
movule.exports = {
    module: {
        rules: [{
            test: /\.js$,
            exclude: 'node_modules',
            use: {
            	loader: 'bable-loader',
            	options: {
            		presets: ['env']
        		}
        	}
        }]
    }
}
~~~

test에 자바스크립트 확장자를 갖는 파일을 정규표현식으로 지정했다. Node_moudle 폴더는 패키지 폴더이므로 제외하기 위해서 exclude에 설정한다. use에 로더를 설정하는 bable-loader를 추가했다.

로더를 사용하기 위해서는 노드 패키지로 제공하는 로더를 npm으로 추가해야한다.

~~~s
npm i --save-dev babel-loader babel-core babel-preset-env
~~~

웹팩 커맨드 라인으로 빌드하고 나면 bundle.js가 ES5 문법으로 변경된것을 확인할 수 있다.



## 플러그인

~~~javascript
plugins: [
    new webpack.optimize.OccurenceOrderPlugin(),
    new webpack.HotModuleReplacementPlugin(),
    new webpack.NoErrorsPlugin(),
    new CommonsChunkPlugin({
        name: "commons",
        filename: "common.js",
        minChunks: Infinity
    })
]
~~~

```
new webpack.optimize.OccurrenceOrderPlugin(preferEntry)
```

- 발생 시점에 따라 ID값을 할당시켜주며 자주 사용되는 ID는 더 낮은 ID를 갖습니다. 그래서 예측 가능하게 해줍니다.
- preferEntry의 우선순위를 높입니다.

```
new HotModuleReplacementPlugin()
```

- dev-server 모드에서 Hot Module Replace를 가능하게 해줍니다.

```
new NoErrorsPlugin()
```

- 컴파일 도중 오류가 일어난 리소스들은 제외시켜주고 컴파일 해줍니다.

```
new webpack.optimize.CommonsChunkPlugin(option)
```

- 공유되는 common script파일을 생성해 주며 각종 옵션을 통해 커스터마이징 설정이 가능합니다.
- [API 스펙](https://github.com/webpack/docs/wiki/list-of-plugins#commonschunkplugin)

```
UglifyJsPlugin
```

- output으로 나오는 스크립트 파일을 minify해 줍니다.
- [API 스펙](https://github.com/webpack/docs/wiki/list-of-plugins#uglifyjsplugin)

```
new ExtractTextPlugin("styles.css")
```

- js파일이 로딩되는 동안 그 안에 있는 css파일들도 같이 로드되지 못합니다.
- ExtractTextPlugin은 js bundle파일에서 css bundle파일을 분리해 줍니다.
- css bundle이 js bundle파일과 병렬로 로드되므로 프로젝트 규모가 클수록 더 빠를 것입니다.
- [API 스펙](https://github.com/webpack-contrib/extract-text-webpack-plugin)

```
EnvironmentPlugin
```

- process.env를 통해 환경 변수를 받습니다.
- 예제에서 watch mode인지 real mode인지 구분시켜주는 변수를 받습니다.

```
webpack-merge
```

- 여러 config파일들을 합쳐줍니다.

```
new webpack.WatchIgnorePlugin(paths)
```

- paths(정규식 or 경로)에 있는 리소스들은 watch시 제외됩니다.



