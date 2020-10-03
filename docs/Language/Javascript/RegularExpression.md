# 정규표현식

- 문자열에서 특정 내용을 찾거나 대체 또는 발췌하는데 사용한다.
- 정규표현식은 `/regexp/i` 와 같이 구성된다.

```jsx
/ // 시작기호
regexp // 패턴
/ // 종료기호
i // 플래그
```

```jsx
const str = "Hello, Jehyuk";
const reg = /jehyuk/i;

console.log(reg.exec(str));         
// ["Jehyuk", index: 7, input: "Hello, Jehyuk", groups: undefined]
console.log(reg.test(str));     // true

console.log(str.match(reg));    
// ["Jehyuk", index: 7, input: "Hello, Jehyuk", groups: undefined]
console.log(str.replace(reg, "JEHYUK"));    // Hello, JEHYUK
console.log(str.search(reg));        // 7
console.log(str.split(reg));         // ["Hello, ", ""]
```

---

## 플래그 의미

- 플래그는 **옵션**이므로 선택적으로 사용한다. 플래그를 사용하지 않은 경우 **문자열 내 검색 매칭 대상이 1개 이상**이더라도 **첫번째 매칭한 대상만을 검색하고 종료**한다.
- i
- Ignore Case, 대소문자를 구별하지 않고 검색한다.
- g
- Global, 문자열 내의 모든 패턴을 검색한다.
- m
- Multi Line, 문자열의 행이 바뀌더라도 검색을 계속한다.

```jsx
const str = "THIS is a gift";
const reg = /is/;     // 플래그가 없다.

console.log(str.match(reg));
// ["is", index: 5, input: "THIS is a gift", groups: undefined]
// 대문자를 스킵하고 'is를 찾아준다.

/////////////////////

const str = "THIS is a gift";
const reg = /is/gi;    // gi플래그를 붙였다.

console.log(str.match(reg));     // ["IS", "is"]
                                 // 대소문자를 가리지 않고 끝까지 전부 찾아준다.
```

---

## 패턴

- 패턴에는 검색하고 싶은 문자열을 지정한다.
- 문자열의 따옴표는 생략한다.
- 따옴표를 포함하면 따옴표까지도 검색한다.
- 패턴은 특별한 의미를 가지는 메타문자 또는 기호로 표현할 수도 있다.

### 기호 .

```jsx
const str = "AA BB Aa Bb";
const reg = /.../gi;      // .은 임의의 문자 1개를 의미한다.
                          // ...은 임의의 문자 3개를 의미한다.

console.log(str.match(reg));  // ["AA ", "BB ", "Aa "]
                              // 3개의 문자들을 전부 가져온다.

/////////

const str = "AA BB Aa Bb";
const reg = /./gi;         // 임의의 문자 1개 , 즉 모든 문자를 가져온다.

console.log(str.match(reg));     
// ["A", "A", " ", "B", "B", " ", "A", "a", " ", "B", "b"]
```

### 기호 +

```jsx
const str = "AA BB Aa Bb AAA";
const reg = /A+/g;        // +기호는 A가 최소 1번이상 반복되는 것들은 모두 가져온다는 뜻이다.

console.log(str.match(reg)); // ["AA", "A", "AAA"]
                             // 플래그에 i가 없으므로 소문자는 가져오지 않는다.
```

### 기호 |

```jsx
const str = "AA BB Aa Bb AAA";
const reg = /A|B/g;    // |기호는 or의 의미를 가진다.

console.log(str.match(reg));  // ["A", "A", "B", "B", "A", "B", "A", "A", "A"]

///////////

const str = "AA BB Aa Bb AAA";
const reg = /A+|B+/g;    // |기호와 +기호를 같이 사용할 수도 있다.
// const reg = /[AB]+/g;    // 위와 동일한 의미를 가진다.
                            // A+|B+ === [AB]+

console.log(str.match(reg));   // ["AA", "BB", "A", "B", "AAA"]
```

### 기호 -

```jsx
const str = "AA BB CC FF HH ZZ";
const reg = /[A-Z]+/g;      // A 부터 Z까지 문자 1개 이상의 값을 가져온다.

console.log(str.match(reg));  // ["AA", "BB", "CC", "FF", "HH", "ZZ"]

///////////

const str = "Aa Bb Cc Ff Hh Zz";
const reg = /[A-Za-z]+/g;
// const regexr = /[A-Z]+/gi;  // 위와 동일하다.
// 'A' ~ 'Z' 또는 'a' ~ 'z'가 한번 이상 반복되는 문자열을 반복 검색

console.log(str.match(reg));
// ["Aa", "Bb", "Cc", "Ff", "Hh", "Zz"]
```

### 숫자

