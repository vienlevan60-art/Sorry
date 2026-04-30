📌 Tổng quan (Overview)
Dự án này là một hệ thống CLI được xây dựng bằng Golang, thiết kế theo mô hình đa thành phần bao gồm server, client và agent.
Hệ thống được phát triển nhằm mô phỏng và triển khai một pipeline giao tiếp hoàn chỉnh qua HTTP/HTTPS, kết hợp với cơ chế thực thi lệnh có kiểm soát và quản lý phiên (session) theo thời gian thực.
Thay vì sử dụng các framework có sẵn, toàn bộ logic được xây dựng từ đầu nhằm kiểm soát chi tiết luồng dữ liệu, cách các thành phần tương tác và cách hệ thống vận hành ở mức thấp.
⚙️ Kiến trúc hệ thống
Hệ thống bao gồm 3 thành phần chính:
Server (C2 Core)
Đóng vai trò trung tâm, chịu trách nhiệm:
Tiếp nhận kết nối từ client/agent
Quản lý session
Phân phối lệnh và nhận kết quả
Client (Operator CLI)
Giao diện dòng lệnh cho người vận hành:
Liệt kê session đang hoạt động
Gửi lệnh thực thi
Nhận và hiển thị kết quả
Agent (Implant)
Thành phần thực thi:
Kết nối về server
Nhận lệnh từ server
Thực thi và trả kết quả
🚀 Tính năng nổi bật (Key Features)
Thiết kế kiến trúc client-server đa tầng, tách biệt rõ vai trò
Giao tiếp qua HTTP/HTTPS với khả năng cấu hình TLS
Quản lý session theo thời gian thực (tracking, trạng thái kết nối)
Cơ chế gửi lệnh và nhận phản hồi theo mô hình bất đồng bộ
Tích hợp mã hóa dữ liệu (AES, RSA) cho luồng giao tiếp
CLI interface tối giản nhưng linh hoạt cho thao tác điều khiển
Xử lý lỗi runtime và tình huống mạng (timeout, port conflict, reconnect)
🧠 Phạm vi kỹ thuật (Technical Scope)
Dự án tập trung vào các khía cạnh kỹ thuật sau:
Networking
TCP/IP
HTTP/HTTPS
TLS handshake và cấu hình cipher
System Interaction
Thực thi lệnh hệ điều hành
Quản lý process và output
Cryptography
Mã hóa bất đối xứng (RSA)
Mã hóa đối xứng (AES-GCM)
Encoding/decoding dữ liệu
Concurrency & Runtime
Goroutines
Channel xử lý bất đồng bộ
Quản lý trạng thái và đồng bộ dữ liệu
Error Handling & Debugging
Xử lý lỗi mạng
Debug xung đột port
Kiểm soát lifecycle của service
🔧 Hướng tiếp cận (Approach)
Dự án được xây dựng theo hướng “from scratch”, tập trung vào:
Hiểu rõ cách dữ liệu di chuyển giữa các thành phần
Kiểm soát chi tiết từng bước trong pipeline giao tiếp
Chủ động xử lý lỗi thay vì phụ thuộc vào abstraction có sẵn
Cách tiếp cận này giúp làm rõ cách một hệ thống thực tế vận hành thay vì chỉ sử dụng công cụ có sẵn.
📊 Ghi chú triển khai
Server hoạt động trên các cổng cấu hình (ví dụ: API và HTTPS listener riêng biệt)
Có thể gặp các vấn đề thực tế như:
xung đột port
timeout kết nối
trạng thái session không đồng bộ
→ Các vấn đề này được xử lý trực tiếp trong quá trình phát triển để đảm bảo tính ổn định.
⚠️ Lưu ý
Dự án này mang tính chất nghiên cứu kỹ thuật và thiết kế hệ thống.
Mục tiêu chính là hiểu rõ cơ chế hoạt động nội tại của các hệ thống giao tiếp và điều khiển từ xa ở mức thấp.
