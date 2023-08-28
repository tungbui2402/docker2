# Docker
## Docker là gì?
Docker là nền tảng cung cấp cho các công cụ, service để các developers, adminsystems có thể phát triển, thực thi, chạy các ứng dụng với containers. Hay nói một cách khác nó là một nền tảng để cung cấp cách để building, deploy và run các ứng dụng một cách dễ dàng trên nền tảng ảo hóa - "Build once, run anywhere". Hay nói một cách dễ hiểu như sau: Khi chúng ta muốn chạy app thì chúng ta phải thiết lập môi trường chạy cho nó. Thay vì chúng ta sẽ đi cài môi trường chạy cho nó thì chúng ta sẽ chạy docker.

Ứng dụng Docker chạy trong vùng chứa (container) có thể được sử dụng trên bất kỳ hệ thống nào: máy tính xách tay của nhà phát triển, hệ thống trên cơ sở hoặc trong hệ thống đám mây. Và là một công cụ tạo môi trường được "đóng gói" (còn gọi là Container) trên máy tính mà không làm tác động tới môi trường hiện tại của máy, môi trường trong Docker sẽ chạy độc lập.

Docker có thể làm việc trên nhiều nền tảng như Linux, Microsoft Windows và Apple OS X.
## Lợi ích của Docker
- Không như máy ảo Docker start và stop chỉ trong vài giây.
- Có thể khởi chạy container trên mỗi hệ thống mà bạn muốn.
- Container có thể build và loại bỏ nhanh hơn máy ảo.
- Dễ dàng thiết lập môi trường làm việc. Chỉ cần config 1 lần duy nhất và không bao giờ phải cài đặt lại các dependencies. Nếu thay đổi máy hoặc có người mới tham gia vào project thì chỉ cần lấy config đó và đưa cho họ.
- Nó giữ cho word-space sạch sẽ hơn khi xóa môi trường mà ảnh hưởng đến các phần khác.
## Cách thức hoạt động của Docker
Một hệ thống Docker được thực thi với 3 bước chính :

`BUILD -> PUSH -> PULL,RUN`

Build: Đầu tiên tạo một dockerfile, trong dockerfile này chính là code của chúng ta. Dockerfile này sẽ được Build tại một máy tính đã cài đặt Docker Engine. Sau khi build ta sẽ có được Container, trong Container này chứa ứng dụng kèm bộ thư viện của chúng ta.

Push: Sau khi có được Container, chúng ta thực hiện push Container này lên cloud và lưu tại đó.

Pull, Run: Nếu một máy tính khác muốn sử dụng Container chúng ta thì bắt buộc máy phải thực hiện việc Pull container này về máy, tất nhiên máy này cũng phải cài Docker Engine. Sau đó thực hiện Run Container này.

## Các thành phần cơ bản của Docker
### 1. Docker Engine
Docker engine là một ứng dụng client-server. có 2 phiên bản phổ biến:

Docker Community Edition (CE): Là phiên bản miễn phí và chủ yếu dựa vào các sản phầm nguồn mở khác.

Docker Enterprise(EE): Khi sử dụng phiên bản này sẽ nhận được sự support của nhà phát hành, có thêm các tính năng quản lý và security.

Các thành phần chính của docker engine gồm có:

Server hay còn được gọi là docker daemon: chịu trách nhiệm tạo, quản lý các Docker objects như images, containers, networks, volume.

REST API: docker daemon cung cấp các api cho Client sử dụng để thao tác với Docker

Client là thành phần đầu cuối cung cấp một tập hợp các câu lệnh sử dụng api để người dùng thao tác với Docker.

### 2. Distribution tools
Là các công cụ phân tán giúp chúng ta lưu trữ và quản lý các Docker Images như: Docker Registry, Docker Trusted Registry, Docker Hub

Docker Hub là một công cụ phần mềm như một dịch vụ cho phép người dùng public hay private các images của chúng ta. Dịch vụ cung cấp hơn 100.000 ứng dụng có sẵn công khai, cũng như các cơ quan đăng ký container công cộng và tư nhân.

### 3. Orchestration tools
Docker Machine : Machine tạo Docker Engine trên laptop của bạn hoặc trên bất cứ dịch vụ cloud phổ biến nào như AWS, Azure, Google Cloud, Softlayer hoặc trên hệ thống data center như VMware, OpenStack. Docker Machine sẽ tạo các máy ảo và cài Docker Engine lên chúng và cuối cùng nó sẽ cấu hình Docker Client để giao tiếp với Docker Engine một cách bảo mật

Docker Compose : là công cụ giúp định nghĩa và khởi chạy multi-container Docker applications

Docker Swarm : là một công cụ giúp chúng ta tạo ra một clustering Docker. Nó giúp chúng ta gom nhiều Docker Engine lại với nhau và ta có thể "nhìn" nó như duy nhất một virtual Docker Engine.

