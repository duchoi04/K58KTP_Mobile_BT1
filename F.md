F. GỠ LỖI

1. Kiểm tra nhanh: docker compose ps giúp biết container nào đang chạy xem log: 

<img width="1704" height="187" alt="Screenshot 2026-04-13 175135" src="https://github.com/user-attachments/assets/5c52043f-8b04-4468-9695-3eb6eb4167dd" />


2. Thêm Healthcheck cho nodered giúp Docker biết container đó có thực sự "khỏe" để phục vụ yêu cầu hay không, thay vì chỉ báo là "Running".
<img width="1361" height="734" alt="image" src="https://github.com/user-attachments/assets/3e5f0c73-c28f-4396-833a-93b140193380" />


3. Giới hạn tài nguyên cho Nodered để tránh bị chiếm quá nhiều ram: 
<img width="1361" height="734" alt="image" src="https://github.com/user-attachments/assets/b19ef891-b39c-4d16-8d0b-97370d5d957f" />


 Sau đi đã giới hạn xong có thể giám sát thời gian thực bằng lệnh: docker compose stats image
<img width="1296" height="268" alt="image" src="https://github.com/user-attachments/assets/69f2e02a-2c1f-4509-b45a-93173d5c1d9c" />
