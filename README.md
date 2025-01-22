# SOA_minimal_APIs

## Tổng Quan Dự Án

Dự án này xây dựng một **API Minimal** sử dụng **ASP.NET Core** để quản lý danh sách các công việc (to-do items). API cung cấp các thao tác CRUD (Create, Read, Update, Delete) cơ bản để người dùng có thể thêm, sửa, xóa và theo dõi các mục công việc. Cơ sở dữ liệu sử dụng **Entity Framework Core** với **In-Memory Database**, giúp quản lý dữ liệu một cách đơn giản và nhẹ nhàng.

## Các Tính Năng Chính

API hỗ trợ các chức năng sau:

1. **Tạo mục Todo** (`POST /todoitems`): Thêm một công việc mới vào danh sách.
2. **Lấy tất cả các mục Todo** (`GET /todoitems`): Lấy danh sách tất cả các công việc.
3. **Lấy các mục Todo đã hoàn thành** (`GET /todoitems/complete`): Lấy danh sách công việc đã hoàn thành.
4. **Lấy mục Todo theo ID** (`GET /todoitems/{id}`): Lấy thông tin chi tiết của một công việc cụ thể.
5. **Cập nhật mục Todo** (`PUT /todoitems/{id}`): Cập nhật thông tin của một công việc.
6. **Xóa mục Todo** (`DELETE /todoitems/{id}`): Xóa một công việc khỏi danh sách.

## Cơ Sở Dữ Liệu

API sử dụng **Entity Framework Core** và **Cơ sở dữ liệu In-Memory** để lưu trữ các mục todo, điều này giúp việc quản lý dữ liệu trở nên nhanh chóng và đơn giản. Dữ liệu được cấu hình qua câu lệnh:

```csharp
builder.Services.AddDbContext<TodoDb>(opt => opt.UseInMemoryDatabase("TodoList"));
```

## Mô Hình Dữ Liệu

### Mô hình Todo:
- **Id**: Số nguyên, khóa chính của mục todo.
- **Name**: Chuỗi, tên hoặc mô tả của mục todo.
- **IsComplete**: Boolean, chỉ ra mục todo đã hoàn thành hay chưa.

## Các Endpoint API

Dưới đây là các endpoint API được triển khai:

| HTTP Method | Endpoint                | Mô tả                              | Request Body   | Response Body |
|-------------|-------------------------|-------------------------------------|----------------|---------------|
| GET         | `/todoitems`            | Lấy tất cả các công việc            | None           | Mảng công việc|
| GET         | `/todoitems/complete`   | Lấy các công việc đã hoàn thành     | None           | Mảng công việc|
| GET         | `/todoitems/{id}`       | Lấy công việc theo ID               | None           | Công việc      |
| POST        | `/todoitems`            | Thêm một công việc mới              | Công việc      | Công việc      |
| PUT         | `/todoitems/{id}`       | Cập nhật một công việc hiện có      | Công việc      | None          |
| DELETE      | `/todoitems/{id}`       | Xóa một công việc                   | None           | None          |

## Các Bước Triển Khai API

### 1. **Khởi tạo dự án:**
   - Tạo dự án ASP.NET Core với mẫu **Empty Project**.
   - Cấu hình các thư viện cần thiết như **Microsoft.EntityFrameworkCore.InMemory** để sử dụng cơ sở dữ liệu trong bộ nhớ.

### 2. **Xây dựng Model và Database Context:**
   - Tạo lớp **Todo.cs** để đại diện cho mục công việc.
   - Tạo lớp **TodoDb.cs** để quản lý các thao tác với cơ sở dữ liệu.

### 3. **Cấu hình API trong Program.cs:**
   - Tạo các endpoint HTTP để thực hiện các thao tác CRUD (Thêm, Sửa, Xóa, Lấy thông tin).

### 4. **Kiểm thử API:**
   - Sử dụng công cụ như **Postman** hoặc **Visual Studio** để gửi các yêu cầu và kiểm tra kết quả.

## Ví Dụ Yêu Cầu API

### Thêm một công việc mới:
**Endpoint:**
```http
POST https://localhost:7090/todoitems
```
**Request Body:**
```json
{
  "name": "walk dog",
  "isComplete": true
}
```
**Response Body:**
```json
{
  "id": 1,
  "name": "walk dog",
  "isComplete": true
}
```

### Cập nhật công việc:
**Endpoint:**
```http
PUT https://localhost:7090/todoitems/1
```
**Request Body:**
```json
{
  "name": "feed fish",
  "isComplete": false
}
```

## Hướng Dẫn Chạy Dự Án

1. **Clone repository** từ GitHub:
   ```bash
   git clone https://github.com/soa-ueh-thanhlam/Excersie3.git
   ```

2. **Điều hướng vào thư mục dự án**:
   ```bash
   cd Excersie3
   ```

3. **Chạy ứng dụng**:
   ```bash
   dotnet run
   ```

4. **Kiểm tra ứng dụng tại**:
   - HTTP: `http://localhost:7090`
   - HTTPS: `https://localhost:7091`

## Tài Liệu Tham Khảo

- [Microsoft Docs: Minimal APIs in ASP.NET Core](https://learn.microsoft.com/en-us/aspnet/core/tutorials/min-web-api?view=aspnetcore-9.0&tabs=visual-studio)
