
# 📘 MyBatis 중간 프로젝트 흐름 정리

이 문서는 `mybatis.Zip` 파일을 기준으로 MyBatis를 사용한 웹 애플리케이션의 전체 구조와 동작 흐름을 정리한 것입니다.

---

## 🧱 1. 전체 구성 파일 목록

- `insertCommentForm.jsp` : 댓글 입력 폼
- `insertCommentSave.jsp` : 댓글 저장 처리
- `listComment.jsp` : 댓글 목록 출력
- `deleteComment.jsp` : 댓글 삭제
- `viewComment.jsp` : 댓글 상세 보기
- `Comment.class` : 댓글 VO (Value Object)
- `CommentService.class` : 서비스 계층 (비즈니스 로직)
- `CommentRepository.class` : DB 접근 계층 (DAO)
- `CommentMapper.xml` : SQL 정의 파일
- `mybatis-config.xml` : MyBatis 설정 파일

---

## 🔄 2. 동작 흐름 (입력 → 저장 → 목록)

### ✅ Step 1. `insertCommentForm.jsp`

- 사용자로부터 입력을 받는 화면.
- form을 통해 `insertCommentSave.jsp`로 POST 요청.

```html
<form action="insertCommentSave.jsp" method="post">
    <input name="userId">
    <textarea name="content"></textarea>
    <button type="submit">저장</button>
</form>
```

---

### ✅ Step 2. `insertCommentSave.jsp`

- 입력된 데이터를 `Comment` 객체로 자동 매핑.
- `CommentService`를 통해 저장 처리 요청.

```jsp
<jsp:useBean id="comment" class="mybatis.guest.model.Comment">
    <jsp:setProperty name="comment" property="*" />
</jsp:useBean>

<%
    CommentService.getInstance().insertComment(comment);
%>
```

---

### ✅ Step 3. `CommentService.java`

```java
public void insertComment(Comment c) {
    new CommentRepository().insertComment(c);
}
```

---

### ✅ Step 4. `CommentRepository.java`

```java
public void insertComment(Comment c) {
    SqlSession session = sqlSessionFactory.openSession();
    session.insert("CommentMapper.insertComment", c);
    session.commit();
    session.close();
}
```

---

### ✅ Step 5. `CommentMapper.xml`

```xml
<insert id="insertComment" parameterType="mybatis.guest.model.Comment">
    INSERT INTO comment_tab (comment_no, user_id, content, reg_date)
    VALUES (seq_comment_no.nextval, #{userId}, #{content}, sysdate)
</insert>
```

---

## 🔍 3. 목록 출력 `listComment.jsp`

```jsp
<%
    List<Comment> mList = CommentService.getInstance().selectComment();
    request.setAttribute("commentList", mList);
%>
```

```java
public List<Comment> selectComment() {
    return new CommentRepository().selectComment();
}
```

```java
public List<Comment> selectComment() {
    SqlSession session = sqlSessionFactory.openSession();
    List<Comment> result = session.selectList("CommentMapper.selectComment");
    session.close();
    return result;
}
```

```xml
<select id="selectComment" resultType="mybatis.guest.model.Comment">
    SELECT * FROM comment_tab ORDER BY comment_no DESC
</select>
```

---

## ⚙️ 4. 설정 파일: `mybatis-config.xml`

```xml
<configuration>
    <environments default="development">
        <environment id="development">
            <transactionManager type="JDBC"/>
            <dataSource type="POOLED">
                <property name="driver" value="oracle.jdbc.driver.OracleDriver"/>
                <property name="url" value="jdbc:oracle:thin:@localhost:1521:xe"/>
                <property name="username" value="scott"/>
                <property name="password" value="tiger"/>
            </dataSource>
        </environment>
    </environments>

    <mappers>
        <mapper resource="CommentMapper.xml"/>
    </mappers>
</configuration>
```

---

## 📌 요약

| 계층 | 파일 | 역할 |
|------|------|------|
| View (화면) | `*.jsp` | 사용자 입력/출력 |
| Controller / Service | `CommentService.class` | 흐름 제어, 유효성 검사 등 |
| DAO | `CommentRepository.class` | DB 접근 |
| SQL 정의 | `CommentMapper.xml` | SQL 문장 정의 |
| VO/DTO | `Comment.class` | 데이터를 담는 객체 |

---

👉 이 구조는 MVC 패턴 + MyBatis 조합의 전형적인 예입니다.
