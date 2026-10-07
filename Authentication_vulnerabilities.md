# 1. LAB 

## 1. Lab: Username enumeration via different responses ##

Nhập bừa vào ô đăng nhập, thông báo trả về cho thấy ta có thê check được username nào tồn tại

<img width="328" height="233" alt="image" src="https://github.com/user-attachments/assets/c45996ff-c2f3-4e86-8208-0fc799bee747" />

Ta sẽ brute force username

<img width="613" height="34" alt="image" src="https://github.com/user-attachments/assets/2e078537-967b-44ce-b7df-374c50de2e31" />

Tiếp tục với password

<img width="531" height="32" alt="image" src="https://github.com/user-attachments/assets/30326464-07b8-4af3-94e9-7d50b8b1262c" />

## 2. Lab: 2FA simple bypass #

Sau khi nhập mã verify thành công, để ý URLS

`https://....web-security-academy.net/my-account?id=wiener`

Tương tự với carlos, sau khi đăng nhập thành công ta sẽ sửa đường dẫn


## 3. Lab: Username enumeration via subtly different responses ##

Thông báo đăng nhập trả về chung chung

<img width="239" height="178" alt="image" src="https://github.com/user-attachments/assets/f6e45a48-8de4-4c04-adb4-060c3bd2a90c" />

## 4. Lab: Password reset broken logic ##

thử brute force cả username và password

<img width="668" height="26" alt="image" src="https://github.com/user-attachments/assets/babc49ea-00c3-4113-9a93-a8286e7f65eb" />

# 5. Lab: 2FA broken logic

Có request GET này để gửi mã xác minh, ta sẽ đổi giá trị verify thành `carlos` để hệ thống gửi mã xác nhận cho tài khoản đó

<img width="320" height="188" alt="image" src="https://github.com/user-attachments/assets/69b8f633-607e-4b6c-a9ec-1cd7168321e2" />

Đây là request để gửi mã xác minh lên hệ thống, xác thực đăng nhập tài khoản

<img width="311" height="207" alt="image" src="https://github.com/user-attachments/assets/35072934-a419-4ff1-b35f-32850445d14e" />

Đổi verfy thành `carlos` và bruteforce giá trị mfa

<img width="709" height="132" alt="image" src="https://github.com/user-attachments/assets/0010f7d5-08b9-44fb-8040-741ad3c56732" />

# 6. Lab: Password brute-force via password change

Nhập sai password hiện tại thì hiện thông báo như sau

<img width="443" height="118" alt="image" src="https://github.com/user-attachments/assets/a2cf1728-b9e7-4e78-9f55-ca204bb80cd1" />

Tận dụng alert này để bruteforce password 

<img width="563" height="28" alt="image" src="https://github.com/user-attachments/assets/167a168e-7e4a-461c-afd7-7ad65d9ca8f1" />

Vậy password là `112233`

# 7. Lab: Broken brute-force protection, multiple credentials per request

Thử bruteforce nhưng bị hệ thống chặn

<img width="678" height="53" alt="image" src="https://github.com/user-attachments/assets/c45d9dad-561d-4c30-a121-4ee3f5c68adf" />

Để ý form đăng nhập trong request đang ở dạng JSON, ta sẽ test nhiều password một lúc trong 1 request 


<img width="632" height="243" alt="image" src="https://github.com/user-attachments/assets/07440e86-e82c-4ba5-a906-092314020c7e" />

























