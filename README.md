# Bài 3: Cài đặt Nginx và cấu hình Website tĩnh cơ bản (Basic Nginx Web Server)

## Mục tiêu
Cài đặt Nginx, cấu hình Server Block lắng nghe cổng 80 và phục vụ trang tĩnh `index.html`.

## Các lệnh đã thực hiện trên máy chủ

### 1. Cài đặt Nginx
```bash
sudo apt update
sudo apt install nginx -y
```

### 2. Tạo thư mục chứa mã nguồn và file `index.html`
Tạo thư mục `ptit-web` theo yêu cầu:
```bash
sudo mkdir -p /var/www/ptit-web/html/
```

Thay đổi owner của thư mục cho user hiện tại (ví dụ `devops`) để có thể ghi file mà không cần sudo:
```bash
sudo chown -R $USER:$USER /var/www/ptit-web/html/
```

Tạo file `index.html` với nội dung yêu cầu (bạn có thể copy nội dung từ file `index.html` đính kèm trong thư mục này lên máy chủ):
```bash
nano /var/www/ptit-web/html/index.html
```

### 3. Tạo cấu hình Server Block (Virtual Host)
Tạo tệp cấu hình mới cho website:
```bash
sudo nano /etc/nginx/sites-available/ptit-web.conf
```
*(Copy nội dung file `ptit-web.conf` đính kèm vào trong nano rồi lưu lại)*

### 4. Kích hoạt Server Block mới và vô hiệu hóa cấu hình mặc định
Xóa (hoặc vô hiệu hóa) file cấu hình mặc định đang chiếm cổng 80 của Nginx:
```bash
sudo rm /etc/nginx/sites-enabled/default
```

Tạo một liên kết tượng trưng (symlink) từ thư mục `sites-available` sang `sites-enabled` để kích hoạt file cấu hình mới:
```bash
sudo ln -s /etc/nginx/sites-available/ptit-web.conf /etc/nginx/sites-enabled/
```

### 5. Kiểm tra và áp dụng cấu hình Nginx
Chạy lệnh kiểm tra cú pháp cấu hình Nginx, đảm bảo nó hiển thị `syntax is ok` và `test is successful`:
```bash
sudo nginx -t
```

Tải lại Nginx để áp dụng cấu hình:
```bash
sudo systemctl reload nginx
```

### 6. Truy cập website
Từ trình duyệt trên máy tính cá nhân, truy cập địa chỉ IP public của Droplet: `http://<IP_ADDRESS_DROPLET>`

> *Chèn ảnh chụp trình duyệt hiển thị giao diện trang web thành công vào đây:*
> 
> `[Chèn ảnh chụp Website tại đây]`
