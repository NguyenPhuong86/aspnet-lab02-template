# BÀI THỰC HÀNH 02
## Tìm hiểu cấu trúc ứng dụng ASP.NET Core MVC

## 1. Mục tiêu

Sau khi hoàn thành bài thực hành, sinh viên có thể:

- Tạo một dự án ASP.NET Core MVC.
- Nhận diện các thành phần chính của mô hình MVC.
- Giải thích vai trò của Model, View và Controller.
- Tạo Controller và các Action.
- Tạo View tương ứng với từng Action.
- Sử dụng Layout chung trong ứng dụng.
- Sử dụng tệp CSS trong thư mục `wwwroot`.
- Hiểu vai trò cơ bản của `Program.cs` và định tuyến.
- Biên dịch và chạy ứng dụng bằng Kestrel.
- Commit và push mã nguồn lên GitHub.
- Kiểm tra kết quả chấm tự động bằng GitHub Actions.

---

## 2. Công cụ được phép sử dụng

Sinh viên được sử dụng một trong các môi trường:

- Visual Studio 2022;
- Visual Studio 2026;
- Visual Studio Code.

Dự án được phép sử dụng:

| Phiên bản | Target Framework |
|---|---|
| .NET 8 | `net8.0` |
| .NET 9 | `net9.0` |
| .NET 10 | `net10.0` |

Sinh viên chỉ chọn một phiên bản phù hợp với .NET SDK đã được cài đặt.

## 3. Yêu cầu chung

- Tên dự án bắt buộc là `Lab02.Web`.
- Dự án phải sử dụng `net8.0`, `net9.0` hoặc `net10.0`.
- Không thay đổi tên và vị trí các tệp được quy định.
- Không sửa hoặc xóa workflow chấm tự động.
- Không đưa các thư mục `.vs`, `bin` và `obj` lên GitHub.
- Sinh viên làm việc trên nhánh `main`.
- Mỗi giai đoạn hoàn thành phải có commit phù hợp.

---

# PHẦN A. CHUẨN BỊ MÔI TRƯỜNG

## 4. Kiểm tra công cụ

Mở Terminal, Command Prompt hoặc PowerShell:

```bash
dotnet --version
dotnet --info
dotnet --list-sdks
git --version
```

Máy phải có ít nhất một trong các SDK:

```text
8.0.x
9.0.x
10.0.x
```

### Nếu sử dụng Visual Studio

Cần cài workload:

```text
ASP.NET and web development
```

### Nếu sử dụng Visual Studio Code

Nên cài các extension:

- C#;
- C# Dev Kit;
- .NET Install Tool.

---

# PHẦN B. NHẬN REPOSITORY

## 5. Nhận bài tập

1. Mở đường dẫn Assignment do giảng viên cung cấp.
2. Đăng nhập đúng tài khoản GitHub.
3. Chọn **Accept assignment**.
4. Chờ Classroom tạo repository.
5. Chọn **Open repository**.

Sao chép địa chỉ HTTPS:

```text
Code → HTTPS → Copy URL
```

Clone repository:

```bash
git clone <repository-url>
cd <repository-name>
```

Không sử dụng **Download ZIP**, vì bài làm cần có lịch sử commit.

---

# PHẦN C. TẠO DỰ ÁN MVC

## 6. Tạo dự án

Mở Terminal tại thư mục gốc của repository.

### Sử dụng .NET 8

```bash
dotnet new mvc -n Lab02.Web --framework net8.0 --no-https
```

### Sử dụng .NET 9

```bash
dotnet new mvc -n Lab02.Web --framework net9.0 --no-https
```

### Sử dụng .NET 10

```bash
dotnet new mvc -n Lab02.Web --framework net10.0 --no-https
```

Chỉ chạy một trong ba lệnh trên.

> Sinh viên có thể viết code bằng Visual Studio hoặc Visual Studio Code, nhưng nên tạo dự án bằng lệnh trên để bảo đảm đúng cấu trúc chấm tự động.

## 7. Kiểm tra cấu trúc dự án

Sau khi tạo, repository phải có:

```text
repository/
├── .github/
│   └── workflows/
│       └── autograding.yml
├── Lab02.Web/
│   ├── Controllers/
│   ├── Models/
│   ├── Views/
│   ├── wwwroot/
│   ├── Program.cs
│   ├── appsettings.json
│   └── Lab02.Web.csproj
└── README.md
```

Biên dịch:

```bash
dotnet build Lab02.Web/Lab02.Web.csproj
```

Chạy ứng dụng:

```bash
dotnet run --project Lab02.Web/Lab02.Web.csproj
```

Mở địa chỉ được hiển thị trong Terminal.

Số cổng có thể khác nhau trên từng máy.

Dừng ứng dụng:

```text
Ctrl + C
```

---

# PHẦN D. TẠO COURSECONTROLLER

## 8. Tạo Controller

Tạo tệp:

```text
Lab02.Web/Controllers/CourseController.cs
```

