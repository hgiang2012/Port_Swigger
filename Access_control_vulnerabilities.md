<img width="959" height="434" alt="image" src="https://github.com/user-attachments/assets/e459f0f9-2e68-4c10-854b-ab3847351a5a" /># 1. LAB 

## 1. Lab: Unprotected admin functionality ##

Kiểm tra file `robots.txt`

<img width="206" height="53" alt="image" src="https://github.com/user-attachments/assets/88b9896a-c262-40c0-b2ab-9f7d10843860" />

Truy cập vào đường dẫn đó

<img width="187" height="128" alt="image" src="https://github.com/user-attachments/assets/e7264580-6ed7-40ca-b5a5-9be1a65f350d" />

## 2. Lab: Unprotected admin functionality with unpredictable URL ##

Kiểm tra source code

<img width="680" height="178" alt="image" src="https://github.com/user-attachments/assets/c09d0d48-1b7b-4c85-829a-abfc5093158d" />

Truy cập và ta vào được trang admin

## 3. Lab: User role controlled by request parameter ##

<img width="332" height="29" alt="image" src="https://github.com/user-attachments/assets/914be029-60cc-4f82-a397-2c1bc30616b8" />

Chuyển trạng thái admin thành true

<img width="158" height="32" alt="image" src="https://github.com/user-attachments/assets/c73c4a5a-6d3a-44d7-9f22-0d6938990941" />

<img width="959" height="277" alt="image" src="https://github.com/user-attachments/assets/a8b8a9a2-1ed8-458a-94dd-0a191d7bcd00" />

Nhưng khi bấm vào admin panel thì thấy hiện như sau
Bắt request đó và chuyển thành true

<img width="101" height="30" alt="image" src="https://github.com/user-attachments/assets/1f08c09a-89ce-484a-ac7b-258370a5e2cd" />

## 4. Lab: User role can be modified in user profile ##

Ở phần update email
Request
```
{"email":"test@gmail.com"}
```
Response
```
{
  "username": "wiener",
  "email": "test@gmail.com",
  "apikey": "SKaruwIc8ZQiZ6ONhjfMKZ8lYPvKC3fY",
  "roleid": 1
}
```
Ta sẽ đổi roleid thành 2 để chuyển thành role admin

## 5. Lab: URL-based access control can be circumvented VIẾT LẠI  ##


<img width="339" height="56" alt="image" src="https://github.com/user-attachments/assets/ab0a1eba-8388-40df-a107-1feb924eb02b" />

Deny again 

<img width="661" height="68" alt="image" src="https://github.com/user-attachments/assets/a9f4e8ec-d1a7-46cc-a692-68c49edc3820" />

##  6. Lab: User role controlled by request parameter VIẾT LẠI ĐẦY ĐỦ  ##

<img width="362" height="34" alt="image" src="https://github.com/user-attachments/assets/485ef14b-64ef-46a1-ae2e-c10af2fe7f76" />

<img width="398" height="38" alt="image" src="https://github.com/user-attachments/assets/92ef9ef3-b50b-4ab2-9033-12d9089f9574" />


<img width="885" height="338" alt="image" src="https://github.com/user-attachments/assets/dedeb3b7-37e5-4def-b907-a92d3c3c024b" />

## 7. Lab: User ID controlled by request parameter, with unpredictable user IDs ##

Ở bài lab này, mỗi bài đăng sẽ do 1 người dùng khác nhau

<img width="688" height="299" alt="image" src="https://github.com/user-attachments/assets/cf57368d-f61b-4aaa-ab49-f4649b35d2db" />

Tìm bài của carlos

<img width="959" height="242" alt="image" src="https://github.com/user-attachments/assets/1436985c-35ae-4599-8fcd-211083ebf49d" />

Bấm vào `carlos` ta thấy hiện userid

`https://.....web-security-academy.net/blogs?userId=d98aa022-4273-421f-9f79-bb00ab170221`

## 8. Lab: User ID controlled by request parameter ##

Khi truy cập `https://....web-security-academy.net/my-account?id=wiener`, ta có API Key là ODRtAB9JES9brqu4jtrrhKKqIsD15HhF
Đổi thành `https://....web-security-academy.net/my-account?id=carlos`, ta có 9VoKFo59XTRp4hvmoPzz0MJoUoNCpNtZ

## 9. Lab: User ID controlled by request parameter with data leakage in redirect ##

Khi đổi `id=carlos`, hệ thống bị rò rỉ thông tin ở response redirect

<img width="959" height="245" alt="image" src="https://github.com/user-attachments/assets/cf3cd3c2-d88b-4233-b2b7-d2bc661bac00" />

## 10. Lab: User ID controlled by request parameter with password disclosure ##

Hệ thống trả về password người dùng dưới dạng plaintext

<img width="717" height="146" alt="image" src="https://github.com/user-attachments/assets/3fd66189-d210-4003-8327-2a3b252d949b" />

Ta đổi thành carlos

<img width="937" height="157" alt="image" src="https://github.com/user-attachments/assets/77b9ffe3-ddfe-4dd7-9de0-937fb068ebfb" />

Tương tự với tài khoản admin

## 11. Lab: Insecure direct object references TÝ LÀM LẠI ##

View transcript và để ý rằng số ở file txt tăng dần và bắt đầu từ 2

<img width="198" height="160" alt="image" src="https://github.com/user-attachments/assets/ea906e49-c5d7-4601-aa94-624f596bb12a" />

Modify request GET để xem file 1.txt ta được password

<img width="647" height="143" alt="image" src="https://github.com/user-attachments/assets/9ec31e54-ba76-41f5-a685-883d2e6e90d9" />



# 2. NOTE 
