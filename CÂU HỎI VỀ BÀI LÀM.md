1. Tại sao phải dùng Nginx làm Reverse Proxy mà không trỏ thẳng Tunnel vào Node-RED?
Dù bạn hoàn toàn có thể trỏ thẳng Tunnel vào Node-RED, nhưng trong môi trường thực tế (Production), Nginx đóng vai trò như một "Lễ tân kiêm Bảo vệ":

Phân luồng (Routing): Nginx giúp bạn chạy nhiều dịch vụ trên cùng một tên miền. Ví dụ: Khách vào / thì Nginx trả về file HTML (Giao diện), khách gọi /api/ thì Nginx mới chuyển yêu cầu (proxy_pass) cho Node-RED xử lý logic.

Hiệu năng: Nginx được thiết kế để phục vụ các file tĩnh (HTML, CSS, JS, hình ảnh) với tốc độ chớp nhoáng. Node-RED là một môi trường chạy logic (Node.js), nó không giỏi và không tối ưu trong việc host file tĩnh.

Bảo mật & Ẩn danh: Người dùng bên ngoài chỉ biết đến Nginx. Kiến trúc thực sự bên trong (như cổng 1880 của Node-RED) được giấu kín hoàn toàn.

2. Sự khác biệt giữa việc Mount file và Mount thư mục trong Docker?
Mount Thư mục (- ./myweb:/usr/share/nginx/html): Ánh xạ toàn bộ nội dung của một thư mục. Nếu bạn tạo thêm file mới, xóa file cũ ở máy Host (máy thật), thư mục bên trong container cũng cập nhật y hệt. Rất phù hợp để chứa source code web.

Mount File (- ./nginx.conf:/etc/nginx/nginx.conf): Chỉ ánh xạ duy nhất một file cụ thể, ghi đè lên file có sẵn trong container mà không làm ảnh hưởng đến các file khác nằm cùng thư mục đó bên trong container. Rất phù hợp để nạp file cấu hình.

3. Thay đổi file index.html ở máy Host, web có đổi ngay không?
Có, nội dung sẽ thay đổi ngay lập tức đối với container (vì cơ chế Bind Mount tạo ra một liên kết trực tiếp theo thời gian thực giữa máy host và container).

Lưu ý nhỏ: Trên góc độ người dùng (End-user), đôi khi họ phải bấm Ctrl + F5 hoặc xóa cache trình duyệt / cache Cloudflare thì mới thấy sự thay đổi, nhưng về mặt hệ thống máy chủ thì nó đã nhận ngay lập tức.

4. Lệnh restart: always và restart: unless-stopped để làm gì?
Đây là cơ chế tự phục hồi (High Availability) của Docker:

always: Docker sẽ LUÔN LUÔN tự động khởi động lại container này trong mọi trường hợp (server bị cúp điện bật lại, container bị crash do lỗi code, v.v.). Thậm chí nếu bạn tự tay gõ lệnh docker stop, lần tới khi Docker service khởi động, nó vẫn sẽ tự bật lại.

unless-stopped: Tương tự như always, nhưng thông minh hơn một chút. Nếu bạn tự tay gõ lệnh docker stop để chủ động tắt nó đi, thì dù server có khởi động lại, Docker cũng sẽ tôn trọng quyết định của bạn và không tự bật nó lên nữa.

5. Khai báo chung 1 network và lợi ích
Lợi ích: Các container nằm trong cùng một network nội bộ có thể "nhìn thấy" và giao tiếp với nhau bằng Tên dịch vụ (Service name) thay vì phải dùng địa chỉ IP. Giúp hệ thống an toàn (cô lập với bên ngoài) và code cấu hình không bao giờ bị lỗi khi IP thay đổi.

Cách cấu hình (Ví dụ):

YAML
services:
  nginx:
    networks:
      - my_app_net
  nodered:
    networks:
      - my_app_net

# Khai báo ở cuối file
networks:
  my_app_net:
    driver: bridge
6. Bảo mật Cloudflare Token với .env và .gitignore
Token của Tunnel chính là "Chìa khóa vạn năng" mở cửa thẳng vào mạng nội bộ của bạn.

Nếu bạn push trực tiếp đoạn mã eyJh... lên Github ở chế độ Public, các con bot quét mã độc có thể nhặt được nó trong vài giây. Kẻ gian có thể dùng token đó cấu hình một Tunnel trên máy họ, chiếm đoạt tên miền của bạn hoặc thâm nhập vào hệ thống ảo của bạn.

Giải pháp: Đưa token vào file .env (ví dụ: TUNNEL_TOKEN=eyJh...), trong docker-compose.yml gọi biến ${TUNNEL_TOKEN}. Cuối cùng, khai báo tên file .env vào trong file .gitignore. Git sẽ lờ file này đi và không bao giờ đẩy nó lên Internet.

7. Tại sao nên thêm hậu tố :ro (Read-only) khi mount file Nginx?
:ro viết tắt của Read-Only (Chỉ đọc). Ví dụ: - ./nginx.conf:/etc/nginx/nginx.conf:ro.
Bảo mật hệ thống luôn tuân theo nguyên tắc "Quyền hạn tối thiểu". Container Nginx chỉ cần ĐỌC file cấu hình để hoạt động, nó không có lý do gì để SỬA file đó. Thêm :ro giúp bảo vệ file gốc trên máy của bạn không bị thay đổi lỡ như container Nginx bị hacker tấn công chiếm quyền hoặc có lỗi phần mềm bên trong làm hỏng file.

8. Dùng Cloudflare Tunnel có cần mở cổng (Port mapping) nữa không?
Hoàn toàn KHÔNG! Đây chính là sức mạnh tuyệt đối của kiến trúc Zero Trust.

Không cần ánh xạ cổng ports: - "8080:80" (chúng ta chỉ dùng nó lúc nãy để debug nội bộ xem Nginx có sống hay không).

Không cần mở cổng (Port Forwarding) trên Modem Wi-Fi hay Firewall.

Cloudflare Tunnel hoạt động theo cơ chế Outbound Connection (Chủ động gọi từ trong máy tính của bạn ra ngoài Cloudflare). Do không có cổng nào được mở ra Internet, các hacker có dùng tool quét IP (Port Scanner) cũng sẽ thấy máy chủ của bạn "tàng hình" hoàn toàn.