```jsx
const str = "Aa Bb Cc 20,500,123";
const reg = /[0-9]+/g;  // '0' ~ '9'가 한번 이상 반복되는 문자열을 반복 검색

console.log(str.match(reg));  // ["20", "500", "123"]

////////////

const str = "Aa Bb Cc 20,500,123";
const reg = /[0-9,]+/g;  // '0' ~ '9' 또는 ','가 한번 이상 반복되는 문자열을 반복 검색

console.log(str.match(reg));  // ["20,500,123"]
```

- 콤마를 통해서 값이 분리되므로 패턴에 포함시킨다.

### \d , \D

- 숫자를 의미

```jsx
const str = "Aa Bb Cc 20,500,123";
const reg = /[\d,]+/g;   // '0' ~ '9' 또는 ','가 한번 이상 반복되는 문자열을 반복 검색

console.log(str.match(reg));  // ["20,500,123"]

/////////////

const str = "Aa Bb Cc 20,500,123";
const reg = /[\D,]+/g;   
// '0' ~ '9'가 아닌 문자(숫자가 아닌 문자) 또는 ','가 한번 이상 반복되는 문자열을 반복 검색

console.log(str.match(reg)); // ["Aa Bb Cc ", ",", ","]

```

### \w , \W

- 알파벳과 숫자를 의미

```jsx
const str = "Aa Bb Cc 20,500,123";
const reg = /[\w,]+/g;    // 알파벳과 숫자 또는 ','가 한번 이상 반복되는 문자열을 반복 검색

console.log(str.match(reg));  // ["Aa", "Bb", "Cc", "20,500,123"]

/////////////

const str = "Aa Bb Cc 20,500,123";
const reg = /[\W,]+/g;   
// 알파벳과 숫자가 아닌 문자 또는 ','가 한번 이상 반복되는 문자열을 반복 검색

console.log(str.match(reg));  // [" ", " ", " ", ",", ","]
```

---

### 자주 사용되는 정규표현식

- 특정 단어로 시작하는지

```jsx
const url = 'http://example.com';

// 'http'로 시작하는지 검사
// ^ : 문자열의 처음을 의미한다.
const regexr = /^http/;

console.log(regexr.test(url)); // true
```

- 특정 단어로 끝나는지

```jsx
const fileName = 'index.html';

// 'html'로 끝나는지 검사
// $ : 문자열의 끝을 의미한다.
const regexr = /html$/;

console.log(regexr.test(fileName)); // true
```

- 숫자인지

```jsx
const targetStr = '12345';

// 모두 숫자인지 검사
// [^]: 부정(not)을 의미한다. 얘를 들어 [^a-z]는 알파벳 소문자로 시작하지 않는 모든 문자를 의미한다.
// [] 바깥의 ^는 문자열의 처음을 의미한다.
const regexr = /^\d+$/;

console.log(regexr.test(targetStr)); // true
```

- 하나 이상의 공백으로 시작하는지

```jsx
const targetStr = ' Hi!';

// 1개 이상의 공백으로 시작하는지 검사
// \s : 여러 가지 공백 문자 (스페이스, 탭 등) => [\t\r\n\v\f]
const regexr = /^[\s]+/;

console.log(regexr.test(targetStr)); // true
```

- 아이디로 사용가능한지

```jsx
const id = 'abc123';

// 알파벳 대소문자 또는 숫자로 시작하고 끝나며 4 ~10자리인지 검사
// {4,10}: 4 ~ 10자리
const regexr = /^[A-Za-z0-9]{4,10}$/;

console.log(regexr.test(id)); // true
```

- 메일 주소 형식에 맞는지

```jsx
const email = 'ungmo2@gmail.com';

const regexr = /^[0-9a-zA-Z]([-_\.]?[0-9a-zA-Z])*@[0-9a-zA-Z]([-_\.]?[0-9a-zA-Z])*\.[a-zA-Z]{2,3}$/;

console.log(regexr.test(email)); // true
```

- 핸드폰 번호 형식에 맞는지

```jsx
const cellphone = '010-1234-5678';

const regexr = /^\d{3}-\d{3,4}-\d{4}$/;

console.log(regexr.test(cellphone)); // true
```

- 특수문자를 포함하고 있는지

```jsx
const targetStr = 'abc#123';

// A-Za-z0-9 이외의 문자가 있는지 검사
let regexr = /[^A-Za-z0-9]/gi;

console.log(regexr.test(targetStr)); // true

// 아래 방식도 동작한다. 이 방식의 장점은 특수 문자를 선택적으로 검사할 수 있다.
regexr = /[\{\}\[\]\/?.,;:|\)*~`!^\-_+<>@\#$%&\\\=\(\'\"]/gi;

console.log(regexr.test(targetStr)); // true

// 특수 문자 제거
console.log(targetStr.replace(regexr, '')); // abc123
```

---

## 정규표현식 생성

```jsx
new RegExp(pattern[, flags])
```

```jsx
// 정규식 리터럴
/ab+c/i;

new RegExp('ab+c', 'i');

new RegExp(/ab+c/, 'i');

new RegExp(/ab+c/i); // ES6
```

---
