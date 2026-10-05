# 1. LAB

## 1. Lab: Basic SSRF against the local server ##

Server đang cho user kiểm soát URL mà server sẽ request tới

<img width="920" height="302" alt="image" src="https://github.com/user-attachments/assets/9e2ccdef-2700-4a44-82e8-d9e9503dec4d" />

Trỏ đến admin interface

<img width="716" height="151" alt="image" src="https://github.com/user-attachments/assets/f3e7d333-d19c-422e-9ead-e324f96aa8b6" />

Trả về thông báo lỗi

<img width="688" height="235" alt="image" src="https://github.com/user-attachments/assets/122c01f0-5ea9-41b2-887e-2f91ef22f862" />

Ta đổi payload thành `stockApi=http://localhost/admin/delete?username=carlos`

## 2. Lab: Basic SSRF against another back-end system ##

```
To solve the lab, use the stock check functionality to scan the internal 192.168.0.X range for an admin interface on port 8080, then use it to delete the user carlos.
```
Ta sẽ bruteforce giá trị x, set giá trị từ 0 đến 255


<img width="938" height="322" alt="image" src="https://github.com/user-attachments/assets/457b70c7-e130-48b6-ba0f-fb760e816adc" />

Sau đó modify request `stockApi=http://192.168.0.83:8080/admin/delete?username=carlos`















