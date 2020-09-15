# Babel로 원하는 타겟 브라우저 설정하기

- 현재 진행하고 있는 프로젝트의 타겟 굉장히 다양할 것이다.
한국,미국,연령층,성별 등 수 없이 많은 선택지가 있지만, '한국에서 1% 이상의 점유율을 가지고 있는 브라우저에서 사용하겠다.' 와 같은 타겟을 설정해줄 수 있는 방법이 있다.

```jsx
// webpack.config.js (webpack을 설정해주는 곳)

module: {
    rules: [
      {
        test: /\.jsx?/,
        loader: "babel-loader",
        options: {
          presets: ["@babel/preset-env", "@babel/preset-react"]
        }
      }
    ]
  }
```

- 이와 같은 모습이 일반적이지만 타겟을 따로 설정해주고 싶을 경우에는 아래와 같이 설정할수도 있다.

```jsx
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
  }
```

- 이처럼 한국에서 5% 이상의 점유율을 가진 브라우저, 지난 2크롬 버전 등 다양한 설정을 해줄 수 있다.

### 세부적인 내용은 아래 링크에서!!

[https://github.com/browserslist/browserslist](https://github.com/browserslist/browserslist)
