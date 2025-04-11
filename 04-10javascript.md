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
const func = x => x * 2; // 인자 1개 + 리턴문만 있으면 소각형 & return 삭제 가능
document.write('결과: ' + func(10));
```

---

#### 3️⃣ DOM 제어와 화살표 함수 사용

```js
let third = () => {
  var txt = document.getElementById('fourth');
  txt.style.color = 'red';
  txt.style.backgroundColor = 'orange';
};
```

---

#### 4️⃣ 호이스팅 (Hoisting)

```js
// 함수 선언문은 hoisting O
doA(); // 정상 실행
function doA() {
  document.write('함수 A <br/>');
}

// 함수 표현식은 hoisting X
doB(); // ❌ 에러 발생
var doB = function() {
  document.write('함수 B <br/>');
};
```

---

#### 5️⃣ 함수도 데이터(값)다

```js
function doA() { document.write('함수 A <br/>'); }
function doB() { document.write('함수 B <br/>'); }

var arr = [doA, doB];
arr[0](); // doA 실행
```

---

#### 6️⃣ 고차 함수 예시 (함수를 인자로 전달)

```js
function f4(x, y, z) {
  return z(x() + y());
}

var f1 = function() { return 2; };
var f2 = function() { return 1; };
var f3 = function(a) { return a * a; };

var result = f4(f1, f2, f3); // => z(2+1) = 9
document.write('결과: ' + result);
```

---

#### 7️⃣ 변수 선언 삭제의 문제점

```js
scope = '그룹 변수';

function getValues() {
  scope = '지역 변수';
  return scope;
}

document.write('1> ' + getValues()); // '지역 변수'
document.write('2> ' + scope);       // '지역 변수' (전역 오염 발생)
```

✅ 변수는 반복문을 통해 `var`, `let`, `const`로 만들어야 함

---

#### 8️⃣ 스코프(Scope) 비교

| 구분 | 설명 | 키워드 |
|------|------|--------|
| 함수 스코프 | 함수 내에서만 유효 | `var` |
| 블록 스코프 | 개방({}) 내에서만 유효 | `let`, `const` |

```js
if (true) {
  var i = 100;
}
document.write('i=' + i + '<br/>'); // var: 전역처럼 동작

if (true) {
  let j = 200;
}
document.write('j=' + j + '<br/>'); // ❌ Error
```

---

#### 9️⃣ 객체에 함수(메서드) 저장하기

```js
var obj = {
  name: '홍길동',
  age: 33,
  display: function() {
    document.write(this.name + '님은 ' + this.age + '세입니다.<br/>');
  }
};

obj.display();
```

축약형 메서드 선언도 가능:
```js
var obj3 = {
  name: '홍길국',
  age: 22,
  display() {
    document.write(this.name + '님은 ' + this.age + '세입니다.<br/>');
  }
};
```

---

#### 🔹 HTML 요소의 속성값 활용

```js
window.onload = function() {
  var mango = frm.mango;
  var avocado = frm.avocado;

  var mango_price = mango.getAttribute("data-price");
  var avocado_price = avocado.getAttribute("data-price");

  mango.onchange = calc;
  avocado.onchange = calc;

  function calc() {
    frm.total.value = mango.value * mango_price
                    + avocado.value * avocado_price;
  }
};
```

---

### ✅ 정리 요조

- `function` 선언 vs 리터럴 vs 화살표 → 문법 및 호이스팅 차이
- `var` → 함수 스코프, `let/const` → 블록 스코프
- 함수는 변수처럼 사용가능한 **일기기 객체**
- 객체에 함수 저장 시 `this`가 현재 객체를 가능
- DOM 접근 후 `getAttribute`, 이벤트 핸들러 연결 등 자주 사용됨

