G. TRIỂN KHAI ỨNG DỤNG ĐẾN END-USER

1. Triển Khai Tunel trên cloudflare và convert vào docker conpose:

Truy cập vào Cloudflare Dashboard:

-Bấm vào chữ add bên góc phải màn hình để tạo hầm

<img width="1912" height="1080" alt="Screenshot 2026-04-13 222427" src="https://github.com/user-attachments/assets/a46e9b29-f4f8-4e60-9976-a5e54793e4df" />

-Tạo tên hầm

<img width="1920" height="1080" alt="Screenshot 2026-04-13 222435" src="https://github.com/user-attachments/assets/4d41d45c-0b1d-417a-b968-6de41c249679" />

-Coppy dòng khóa và cho vào code ở file docker-compose.yml

<img width="1920" height="1077" alt="Screenshot 2026-04-13 222450" src="https://github.com/user-attachments/assets/b39d1eee-9a1b-4191-939b-7094643318bd" />

<img width="1666" height="291" alt="image" src="https://github.com/user-attachments/assets/46e0edf9-89cd-4137-9e6a-4e83afb5e68e" />

Chạy lại docker compose bằng lệnh: docker compose up -d để đảm bảo Docker xóa các container cũ và tạo lại mới hoàn toàn theo cấu hình vừa sửa:

<img width="607" height="164" alt="image" src="https://github.com/user-attachments/assets/f6dd45ff-aefc-43eb-95f7-8465673783c9" />


2. Public ứng dụng:


Trong giao diện quản lý Tunel trước đó, bấm Next và cấu hình trong phần Add a published application route for tunel như sau:


<img width="1920" height="1079" alt="image" src="https://github.com/user-attachments/assets/3b251a0a-d6fb-49aa-9788-73cc34ab76f7" />

Sau khi điền xong:

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/829c654a-fcb0-45bd-bfee-9168ab74c4bd" />

3. Kiểm tra url sub-domain đã hoạt động public cho mọi end-user:
Trên máy tính:
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/e62c9fa5-b586-48a5-9b88-dfdf2c45ed32" />


Trên điện thoại:
<img width="1179" height="2556" alt="image" src="https://github.com/user-attachments/assets/fc87191d-339c-4c47-9ae3-80493988f7b8" />


