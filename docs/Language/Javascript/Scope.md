### 변수의 유효범위 (Scope)

- 변수를 인식할 수 있는 범위를 의미한다.

### 전역변수

```jsx
var a = 100;       //전역변수

function scope() {
  console.log(a);
}

// 100
```

### 지역변수

```jsx
function scope() {
  var a = 100;          // 지역변수
}

console.log(a);

// Error

function scope() {
  var a = 100;
  console.log(a);
}

scope();

// 100
```

- 함수 안에서 만들어진 변수는 함수 안에서만 사용가능하고, 함수 바깥에서는 사용할 수 없다.

```jsx
var a = 100;              // a 함수 첫번째

function scope() {
  var a = "function 100";        // a 함수 두번째
  console.log(a);
}

scope();

// function 100
```

- 전역변수 a가 출력되지 않고 함수 안에 있는 a가 출력된다.
- 방이라고 생각했을 때 같은 방에 있는 사람을 우선적으로 부른다고 생각하면 된다.

```jsx
function scope() {
  var a = 100;

  function scope2() {
    console.log(a);
  }
  scope2();
}

scope();

// 100

function scope() {
  console.log(a);

  function scope2() {
    var a = 100;
  }
  scope2();
}

scope();

// Error
```

- 지역변수라고 무조건 다른 함수에서 접근을 못하는 것이 아니라, scope2() 입장에서는 scope()가 거실인 느낌으로 생각할 수 있다. 함수의 레벨과 포함범위에 따라서 변수 접근성이 달라진다.
- 하지만 반대로 scope2() 안에 있는 변수에는 scope()가 접근할 수 없다.
- 간단하게 말해서 방 안에서는 방 밖의 변수를 사용할 수 있지만, 방 밖에서는 방 안의 변수를 사용할 수 없다.
- 협업을 할 때 변수 유효범위와 변수 이름을 잘 생각하면서 코드를 짜야 한다. 그래서 프로젝트가 커질수록 **전역변수를 최소화**하는 게 좋다.
