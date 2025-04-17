## ✅ 비동기 vs 동기 (AJAX의 핵심)

| 구분 | 설명 | 예 |
|------|------|----|
| **동기 (Synchronous)** | 요청을 보내고 응답이 올 때까지 **기다림** | 기본 폼 제출 방식 |
| **비동기 (Asynchronous)** | 요청을 보내고 **응답이 오기 전에 다음 코드 실행** | AJAX, fetch, setTimeout 등 |

---

## ✅ AJAX 기본 구조 (jQuery)

```javascript
$.ajax({
    type: 'post',               // 전송 방식 ('get'도 가능)
    url: '02_server.jsp',       // 요청 보낼 서버 페이지
    data: param,                // 보낼 데이터 (key=value 형태)
    dataType: 'text',           // 서버에서 받을 데이터 타입
    success: parseData,         // 성공 시 실행할 함수
    error: function(err) {
        alert('문제발생');
        console.log(err);      // 에러가 나는지 작성하는 습관을 들이자!!
    }
});
```

### ✅ dataType 종류

| 타입 | 설명 |
|------|------|
| `'text'` | 일반 텍스트 |
| `'html'` | HTML 조각 |
| `'json'` | JSON 객체 |
| `'xml'` | XML 문서 |

---

## ✅ get / post 생략 시 주의사항

- `type` 또는 `method`를 명시하지 않으면, **기본은 GET**
- 단, **브라우저/툴 상황에 따라 오동작 가능 → 명시적으로 선언할 것!**

> ex) 일부 개발도구 또는 확장기능에서는 자동으로 POST 요청이 될 수 있음

---

## ✅ jQuery 주요 메서드 정리

| 메서드 | 설명 | 예 |
|--------|------|----|
| `.val()` | `input`, `select` 등의 값을 읽거나 설정 | `$('#name').val('홍길동')` |
| `.text()` | 요소 안의 **텍스트만** 가져오거나 설정 | `$('p').text('안녕')` |
| `.html()` | 요소 안의 **HTML 전체**를 가져오거나 설정 | `$('.box').html('<b>굵게</b>')` |
| `.attr()` | 속성 값을 읽거나 설정 | `$('#img').attr('src', 'a.jpg')` |
| `trim()` | 문자열의 앞뒤 공백 제거 | `'  hello  '.trim()` |

---

## ✅ 실전 예시

### 🔹 XML에서 특정 태그 추출해서 input에 넣기
```javascript
$('#cate').val( $(result).find('first').text() );
```

### 🔹 HTML 데이터 받아서 특정 영역에 출력
```javascript
$('.notebook').html(data);
```

---

## ✅ 보너스 팁 & 해석 정리

### 🔹 `$('form[name="inForm"]').submit();`
- `name="inForm"`인 `<form>` 요소를 선택해서, 그 폼을 직접 전송(submit)한다.

### 🔹 `if(result.trim() == '1')`
- result 값에서 앞뒤 공백을 제거한 후, 그 값이 `'1'`이면 해당 블록을 실행한다. (예: 입력 성공 여부 확인)

### 🔹 `$('#name,#age,#tel,#addr').val('');`
- 각 요소의 값을 빈 문자열로 설정하여, 여러 입력 필드를 한 번에 초기화한다.

---

## ✅ 요약

- AJAX는 **비동기 요청**을 통해 서버와 통신 가능
- `type`은 기본값이 GET이지만, **명확하게 지정하는 것이 좋음**
- jQuery에서 `.val()`, `.text()`, `.html()`, `.attr()` 등 다양한 DOM 제어 함수 사용
- 브라우저별 AJAX 처리 방식에 **차이날 수 있으니 명시적으로 작성**할 것!