### 4. Một số thành phần khác
Dockerfile : như một script dùng để build các image trong container. Dockerfile bao gồm các câu lệnh liên tiếp nhau được thực hiện tự động trên một image gốc để tạo ra một image mới. Dockerfile giúp đơn giản hóa tiến trình từ lúc bắt đầu đến khi kết thúc

Docker Toolbox : Bởi vì Docker Engine dùng một số feature của kernel Linux nên ta sẽ không thể chạy Docker Engine natively trên Windows hoặc BSD được. Ở các phiên bản trước đây thì ta sẽ cần một máy ảo cài một phiên bản Linux nào đó và sau đó cài Docker Engine lên máy ảo đó.

## Kiến trúc của Docker
Docker Daemon: lắng nghe các yêu cầu từ Docker Client để quản lý các đối tượng như Container, Image, Network và Volumes. Các Docker Daemon cũng giao tiếp với nhau để quản lý các Docker Service.

Docker Client: là một công cụ giúp người dùng giao tiếp với Docker host. Khi người dùng gõ lệnh `docker run image ABC` tức là người dùng sử dụng CLI và gửi request đến dockerd thông qua api, và sau đó Docker daemon sẽ xử lý tiếp. Docker client có thể giao tiếp và gửi request đến nhiều Docker daemon.

Docker Registry (Docker Hub): là một kho chứa các image được publish bởi cộng đồng Docker. Nó giống như GitHub và có thể tìm những image cần thiết và pull về sử dụng.

Docker object: chính là các đối tượng mà ta thường xuyên gặp khi sử dụng Docker. Gồm có Images và Containers .

Images: hiểu nôm na là một khuôn mẫu để tạo một container. Thường thì image sẽ base trên 1 image khác với những tùy chỉnh thêm. ví dụ bạn build 1 image dựa trên image ubuntu để chạy Apache web service và ứng dụng của bạn và những tùy chỉnh, cấu hình để ứng dụng của bạn có thể chạy được. Bạn có thể tự build một image riêng cho mình hoặc sử dụng những image được publish từ cộng đồng Docker Hub. Một image sẽ được build dựa trên những chỉ dẫn của Dockerfile.

Containers: là một instance của một image. Bạn có thể create, start, stop, move or delete container dựa trên Docker API hoặc Docker CLI.

### Sự khác biệt giữa Docker Images và Docker Containers

Docker Images: Là một template chỉ cho phép đọc, ví dụ một image có thể chứa hệ điều hành Ubuntu và web app. Images được dùng để tạo Docker container. Docker cho phép chúng ta build và cập nhật các image có sẵn một cách cơ bản nhất, hoặc có thể download Docker images của người khác.

Docker Containers: Docker container có nét giống với các directory. Một Docker container giữ mọi thứ chúng ta cần để chạy một app. Mỗi container được tạo từ Docker image. Docker container có thể có các trạng thái run, started, stopped, moved và deleted.

## Cài đặt
B1: Cập nhật hệ thống:
```
sudo apt-get update
sudo apt-get upgrade
```
B2: Cài gói dịch vụ cần thiết
```
sudo apt-get install curl apt-transport-https ca-certificates software-properties-common
```
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
- Sau khi cài đặt, cấp quyền cho user hiện tại thuộc group docker, để khi gõ lệnh không cần xin quyền sudo: `sudo usermod -aG docker $(whoami)`
- Logout sau đó login lại để có hiệu lực.
- Ngoài ra khi sử dụng đến thành phần docker-compose thì cài thêm: `sudo apt install docker-compose`
## Sử dụng docker:
![Screenshot (50)](https://github.com/tungbui2402/docker2/assets/129025623/f76232d1-c1ad-45d0-8210-70bc555432e9)

## Dockerfile
Dockerfile là một file dạng text, không có đuôi, giúp thiết lập cấu trúc cho docker image nhờ chứa một tập hợp các câu lệnh. Dockerfile giúp đơn giản hóa tiến trình từ lúc bắt đầu đến khi kết thúc.



## So sánh giữa docker và vm
Sự khác biệt giữa Docker và Virtual Machine

Docker : Dùng chung kernel, chạy độc lập trên Host Operating System và có thể chạy trên bất kì hệ điều hành nào cũng như cloud. Khởi động và làm cho ứng dụng sẵn sàng chạy trong 500ms, mang lại tính khả thi cao cho những dự án cần sự mở rộng nhanh.

Virtual Machine : Cần thêm một Guest OS cho nên sẽ tốn tài nguyên hơn và làm chậm máy thật khi sử dụng. Thời gian khởi động trung bình là 20s có thể lên đến hàng phút, thay đổi phụ thuộc vào tốc độ của ổ đĩa
