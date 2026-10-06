# Bài 2: Cấu hình phân quyền nhóm và sudoers bằng visudo

## 1. Tạo nhóm và user
(dán lệnh groupadd, adduser, usermod và đầu ra của `id deployer`)

## 2. Cấu hình sudoers
Mở bằng `sudo visudo`, dòng đã thêm:
```
%devops-admin ALL=(ALL) NOPASSWD: /usr/bin/systemctl start *, /usr/bin/systemctl stop *, /usr/bin/systemctl restart *, /usr/bin/systemctl status *
```
Kết quả `sudo visudo -c`: (dán đầu ra thật)

## 3. Kiểm tra với user deployer
(dán đầu ra thật của `sudo -l`)
(dán kết quả `sudo systemctl restart cron`, không hỏi mật khẩu)
(dán kết quả `sudo -n whoami`, bị từ chối vì ngoài phạm vi cho phép)

## 4. Giải thích
- `%devops-admin`: áp dụng cho mọi thành viên của nhóm.
- `NOPASSWD`: chạy các lệnh được liệt kê mà không cần nhập mật khẩu.
- Chỉ liệt kê 4 hành động của systemctl nên không cấp toàn quyền root (nguyên tắc đặc quyền tối thiểu).
- Dùng đường dẫn tuyệt đối để tránh bị giả mạo lệnh qua PATH.
