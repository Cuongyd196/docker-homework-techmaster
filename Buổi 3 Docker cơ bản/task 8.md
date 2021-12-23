## Task 7. Triển khai trang web viết blog bằng Docker

### 1. Tạo một docker network có tên là ghost-network
```sh
docker network create -d bridge ghost-network
```
### 2. Chạy container PostgreSQL
```sh
• Chạy ngầm
• Tên của container là db
• Đặt trong network ghost-network
• Mount thư mục /var/lib/mysql của container sử dụng volume quản lý bởi docker
• Đặt giá trị cho biến môi trường MYSQL_ROOT_PASSWORD là example
• Sử dụng image là mysql:5.7
```
- Câu lệnh:
```sh
docker run -d --name db \
--net=ghost-network \
-v /home/cuongit/docker-practice/Buoi3-Task8/data:/var/lib/mysql \
-e MYSQL_ROOT_PASSWORD=example \
mysql:5.7
```
### 3. Chạy container Ghost blog
```sh
• Chạy ngầm
• Tên container: ghostblog
• Đặt trong network ghost-network
• Expose cổng 2368 của container ra cổng 80 trên máy host
• Thiết lập biến môi trường cho container:
• database__client = mysql
• database__connection__host = db
• database__connection__user = root
• database__connection__password = example
• database__connection__database = ghost
• Sử dụng image là ghost:alpine
```
- Câu lệnh:
```sh
docker run -d --name ghostblog \
--net=ghost-network \
-e database_client=mysql \
-e database_connection_host=db \
-e database_connection_user=root \
-e database_connection_password=example \
-e database_connection_database=ghost \
-p 80:2368 \
ghost:alpine
```
Địa chỉ kiểm tra: `http://45.76.186.96:80`

