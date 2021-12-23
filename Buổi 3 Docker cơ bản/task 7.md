## Task 7 yêu cầu
• Tạo một docker network có tên là todo-app
• Chạy container PostgreSQL
• Chạy container cho ứng dụng ToDo App
• Kiểm tra kết quả

### 1. Tạo một docker network có tên là todo-app
```sh
docker network create -d bridge todo-app
```
### 2. Chạy container PostgreSQL
```sh
• Chạy ngầm
• Tên của container là postgresql
• Đặt trong network todo-app
• Mount thư mục /var/lib/postgresql/data của container ra một thư mục bất kỳ trên máy host
• Đặt giá trị cho biến môi trường POSTGRES_USER là postgres
• Đặt giá trị cho biến môi trường POSTGRES_PASSWORD là root123
• Đặt giá trị cho biến môi trường POSTGRES_DB là registry
• Sử dụng image là thuongnn1997/todo-app-db:latest
```
- Câu lệnh:
```sh
docker run -d --name postgresql \
--net=todo-app \ 
-v /home/cuongit/docker-practice/Buoi3-Task7/data:/var/lib/postgresql/data \
-e POSTGRES_USER=postgres \
-e POSTGRES_PASSWORD=root123 \
-e POSTGRES_DB=registry \
thuongnn1997/todo-app-db:latest
```
### 3. Chạy container cho ứng dụng Golang
```sh
• Chạy ngầm
• Đặt trong network todo-app
• Expose cổng 8080 của container ra cổng 8081 trên máy host
• Sử dụng image là thuongnn1997/todo-app:latest
```
- Câu lệnh:
```sh
docker run -d --name golang \
--net=todo-app \
-p 8081:8080 \
thuongnn1997/todo-app:latest
```

Địa chỉ kiểm tra: `http://45.76.186.96:8081/`