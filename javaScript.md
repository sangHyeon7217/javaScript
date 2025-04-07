**JavaScript 정리노트**

---

### 변수 선언 방식

- `var` 변수는 **중복 선언** 가능  
- `let` 변수는 **중복 선언 불가**
- `const`는 **값 변경 불가**

---

### 함수는 자료형이다
- JavaScript에서 `function`은 자료형이다.

---

### 컴파일 언어 vs 인터프리터 언어

| 구분 | 컴파일 언어 | 인터프리터 언어 |
|------|--------------|------------------|
| 예시 | C, Java       | JavaScript, Python |

---

### `const`의 사용 예

```js
// 오류 발생 예
const data = [1, 2, 3];
document.write('1.결과: ' + data + '<br/>');
// data = [100, 200]; // 오류 발생
```

```js
// 배열 요소 변경은 가능
const data = [1, 2, 3];
document.write('1.결과: ' + data + '<br/>');
data[1] = 1004;
document.write('1.결과: ' + data + '<br/>');
```

> `const`로 선언된 변수는 **참조값 변경 불가**  
> → 참조 대상의 **내부 값 변경은 가능**

---

### 배열과 객체 다루기

```js
var arr = ['안녕', 'Hello', 'Hola', '곤니찌와'];
document.write(arr[2] + '<br/>');

var arr2 = ['안녕', ['Hello', 'Hola'], '곤니찌와'];
document.write(arr2[1][1] + '<br/>');

var obj = { x: '안녕', y: 'Hello', z: '곤니찌와' };
document.write('객체 프로퍼티: ' + obj.y + '<br/>');
document.write('객체 프로퍼티: ' + obj['y'] + '<br/>');

// obj.a는 undefined
document.write(obj.a);
```

---

### 변수 스왑 (비구조화 할당)

```js
let v1 = 100, v2 = 200;
[v2, v1] = [v1, v2];
document.write('v1: ' + v1);
document.write('v2: ' + v2);
```

---

### 객체 분해 할당

```js
let book = {
  title: "Master book",
  publish: "ICT",
  price: 10000
};

document.write('제목: ' + book.title + '<br/>');
document.write('가격: ' + book.price + '<hr/>');

let { title, price } = book;
document.write('제목: ' + title + '<br/>');
document.write('가격: ' + price + '<hr/>');
```

---

### 실수형 계산 주의

```js
document.write(0.2 * 3 == 0.6);        // false
document.write(0.2 * 10 * 3 == 0.6 * 10); // true
```

---

### 타입 비교

```js
if (num == str) document.write('[같다]');
else document.write('[다르다]');  // 값 비교만

if (num === str) document.write('[같다2]');
else document.write('[다르다2]'); // 타입까지 비교
```

---

### 기본형 vs 참조형

```js
var a = 10, b = 10;
if (a == b) document.write('같다1'); // 기본형은 값 비교

var a = ['java', 'script'], b = ['java', 'script'];
if (a == b) document.write('같다2');
else document.write('다르다2'); // 참조형은 주소 비교

var a = 'Hello', b = "Hello";
if (a == b) document.write('같다3');
```

---

### Boolean 비교

```js
document.write((1 == true) + '<br/>');   // true
document.write((0 == true) + '<br/>');   // false
document.write((1 == false) + '<br/>');  // false
document.write((0 == false) + '<br/>');  // true
```

---

### null과 논리 연산자

```js
const num = null;
const result = num || '숫자를 입력하세요';
document.write(result + '<br/>');

const num2 = 100;
const result2 = num2 || '숫자를 입력하세요';
document.write(result2 + '<br/>');

const num3 = null;
const result3 = num3 && '입력값입니다';
document.write(result3 + '<br/>');

const num4 = 100;
const result4 = num4 && '입력값입니다';
document.write(result4 + '<br/>');

const num5 = 0;
const result5 = num5 && '입력값입니다';
document.write(result5 + '<br/>');
```

> `||`: 좌측이 false면 우측 반환  
> `&&`: 좌측이 true면 우측 반환

---

### 삼항 연산자

```js
var num = 100;
var result = (typeof num === 'number') ? num : '숫자를 입력하세요';
document.write(result + '<br/>');
```

---

### for...of / for...in

```js
var arr = ['안녕', 'Hello', 'Hola'];
for (var i of arr) {
  document.write(i + '<br/>');
}

var obj = { first: '길동', last: '김' };
for (var k in obj) {
  document.write(k + '<br/>');
  document.write(obj[k] + '<br/>');
}
```

> `for...of`: 배열 요소 순회  
> `for...in`: 객체 속성(key) 순회

---

### `indexOf()`

- 문자열에서 특정 문자열의 **첫 등장 위치(index)**를 반환

---

### 문자열 템플릿

```js
const myname = '홍길동';
const myage = 22;

const message = '내 이름은 ' + myname + '입니다. 나이는 ' + myage + '입니다';
document.write(message + '<br/>');

const message2 = `내 이름은 ${myname}입니다. 나이는 ${myage}입니다`;
document.write(message2 + '<br/>');
```

---

### 형 변환

```js
var n = 'a700';
document.writeln(Number(n) + '<br/>');       // NaN
document.writeln(typeof Number(n) + '<hr/>'); // number

document.writeln(parseInt(n) + '<br/>');      // NaN
```

> `NaN`: Not a Number
