Viết các lệnh docker thực hiện yêu cầu:

1. Tạo 1 docker network có tên là my-app
$ docker network create -d bridge  my-app

• Chạy 1 nginx container có tên là my-nginx, chạy ngầm và đặt trong network my-app
$ docker run --name my-nginx --net=my-app -d nginx:latest

• Chạy 1 container sử dụng image jwilder/whoami,tên container là hello-whoami, chạy ngầm và
cũng đặt trong network my-app.
$ docker run --name hello-whoami --net=my-app -d jwilder/whoami

• docker exec vào 2 container my-nginx và hello-whoami, sau đó tiến hành cài 2 gói package
ping và curl (nếu chưa có)
-  Truy cập vào container my-nginx

$ docker exec -it my-nginx bash
- Nếu chưa có package ping và curl thì cài đặt
$ apt-get update
$ apt-get install iputils-ping

-  Truy cập vào container hello-whoami
$ docker exec -it hello-whoami sh
- Nếu chưa có package ping và curl thì cài đặt:
+ Cập nhật apk:
$ apk update
+ Áp dụng tất cả các bản cập nhật bảo mật đang chờ xử lý trên Alpine Linux:
$ apk upgrade
+ Tìm kiếm các curl packages trong Alpine:
$ apk search curl
+ Liệt kê thông tin các gói có tên là curl
$ apk -a info curl
+ Tiến hành cài đặt
$ apk add curl

• Từ bên trong container my-nginx, lần lượt chạy 2 lệnh: ping hello-whoami và curl hellowhoami:8000. Kiểm tra kết quả.
$ ping hello-whoami
$ curl hello-whoami:8000 
• Từ bên trong container hello-whoami, lần lượt chạy 2 lệnh: ping my-nginx và curl mynginx:80. Kiểm tra kết quả.
$ ping my-nginx
$ curl mynginx:80

-> Kết quả cho thấy container ở trong cùng 1 mạng thì có thể kết nối tới nhau thông qua tên container.