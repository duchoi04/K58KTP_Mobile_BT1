C. Cấu hình docker compose 
1. Tạo dự án

Tạo thư mục: ~/myapp

Chuyển vào trong thư mục ~/myapp

Tạo thư mục: ./myweb

<img width="339" height="726" alt="Screenshot 2026-04-13 213208" src="https://github.com/user-attachments/assets/0d4ff9e8-446a-4ea7-bda1-a1e95d1de522" />



Tạo file ./myweb/index.html (với nội dung là thông tin cá nhân của em)

<img width="1383" height="994" alt="image" src="https://github.com/user-attachments/assets/91b4bb0b-3129-4d9c-8adc-0314ae8b97cd" />


Tạo file cấu hình để Nginx biết cách trỏ tên miền và Proxy sang Node-RED: nano ~/myapp/nginx/nginx.conf

<img width="1381" height="1004" alt="image" src="https://github.com/user-attachments/assets/371945a7-9717-46a3-ad82-b7b82bc00aeb" />


Tạo file docker-compose.yml ( file cốt lõi để khởi chạy được cả 2 dịch vụ trên):nano ~/myapp/docker-compose.yml

<img width="1383" height="1002" alt="image" src="https://github.com/user-attachments/assets/abdb5d0e-9a4d-4a30-b990-585d04b1b121" />


Khởi chạy docer-compose trước để NodeRed sinh ra file cấu hình: docker compose up -d

Sửa mật khẩu "admin" và chỉnh sửa vào file setting.js trong nodered:

<img width="1383" height="994" alt="image" src="https://github.com/user-attachments/assets/09ade5ac-8a37-4419-a3e6-e7e2136f70a2" />
