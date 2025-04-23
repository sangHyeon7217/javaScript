
# 🗑️ MyBatis 댓글 삭제 흐름 정리

이 문서는 MyBatis를 사용하는 프로젝트에서 댓글 삭제 기능의 전체 흐름을 이해하기 쉽게 정리한 것입니다.

---

## ✅ 1. 시작: deleteComment.jsp 호출

사용자는 목록에서 `?cId=3` 형태의 URL을 클릭하여 삭제 요청을 보냅니다.

```jsp
long commentNo = Long.parseLong(request.getParameter("cId"));
CommentService.getInstance().deleteComment(commentNo);
response.sendRedirect("listComment.jsp");
```

---

## ✅ 2. 서비스 계층: CommentService.java

```java
public void deleteComment(long commentNo) {
    repo.deleteComment(commentNo);
}
```

- `CommentRepository`의 `deleteComment()`를 호출해 실제 삭제 요청을 전달

---

## ✅ 3. DAO 계층: CommentRepository.java

```java
public void deleteComment(long commentNo) {
    SqlSession session = sqlSessionFactory.openSession();
    try {
        session.delete("CommentMapper.deleteComment", commentNo);
        session.commit();
    } finally {
        session.close();
    }
}
```

- MyBatis의 세션을 열고, `Mapper`에 등록된 SQL을 실행
- 트랜잭션 커밋 후 세션 종료

---

## ✅ 4. Mapper XML: CommentMapper.xml

```xml
<delete id="deleteComment" parameterType="long">
    DELETE FROM comment_tab WHERE comment_no = #{commentNo}
</delete>
```

- `#{commentNo}`는 자바에서 넘긴 파라미터 값을 SQL에 주입

---

## ✅ 5. 전체 흐름 요약
    
1. JSP에서 댓글 번호를 전달 (`?cId=3`)
2. `deleteComment.jsp`에서 해당 번호 받아 처리
3. `CommentService` → `CommentRepository` → `Mapper.xml` 순으로 삭제 실행
4. 삭제 완료 후 목록 페이지로 리다이렉트


🧠 삭제 전체 흐름 요약
listComment.jsp에서 댓글 번호를 가진 URL (?cId=...)로 이동

deleteComment.jsp에서 request.getParameter("cId")로 번호 받음

CommentService.deleteComment(long) 호출

CommentRepository.deleteComment(long) 실행

CommentMapper.xml에서 DELETE FROM comment_tab WHERE comment_no = #{commentNo} 수행

삭제 완료 후 listComment.jsp로 리다이렉트




---

💡 이 흐름을 이해하면 수정, 조회 기능도 쉽게 이어서 학습할 수 있습니다!
