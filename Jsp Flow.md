## 📄 BoardList.jsp 완전 정리 (화면 JSP의 역할과 흐름)

### ✅ BoardList.jsp란?
> DB에 저장된 게시글 목록을 웹 화면에 출력하는 JSP 페이지.

---

### ✅ 주요 역할 요약
| 단계 | 설명 |
|------|------|
| 1️⃣ | Service에서 게시글 목록을 가져옴 |
| 2️⃣ | 반복문을 이용해 게시글 하나씩 `<table>`로 출력함 |
| 3️⃣ | 각 게시글의 제목, 작성자, 작성일, 조회수 등을 보여줌 |
| 4️⃣ | 제목에 링크를 걸어 상세보기(`BoardView.jsp`)로 이동함 |

---

### ✅ JSP 핵심 코드 구조
```jsp
<%@ page contentType="text/html;charset=utf-8" %>
<%@ page import="java.util.*, board_ex.model.BoardVO, board_ex.service.ListArticleService" %>

<%
	// [1] 서비스에서 게시글 목록 가져오기
	ListArticleService service = ListArticleService.getInstance();
	List<BoardVO> mList = service.getArticleList();
%>

<html>
<head><title>게시판 목록</title></head>
<body>

<h3>게시판 목록</h3>

<table border="1">
	<tr>
		<th>글번호</th>
		<th>제목</th>
		<th>작성자</th>
		<th>작성일</th>
		<th>조회수</th>
	</tr>

	<% if(mList.isEmpty()) { %>
		<tr><td colspan="5">등록된 게시물이 없습니다.</td></tr>
	<% } else {
		for(BoardVO m : mList) {
	%>
	<tr>
		<td><%= m.getSeq() %></td>
		<td><a href="BoardView.jsp?seq=<%= m.getSeq() %>"><%= m.getTitle() %></a></td>
		<td><%= m.getWriter() %></td>
		<td><%= m.getRegdate() %></td>
		<td><%= m.getCnt() %></td>
	</tr>
	<% 	}
	} %>
</table>

<br>
<a href="BoardInputForm.jsp">글쓰기</a>

</body>
</html>
```

---

### ✅ 사용된 객체 설명

| 객체 | 설명 |
|-------|--------------------------------------------------|
| `BoardVO` | 게시글 하나의 정보를 담는 객체 (번호, 제목, 작성자 등) |
| `List<BoardVO>` | 여러 게시글을 담은 리스트 |
| `ListArticleService` | DB에서 게시글 목록을 가져오는 서비스 객체 |

---

### ✅ 질문으로 다시 보는 핵심

#### 🔹 왜 `getInstance()`를 쓰나요?
- Service 객체를 하나만 만들어서 공유하기 위한 **Singleton 패턴** 때문
- `new` 대신 `getInstance()`를 쓰면 메모리 낭비 없이 한 번만 생성됨

#### 🔹 `List<BoardVO> mList = service.getArticleList();` 의미는?
- 게시글 목록 전체를 `BoardVO` 리스트로 받아옴
- DB → DAO → Service → JSP까지 흐름을 통해 전달받음
- `for`문으로 하나씩 꺼내 출력할 수 있음

#### 🔹 게시글을 어떻게 출력하나요?
- `for(BoardVO m : mList)` 반복문으로 하나씩 꺼내어 `<tr>`로 출력
- `m.getTitle()` 등으로 각 게시글 속성에 접근함

---

### ✅ 한 줄 요약
> `BoardList.jsp`는 Service에서 게시글 리스트를 받아서, for문으로 반복 출력하는 화면 JSP이다.

---

필요한 항목이 생기면 이 파일에 계속 이어서 추가 가능합니다 ✅



## 📄 BoardSave.jsp & BoardDelete.jsp 완전 정리 (처리 JSP 흐름 이해)

### ✅ 처리 JSP란?
> 사용자가 입력한 데이터를 받아서 → DB에 저장하거나 삭제하거나 수정하는 작업을 처리하는 JSP 파일입니다.

---

## ✅ BoardSave.jsp 흐름 분석

### 📌 주요 코드
```java
int id = WriteArticleService.getInstance().write(rec);
response.sendRedirect("BoardView.jsp?id=" + id);
```

### 📌 설명
| 코드 | 설명 |
|------|------|
| `WriteArticleService.getInstance()` | 서비스 객체를 가져온다 (싱글톤 방식) |
| `.write(rec)` | 사용자가 입력한 글 정보를 넘겨서 DB에 저장함 |
| `int id = ...` | 저장된 글의 고유 글번호(PK)를 받아옴 |
| `response.sendRedirect(...)` | 해당 글을 바로 볼 수 있도록 상세보기 페이지로 이동함 |

### 📦 흐름 요약
1. 사용자가 글쓰기 폼을 작성해 제출
2. `BoardVO rec`에 사용자 입력 정보 저장
3. `write(rec)` 호출해 DB 저장 요청
4. 저장된 글의 id를 받아서 → View 페이지로 이동시킴

---

## ✅ BoardDelete.jsp 흐름 분석

