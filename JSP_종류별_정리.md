# 📘 JSP 종류별 흐름 정리

---

## 1️⃣ 화면 JSP
> **역할**: 사용자에게 정보를 보여주는 화면 (폼, 목록, 결과 등)

### 📄 BoardList.jsp
- 게시글 목록을 DB에서 조회하여 `<table>` 형태로 출력함
- Service를 통해 `List<BoardVO>` 데이터를 받아와 출력
- 사용자가 글 제목을 클릭하면 → BoardView.jsp로 이동

### 📄 BoardView.jsp
- 사용자가 선택한 글 번호(seq)를 받아 해당 글 정보를 조회함
- Service의 `getArticleById(seq)`를 호출해 `BoardVO`를 얻음
- 제목, 내용, 작성자 등을 출력함

---

## 2️⃣ 처리 JSP
> **역할**: DB에 데이터를 저장, 수정, 삭제하는 역할

### 📄 BoardSave.jsp
- 사용자가 입력한 제목/내용 등을 `BoardVO`에 담아 Service에 전달
- `write(BoardVO vo)` 메서드를 통해 DB에 저장
- 저장된 글번호(id)를 받아 → BoardView.jsp로 이동

### 📄 BoardDelete.jsp
- 사용자가 입력한 글번호와 비밀번호를 받아
- Service의 `delete(seq, password)` 메서드를 호출해 삭제 처리
- 성공/실패 결과에 따라 메시지 출력

### 📄 BoardModify.jsp
- 수정된 글 정보를 받아 `BoardVO`에 담고
- Service → DAO를 통해 `update()` 실행
- 성공 시 BoardView.jsp로 리다이렉트

---

## 3️⃣ 중간 JSP
> **역할**: 삭제 전 비밀번호 입력, 수정 전 확인 등 중간 처리 화면

### 📄 BoardDeleteForm.jsp
- 사용자가 글 삭제 버튼을 클릭했을 때
- 비밀번호를 입력하는 `form`을 보여줌
- form action → BoardDelete.jsp

---

## ✅ 요약

| JSP 파일명            | JSP 유형   | 주요 역할                          |
|------------------------|------------|------------------------------------|
| BoardList.jsp          | 화면 JSP   | 글 목록을 출력                     |
| BoardView.jsp          | 화면 JSP   | 글 상세 내용을 출력                |
| BoardSave.jsp          | 처리 JSP   | 글을 저장하고 글번호 리턴         |
| BoardDelete.jsp        | 처리 JSP   | 글을 삭제함                        |
| BoardModify.jsp        | 처리 JSP   | 글을 수정함                        |
| BoardDeleteForm.jsp    | 중간 JSP   | 삭제 전에 비밀번호 입력받는 화면 |

