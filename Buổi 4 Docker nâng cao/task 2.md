## Task 2. Viết các lệnh docker thực hiện yêu cầu:
- Yêu cầu
```sh
Cho source code của 1 ứng dụng React tại địa chỉ
https://github.com/ahfarmer/calculator
Thực hiện các bước sau
• Clone source code về máy
• Bên trong thư mục chứa source code, viết file Dockerfile
• Build ra Docker image
• Chạy thử Docker image, expose cổng 3000 ra cổng 8080 trên máy host
```
```sh
Sử dụng base image node:12-alpine
• Copy các file package.json và package-lock.json từ host vào base image
• Chạy lệnh npm install để download các thư viện dependencies
• Copy toàn bộ file và thư mục từ host vào image
• Viết lệnh CMD (tham khảo source code trên Github lệnh để chạy ứng dụng)
    ```