### 📌 주요 코드
```java
int seq = Integer.parseInt(request.getParameter("seq"));
String password = request.getParameter("password");
int result = DeleteArticleService.getInstance().delete(seq, password);
```

### 📌 설명
| 코드 | 설명 |
|------|------|
| `request.getParameter("seq")` | 삭제할 글 번호를 문자열(String)로 받아옴 |
| `Integer.parseInt(...)` | 문자열을 숫자(int)로 변환해 사용 |
| `request.getParameter("password")` | 사용자가 입력한 비밀번호를 받아옴 |
| `DeleteArticleService.getInstance()` | 삭제 요청을 처리할 서비스 객체 가져옴 |
| `.delete(seq, password)` | 글 번호와 비번을 넘겨 삭제 시도 → 성공/실패 결과 리턴 |

### 📦 흐름 요약
1. 사용자가 글 삭제 요청
2. 글번호와 비밀번호를 입력함
3. Service에서 `delete(seq, password)` 실행
4. 삭제 성공 여부를 `result`에 저장
5. `result` 값에 따라 화면에서 성공/실패 메시지 출력

---

## ✅ 관련 개념 정리

### ▶ request.getParameter()
- 브라우저에서 보낸 값(form, URL)을 받아오는 메서드
- 무조건 **문자열(String)** 로 받아옴

### ▶ Integer.parseInt()
- 문자열을 정수(int)로 바꾸는 메서드
- DB에서 숫자 비교하려면 꼭 필요함

### ▶ Service 객체의 역할
- 비즈니스 로직 처리 전담 (DB 저장, 삭제 등)
- JSP는 처리 로직을 직접 하지 않고 Service에 맡김

### ▶ 왜 객체(rec)를 넘겨주는가?
- 제목, 내용, 작성자 등을 하나하나 넘기면 복잡함
- BoardVO에 담아서 통째로 넘기면 관리 편함

---

## ✅ JSP 파일 분류표

| JSP 파일명 | JSP 종류 | 설명 |
|------------|-----------|-------------------------------|
| `BoardSave.jsp` | 처리 JSP | 사용자가 작성한 글을 DB에 저장함 |
| `BoardDelete.jsp` | 처리 JSP | 사용자가 선택한 글을 DB에서 삭제함 |
| `BoardView.jsp` | 화면 JSP | 글 하나의 내용을 사용자에게 보여줌 |
| `BoardModify.jsp` | 처리 JSP | 수정된 글 정보를 DB에 반영함 |

> 💡 처리 JSP는 사용자의 입력을 받아 Service를 통해 DB 작업을 요청하고,
> 그 결과에 따라 다음 페이지로 이동하거나 메시지를 보여주는 역할을 합니다.

# 📄 BoardView.jsp 핵심 코드 설명

이 문서는 BoardView.jsp에서 사용되는 핵심 코드:

```jsp
<%
    // 게시글번호 넘겨받아
    String seq = request.getParameter("seq");
    
    // 서비스의 함수를 호출하여 해당 BoardVO를 넘겨받는다.
    BoardVO result = ViewArticleService.getInstance().getArticleById(seq);
%>
```

이 코드의 구조와 흐름을 쉽게 설명한 내용입니다.

---

## ✅ 전체 목적

- 사용자가 클릭한 **글번호(`seq`)** 를 URL에서 받아서
- 그 번호에 해당하는 글 정보를 DB에서 조회한 후,
- 화면에 보여주기 위해 `BoardVO result`에 저장하는 작업

---

## ✅ 코드 설명

### 🔹 1. `String seq = request.getParameter("seq");`

- 사용자가 URL을 통해 넘긴 글 번호를 받아오는 코드
- 예: `BoardView.jsp?seq=3` 이면 → `seq = "3"`
- 무조건 **문자열(String)** 로 받음

---

### 🔹 2. `BoardVO result = ViewArticleService.getInstance().getArticleById(seq);`

- ViewArticleService: 글 조회용 서비스 클래스
- `getInstance()` : 서비스 객체를 싱글톤 방식으로 1개만 가져옴
- `getArticleById(seq)` : 해당 글 번호를 전달해서 DB에서 글 내용을 가져오는 메서드
- `BoardVO` : 글 1개의 정보 (제목, 내용, 작성자 등)를 담는 객체

---

## 🧠 흐름 예시

1. 사용자: `BoardView.jsp?seq=3` 클릭
2. `seq = "3"` 받아옴
3. `getArticleById("3")` 호출
4. DAO → DB에서 3번 글 찾기
5. 결과를 `BoardVO result`에 담아 JSP로 반환

---

## ✅ 결과로 얻은 BoardVO (`result`) 안에는?

| 메서드 | 설명 |
|--------|------|
| `result.getTitle()` | 글 제목 |
| `result.getContent()` | 글 내용 |
| `result.getWriter()` | 작성자 |
| `result.getRegdate()` | 작성일 |

---

## ✅ 한 줄 요약

> **사용자가 선택한 글 번호를 가지고 → DB에서 해당 글을 찾아 → 화면에 출력하기 위해 데이터를 불러오는 코드**






