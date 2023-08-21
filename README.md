# Docker
## I. Docker là gì?
Docker là một nền tảng cho developers và sysadmin để develop, deploy và run application với container. Nó cho phép tạo các môi trường độc lập và tách biệt để khởi chạy và phát triển ứng dụng và môi trường này được gọi là container. Khi cần deploy lên bất kỳ server nào chỉ cần run container của Docker thì application sẽ được khởi chạy ngay lập tức.
## II. Lợi ích của Docker
- Không như máy ảo Docker start và stop chỉ trong vài giây.
- Có thể khởi chạy container trên mỗi hệ thống mà bạn muốn.
- Container có thể build và loại bỏ nhanh hơn máy ảo.
- Dễ dàng thiết lập môi trường làm việc. Chỉ cần config 1 lần duy nhất và không bao giờ phải cài đặt lại các dependencies. Nếu bạn thay đổi máy hoặc có người mới tham gia vào project thì bạn chỉ cần lấy config đó và đưa cho họ.
- Nó giữ cho word-space của bạn sạch sẽ hơn khi bạn xóa môi trường mà ảnh hưởng đến các phần khác.
## III. Cách thức hoạt động của Docker
Docker hoạt động bằng cách cung cấp phương thức tiêu chuẩn để chạy mã. Docker là hệ điều hành dành cho container. Cũng tương tự như cách máy ảo ảo hóa (loại bỏ nhu cầu quản lý trực tiếp) phần cứng máy chủ, các container sẽ ảo hóa hệ điều hành của máy chủ. Docker được cài đặt trên từng máy chủ và cung cấp các lệnh đơn giản mà bạn có thể sử dụng để dựng, khởi động hoặc dừng container.
## IV. Lý do nên sử dụng Docker
Việc sử dụng Docker cho phép vận chuyển mã nhanh hơn, tiêu chuẩn hóa hoạt động của ứng dụng, di chuyển mã một cách trơn tru và tiết kiệm tiền bằng cách cải thiện khả năng tận dụng tài nguyên. Với Docker, bạn sẽ được nhận một đối tượng duy nhất có khả năng chạy ổn định ở bất kỳ đâu. Cú pháp đơn giản và không phức tạp của Docker sẽ cho bạn quyền kiểm soát hoàn toàn. Việc đưa vào áp dụng rộng rãi nền tảng này đã tạo ra một hệ sinh thái bền vững các công cụ và ứng dụng có thể sử dụng ngay đã sẵn sàng sử dụng với Docker.
## V. Cài đặt
B1: Cập nhật hệ thống:
```
sudo apt-get update
sudo apt-get upgrade
```
B2: Cài gói dịch vụ cần thiết
```
sudo apt-get install curl apt-transport-https ca-certificates software-properties-common
```
Trong đó:
- apt-transport-https – giúp package manager chuyển file và data qua https
- ca-certificates – giúp web browser và hệ thống kiểm tra certificate bảo mật
- curl – chuyển data
- software-properties-common – thêm script để quản lý software

B3: Chèn key GPG
```
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
sudo apt update
```
- Kiểm tra bằng lệnh sau: `apt-cache policy docker-ce`
Output:
```
docker-ce:
   Installed: (none)
   Candidate: 16.04.1~ce~4-0~ubuntu
   Version table:
       16.04.1~ce~4-0~ubuntu 500
            500 https://download.docker.com/linux/ubuntubionic/stableamd64packages
```

B4: Cài đặt docker
```
sudo apt-get install docker-ce
```
- Sau khi cài đặt, bạn có thể cho user hiện tại thuộc group docker, để khi gõ lệnh không cần xin quyền sudo: `sudo usermod -aG docker $(whoami)`
- Logout sau đó login lại để có hiệu lực.
- Ngoài ra khi sử dụng đến thành phần docker-compose thì cài thêm: `sudo apt install docker-compose`
## VI. Sử dụng docker:
### 1. Tải về 1 image
```
sudo docker pull [name_image]:[tag]
```
### 2. Xóa đi 1 image
Có thể dùng 1 trong 2:
```
sudo docker rm [name_image]:[tag]
sudo docker rm [image_id]
```
- Lưu ý: Khi image chạy, các phiên bản thực thi của image là các container (1 image có thể tạo nhiều container)

### 3. Khởi tạo và chạy 1 image
```
docker run [param] IMAGE command [param_command]
```
### 4. Xem những container đang chạy
```
docker ps
```
### 5. Để xem tất cả những container
```
docker ps -a
```
### 6. Để tắt container
Trong terminal của container: `exit`
Trong cửa sổ terminal khác: `docker stop [container_ID]`
Để đóng cửa sổ terminal của container nhưng container vẫn chạy: `Ctrl + P + Q`

### 7. Khởi chạy lại những container đã tắt
```
docker start [container_ID]
```
### 8. Để xóa container
```
docker rm [container_ID]
```
- Khi container đang chạy mà vẫn muốn xóa: `docker rm -f [container_ID]`
### 9. Danh sách images
```
docker images
```
## VII. So sánh giữa docker và vm
### 1. Giống:
Là công nghệ ảo hóa, Docker và máy ảo (VM) có những điểm tương đồng nhất định.
- Hình ảnh: Các bộ chứa Docker và máy ảo đều được tạo từ hình ảnh. Mỗi hình ảnh đóng vai trò như một kế hoạch chi tiết của môi trường ảo hóa. Hình ảnh cho phép người dùng tạo và chia sẻ môi trường nhất quán mà không cần phải định cấu hình từng lần một.
- Versioning: Cả hình ảnh bộ chứa Docker và hình ảnh máy ảo đều có thể được lập phiên bản để theo dõi các thay đổi cấu hình môi trường theo thời gian.
- Tính di động: Cả máy ảo và Docker đều được thiết kế để giải quyết những khó khăn khi phải phát triển các cấu hình ứng dụng khác nhau cho các loại kiến trúc cơ sở khác nhau. Mặc dù chúng có các cách tiếp cận khác nhau đối với vấn đề, cả hình ảnh Docker và máy ảo đều có tính di động cao trên các kiến trúc, cho dù tại chỗ hay trên đám mây.
### 2. Khác:
|       TT       |      Máy ảo        | Docker container     |
| :-----------: |:-------------:| :----:|
|    1          |        Kích thước (dung lượng) lớn.      |  Kích thước (dung lượng) nhỏ.    |
|     2         |        Hiệu suất hạn chế.      |   Hiệu suất gốc (native).   |
|     3         | Mỗi máy ảo sẽ có một hệ điều hành riêng.             |    Container sẽ sử dụng hệ điều hành của host.  | 
|     4         | Ảo hóa về mặt phần cứng             |    Ảo hóa về mặt hệ điều hành  |
|     5         | Thời gian khởi động tính theo phút             |    Thời gian khởi động tính theo mili giây  |
|     6         | Phân bổ bộ nhớ theo nhu cầu cần thiết             |    Yêu cầu ít dung lượng bộ nhớ hơn  |
|     7         | Hoàn toàn bị cô lập và an toàn hơn             |    Cô lập ở mức tiến trình, có thể kém an toàn hơn  |
