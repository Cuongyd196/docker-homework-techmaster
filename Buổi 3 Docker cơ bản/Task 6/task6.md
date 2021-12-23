## Task 6. Viết các lệnh docker thực hiện yêu cầu:

- Tạo 1 docker network có tên là my-app:
    ```sh
    $ docker network create -d bridge  my-app
    ```
-  Chạy 1 nginx container có tên là my-nginx, chạy ngầm và đặt trong network my-app:
    ```sh
    $ docker run --name my-nginx --net=my-app -d nginx:latest
    ```
-  Chạy 1 container sử dụng image jwilder/whoami,tên container là hello-whoami, chạy ngầm và cũng đặt trong network my-app:
    ```sh
    $ docker run --name hello-whoami --net=my-app -d jwilder/whoami
    ```
- Docker exec vào 2 container my-nginx và hello-whoami, sau đó tiến hành cài 2 gói package ping và curl (nếu chưa có)
  - Truy cập vào container my-nginx:
   ```sh
   $ docker exec -it my-nginx bash
   ```
  - Nếu chưa có package ping và curl thì cài đặt
  ```sh
  $ apt-get update
  $ apt-get install iputils-ping
   ```


-  Truy cập vào container hello-whoami
      ```sh
      $ docker exec -it hello-whoami sh
      ```

- Nếu chưa có package ping và curl thì cài đặt:
  - Cập nhật apk:
   ```sh
   $ apk update
   ```
  -  Áp dụng tất cả các bản cập nhật bảo mật đang chờ xử lý trên Alpine Linux:
   ```sh
   $ apk upgrade
   ```
  - Tìm kiếm các curl packages trong Alpine:
  ```sh
  $ apk search curl
  ```
  - Liệt kê thông tin các gói có tên là curl
  ```sh
  $ apk -a info curl
  ```
  - Tiến hành cài đặt
  ```sh
  $ apk add curl
  ```
- Từ bên trong container my-nginx, lần lượt chạy 2 lệnh: ping hello-whoami và curl hellowhoami:8000. Kiểm tra kết quả.
    ```sh
    $ ping hello-whoami
    $ curl hello-whoami:8000 
    ```
- Từ bên trong container hello-whoami, lần lượt chạy 2 lệnh: ping my-nginx và curl mynginx:80. Kiểm tra kết quả.
    ```sh
    $ ping my-nginx
    $ curl mynginx:80
    ```
#### => Kết quả cho thấy container ở trong cùng 1 mạng thì có thể kết nối tới nha bằng tên container.