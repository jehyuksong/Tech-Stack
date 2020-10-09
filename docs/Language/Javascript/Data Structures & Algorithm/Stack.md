# Stack(스택)

- 데이터를 집어넣을 수 있는 선형 자료형이다.
- 나중에 넣은 데이터가 먼저 나온다.
- LIFO(Last In First Out) 이라고도 부른다.
- 데이터를 집어넣는 push, 데이터를 꺼내는 pop, 데이터를 확인하는 peek 등의 작업이 가능하다.

```jsx
/* Stacks! */

// functions: push, pop, peek, length

// 이 배열이 사용할 스택이다.
const letters = []; 

// 임의의 단어를 만든다.
const word = "songjehyuk"

// 단어를 거꾸로 했을 때 뭐라고 나오는 지 확인해야 하기 때문에 빈 문자열로 만든다.
let rword = "";

// 스택에 아까 만든 단어를 1글자씩 넣는다.
for (var i = 0; i < word.length; i++) {
   letters.push(word[i]);
}
console.log(letters) // ["s", "o", "n", "g", "j", "e", "h", "y", "u", "k"]

// 스택에서 아까 만든 단어를 1글자씩 빼낸다.
for (var i = 0; i < word.length; i++) {
   rword += letters.pop(); 
}
console.log(rword) // kuyhejgnos

// 만약 단어와 거꾸로 한 단어가 같다면 bob 처럼 거꾸로 해도 같은 회문 구조의 단어이고,
// 그렇지 다르다면 회문 구조가 아닌 단어이다.
if (rword === word) {
   console.log(word + "은 회문 구조이다.");
}else {
   console.log(word + "은 회문 구조가 아니다.");
}
// songjehyuk은 회문 구조가 아니다.

// 스택함수 만들기
const Stack = function() {
    this.count = 0;
    this.storage = {};
  
    // 스택의 마지막에 값을 넣는다.
    // 값을 넣고 count를 1 더해준다.
    this.push = function(value) {
        this.storage[this.count] = value;
        this.count++;
    }
    
    // 스택의 마지막에 있는 값을 추출하고 리턴한다.
    this.pop = function() {
        if (this.count === 0) {
            return undefined;
        }

        this.count--;
        var result = this.storage[this.count];
        delete this.storage[this.count];
        return result;
    }
    
    this.size = function() {
        return this.count;
    }
    
    // 스택의 마지막의 값을 확인하고 리턴한다.
    this.peek = function() {
        return this.storage[this.count-1];
    }
}

// 새로운 스택을 만든다.
const myStack = new Stack();
myStack.push(1); // 1 추가
myStack.push(3); // 3 추가
myStack.push(2); // 2 추가
console.log(myStack.count); // 3,
console.log(myStack.size()); // 3, myStack에 3개의 값이 있다.
console.log(myStack.peek()); // 2, myStack의 마지막 값은 2 이다.
myStack.pop(); // 값을 추출해낸다.
console.log(myStack.count); // 2
console.log(myStack.size()); // 2, myStack에 2개의 값이 있다.
console.log(myStack.peek()); // 3, myStack의 마지막 값은 3이다.
```
