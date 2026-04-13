B. Cài đặt Ubuntu + Docker

1. Cài đặt hệ điều hành Ubuntu 24.04.4 LTS

Sử dụng một trong các công cụ để giả lập: VirutualBox (Miễn phí)

Download file iso để cài đặt.

<img width="1920" height="1080" alt="Screenshot 2026-04-12 224502" src="https://github.com/user-attachments/assets/7ae8950a-d8f9-4b04-992f-cd4b17e8ebd9" />


Cấu hình mạng trong Ubuntu (và công cụ giả lập) để cho phép truy cập SSH vào Ubuntu từ cmd của windows

Để ssh tới ubuntu ở ip 192.168.100.123, user là admin thì mở CMD trên windows,

Gõ lệnh: ssh admin@192.168.100.123

Hệ thống sẽ yêu cầu nhập password (chú ý : password sẽ không hiện ra)

Sau khi login thành công sẽ thấy màn hình chào hỏi của ubuntu

<img width="744" height="526" alt="image" src="https://github.com/user-attachments/assets/bf59437a-ac33-40b9-b9ac-22c4dcba5583" />


3. Tìm hiểu các lệnh cơ bản của ubuntu

Liệt kê các file trong thư mục: ls

<img width="1106" height="640" alt="Screenshot 2026-04-12 232607" src="https://github.com/user-attachments/assets/12547bc5-70f3-465c-9762-0c4fd28d5cbb" />


Tạo thư mục: mkdir nameFolder

<img width="1106" height="640" alt="Screenshot 2026-04-12 232607" src="https://github.com/user-attachments/assets/b835c4b2-3d5b-4748-aefc-4542c5345f7e" />


Chuyển thư mục làm việc: cd path

<img width="1119" height="647" alt="Screenshot 2026-04-12 232943" src="https://github.com/user-attachments/assets/50bb145d-0cb8-42ba-a90c-2f26cf1a38c4" />


Copy file: cp file_nguồn path/file_đích

<img width="1119" height="647" alt="Screenshot 2026-04-12 232943" src="https://github.com/user-attachments/assets/89491b0c-8632-4da4-961d-ad90a9ce1c94" />


Thay đổi quyền thao tác file: sudo chmod xxx filename

<img width="1102" height="635" alt="Screenshot 2026-04-12 233246" src="https://github.com/user-attachments/assets/c3e80d9f-4cd9-4f24-874a-3e20ae51b183" />


Edit file: sudo nano tenfile

CTRL+o : lưu nội dung sau khi edit

CTRL+x : thoát edit file

<img width="1101" height="638" alt="Screenshot 2026-04-12 232412" src="https://github.com/user-attachments/assets/dd097e26-f28d-423e-b05e-668aff779900" />

Xem ip của máy ubuntu: ip -4 addr

<img width="1006" height="268" alt="image" src="https://github.com/user-attachments/assets/20a551e2-b64d-4bdd-8fb3-4665c37f9c24" />


4. Cài đặt docker cho Ubuntu

4.1 Kiểm tra phiên bản docker vừa cài đặt, kiểm tra phiên bản của docker compose

<img width="584" height="119" alt="image" src="https://github.com/user-attachments/assets/491c350f-3254-40ed-9313-490324804a48" />


4.2 Cấu hình để docker chạy mà không cần tiền tố sudo

<img width="729" height="132" alt="Screenshot 2026-04-13 133404" src="https://github.com/user-attachments/assets/460b0db1-0065-48ae-9900-1489806b9492" />

5. Tìm hiểu tập lệnh của docker và docker compose:

5.1. Các tập lệnh thường dùng trong docker:

Tải một image từ Docker Hub: docker pull nginx

Chạy một container mới từ image (chạy ngầm, mở cổng 80): docker run -d -p 80:80 --name web-server nginx

Liệt kê các container đang chạy: docker ps

Liệt kê tất cả container (cả đang chạy và đã dừng): docker ps -a

Dừng một container: docker stop web-server

Xóa một container: docker rm web-server

Xem danh sách các image đang có trên máy: docker images

5.2. Tập lệnh docker conpose:

Khởi chạy các dịch vụ được định nghĩa trong file docker-compose.yml (chạy ngầm): docker compose up -d

<img width="1692" height="158" alt="Screenshot 2026-04-13 153036" src="https://github.com/user-attachments/assets/bb799151-7f19-4bdb-8933-7d759a97658a" />

Dừng và xóa các container trong file compose: docker compose down

<img width="658" height="158" alt="image" src="https://github.com/user-attachments/assets/9ad027bb-7621-441b-92cf-96c3aa830f02" />

Xem log hoạt động của các container: docker compose logs -f

<img width="1106" height="554" alt="Screenshot 2026-04-13 143437" src="https://github.com/user-attachments/assets/9aa7f2d3-9f2d-46a5-bccb-742213631186" />

Khởi động lại các dịch vụ: docker compose restart

<img width="849" height="139" alt="image" src="https://github.com/user-attachments/assets/cdb46d4f-45fb-41ad-a41b-95591021f230" />

5.3. Cấu hình tường lửa( UFW):

Cho phép kết nối SSH (Cực kỳ quan trọng để không bị mất kết nối): sudo ufw allow 22/tcp

Cho phép cổng 80 (Web): sudo ufw allow 80/tcp

Cho phép cổng 1880 (Node-RED): sudo ufw allow 1880/tcp

Cho phép cổng 9630: sudo ufw allow 9630/tcp

Kích hoạt tường lửa (Chọn 'y' khi được hỏi): sudo ufw enable

Kiểm tra trạng thái các cổng đã mở: sudo ufw status

<img width="1115" height="499" alt="Screenshot 2026-04-13 143639" src="https://github.com/user-attachments/assets/f9928d30-d44b-4bb6-a142-c3843998d2c9" />

