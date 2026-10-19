<img width="803" height="53" alt="image" src="https://github.com/user-attachments/assets/c047cb9c-ec62-4ce1-951f-00473f3de664" /># 1. LAB 

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

<img wTa idth="606" height="82" alt="image" src="https://github.com/user-attachments/assets/285a7c1e-17e5-476a-afae-eb0714c23783" />

## 4. Lab: Web shell upload via extension blacklist bypass ## LÀM LẠI

Up thử file png thì thành công

<img width="812" height="90" alt="image" src="https://github.com/user-attachments/assets/c56161a3-6baf-4dc6-9854-784570b33215" />

Nhưng thử sang file php thì bị chặn

<img width="923" height="81" alt="image" src="https://github.com/user-attachments/assets/582a5c2b-c81b-426f-890b-76d68abae0e7" />

Thử với file `.htaccess`

<img width="803" height="53" alt="image" src="https://github.com/user-attachments/assets/bba49e7d-21d1-479f-a99c-069f615aefc5" />

Ta sẽ add 1 thêm thông tin về đuôi file có thể chạy php vào file này `AddType application/x-httpd-php .abc`



# 5. Lab: Web shell upload via obfuscated file extension  # 

<img width="782" height="84" alt="image" src="https://github.com/user-attachments/assets/60ea43a0-a574-4957-82e0-82a9640075c6" />

Hệ thống chỉ cho upload file PNG, JPG

Ta sẽ sử dụng dấu chấm phẩy, null byte để bypass vì hệ thống kiểm tra đuôi file cuối cùng

<img width="801" height="98" alt="image" src="https://github.com/user-attachments/assets/e92d67f4-9feb-4560-a12e-33d4907003ed" />

<img width="831" height="104" alt="image" src="https://github.com/user-attachments/assets/9776536b-aeac-477c-8d2a-7a375eaacc58" />

Thành công up file test.php

<img width="714" height="71" alt="image" src="https://github.com/user-attachments/assets/28ff2517-4c48-4835-a59a-8c485dae88ba" />

Thay đổi nội dung file thành `<?php echo file_get_contents('/home/carlos/secret'); ?>` để lấy thông tin cần lấy

# 6. Lab: Remote code execution via polyglot web shell upload #

Ta thử chèn đoạn script vào thì response phản hồi không hợp lệ

<img width="855" height="135" alt="image" src="https://github.com/user-attachments/assets/d33ace95-84db-468d-b755-efb4598e4c2d" />

Nhưng hệ thống lại không cấm đuôi file php --> chỉ kiểm tra định dạng của ảnh chứ không kiểm tra đuôi file

Signature của file gif

<img width="1219" height="171" alt="image" src="https://github.com/user-attachments/assets/67fb8d3c-b10a-4a15-b150-7a005b541df9" />

Modify lại request

<img width="867" height="157" alt="image" src="https://github.com/user-attachments/assets/3db2cd77-8340-4652-bc15-672464466dfe" />

Đổi lại thành đuôi php

<img width="857" height="106" alt="image" src="https://github.com/user-attachments/assets/ffbff644-4d2d-4b5b-be35-1275219241b4" />

Lấy thành công nội dung file

<img width="706" height="125" alt="image" src="https://github.com/user-attachments/assets/25736695-c43f-46cb-850a-23d1898a9747" />

























