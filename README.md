# jsp-servlet-dictionary

Dự án Maven Webapp Java JSP/Servlet theo bài Từ điển Anh - Việt.

## Cấu trúc
- pom.xml
- src/main/java/com/codegym/DictionaryServlet.java
- src/main/webapp/index.jsp
- src/main/webapp/WEB-INF/web.xml
- De_bai_goc.md

## Từ có sẵn
- hello -> Xin chào
- how -> Thế nào
- book -> Quyển sách
- computer -> Máy tính
- student -> Sinh viên

## Chạy với Maven
```bash
mvn clean package
```

File WAR tạo tại:
```text
target/jsp-servlet-dictionary.war
```

## Chạy trên Tomcat 10.1+
Triển khai file WAR vào thư mục `webapps` của Tomcat rồi khởi động Tomcat.

Trang:
http://localhost:8080/jsp-servlet-dictionary/
