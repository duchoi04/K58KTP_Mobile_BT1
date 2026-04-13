C. Cấu hình docker compose và Triển khai dự án
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


2. Kiểm tra dự án

2.1. Sau khi hoàn tất thì sử dụng lệnh: docker compose restart để khởi động lại các dịch vụ và kiểm tra bằng cách truy cập vào các cổng của nginx và nodered trên trình duyệt:
   

Nginx:

<img width="1920" height="1080" alt="Screenshot 2026-04-13 003155" src="https://github.com/user-attachments/assets/1f831459-e93d-43ff-9e6a-7ab24349b489" />


Nodered:

<img width="1920" height="1080" alt="Screenshot 2026-04-13 003138" src="https://github.com/user-attachments/assets/98553e22-9ed6-4568-983a-0a1bcdbe19c1" />


Proxy qua nginx:
<img width="959" height="452" alt="image" src="https://github.com/user-attachments/assets/5be1713d-0e95-4bfc-beae-04eea21f7c94" />


2.2. Kiểm tra location /api dùng proxy_pass trỏ tới 1 (hoặc nhiều) node http_in của nodered:

Cấu hình nodered:

<img width="694" height="331" alt="image" src="https://github.com/user-attachments/assets/ef56e169-dd73-46db-8155-71a806e81003" />


Kiểm tra truy cập proxy: 192.168.1.46:8080/api/hello

<img width="1920" height="1080" alt="Screenshot 2026-04-13 160258" src="https://github.com/user-attachments/assets/f32eafc0-e49a-44fb-8180-36a194b82659" />


3. Chỉnh sửa file index.html, nodered để sử dụng được API đã khai báo proxy_pass:

Index.html: thêm JS để nginx có thể get và post API trực tiếp tới nodered thay vì phải thay đổi đường dẫn bằng tay:

<img width="993" height="867" alt="image" src="https://github.com/user-attachments/assets/55b069dd-38e6-42de-8d29-f758ebdad530" />

Kết quả:

<img width="963" height="980" alt="image" src="https://github.com/user-attachments/assets/b7488f3f-a596-48b6-8c12-1b3715f3882f" />
