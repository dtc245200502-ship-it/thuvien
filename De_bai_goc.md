### **Mục tiêu:**

Luyện tập tạo Servlet.

### **Điều kiện:**

Biết cách tạo Servlet.

### **Mô tả bài toán:**

Xây dựng một trang web để tra cứu từ Anh – Việt (với các từ - nghĩa của từ cho sẵn trong một cấu trúc dữ liệu). Tạo trang index.jsp chứa một form tra cứu từ. Nếu tìm thấy từ thì hiển thị nghĩa bằng tiếng Việt. Nếu không tìm thấy thì hiển thị thông báo không tìm thấy.

### **Hướng dẫn:**

**Bước 1: Kích hoạt và ra lệnh cho AI Agent**

**1. Mở khung chat AI Agent**

- **Windows / Linux:** Nhấn tổ hợp phím Ctrl + L
- **macOS:** Nhấn tổ hợp phím Cmd + L Một cửa sổ chat với trợ lý Gemini Pro sẽ ngay lập tức xuất hiện ở góc phải màn hình của bạn.

**2. Chuẩn bị đường dẫn lưu dự án** Hãy xác định trước một thư mục tuyệt đối trên máy tính của bạn để lưu dự án này.

- **Ví dụ trên Windows:** C:\Workspace\jsp-servlet-dictionary
- **Ví dụ trên macOS:** /Users/admin/Workspace/jsp-servlet-dictionary

**3. Gửi câu lệnh (Prompt)** Hãy sao chép nguyên văn đoạn lệnh dưới đây, thay thế đoạn chữ viết hoa [ĐIỀN_ĐƯỜNG_DẪN_TUYỆT_ĐỐI_THƯ_MỤC_DỰ_ÁN_CỦA_BẠN_VÀO_ĐÂY] bằng đường dẫn bạn vừa chọn ở trên, rồi dán vào ô chat AI:

