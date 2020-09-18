### 1\. join()

```jsx
const color = ["red", "blue", "green"];

const result = color.join();  // 인자가 없으면 쉼표가 디폴트이고, 인자를 넣으면 쉼표 대신 들어감

console.log(result);

// red,blue,green
const arr = arr.join();                // 콤마로 기본 인식
const arr2 = arr2.join( ' / ' );       // 콤마 대신 ' / ' 로 인식
```

-   배열에 있는 원소들을 하나의 값으로 만들어주는 메서드이다.
-   원소들의 구분은 콤마(,)가 디폴트, 구분을 다른 문자로 하고 싶으면 ()안에 넣고 싶은 문자를 넣으면 된다.

### 2\. split()

```jsx
const color = "red,blue,green,yellow";

const result = color.split(",", 3);   // 쉼표를 기준으로 나눔 , 뒤에 limit를 정해놓을 수 있음 
                                      // 옵션이므로 limit은 생략이 가능하다.
console.log(result);

// ["red", "blue", "green"]           // limit 이 3이라서 yellow는 짤리고 출력

const color = "red,blue,green,yellow";

const result = color.split("and", 3);  // 쉼표를 기준으로 나누지 않고, and로 작성을 해봤다.

console.log(result);

// ["red,blue,green,yellow"]           // 쉼표 기준으로 분할되지 않아서 하나의 문자열이 배열에 담김.
string.split( separator, limit )      // separator에는 분할의 기준을 넣고,  ex) ','
                               // limit에는 최대 분할 개수를 지정,값을 정하지 않으면 전체 분할
```

-   문자열을 분할하는 메서드이다.

### 3\. reverse()

```jsx
const color = ["red", "blue", "green", "yellow"];

const result = color.reverse();

console.log(color);          // ["yellow", "green", "blue", "red"]
console.log(result);         // ["yellow", "green", "blue", "red"]
```

-   배열의 원소 순서를 반대로 만드는 메서드이다.
-   **순서가 바뀐 배열을 새로 만드는 것이 아니라, 기존 배열의 순서를 바꾼다.**

### 4\. slice()

```jsx
const color = ["red", "blue", "green", "yellow"];

const result = color.slice(1, 3);   // 1번 인덱스(blue)부터 3번 인덱스 전(green)까지 출력

console.log(result);

// ["blue", "green"]
array.slice(start, end)      // start와 end에는 숫자가 들어간다.
                         // 배열의 start에 해당하는 인덱스부터 end 바로 전의 인덱스까지 선택해서
                         // 새로운 배열을 만든다.
                         // end 값이 없으면 마지막까지 출력
```

### 5\. find()

```jsx
const color = ["red", "blue", "green", "yellow"];

const result = color.find((a) => a === "blue");      // a가 blue인 것을 찾아옴

console.log(result);

// blue

const color = ["red", "blue", "green", "yellow"];

const result = color.find((a) => a === "purple");    // a가 purple인 것을 찾음

console.log(result);

// undefined
array.find(callback[, thisArg])       
```

-   주어진 콜백 함수를 만족하는 **첫 번째 요소의 값**을 반환하는 메서드이다. 그런 요소가 없다면 undefined를 반환한다.

### 6\. filter()

```jsx
const color = [1, 2, 3, 4, 5, 6];

const result = color.filter((a) => a % 2 == 1);   // a 나누기 2의 나머지가 1인 것을 찾음

console.log(result);

// [1, 3, 5]
array.filter(callback(element[, index[, array]])[, thisArg])
```

-   콜백함수에서 true의 값을 출력한 요소로 이루어진 새로운 배열을 만드는 메서드이다. 어떤 요소도 테스트를 통과하지 못했으면 빈 배열을 반환한다.

### 7\. map()

```jsx
const color = [1, 2, 3, 4, 5, 6];

const result = color.map((item) => item * 2);    // color의 모든 요소를 가져와서 2를 곱해줌

console.log(result);

// [2, 4, 6, 8, 10, 12]
array.map(callback(currentValue[, index[, array]])[, thisArg])
```

