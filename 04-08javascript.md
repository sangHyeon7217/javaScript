### 📘 JavaScript 함수 & 스코프 정보 정리

---

#### 1️⃣ 함수 선언 방식 비교

```js
// 함수 선언문 (Function Declaration)
function triangle(base, height) {
  return base * height / 2;
}
document.write('1. 삼각형 면적: ' + triangle(3, 4) + '<hr/>');
```

```js
// 함수 리터럴 (Function Expression)
var triangle = function(base, height) {
  return base * height / 2;
};
document.write('2. 삼각형 면적: ' + triangle(3, 4) + '<hr/>');
```

```js
// 화살표 함수 (Arrow Function)
var triangle = (base, height) => {
  return base * height / 2;
};
document.write('3. 삼각형 면적: ' + triangle(3, 4) + '<hr/>');
```

---

#### 2️⃣ 화살표 함수 간소화 예시

```js
const func = x => x * 2;
document.write('결과: ' + func(10));
```

---

#### 3️⃣ 배열 & join, slice, sort

```js
let arr2 = [5, 15, 20, 9];
document.writeln(arr2.sort() + '<br/>');
// 값이 문자로 처리되어 오른상순 X (15, 20, 5, 9)
```

- `join(del)` : 배열 요소를 del로 연결
- `slice(start, end)` : start부터 end-1까지 추출
- `slice(start)` : start부터 끝까지 추출

---

#### 4️⃣ 슈트얀 & 큐

```js
// 큐: FIFO
var data = [];
data.push('박서준');
data.push('현빈');
data.push('박보검');
document.writeln(data.shift() + '<br/>'); // 박서준
```

```js
// 스테크: LIFO
var data = [];
data.push('박서준');
data.push('현빈');
data.push('박보검');
document.writeln(data.pop() + '<br/>'); // 박보검
```

---

#### 5️⃣ ES6 반복문

```js
var data = ['강', '갑', '박'];
data.forEach(function(value, index) {
  document.writeln(index + ': ' + value + '<br/>');
});
```

---

#### 6️⃣ Map 객체

```js
let m = new Map();
m.set('java', '1111');
m.set('script', '2222');
m.set('nodejs', '2222');
m.set('java', '3333'); // key 중복으로 덮어씀

for (let [k, v] of m) {
  document.write(k + ':' + v + '<br/>');
}
```

---

#### 7️⃣ 로그인 확인 로직

```js
let inputId = 'java';
let inputPw = '3333';
let flag = false;

for (let [Id, Pw] of m) {
  if (Id === inputId && Pw === inputPw) {
    document.write('<h1> 로그인성공 </h1>');
    flag = true;
    break;
  }
}

if (!flag) {
  document.write('<h1> 로그인실패 </h1>');
}
```

---

#### 8️⃣ 로또 만들기

```js
let lotto = new Set();
while (lotto.size < 6) {
  lotto.add(parseInt(Math.random() * 45) + 1);
}

for (let item of lotto) {
  document.write(item + '/');
}
```

---

#### 9️⃣ Date 객체 활용

```js
var d = new Date();
d.setFullYear(2030);
d.setMonth(11);
d.setDate(25);
document.writeln(d + '<br/>');
document.writeln(d.getFullYear() + '<br/>'); // 2030
```

요일 정보:
- `getDay()` : 0 = 일요일, 1 = 월요일, 2 = 화요일 ...

날짜 비교:
```js
const date3 = new Date('2025-12-25');
const date4 = new Date('2025-12-25');
document.write((date3 == date4) + '<br/>'); // false (주소값)
document.write((date3.getTime() == date4.getTime()) + '<br/>'); // true
```

---

#### 🔟 eval() 사용

```js
var msg = "alert('안녕')";
eval(msg);
```

- `eval()` : 문자열로 된 자바스크립트 코드를 실행

---

#### 🔁 window.onload 이벤트 등록 축약형

```js
window.onload = function windowInit() {
  let b = document.getElementById('btn');

  b.onclick = function btn_click() {
    alert('이벤트 발생3');
  };
};
```

---