> ***Hãy tạo một dự án Maven Webapp tiêu chuẩn cho Java JSP/Servlet tương thích với máy chủ Tomcat 10.1+.***
>
> ***·       Nơi lưu trữ dự án: Hãy ghi và khởi tạo toàn bộ dự án tại đường dẫn tuyệt đối sau trên máy của tôi: [ĐIỀN_ĐƯỜNG_DẪN_TUYỆT_ĐỐI_THƯ_MỤC_DỰ_ÁN_CỦA_BẠN_VÀO_ĐÂY]***
>
> ***·       Đặt cấu hình Maven: groupId là com.codegym, artifactId là jsp-servlet-dictionary***
>
> ***·       Thiết lập cấu trúc thư mục tiêu chuẩn:***
>
> ***o   Có thư mục src/main/java để chứa mã nguồn Java Servlets.***
>
> ***o   Có thư mục src/main/webapp/WEB-INF chứa file cấu hình web.xml tương thích hoàn toàn với Jakarta Servlet API (Tomcat 10+).***
>
> ***·       Yêu cầu bổ sung về chức năng Từ điển:***
>
> ***1.     Sinh tự động một file index.jsp chứa một form nhập liệu (gồm 1 ô input name là 'word' để nhập từ tiếng Anh và 1 nút submit 'Tìm kiếm'), form này sử dụng phương thức POST gửi dữ liệu tới endpoint /translate.***
>
> ***2.     Sinh một class** [**DictionaryServlet.java**](http://dictionaryservlet.java/) **xử lý request POST từ form trên. Trong Servlet này, hãy khởi tạo sẵn một danh sách từ vựng (Map) gồm vài từ cơ bản (ví dụ: hello-Xin chào, book-Quyển sách, computer-Máy tính). Lấy từ khóa người dùng nhập vào, tìm trong Map, nếu có thì in ra nghĩa tiếng Việt, nếu không có thì in ra dòng chữ 'Không tìm thấy từ: [từ_khóa]'.***

**4. Phê duyệt tạo file** Bấm **Enter**. AI Agent sẽ phân tích đường dẫn, tự động xây dựng cây thư mục, tạo file pom.xml, web.xml và các mã nguồn mẫu.

- Khi AI Agent hoàn thành, hãy click nút **Accept** hoặc **Create File** hiển thị bên cạnh mỗi tệp tin để xác nhận ghi dữ liệu vào ổ đĩa.

**Bước 2: Kiểm tra cấu trúc thư mục tiêu chuẩn**

Click vào biểu tượng **Explorer** (hình thư mục ở góc trên cùng bên trái màn hình) để rà soát xem cấu trúc dự án của bạn đã khớp chính xác với sơ đồ chuẩn dưới đây chưa:

jsp-servlet-dictionary/

├── pom.xml                        # File cấu hình khai báo thư viện quản lý bởi Maven

└── src/

    └── main/

        ├── java/                  # Nơi viết code logic Java

        │   └── com/

        │       └── codegym/

        │           └── [**DictionaryServlet.java**](http://dictionaryservlet.java/)  # Xử lý logic tra cứu từ vựng

        └── webapp/                # Thư mục chứa giao diện

            ├── index.jsp          # Trang chủ chứa Form tra cứu từ

            └── WEB-INF/           # Thư mục bảo mật cấu hình của ứng dụng Web

                └── web.xml        # File cấu hình ánh xạ URL tới Servlet

**Bước 3: Chi tiết mã nguồn mẫu (chuẩn Jakarta EE)**

**LƯU Ý CỐT LÕI:** Kể từ phiên bản Tomcat 10 trở đi, toàn bộ đặc tả Java Web cũ đã chuyển đổi tên gói (package) từ javax.servlet sang jakarta.servlet. Đảm bảo mã nguồn của bạn import đúng thư viện mới để tránh lỗi ClassNotFoundException.

**1. File cấu hình pom.xml**

Mở file pom.xml tại thư mục gốc và đảm bảo các thẻ thư viện được thiết lập chuẩn xác như sau:

```
<project xmlns="[http://maven.apache.org/POM/4.0.0](http://maven.apache.org/POM/4.0.0)" 
         xmlns:xsi="[http://www.w3.org/2001/XMLSchema-instance](http://www.w3.org/2001/XMLSchema-instance)" 
         xsi:schemaLocation="[http://maven.apache.org/POM/4.0.0](http://maven.apache.org/POM/4.0.0) [http://maven.apache.org/maven-v4_0_0.xsd](http://maven.apache.org/maven-v4_0_0.xsd)">
    <modelVersion>4.0.0</modelVersion>
    <groupId>com.codegym</groupId>
    <artifactId>jsp-servlet-dictionary</artifactId>
    <packaging>war</packaging>
    <version>1.0-SNAPSHOT</version>
    <name>Dictionary Maven Webapp</name>

    <properties>
        <maven.compiler.source>17</maven.compiler.source>
        <maven.compiler.target>17</maven.compiler.target>
        <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
    </properties>

    <dependencies>
        <dependency>
            <groupId>jakarta.servlet</groupId>
            <artifactId>jakarta.servlet-api</artifactId>
            <version>6.0.0</version>
            <scope>provided</scope>
        </dependency>
        
        <dependency>
            <groupId>jakarta.servlet.jsp</groupId>
            <artifactId>jakarta.servlet.jsp-api</artifactId>
            <version>3.1.1</version>
            <scope>provided</scope>
        </dependency>
    </dependencies>

    <build>
        <finalName>jsp-servlet-dictionary</finalName>
        <plugins>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-war-plugin</artifactId>
                <version>3.4.0</version>
            </plugin>
        </plugins>
    </build>
</project>
```

**2. File [DictionaryServlet.java](http://dictionaryservlet.java/) (Tầng xử lý Logic tra cứu)**

Kiểm tra file tại đường dẫn src/main/java/com/codegym/[**DictionaryServlet.java**](http://dictionaryservlet.java/):

```
package com.codegym;

import java.io.IOException;
import java.io.PrintWriter;
import java.util.HashMap;
import java.util.Map;
import jakarta.servlet.ServletException;
import jakarta.servlet.annotation.WebServlet;
import jakarta.servlet.http.HttpServlet;
import jakarta.servlet.http.HttpServletRequest;
import jakarta.servlet.http.HttpServletResponse;

// Khai báo định tuyến URL: Khi gõ "/translate", trình duyệt sẽ kích hoạt Servlet này
@WebServlet(name = "DictionaryServlet", urlPatterns = {"/translate"})
public class DictionaryServlet extends HttpServlet {

    @Override
    protected void doPost(HttpServletRequest request, HttpServletResponse response) 
            throws ServletException, IOException {
        
        // Cấu hình phản hồi hiển thị HTML và hỗ trợ hiển thị Tiếng Việt
        response.setContentType("text/html;charset=UTF-8");
        request.setCharacterEncoding("UTF-8");
        
        // Khởi tạo danh sách từ vựng (Từ điển)
        Map<String, String> dictionary = new HashMap<>();
        dictionary.put("hello", "Xin chào");
        dictionary.put("how", "Thế nào");
        dictionary.put("book", "Quyển sách");
        dictionary.put("computer", "Máy tính");
        dictionary.put("student", "Sinh viên");

        // Nhận tham số từkhóa từ form
        String searchWord = request.getParameter("word");

        try (PrintWriter out = response.getWriter()) {
            out.println("<!DOCTYPE html>");
            out.println("<html>");
            out.println("<head><title>Kết quả tra cứu</title></head>");
            out.println("<body style='font-family: Arial, sans-serif; text-align: center; margin-top: 100px;'>");
            
            if (searchWord != null && !searchWord.trim().isEmpty()) {
                // Chuyển từ khóa về chữ thường để dễ tìm kiếm
                String result = dictionary.get(searchWord.trim().toLowerCase());
                
                if (result != null) {
                    out.println("<h2 style='color: #1b2a7a;'>Từ khóa: " + searchWord + "</h2>");
                    out.println("<h3 style='color: #27ae60;'>Nghĩa tiếng Việt: " + result + "</h3>");
                } else {
                    out.println("<h2 style='color: red;'>Không tìm thấy từ: " + searchWord + "</h2>");
                }
            } else {
                out.println("<h2 style='color: orange;'>Vui lòng nhập từ khóa hợp lệ!</h2>");
            }
            
            out.println("<br><a href='index.jsp' style='text-decoration: none; padding: 10px 20px; background-color: #1b2a7a; color: white; border-radius: 4px;'>Quay lại</a>");
            out.println("</body>");
            out.println("</html>");
        }
    }
}
```

**3. File index.jsp (Tầng giao diện Form)**

Kiểm tra file tại đường dẫn src/main/webapp/index.jsp. Đảm bảo Action của Form trỏ đúng đến Servlet:

```
<%@page contentType="text/html" pageEncoding="UTF-8"%>
<!DOCTYPE html>
<html>
    <head>
        <meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
        <title>Từ điển Anh - Việt</title>
        <style>
            body { font-family: 'Arial', sans-serif; display: flex; justify-content: center; margin-top: 100px; background-color: #f8fafc; }
            .dictionary-container { background: white; padding: 40px; border-radius: 8px; box-shadow: 0 4px 10px rgba(0,0,0,0.1); text-align: center; width: 350px; }
            input { padding: 12px; margin: 15px 0; width: 90%; border: 1px solid #ccc; border-radius: 4px; box-sizing: border-box; font-size: 16px;}
            button { background-color: #1b2a7a; color: white; padding: 12px 20px; border: none; border-radius: 4px; cursor: pointer; width: 90%; font-weight: bold; font-size: 16px;}
            button:hover { background-color: #121c54; }
        </style>
    </head>
    <body>
        <div class="dictionary-container">
            <h2 style="color: #1b2a7a;">Từ Điển Anh - Việt</h2>
            <!-- Form gửi dữ liệu bằng phương thức POST tới đường dẫn /translate -->
            <form action="translate" method="POST">
                <input type="text" name="word" placeholder="Nhập từ tiếng Anh..." required autofocus />
                <button type="submit">Tìm kiếm</button>
            </form>
        </div>
    </body>
</html>
```

**Bước 4: Đóng gói và triển khai lên server Tomcat**

**1. Biên dịch và Đóng gói file .war**

- **Bước 4.1:** Mở Terminal tích hợp trong IDE bằng phím tắt Ctrl + \` (phím dấu nháy đơn nằm cạnh phím số 1).
- **Bước 4.2:** Thực hiện gõ lệnh biên dịch chuẩn Maven:

```
mvn clean package
```

- **Bước 4.3:** Chờ màn hình Terminal thông báo dòng chữ **BUILD SUCCESS**. Lúc này, một tệp tin phân phối mang tên jsp-servlet-dictionary.war đã được tạo ra nằm gọn bên trong thư mục target/.

**2. Khởi chạy Tomcat Server trực quan từ IDE**

Chúng ta sẽ sử dụng plugin **Community Server Connectors** tích hợp sẵn trong IDE để vận hành hệ thống:

1. **Mở Tab Servers:** Tại dải bảng điều khiển bên trái, nhấp chọn tab có biểu tượng máy chủ (SERVERS).
2. **Khởi tạo Máy chủ:** Click vào dấu cộng (+) hoặc liên kết **Create New Server...**
   - Chọn danh mục **Apache Tomcat** ➔ Chọn phiên bản **Tomcat 10.x**.
   - Hệ thống yêu cầu cung cấp vị trí cài đặt ➔ Trỏ đường dẫn đến thư mục chứa bộ cài Apache Tomcat đã giải nén trên máy của bạn (Ví dụ: C:\tomcat hoặc /Users/machine/tomcat). Bấm **Finish**.
3. **Deploy (Triển khai ứng dụng):**
   - Click chuột phải vào Server Tomcat bạn vừa cấu hình ➔ Chọn **Add Deployment...**
   - Chọn phương thức nạp dạng **File** ➔ Chọn đường dẫn trỏ thẳng đến tệp tin jsp-servlet-dictionary.war nằm bên trong thư mục target/ của dự án.
4. **Kích hoạt hệ thống:** Click chuột phải vào máy chủ Tomcat ➔ Chọn **Start Server**. Kiểm tra tab Output, khi log màu trắng hiển thị thông điệp báo hoàn tất startup in [xxxx] ms tức là Server đã sẵn sàng phục vụ.

**3. Kiểm nghiệm thực tế trên Trình duyệt**

Mở trình duyệt Web (Chrome, Edge, Safari...) và truy cập địa chỉ sau để kiểm tra:

- **Trang chủ chứa Form:** [**http://localhost:8080/jsp-servlet-dictionary/**](http://localhost:8080/jsp-servlet-dictionary/)
- Hãy nhập một từ có trong thư viện (ví dụ: hello, book) để xem kết quả trả về. Sau đó thử nhập một từ bất kỳ không có để kiểm chứng thông báo lỗi.

### Prompt ra lệnh cho AI Agent triển khai dự án

**Chuẩn bị trước:** Hãy đảm bảo bạn đã biết chính xác đường dẫn thư mục cài đặt Tomcat trên máy tính (Ví dụ: **`C:\Tomcat 10.1`** trên Windows hoặc **`/Library/Tomcat`** trên macOS).

**Copy đoạn lệnh dưới đây và dán vào khung chat của AI Agent:**

> ***Đóng vai là một chuyên gia DevOps, hãy giúp tôi tự động hóa quá trình đóng gói và triển khai dự án Java Web hiện tại lên máy chủ Tomcat.***
>
> ***Yêu cầu thực thi:***
>
> ***1.     Biên dịch dự án: Mở terminal tại thư mục gốc của dự án này và chạy lệnh `mvn clean package` để dọn dẹp và đóng gói dự án. Hãy chờ cho đến khi xuất hiện thông báo `BUILD SUCCESS`.***
>
> ***2.     Xác định file: Tìm file `.war` vừa được tạo ra bên trong thư mục `target/` của dự án.***
>
> ***3.     Triển khai (Deploy): Sử dụng lệnh hệ thống (terminal/bash/powershell) để copy file `.war` này và dán vào thư mục `webapps` của máy chủ Tomcat tại đường dẫn tuyệt đối sau: [ĐIỀN_ĐƯỜNG_DẪN_THƯ_MỤC_TOMCAT_CỦA_BẠN_VÀO_ĐÂY]***
>
> ***4.     Khởi động Server: Sau khi copy thành công, hãy điều hướng terminal tới thư mục `bin` của Tomcat và chạy file khởi động (`startup.bat` cho Windows hoặc `./startup.sh` cho macOS/Linux).***
>
> ***Hãy hiển thị cho tôi các lệnh bạn sẽ chạy trước khi thực thi để tôi phê duyệt.***