Nội dung:

```csharp
using Microsoft.AspNetCore.Mvc;

namespace Lab02.Web.Controllers
{
    public class CourseController : Controller
    {
        public IActionResult Index()
        {
            return View();
        }

        public IActionResult Structure()
        {
            return View();
        }
    }
}
```

Controller phải có đúng hai Action:

```text
Index
Structure
```

---

# PHẦN E. TẠO VIEW INDEX

## 9. Tạo thư mục View

Tạo thư mục:

```text
Lab02.Web/Views/Course
```

Trong thư mục này, tạo:

```text
Index.cshtml
Structure.cshtml
```

## 10. Nội dung Index.cshtml

Tạo tệp:

```text
Lab02.Web/Views/Course/Index.cshtml
```

Nội dung:

```cshtml
@{
    ViewData["Title"] = "Thông tin học phần";
}

<link rel="stylesheet" href="~/css/lab02.css" />

<div class="lab02-container">
    <header class="lab02-header">
        <h1>Công nghệ phát triển ứng dụng</h1>
        <p>Bài thực hành 02 - Mô hình MVC</p>
    </header>

    <section class="lab02-card">
        <h2>Thông tin sinh viên</h2>

        <p>
            <strong>Họ và tên:</strong>
            Nguyễn Văn A
        </p>

        <p>
            <strong>Mã sinh viên:</strong>
            DTC123456
        </p>

        <p>
            <strong>Lớp:</strong>
            CNTT KXX
        </p>

        <p>
            <strong>Phiên bản .NET:</strong>
            .NET 8/9/10
        </p>
    </section>

    <section class="lab02-card">
        <h2>Mô hình MVC</h2>

        <p>
            MVC là mô hình tổ chức ứng dụng thành ba thành phần:
            Model, View và Controller.
        </p>

        <a asp-controller="Course"
           asp-action="Structure"
           class="lab02-button">
            Xem cấu trúc MVC
        </a>
    </section>
</div>
```

Sinh viên phải thay:

```text
Nguyễn Văn A
DTC123456
CNTT KXX
.NET 8/9/10
```

bằng thông tin thực tế.

Không được xóa các cụm từ:

```text
Công nghệ phát triển ứng dụng
Bài thực hành 02
Mô hình MVC
Họ và tên
Mã sinh viên
Lớp
```

---

# PHẦN F. TẠO VIEW STRUCTURE

## 11. Nội dung Structure.cshtml

Tạo tệp:

```text
Lab02.Web/Views/Course/Structure.cshtml
```

Nội dung:

```cshtml
@{
    ViewData["Title"] = "Cấu trúc MVC";
}

<link rel="stylesheet" href="~/css/lab02.css" />

<div class="lab02-container">
    <header class="lab02-header">
        <h1>Cấu trúc ứng dụng ASP.NET Core MVC</h1>
        <p>Vai trò của các thành phần trong dự án</p>
    </header>

    <section class="mvc-grid">
        <article class="lab02-card">
            <h2>Model</h2>
            <p>
                Model biểu diễn dữ liệu và các quy tắc nghiệp vụ
                của ứng dụng.
            </p>
        </article>

        <article class="lab02-card">
            <h2>View</h2>
            <p>
                View chịu trách nhiệm trình bày dữ liệu và tạo
                giao diện gửi đến người sử dụng.
            </p>
        </article>

        <article class="lab02-card">
            <h2>Controller</h2>
            <p>
                Controller tiếp nhận yêu cầu, điều phối xử lý
                và lựa chọn View phù hợp.
            </p>
        </article>

        <article class="lab02-card">
            <h2>wwwroot</h2>
            <p>
                wwwroot chứa các tài nguyên tĩnh như CSS,
                JavaScript và hình ảnh.
            </p>
        </article>

        <article class="lab02-card">
            <h2>Program.cs</h2>
            <p>
                Program.cs cấu hình dịch vụ, middleware,
                định tuyến và khởi động ứng dụng.
            </p>
        </article>
    </section>

    <a asp-controller="Course"
       asp-action="Index"
       class="lab02-button">
        Quay lại trang học phần
    </a>
</div>
```

Trang này phải có đủ các cụm từ:

```text
Model
View
Controller
wwwroot
Program.cs
```

---

# PHẦN G. TẠO TỆP CSS

## 12. Tạo lab02.css

Tạo tệp:

```text
Lab02.Web/wwwroot/css/lab02.css
```

Nội dung:

```css
.lab02-container {
    max-width: 1000px;
    margin: 30px auto;
    padding: 20px;
}

.lab02-header {
    margin-bottom: 24px;
    padding: 24px;
    color: white;
    background-color: #0d6efd;
    border-radius: 10px;
    text-align: center;
}

.lab02-card {
    margin-bottom: 20px;
    padding: 20px;
    background-color: #f8f9fa;
    border: 1px solid #dee2e6;
    border-radius: 8px;
}

.mvc-grid {
    display: grid;
    grid-template-columns: repeat(
        auto-fit,
        minmax(250px, 1fr)
    );
    gap: 20px;
}

.lab02-button {
    display: inline-block;
    padding: 10px 18px;
    color: white;
    background-color: #198754;
    border-radius: 6px;
    text-decoration: none;
}

.lab02-button:hover {
    color: white;
    background-color: #146c43;
}
```

