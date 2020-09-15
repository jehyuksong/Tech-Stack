# Webpack

- 웹팩은 모듈 번들러이다.
- 코딩할 때 편의를 위해 여러 개의 모듈로 나눠서 작업하는 경우가 많은데, 브라우저에서 파일 단위 모듈 시스템을 이용하는 것은 많은 네트워크 비용 낭비를 유발한다. 이러한 문제를 해결하기 위해서 여러 개의 모듈을 하나의 파일로 묶어서 보낼 모듈 번들러가 웹팩이다.
- 웹팩에서는 자바스크립트, 스타일시트, 이미지 등 모든 것을 모듈로 취급한다.

### Webpack의 4가지 속성

### 1. Entry

- 시작하는 파일들을 넣고, 모듈을 로딩 후에 하나로 묶어준다.

### 2. Output

- 결과물을 처리할 위치를 설정해준다.

### 3. Loader (Module)

- 다른 타입의 파일들을 웹팩이 이해하고 처리 가능한 모듈로 변환시켜준다.

### 4. Plugin

- 추가적으로 해주고 싶은 작업을 설정할 수 있다.

### Webpack  설정 예시

```jsx
// webpack.config.js

const path = require("path");
const webpack = require("webpack");

module.exports = {
  name: "wordrelay-settings",
  mode: "development",
  devtool: "eval",

  entry: {
    app: ["./client"]
  },
  module: {
    rules: [
      {
        test: /\.jsx?/,
        loader: "babel-loader",
        options: {
          presets: [
            [
              "@babel/preset-env",
              {
                targets: { browsers: [">5% in KR", "last 2 chrome versions"] }
              }
            ],
            "@babel/preset-react"
          ]
        }
      }
    ]
  },
  plugins: [new webpack.LoaderOptionsPlugin({ debug: true })],
  output: {
    path: path.join(__dirname, "dist"),
    filename: "App.js"
  }
};
```

- `entry`로 시작해서 `module`을 거치고 `output`으로 나간다고 생각하면 이해하기 쉬울 수 있다. 또한 플러그인은 추가적인 것들을 해주는데 위에 보이는 **plugins: [new webpack.LoaderOptionsPlugin({ debug: true })]**은 `loader의 options`에 전부 `{debug : true}`를 넣어주는 역할을 한다.

---
