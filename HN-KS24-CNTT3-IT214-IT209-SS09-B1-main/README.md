# Bài 2: Khởi chạy Nginx Web Server với Port Mapping

## 1. Mục tiêu

- Khởi chạy Nginx bằng Docker với image `nginx:alpine`.
- Đặt tên container là `my-web`.
- Ánh xạ cổng `8080` trên máy host tới cổng `80` bên trong container.
- Kiểm tra phản hồi HTTP bằng `curl`.
- Dừng và xóa container sau khi thử nghiệm.

## 2. Khởi chạy container

Chạy lệnh:

```bash
docker run -d -p 8080:80 --name my-web nginx:alpine
```

Ý nghĩa các tham số:

- `-d`: Chạy container ở chế độ nền.
- `-p 8080:80`: Ánh xạ cổng `8080` của máy host tới cổng `80` trong container.
- `--name my-web`: Đặt tên container là `my-web`.
- `nginx:alpine`: Image Nginx dựa trên Alpine Linux.

## 3. Kiểm tra container

Chạy:

```bash
docker ps
```

Kiểm tra container `my-web` có trạng thái đang chạy và cột `PORTS` thể hiện ánh xạ cổng `8080` tới `80/tcp`.

**Kết quả thực tế:** Container `my-web` đã chạy với image `nginx:alpine` và port mapping `8080:80`.

### Ảnh minh chứng 1: Container đang chạy

Nếu đã lưu ảnh chụp tại `screenshots/01-container-running.png`, ảnh sẽ hiển thị bên dưới.

![Container my-web đang chạy với port mapping 8080:80](screenshots/01-container-running.png)

## 4. Kiểm tra phản hồi HTTP

Chạy lệnh:

```bash
curl -i http://localhost:8080
```

**Kết quả thực tế:** Máy chủ trả về mã trạng thái `HTTP/1.1 200 OK` cùng HTML của trang Nginx mặc định, có tiêu đề `Welcome to nginx!`.

Có thể mở trình duyệt tại địa chỉ:

<http://localhost:8080>

### Ảnh minh chứng 2: Phản hồi của Nginx

Nếu đã lưu ảnh chụp tại `screenshots/02-nginx-response.png`, ảnh sẽ hiển thị bên dưới.

![Nginx trả về HTTP 200 OK](screenshots/02-nginx-response.png)

## 5. Dừng và xóa container

Sau khi kiểm tra xong, chạy:

```bash
docker stop my-web
docker rm my-web
```

Hoặc gộp hai lệnh:

```bash
docker stop my-web && docker rm my-web
```

Kiểm tra lại danh sách container:

```bash
docker ps -a
```

Container `my-web` sẽ không còn xuất hiện sau khi được xóa. Thao tác này không xóa các container khác đang chạy trên máy.

### Ảnh minh chứng 3: Dọn dẹp container

Nếu đã lưu ảnh chụp tại `screenshots/03-container-cleanup.png`, ảnh sẽ hiển thị bên dưới.

![Kiểm tra sau khi xóa container my-web](screenshots/03-container-cleanup.png)

## 6. Kết luận

Đã khởi chạy thành công Nginx bằng Docker, cấu hình port mapping từ cổng `8080` của máy host tới cổng `80` của container, xác nhận phản hồi HTTP `200 OK` và thực hiện dọn dẹp container sau khi thử nghiệm.

## 7. Cấu trúc thư mục nộp bài

```text
homework/
└── session_09/
    └── ex2/
        ├── README.md
        └── screenshots/
            ├── 01-container-running.png, nginx-response.png.
            └── 02-container-cleanup.png
```

> Lưu ý: Các ảnh minh chứng là phần bổ sung. Nếu chưa chụp ảnh, hãy chụp kết quả thực tế và lưu đúng tên, đúng vị trí như cấu trúc trên; nếu đề chỉ yêu cầu `README.md`, có thể bỏ thư mục `screenshots`.
