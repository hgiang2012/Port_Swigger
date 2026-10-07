# 1. LAB 

## 1. Lab: Remote code execution via web shell upload ##

Hệ thống cho phép up file php

<img width="697" height="118" alt="image" src="https://github.com/user-attachments/assets/9d1713de-fbc0-4eb6-ba6e-f09d00908cc9" />

Thực thi thành công

<img width="557" height="82" alt="image" src="https://github.com/user-attachments/assets/3d0ee9ad-c23b-480e-8925-7466307ca53b" />

Đọc file

<img width="707" height="104" alt="image" src="https://github.com/user-attachments/assets/2d2f53d8-e9c6-478b-ba07-cad5f7287e5c" />

<img width="641" height="86" alt="image" src="https://github.com/user-attachments/assets/a54ad332-8299-4c5d-b1cc-fe3d8d119374" />

## 2. Lab: Web shell upload via Content-Type restriction bypass ##

Hệ thống chỉ cho phép up file ảnh

<img width="781" height="27" alt="image" src="https://github.com/user-attachments/assets/df9f646e-e3c5-4181-8691-12979525befb" />

Up ảnh lên hệ thống nhưng ta sẽ chỉnh sửa lại trong request, đổi tên file và nội dung

<img width="736" height="164" alt="image" src="https://github.com/user-attachments/assets/4941b82d-c712-48b9-b3d7-46853503b75f" />

<img width="605" height="78" alt="image" src="https://github.com/user-attachments/assets/cd7dbb28-6593-4332-a707-e2cbdf502217" />

## 3. Lab: Web shell upload via path traversal ##

<img width="672" height="164" alt="image" src="https://github.com/user-attachments/assets/ec545d29-2048-4353-8791-155491748c84" />

Ban đầu upload file, ta thấy hệ thống chỉ trả về plaintext mà không thực thi --> folder `avatars` chặn thực thi --> ta sẽ thực thi ở `files`

<img width="704" height="100" alt="image" src="https://github.com/user-attachments/assets/db274b23-d412-4b32-9386-e96179a9fcb5" />

Hệ thống chặn `../` nên ta sẽ thử encode

Sử dụng `..%2f` và thành công

<img width="682" height="144" alt="image" src="https://github.com/user-attachments/assets/d68b6e97-175e-40eb-a9ee-32b52c75d26f" />

<img width="606" height="82" alt="image" src="https://github.com/user-attachments/assets/285a7c1e-17e5-476a-afae-eb0714c23783" />

## 4.


<img width="588" height="160" alt="image" src="https://github.com/user-attachments/assets/5d497e2d-2ce3-4e7e-aa6f-3c5387eccf3f" />

# 5. 