-   배열의 각 요소에 대해 실행한 콜백함수의 결과를 모아서 새로운 배열을 만들어 주는 메서드이다.

### 8\. every()

```jsx
const person = [
  { name: "jehyuk", color: "red" },
  { name: "jisu", color: "black" },
  { name: " hyangsuk", color: "brown" },
];

const result = person.every((person) => person.name == "jehyuk");   

console.log(result);         // 모든 name의 value가 "jehyuk"이 아니라면 false

// false
```

-   조건을 만족하지 않는 값이 발견되면 즉시 중단되면서 false를 , 모든 조건을 만족하면 true를 리턴한다.

### 9\. some()

```jsx
const person = [
  { name: "jehyuk", color: "red" },
  { name: "jisu", color: "black" },
  { name: " hyangsuk", color: "brown" },
];

const result = person.some((person) => person.name === "jehyuk");

console.log(result);

// true
```

-   조건을 만족하는 값이 발견되면 즉시 중단하면 true를, 모든 조건에 만족하지 않으면 false를 리턴한다.

### 10\. reduce() - 어려움🔥

```jsx
let number = [1, 2, 3, 4, 5];

let result = number.reduce((a, b) => a + b, 0);  // 초기값 0부터 시작해서 아래의 과정을 거친다

console.log(result);
                    // 초기값 0부터 더해지기 시작한다.
// 0 1              // a에는 누적값이 없으므로 0, b에는 0번째 인덱스인 1
// 1 2              // a에는 누적값인 1, b에는 1번째 인덱스인 2
// 3 3              // a에는 누적값인 3, b에는 2번째 인덱스인 3
// 6 4              // a에는 누적값인 6, b에는 3번째 인덱스인 4
// 10 5             // a에는 누적값인 10, b에는 4번째 인덱스인 5
// 15          => 결국 15 가 출력된다.
array.reduce((누적값, 현잿값, 인덱스, 요소) => { return 결과 }, 초깃값);
```

-   굉장히 어려운 개념이지만 덧셈말고도 다양하게 활용된다. 이전까지 배웠던 개념들도 reduce()로 충분히 구현할 수 있다.

### 11\. sort()

-   숫자

```jsx
const num = [222, 123, 135, 31];

const result = num.sort();    // 아스키코드 순으로 정렬되어 숫자의 크기대로 정렬되지 않는다.

console.log(result);

// [123, 135, 222, 31]
// 오름차순 정렬

const num = [222, 123, 135, 31];

const result = num.sort((a, b) => a - b);

console.log(result);

// [31, 123, 135, 222]
// 내림차순 정렬

const num = [222, 123, 135, 31];

const result = num.sort((a, b) => b - a);

console.log(result);

// [222, 135, 123, 31]
```

-   문자

```jsx
const num = ["abc", "ag", "daf", "z"];

const result = num.sort();

console.log(result);

// ["abc", "ag", "daf", "z"]
// 이름 오름차순 정렬

const num = [
  { name: "john", age: 27 },
  { name: "alice", age: 25 },
  { name: "adam", age: 29 },
  { name: "smith", age: 31 },
  { name: "sujan", age: 19 },
];

const result = num.sort((a, b) =>
  a.name < b.name ? -1 : a.name > b.name ? 1 : 0
);

console.log(result);

// 0: {name: "adam", age: 29}
// 1: {name: "alice", age: 25}
// 2: {name: "john", age: 27}
// 3: {name: "smith", age: 31}
// 4: {name: "sujan", age: 19}
// 이름 내림차순 정렬

const num = [
  { name: "john", age: 27 },
  { name: "alice", age: 25 },
  { name: "adam", age: 29 },
  { name: "smith", age: 31 },
  { name: "sujan", age: 19 },
];

const result = num.sort((a, b) =>
  a.name > b.name ? -1 : a.name < b.name ? 1 : 0
);

console.log(result);

// 0: {name: "sujan", age: 19}
// 1: {name: "smith", age: 31}
// 2: {name: "john", age: 27}
// 3: {name: "alice", age: 25}
// 4: {name: "adam", age: 29}
```
