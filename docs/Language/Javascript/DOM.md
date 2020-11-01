# DOM(Document Object Model)

DOM은 웹사이트를 유저와 상호작용할 수 있도록 만들기 위해서 꼭 필요합니다.

DOM은 프로그래밍 언어가 웹사이트의 내용(content), 구조(structure) 그리고 스타일을 조작할 수 있게 만들어줍니다.

웹사이트는 액션을 취하는데 사용자가 불완전한 형태의 폼을 제출했을 때는 에러를 보여주고 네비게이션 메뉴를 토글했을 때는 이미지를 보여주는 것과 같이 화면을 전환합니다. 

이러한 일들이 자바스크립트에 접근하여 DOM을 조작한 결과입니다.

- 웹사이트는 HTML Document라는 것을 포함합니다. 웹사이트를 보기 위해 HTML과 CSS를 브라우저가 해석합니다. 그리고 페이지에 렌더링을 하게 되는 것입니다.
- HTML과 CSS를 파싱하기 위해서, 브라우저는 Document Object Model이라 불리는 document의 겉모양(representation)을 만듭니다. 이 **모델(model)** 은 자바스크립트가 오브젝트로서의 웹사이트 document의 컨텐트와 엘리먼트에 접근할 수 있도록 해줍니다.

# Document 객체(Document Object)

document 객체는 우리가 웹사이트에 접근하고 수정할 수 있는 많은 **프로퍼티(properties)** 와 **메소드(methods)** 를 가진 빌트인 오브젝트입니다.

- 콘솔에 `document` 를 타이핑해보면 document 객체에 대한 결과를 볼 수 있다.

```jsx
// #document
<!DOCTYPE html>
<html lang="en">

  <head>
    <title>Learning the DOM</title>
  </head>

  <body>
    <h1>Document Object Model</h1>
  </body>

</html>
```

# DOM과 HTML의 차이점

- DOM은 자바스크립트 클라이언트 사이드에 의해 수정이 되고, 브라우저는 소스코드에 존재하는 에러를 자동으로 고친다. 하지만 html은 그렇지 않다.
