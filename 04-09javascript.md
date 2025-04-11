# 📘 자바스크립트 DOM 노드 검색 및 이벤트 처리 정리

---

## 📌 1. 노드 검색 방법

### ✅ 기본 메서드

| 목적 | 사용법 | 설명 |
|------|--------|------|
| ID로 검색 | `document.getElementById('id명')` | 가장 빠르고 단순 |
| 클래스명으로 검색 | `document.getElementsByClassName('클래스명')` | HTMLCollection 반환 (배열처럼 사용) |
| 태그명으로 검색 | `document.getElementsByTagName('태그명')` | HTMLCollection 반환 |
| CSS 선택자 방식 (ID) | `document.querySelector('#id명')` | 첫 번째 일치 요소 |
| CSS 선택자 방식 (Class) | `document.querySelector('.클래스명')` | 첫 번째 일치 요소 |
| CSS 선택자 방식 (다중) | `document.querySelectorAll('선택자')` | NodeList 반환 |

---

## 📌 2. DOM 노드 예제

### 🧪 ID로 노드 선택

```js
let name = document.getElementById('name');
result.innerHTML = '안녕, ' + name.value + '님';
🧪 클래스명으로 노드 선택 (배열처럼 인덱스 필요)
js
복사
편집
let names = document.getElementsByClassName('cname');
result.innerHTML = '안녕, ' + names[0].value + '님';
🧪 태그명으로 노드 선택 (배열처럼 사용)
js
복사
편집
let inputList = document.getElementsByTagName('input');
for (let i = 0; i < inputList.length; i++) {
  if (inputList[i].type === 'text' && inputList[i].value === '') {
    alert('각 항목을 입력하세요');
    return;
  }
}
📌 3. 이벤트 등록 예제
✅ 단일 요소 클릭 이벤트
js
복사
편집
let h3 = document.querySelector('#btn');
h3.onclick = function () {
  img.src = 'images/me.png';
};
✅ window.onload로 초기 설정
js
복사
편집
window.onload = function () {
  let img = document.querySelector('#profile > img');
  let users = document.querySelectorAll('.user');
  let h3 = document.querySelector('#btn');

  h3.onclick = function () {
    img.src = 'images/me.png';
    users[0].innerHTML = '이름 : 한상현';
  };
};
📌 getElementById() vs querySelector() 차이 정리
✅ 공통점
둘 다 DOM 요소를 선택하는 메서드

id 값으로 요소를 선택할 때는 같은 결과 반환

js

document.getElementById('myId');
document.querySelector('#myId');
⚠️ 차이점
항목	getElementById()	querySelector()
선택자 형식	'id명'만 (# 없이)	CSS 선택자 형식 (#id, .class, tag, 등 가능)
반환값	요소 1개 (Element) 또는 null	요소 1개 (Element) 또는 null
속도	빠름 (ID 직접 검색)	느림 (CSS 파싱 필요)
유연성	오직 id 검색	다양한 선택자 지원
🎯 결론
id만 사용할 땐 → getElementById() 추천 (더 빠르고 간단)

복잡한 CSS 선택자 필요 시 → querySelector()가 더 유용



//[1]id값으로 찿기
    		  
    		  //입력한 칸에 사용자가 입력한 변수
    		  //let userName = document.getElementById('UserName').value;
    		  //var userName = document.querySelector('#userName').value;
    		  
    		 
    		  //[2]폼안의 name찿기 ?? value를 넣는거랑 안넣는거랑 차이점??
    		   //var userName =document.frm.username.value;
    		   var userName =.frm.username.value; //form은 doucument생략가능
    		  //var userName = document.forms[0].username.value;
              
              
    		  
    		  document.querySelector('#result').innerHTML = userName +"님 반갑";
              
              
              
            getAttribute()
            
            Element.getAttribute() 사용법
            
            getAttribute() 함수는
            DOM 요소에서 속성 값을 가져오는 함수입니다.
            주어진 요소에서 속성이 존재할 경우, 그 속성의 값을 문자열로 반환합니다.

            만약 속성의 값이 존재하지 않으면 빈 문자열("")을 반환하고,
            해당 요소에서 일치하는 속성이 없다면 null을 반환합니다.


            
            
            this.innerHTML