Sinh viên có thể bổ sung CSS nhưng không được xóa các class:

```text
.lab02-container
.lab02-header
.lab02-card
.mvc-grid
.lab02-button
```

---

# PHẦN H. TẠO ENDPOINT KIỂM TRA

## 13. Cập nhật Program.cs

Mở:

```text
Lab02.Web/Program.cs
```

Thêm dòng sau trước `app.Run();`:

```csharp
app.MapGet("/health", () => "LAB02_OK");
```

Phần cuối của `Program.cs` phải có dạng:

```csharp
app.MapControllerRoute(
    name: "default",
    pattern: "{controller=Home}/{action=Index}/{id?}");

app.MapGet("/health", () => "LAB02_OK");

app.Run();
```

Không thay đổi:

```text
/health
LAB02_OK
```

---

# PHẦN I. CHẠY VÀ KIỂM TRA

## 14. Chạy ứng dụng

```bash
dotnet run --project Lab02.Web/Lab02.Web.csproj
```

Kiểm tra các địa chỉ:

### Trang học phần

```text
http://localhost:<port>/Course
```

### Trang cấu trúc MVC

```text
http://localhost:<port>/Course/Structure
```

### Endpoint kiểm tra

```text
http://localhost:<port>/health
```

Kết quả của `/health` phải là:

```text
LAB02_OK
```

Nếu cả ba địa chỉ hoạt động thì dừng chương trình:

```text
Ctrl + C
```

---

# PHẦN J. COMMIT VÀ PUSH

## 15. Yêu cầu lịch sử commit

Sinh viên phải có ít nhất năm commit phát triển, không tính các commit được Classroom tạo tự động.

### Commit 1: tạo dự án

```bash
git add .
git commit -m "Create ASP.NET Core MVC project"
git push
```

### Commit 2: tạo Controller

```bash
git add .
git commit -m "Add Course controller and actions"
git push
```

### Commit 3: tạo các View

```bash
git add .
git commit -m "Add Course views"
git push
```

### Commit 4: hoàn thiện giao diện

```bash
git add .
git commit -m "Add Lab 02 stylesheet"
git push
```

### Commit 5: hoàn thiện bài

```bash
git add .
git commit -m "Complete Lab 02"
git push
```

Không sử dụng commit message không rõ nghĩa như:

```text
update
fix
abc
123
nop bai
```

---

# PHẦN K. KIỂM TRA KẾT QUẢ TỰ ĐỘNG

Sau mỗi lần push:

1. Mở repository trên GitHub.
2. Chọn tab **Actions**.
3. Chọn workflow **Autograding Lab 02**.
4. Mở lần chạy mới nhất.
5. Kiểm tra từng bước.

Trạng thái:

- Dấu tích xanh: kiểm tra thành công.
- Dấu X đỏ: có yêu cầu chưa đạt.
- Dấu tròn vàng: hệ thống đang kiểm tra.
- Dấu tròn gạch chéo: workflow được bỏ qua.

Nếu workflow báo lỗi:

1. Mở bước có dấu X.
2. Đọc thông báo.
3. Sửa mã nguồn trên máy.
4. Chạy lại ứng dụng.
5. Commit và push lại.

---

# PHẦN L. TIÊU CHÍ ĐÁNH GIÁ

| Nội dung | Điểm |
|---|---:|
| Đúng tên và cấu trúc dự án | 1,0 |
| Sử dụng .NET 8, .NET 9 hoặc .NET 10 | 1,0 |
| Dự án biên dịch thành công | 2,0 |
| Có Controller và các Action theo yêu cầu | 1,0 |
| Có đủ View và nội dung bắt buộc | 1,0 |
| Các URL hoạt động đúng | 2,0 |
| Có và sử dụng tệp CSS | 1,0 |
| Có ít nhất năm commit hợp lệ | 1,0 |
| **Tổng cộng** | **10,0** |

Hệ thống tự động kiểm tra 9 điểm. Giảng viên kiểm tra lịch sử commit để chấm 1 điểm còn lại.

## Lưu ý cuối cùng

- Không đổi tên dự án `Lab02.Web`.
- Không đổi tên `CourseController`.
- Không đổi tên các Action `Index` và `Structure`.
- Không đổi các đường dẫn `/Course`, `/Course/Structure` và `/health`.
- Không thay đổi chuỗi `LAB02_OK`.
- Không sửa hoặc xóa `.github/workflows/autograding.yml`.
- Không đưa `.vs`, `bin` và `obj` lên GitHub.
- Sinh viên phải kiểm tra trạng thái Actions trước hạn nộp bài.
