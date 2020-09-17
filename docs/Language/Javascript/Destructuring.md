# 구조 분해 할당

- 배열과 객체를 분해해서 할당하는 것을 말한다.

```jsx
// 분해할 배열과 객체
const animals = [
  { name: "cat", sound: "meow" },
  { name: "dog", sound: "woof" }
];

// 배열 구조 분해 할당
const [cat, dog] = animals;  // animals의 [0],[1] 인덱스를 각각 할당한다.
console.log(cat);  // {name: "cat", sound: "meow"}
console.log(dog);  // {name: "dog", sound: "woof"}

// 객체 구조 분해 할당
const { name, sound } = cat;  // 구조 분해된 객체를 구조 분해 할당한다.
console.log(name);     // cat
console.log(sound);    // meow
```

- 여기서 중요한 점은 **배열을 구조 분해 할당할 때는 변수명을 원하는 대로** 지어도 되지만, **객체를 구조 분해 할당할 때는 key에 맞는 정확한 이름**으로 분해해야 한다.

```jsx
// 분해할 배열과 객체
const animals = [
  { name: "cat", sound: "meow" },
  { name: "dog", sound: "woof" }
];

// 배열 구조 분해 할당
const [a, b] = animals;  
console.log(a);  // {name: "cat", sound: "meow"}
console.log(b);  // {name: "dog", sound: "woof"}

// 객체 구조 분해 할당
const { c, d } = a;  // 구조 분해된 객체를 구조 분해 할당한다.
console.log(c);     // Error
console.log(d);     // Error
```

- **배열**은 **인덱스 순서대로 분해**되지만, **객체**는 인덱스가 없기 때문에 **정확한 Key를 입력**해줘야 한다. 혹은, 아래와 같이 사용할 수도 있다.

```jsx
// 분해할 배열과 객체
const animals = [
  { name: "cat", sound: "meow" },
  { name: "dog", sound: "woof" }
];

const [cat, dog] = animals;

const { name: catName, sound: catSound } = cat;   // 변수명을 수정해줄 수 있다.
console.log(catName);    // cat
console.log(catSound);   // meow
```

- 또한, 객체에서 특정한 값을 더하고 싶을 때 사용할 수 있는 방법이 있다.

```jsx
// 분해할 배열과 객체
const animals = [
  { name: "cat", sound: "meow" },
  { name: "dog", sound: "woof" }
];

const { name = "not cat", sound } = cat;
console.log(name);     // cat         // 이미 있는 값이 수정되지는 않는다.

const { name, sound, age = 5 } = cat;
console.log(name);     // cat
console.log(sound);    // meow
console.log(age);      // 5           // 값이 추가된

```

- 객체 안에 객체가 또 있다면 아래와 같이 분해할 수도 있다.

```jsx
const animals = [
  { name: "cat", 
    sound: "meow", 
    feedingRequirements: { 
      food: 2, water: 3 
    } 
  },
  { name: "dog", sound: "woof" }
];

const [cat, dog] = animals;

const {
  name,
  sound,
  feedingRequirements: { food, water }    // 분해하면서 안에 키의 변수를 설정해준다.
} = cat;
console.log(name);   // cat
console.log(sound);  // meow
console.log(food);   // 2
console.log(water);  // 3
```

---

```jsx
// data.js

const animals = [
  {
    name: "cat",
    sound: "meow"
  },
  {
    name: "dog",
    sound: "woof"
  }
];

const useAnimals = (animal) => {
  return [animal.name, () => console.log(animal.sound)];
};

export default animals;
export { useAnimals };

// index.js

import animals, { useAnimals } from "./data";

const [cat, dog] = animals;

const [animal, makeSound] = useAnimals(cat);

console.log(animal);
makeSound();
```

- animals 을 이용한 함수를 만들고 모듈로 불러와서 위와 같이 사용할 수도 있다.

---
