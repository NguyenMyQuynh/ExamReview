<br>

# Tổng quan về ATTT:

- Bảo mật thông tin là đảm bảo `tính bí mật, tính toàn vẹn, tính sẵn sàng (CIA)` của thông tin trên các thiết bị lưu trữ, trong quá trình sử dụng và truyền thông.
  - Confidentiality: tinh bao mat, chỉ được phép truy cập bởi những đối tượng được cấp phép, đảm bảo rằng thông tin cá nhân hoặc bí mật không được cung cấp hoặc tiết lộ cho các cá nhân trái phép => mã hóa
  - Integrity: Đảm bảo tính toàn vẹn thông tin, Đảm bảo rằng thông tin (cả được lưu trữ và trong các gói được truyền đi) và các chương trình chỉ được thay bởi người so huu or ng có thẩm quyền và có thể truy vết đc ai sửa sửa những j và neu dl bị thdoi 1 cách trái phép thì chúng ta phải fat hiện đc => hash 
  - Availability: Đảm bảo dl luon o trang thai san sang khi ng so hưu or 1 ng nào đó muốn truy xuát vào để sd, Dam bao rằng hệ thống hoạt động kịp thời và dịch vụ không bị từ chối đối với người dùng có thẩm quyền. Load Balancing, dự phòng nguồn điện
  - Authenticity(Tính xác thực): bảo rằng thông tin là thật, được xác thực nguồn gốc của thông tin (thuốc sở hữu của đối tượng nào) để đảm bảo thông tin đến từ một nguồn đáng tin cậy. Authorization: Sau bước xac thuc danh tinh he thong cho phep truy cap tai Nguyen nhat dinh, xd mưc do thao tac of ng đc uy quyen tren dl.
  - Accountability (non-repudiation) - Tính chống thoái thác trách nhiệm: doi tuong thao tac trên dl thì phải chịu trách nhiejm tren dl đó => Dùng chữ kí số.

![image](https://user-images.githubusercontent.com/62002485/175187067-b1515a8a-b072-460a-9bb4-0998f796f1b2.png)
![image](https://user-images.githubusercontent.com/62002485/175187084-b5d8553c-93e5-4aaf-bae3-8bd26c7a3b9c.png)
![image](https://user-images.githubusercontent.com/62002485/175187094-cb6d6c54-8b15-4460-ae8a-bae043e6933d.png)

- Data: encryption, access control
- App: hashing 
- Host: enpoint security, IA
- Internal network: Internal FW, IDS/IPS, based-hot
- Perimeter: honey pot, external FW
- Physical: tất cả cá thiết bị phải được đặt trong data center đạt tiêu chuẩn 27001

![image](https://user-images.githubusercontent.com/62002485/175187177-d210ab24-49ff-439d-ab2e-2ab994f66631.png)
![image](https://user-images.githubusercontent.com/62002485/175187255-ebd8e75c-71f7-4cde-90c9-3fdf6c2737e3.png)


<br><br>


# Firewall

- Firewall hay còn được còn là Tường Lửa. Là thiết bị, ỏa hóa hay phần mềm bảo mật được sử dụng để quản lý luồng gói tin qua nó : cho phép (permit) hay cấm (deny). 
- Được đặt ở vị trí giao thương giữa các mạng với nhau, đặc biệt là mạng private và public. Trong mạng private, muốn bảo vệ vùng nào thì đặt firewall trước vùng đó.
- Antivirus khác gì FW?
  - Antivirus: nằm trên máy server, protect về file cho server, nếu tích hợp thêm IPS/IDS thì phân tích behaviour về mặt system, phát hiện đối tượng file run trên hệ thống có an toàn không.
  - Filewall có nhiều function: không nằm trên máy server, protect về Network Security cho server là chính, protect đc host(tính năng NAT, ẩn địa chỉ IP của server), cho phép thiết lập rule cho phép kiểm soát cho máy này ra internet ở những port nào, có thể tích hợp thêm AV, IDS/IPS


<br>

### Phân loại tường lửa:
- Appliances- Phần cứng: Thiết bị mạng (có hardware của thiết bị, có formware có hdh tối ưu hóa lại và install software firewall lên)
  - Checkpoint, Cisco ASA, Astaro, Cyberoam,…
- Software- Phần mềm : Ứng dụng bảo mật được cài trên
máy tính (Chúng ta phải có 1 con server vật lí RAM, CPU, cài hdh, cài software firewall lên và tiến hành sdung: cài các rules... ==> hdh chưa đc tối ưu hóa và khi xảy ra lỗi ở mức hdh thi ta phải tự xử lí)
  - ISA Server, IPCop, Smoothwall, Pfsense,…
- Virtual Appliances- Ảo hóa: nhà cung cấp sẽ cung cấp 1 file để ta import vào hạ tầng ảo hóa và nó sẽ bung ra cho chúng ta máy virtual client đã có hdh và phần mềm security và chúng ta chỉ cần bật máy lên và sử dụng
  - SOPHOS, Palo Alto,...

Cả Personal Firewall và Network Firewall
được chia làm 3 loại chính(tường lửa truyền thống):
- Simple Packet Filter Firewalls (Access control list layer3-netwwork)
- Stateful Packet Filter Firewalls (IP table layer4-transport)
- Application Level Firewalls (pfsense layer7-application)

<br>

### Simple Packet Filter Firewalls
Kiểm tra gói tin qua firewall bằng cách so sánh nó với
những nguyên tắc (Rule) đã được đặt ra, để quyết định
gói tin đó được cho phép hay bị từ chối. 
Những thông tin sẽ được kiểm tra:
- IP Nguồn
- IP Đích
- Giao thức
- Port Nguồn
- Port Đích

Hoạt động ở Layer 2 và Layer 3

Điểm yếu 
- Không thấy được sâu bên trong application work như thế nào (VD giao thức https chỉ thấy được traffic nhưng ko biết được port 443 chạy những application nào).
- Không hỗ trợ authentication, dễ bị giả mạo(Spoofing), không ngăn chặn ddos, tcp/ip.
- Ghi nhật ký hạn chế, log dạng text chứ không hiện lên darkbroad.
- Dễ định cấu hình sai

<br>

### Stateful Packet Filter Firewalls

Chức năng tương tự Simple Packet Filter nhưng có những khắc phục so với Simple Packet Filter Firewalls:  
  - Có stateful table lưu được trạng thái của gói tin đi trước ghi lại source nào yêu cầu destination nào, so sánh với gói đi sau nếu không phù hợp thì drop(VD: IP A request ip server C stateful table lưu lại, nếu ip attacker kết nối gửi response giả mạo cho ip A thì FW se drop gói tin).
  - Footprint được nên giảm được attack.
  - Ít giả mạo được hơn vì FW sẽ phát hiện IP Spoofing nhờ stateful table.
  - Cấu hình Black hole dễ dàng.
  - Chuyên sâu về tài nguyên ít hơn
  
Hoạt động ở Layer 2, 3, 4.

![image](https://user-images.githubusercontent.com/62002485/147690843-6c2c5f54-0fa8-446a-93e0-268cd48768cc.png)

- Simple: A communication với B cần thiết lập rule 2 chiều, còn Stateful chỉ cần  xét từ A đến B thì connection sẽ được cập nhật trong stateful table 

![image](https://user-images.githubusercontent.com/62002485/159025511-ec0d177f-ec4b-4b9c-803b-d351db3f33c8.png)


<br>

### Application Level Firewalls:
- Còn được gọi Application-Proxy Gateways.
- Hoạt động ở Layer 7
- Có khả năng xác thực :
  - UserID và Password(tích hợp được LDAP, active directory để xác thực user password)
  - Hardware hoặc Software Token(tích hợp VPN xác thực Token)
  - Source Address
  - Biometric: one time password - xác thực vân tay.
- Decryption SSL.
- Có khả năng điểu khiển truy cập từ Layer 2 đến Layer 7
- Deep Packet Inspection : kiểm tra chi tiết gói tin
nên có khả ngăn chặn các ứng dụng Instant
Message, Peer to Peer,... hiển thị các application đang chạy ở các port cụ thể, băng thông và người dùng.
==> Giám sát mạng chạy ntn, nhắc nhở ai đang sdung giao thức quá ngưỡng...
- Cơ chế Buffering: vd khi download gom tất cả các mẫu nhỏ và discapsulation thành 1 file và scan nó, nếu ok cho qua.


Ưu điểm:
- Khả năng ghi nhật ký mở rộng
- Thực thi xác thực
- Ít nhạy cảm hơn với các lỗ hổng TCP / IP
- Có khả năng tạo quy tắc ngăn cản gói tin đã mã hóa(file ko đọc được FW sẽ block luôn)

<br><br>

###  Mô hình triển khai tường lửa

#### Gateway Mode: 
FW là nơi giao tiếp giữa 3 mạng, kết nôi các mạng với nhau, filter trafic đi qua các mạng (client ra I, client qua server, DMZ ra I)

![image](https://user-images.githubusercontent.com/62002485/147693402-c34419c8-bfaf-4c3b-bc3e-f54fbcca3313.png)

#### Bridge Mode: 
không phá vỡ kiến trúc network của hệ thống hiện tại, chỉ cần cắt dây ra ra nhét FW vào và thiết lập FW đó ở chế độ Bridge mode là xong.

![image](https://user-images.githubusercontent.com/62002485/147694017-0e50e948-8188-44b0-8f65-4631ce29cad0.png)


<br>
<br>

## Next Generation Firewall:
### New Requirements for the Firewall: (1), (2), (3), (4), (5)
![image](https://user-images.githubusercontent.com/62002485/175271414-03b21a0b-1ecc-479b-b895-832a946d2f63.png)
![image](https://user-images.githubusercontent.com/62002485/175337019-b78d3bcd-5fd6-4cb4-8f83-bfdc83b47fac.png)
![image](https://user-images.githubusercontent.com/62002485/175342680-3812cc87-1b6d-4120-8694-7d01a5a5775b.png)

- Protect phía client:
  - Nó có thể nhận diện được các ứng dụng thay vì port, giao thức, SSL (1)
  - Nhận diện user thay vì IP (2)
  - Hiển thị chi tiết và kiểm soát chính sách quyền truy cập/chức năng của ứng dụng. (3) VD: cho phép truy cập facebook để đọc, không đc post 
  - Bảo vệ trong thời gian thực chống lại mối đe dọa được nhúng trên các ứng dụng. (4) VD: Detect đc version ứng dụng, kiểm tra xem version đó có bị lỗ hổng nào không dựa vào signature trong database của ứng dụng cập nhật theo thời gian thực.
  - Multigigabit, triển khai in-line mà không làm giảm hiệu suất. (5) VD: không phải xử lí gói tin tuần tự như traditional firewall(network -> web -> antivirus) mà NGFW sẽ kiểm tra song song cùng lúc, chỉ cần encapsulation và decapsulation 1 lần (network & web & anti virus).
  - Mở API để các hệ thống security như là IDS/IPS, sanbox giao tiếp qua lại để tạo thành 1 giải pháp tổng thể cho toàn bộ hệ thống.
  - Tích hợp antivirus, IDS/ IPS
- Protect phía server:
  - NAT: hidden IP của server 
  - chặn 1 phần được DOS, DDOS
  - ACL: kiểm tra truy cập ra vào của server, cho phép port cụ thể kêt nối ra ngoài internet 

<br>

## Web application firewall

### Injection: sql, command
- sql: dùng các câu truy vấn để khai thác ô input để bypass authentication, lấy thông tin database.
- command: kết nối vào đc server, dùng command khai thác vulnerability trên server từ đó leo thang đặc quyền(với những quyền user đang có khai thác để lấy được quyền cao hơn).
- Broken authentication: sd tool attack web, crack password (hiện challenge page, hiện option yêu cần điền challenge character)
- Sensitive data: Client gửi request lấy sensitive data, can thiệp http response detect sensitive key word và block lại và ko để truyền ra bên ngoài. 
  
<br>

### HTTP/HTTPS:
- Next Generation Firewall:
  - SSL offload - Decryption HTTPS->HTTP ra thành 2 phần payload(detect anti virus, dung lượng bất thường chặn đc ddos dos nhờ database pattern attack - signature để detect) và header(kiểm tra được url, ip, application đưa ra các ACL chặn ip, port nào đó, C&C server).
  - Malware: client download về sẽ kiểm tra nếu ok thì chuyển xuống cho client (forward proxy)
  - Public dịch vụ web port 80,443, firewall thường ko có pattern về các cuộc tấn công web nên ko detect ra đc.
<br>

- Web application firewall:
  - Tường lửa ứng dụng web (hoặc WAF) lọc, giám sát và chặn lưu lượng truy cập HTTP / HTTPS đến và đi từ một ứng dụng web.
  - WAF được phân biệt với tường lửa thông thường ở chỗ WAF có thể lọc nội dung của các ứng dụng web cụ thể trong khi tường lửa thông thường đóng vai trò như một cổng an toàn giữa các máy chủ.
  - Bằng cách kiểm tra lưu lượng HTTP, nó có thể ngăn chặn các cuộc tấn công bắt nguồn từ các lỗi bảo mật ứng dụng web, chẳng hạn như chèn SQL, tập lệnh trang web chéo (XSS), bao gồm tệp và cấu hình sai bảo mật
  - Malware: up file lên thì kiểm tra nếu ok thì chuyển lên cho server (Đóng vai trò là reverse proxy)

<br>

- Web server tương tác với người dùng

![image](https://user-images.githubusercontent.com/62002485/160228407-47e8f94e-db03-4ffc-adda-58981bb1687c.png)

![image](https://user-images.githubusercontent.com/62002485/160228514-6d9bf1a7-d52b-4072-b259-71c21ee253ab.png)

![image](https://user-images.githubusercontent.com/62002485/175834265-f57b23fb-607f-4cbf-86e0-4471dd6dab07.png)

![image](https://user-images.githubusercontent.com/62002485/160228593-acd6d996-3fd3-4513-a1c5-a7030e6cdb8f.png)

![image](https://user-images.githubusercontent.com/62002485/175834966-0d873d14-609d-4223-bdc4-3c766b81e340.png)

![image](https://user-images.githubusercontent.com/62002485/175834980-fcdc8510-10e2-4938-97c1-dbdcf6e26377.png)

![image](https://user-images.githubusercontent.com/62002485/175834987-8b483848-b934-4cf9-89f5-c47fb6db933c.png)

![image](https://user-images.githubusercontent.com/62002485/160228695-48567968-da83-4b33-b536-a596b77341a9.png)


<br><br>

##  Endpoint Security
### Endpoint Security là gì
- Endpoint Security là công nghệ bảo mật đầu cuối (User và Computer)
- Endpoint Security cho phép:
    - Quản lý thông tin phần cứng máy tính
    - Quản lý ứng dụng trên máy tính người dùng
    - Quản lý việc truy cập internet của người dùng
    - Quản lý các device (USB, Bluetooth, CD-ROM,…)

### Tại sao sử dụng Endpoint Security
- Quản lý bảo mật trực tiếp ở mức đầu cuối
    - Hardware
    - Device
    - Application
    - User
- Giảm lưu lượng gói tin trong mạng (traffic ko hợp lệ sẽ bị chặn ngay tại enpoint)
- Chi phí rẻ và linh động trong việc thay đổi công nghệ

### Data Loss Prevention
Hạn chế tối đa việc bộc phát dl
![image](https://user-images.githubusercontent.com/54493212/175497168-80ba3a78-53fd-44a7-b505-9b801081868a.jpg)

![image](https://user-images.githubusercontent.com/54493212/175497172-da278603-daf7-4dbe-8eea-1964ea19ce7c.jpg)

![image](https://user-images.githubusercontent.com/54493212/175497173-a07e6ebe-00ff-461f-9bd3-28972c603890.jpg)
![image](https://user-images.githubusercontent.com/54493212/175497176-251825c6-be8d-41d8-837d-27c22580086d.jpg)
![image](https://user-images.githubusercontent.com/54493212/175497178-051a3dd4-f68f-4d9b-82db-7c2ad94c6a53.jpg)

### Mô hình hoạt động của Endpoint Security
![image](https://user-images.githubusercontent.com/54493212/175497181-74bdb096-fac3-4b26-9819-64108150c95f.jpg)
- Server
    - Lưu trữ dữ liệu từ agent gửi lên
    - Quản lý các chính sách cho agent thực hiện
- Agent
    - Software được cài đặt ở máy user
    - Được quản lý tập trung bởi server, giao tiếp với server để thực hiện các chính sách
    - Thu thập dữ liệu và đưa log activity thu được trên máy đến server
- Console
    - Hiển thị thông tin từ cơ sở dữ liệu của server lên màn hình 
    - Cho phép người quản trị có thể cấu hình bằng giao diện
    - Thực hiện bảo trì thời gian thực

### Mục đích của IP-Guard: 
![image](https://user-images.githubusercontent.com/62002485/175836375-c181ea64-67a0-4f08-acc7-d69953a14a98.png)

### Tính năng của IP-Guard (quyền cho hay không, filter, block, lưu log ...)
![image](https://user-images.githubusercontent.com/54493212/175497183-9a136756-2dab-42d8-88ae-08bcce98a071.jpg)

#### Basic Management Module: quản lí thông tin cơ bản enpoint
Mô-đun cơ bản và thiết yếu của IP-Guard. Đây là một mô-đun bắt buộc phải có.
- Basic Events Log: ghi nhật ký khi máy khởi động, logon, logoff, shutdown
- Basic Control: Tương tác với máy từ xa: lock, logoff, shutdown
- Basic Policy: Chặn người dùng sửa đổi cài đặt hệ thống một cách ngẫu nhiên để ngăn chặn việc phá hủy vô tình hay cố ý, cũng như cải thiện bảo mật hệ thống.

#### Document Management Module: 
Kiểm tra và giám sát các hoạt động của tài liệu nhằm bảo vệ bản quyền
- Document Control: Kiểm soát hiệu quả các hoạt động của tài liệu
- Document Backup: Backup tài liệu trước khi gửi hoặc xóa
- Document Logging: Ghi lại chi tiết các hoạt động của tài liệu trên bất cứ máy nào thực hiện chia sẻ dữ liệu

#### Print Management
Giám sát quá trình in để tránh rò rỉ dữ liệu
- Print Control: Kiểm tra các quyền in
- Print Logging: Ghi lại chi tiết các hoạt động in cho quản trị viên
- Print Backup: Backup hình ảnh của tệp được in

#### Device Management
Kiểm tra và giám sát việc sử dụng các thiết bị khác nhau để ngăn chặn rò rỉ dữ liệu
Device Control: Block các thiết bị bên ngoài kết nối với mạng nội bộ, kiểm tra chi tiết và cụ thể

#### Removable Storage (Kho lưu trữ có thể tháo rời, di chuyển. VD: USB) Management 
Cho phép và mã hóa thiết bị lưu trữ di động để bảo vệ dữ liệu quý giá mọi lúc, mọi nơi.
- Permission Control: Kiểm soát chặt chẽ tệp đang di chuyển
- Automatic Encryption & Decryption: Tự động mã hóa dữ liệu khi tệp được ghi vào bất kỳ removable storage device
- Whole Disk Encryption: Format corporate removable storage device as encrypted removable storage device. Automatically encrypt and decrypt data stored on the encrypted removable storage device within the corporate environment.
*NOTE: Encrypted removable storage device only can be used within the corporate environment*

#### Email Management
Kiểm tra và giám sát các email đến và đi để ngăn chặn rò rỉ dữ liệu
- Email Control: Chặn việc gửi các emails POP3/SMTP cụ thể hoặc trao đổi mail với email bên ngoài tổ chức
- Email Logging: Ghi lại đầy đủ người gửi, người nhận, chủ đề, nội dung và tệp đính kèm

#### Instant Messaging Management
Kiểm tra và giám sát các instant messaging để bảo vệ an toàn dữ liệu và nâng cao hiệu quả công việc
- IM Logging: Ghi lại toàn bộ các instant messages, người tham gia, thời gian
- File Transfer Control: Chặn gửi tệp ra khỏi công ty với kích thước hạn chế hoặc với tên tệp giới hạn
- File Backup: Back up các tệp đã chuyển

#### Application Management
Kiểm tra và giám sát việc sử dụng ứng dụng để nâng cao hiệu quả công việc
- Application Statistics: Thu thập số liệu thống kê theo danh mục, tên, bộ phận và nhóm
- Application Control: Lọc các ứng dụng không liên quan đến công việc, block các ứng dụng độc hại
- Application Log: Ghi lại việc bắt đầu, dừng, chuyển đổi cửa sổ ứng dụng

#### Website Management
Ghi lại các hoạt động duyệt web của nhân viên; giới hạn quyền truy cập trang web để điều chỉnh hoạt động trực tuyến của nhân viên
- Website Statistics: Thu thập số liệu thống kê bằng nhiều cách khác nhau
- Website Management: Lọc các trang web không liên quan đến công việc trong một khoảng thời gian cụ thể. Chặn các trang web độc hại và không phù hợp
- Website Log: Ghi lại URL, tiêu đề và thời gian của các trang web đã truy cập

#### Bandwidth Management
Giới hạn và kiểm soát băng thông để tránh bất kỳ lạm dụng băng thông nào
- Traffic Statistics: Thu thập số liệu thống kê bằng nhiều cách khác nhau
- Bandwidth Control: Giới hạn băng thông theo địa chỉ IP hoặc port. Hạn chế băng thông tải xuống, xem video trực tuyến

#### Network Management
Ngăn chặn các máy tính bên ngoài trái phép truy cập vào mạng nội bộ
- Network Control: Cung cấp chức năng tường lửa và chặn máy tính trái phép giao tiếp với máy tính nội bộ
- Network Intrusion Detection: Quét toàn bộ mạng để ngăn chặn ngay lập tức các máy tính không được phép kết nối vào mạng nội bộ

#### Screen Monitoring
Ghi lại và phát lại ảnh chụp màn hình để cho biết từng bước các hoạt động của nhân viên
- Screen Monitoring: Xem màn hình trong thời gian thực của bất kỳ máy tính nào. Giám sát máy tính với nhiều màn hình. Giám sát tập trung nhiều máy tính cùng một lúc
- Screen Record: Ghi lại hoàn toàn lịch sử màn hình. Đặt các khoảng thời gian khác nhau để chụp ảnh màn hình khi ứng dụng khác nhau đang được sử dụng. Có thể lưu nhiều ảnh chụp nhanh màn hình do tính năng nén hiệu quả. Lịch sử màn hình có thể được xuất sang định dạng wmv

#### Remote Maintenance
Hỗ trợ bảo trì từ xa cho phép rút ngắn thời gian chết và nhanh chóng giải quyết sự cố hệ thống
- Remote Troubleshooting: Kiểm tra các quy trình chạy trong thời gian thực của các máy khách. Phân tích từ xa trạng thái đang chạy, lỗi hệ thống và trạng thái thiết bị của máy tính khách
- Remote Control: Thực hiện hỗ trợ từ xa hoặc hướng dẫn vận hành
- Remote File Transfer: Truyền tệp từ máy tính từ xa sang máy tính cục bộ và từ máy tính cục bộ đến máy tính từ xa để nhanh chóng thu thập các mẫu lỗi để chẩn đoán sự cố và cập nhật tệp

#### IT Asset Management(thống kê, quản lí tự động, số lượng lớn enpoint)
- Dễ dàng quản lý các tài sản CNTT để giảm chi phí quản lý
- Asset Information: Tự động thu thập thông tin phần mềm và phần cứng, đồng thời cung cấp kiểm kê tài sản. Cung cấp chức năng quản lý tài sản không phải CNTT
- Asset Change: Ghi lại các thay đổi phần mềm và phần cứng một cách chi tiết. Cảnh báo tức thì về các thay đổi
- Vulnerability Management: Tự động quét lỗ hổng hệ thống của máy tính tác nhân và cung cấp báo cáo và giải pháp dễ đọc
- Patch Management: Kiểm tra Microsoft để biết các bản vá mới định kỳ. Tự động tải xuống và triển khai các bản vá mới cho máy tính đại lý
- Software Deployment: Triển khai các tệp và chương trình một cách dễ dàng. Hỗ trợ truyền điểm ngắt để tạo điều kiện cài đặt nền và cài đặt tương tác

<br><br>

## DATABASE SECURITY

4 vấn đề chính trong Database Security
- Confidentiality
- Integrity
- Authenticity
- Availability

#### Confidentiality
- Đảm bảo dữ liệu bí mật chỉ sẵn sàng với đúng người nhận (Dựa trên ACL : IP, User, Application)
- Đảm bảo toàn bộ cơ sở dữ liệu được bảo mật khỏi các vi phạm hệ thống cả bên ngoài lẫn bên trong
- Cung cấp báo cáo về những ai đã truy cập vào dữ liệu nào và họ đã làm gì với dữ liệu đó
- Dữ liệu quan trọng và dữ liệu nhạy cảm về mặt pháp lý phải được bảo mật cao trước nguy cơ bị tổn thất và kiện tụng

#### Integrity
- Xác minh rằng mọi dữ liệu bên ngoài có định dạng chính xác
- Xác minh rằng tất cả dữ liệu đầu vào là chính xác và có thể xác minh được
- Đảm bảo rằng dữ liệu tuân theo các quy chuẩn công việc chính xác của tổ chức / công ty
- Có thể báo cáo về tất cả các thay đổi dữ liệu và ai là tác giả của chúng để đảm bảo tuân thủ các quy tắc của công ty và chính sách bảo mật

#### Authenticity
- Đảm bảo rằng dữ liệu đã được chỉnh sửa bởi một nguồn được ủy quyền
- Xác nhận rằng người dùng truy cập hệ thống đúng là người mà họ tự nhận
- Xác minh rằng mọi dữ liệu gửi đi đúng người nhận
- Xác minh rằng tất cả các yêu cầu báo cáo là từ người dùng được ủy quyền

#### Availability
- Đảm bảo dữ liệu luôn sẵn sàng mọi lúc cần thiết
- Dữ liệu chỉ có sẵn cho những người dùng thích hợp
- Có khả năng theo dõi ai có quyền truy cập và người đó có đã truy cập dữ liệu nào

![image](https://user-images.githubusercontent.com/62002485/175838562-a9eaf35c-e695-4152-8c3c-a7341d240a1e.png)


### Database Security Technical
Kiểm soát truy cập: Access Control, FW, AD Authentication, AD Authentication, Permission

- Quản lý thông tin đăng nhập và role để hạn chế quyền truy cập dữ liệu

- Ngăn chặn những người không được phép lấy thông tin nhạy cảm

Mã hóa dữ liệu

- Làm xáo trộn dữ liệu bằng cách sử dụng mật mã dựa trên khóa hoặc làm mờ dữ liệu bằng văn bản thay thế

- Đảm bảo dữ liệu chỉ hiển thị đối với đối tượng dự kiến

Giám sát chủ động

- audit sensitive data + Data Theft prevention/Protection: Ghi nhật ký chi tiết các lần xác thực không thành công để sử dụng trong kiểm tra giám sát quyền truy cập, cũng như đưa ra cảnh báo về hoạt động bất thường có thể cho thấy mối đe dọa bảo mật
- Database Vulnerability: quét và vá lỗ hổng bảo mật

![image](https://user-images.githubusercontent.com/54493212/175497157-956b7e1e-0383-4157-86e6-115fd07a3a9d.jpg)

### Desploy :
![image](https://user-images.githubusercontent.com/62002485/175839106-adcae0a6-38ba-43fb-b74b-ca43e25a3ab3.png)

<br><br>

## QUIZ:

<br>

### 1. Trình bày cơ chế hoạt động và tính năng theo bạn là quan trọng của Next-Generation Firewall?
Next-generation Firewall đóng vai trò như một cổng an toàn giữa các máy chủ, Kiểm tra gói tin qua firewall bằng cách so sánh nó với những nguyên tắc (Rule) đã được đặt ra, để quyết định gói tin đó được cho phép (permit) hay cấm (deny). Ngoài các tính năng cơ bản của firewall truyền thống, nó còn có các cơ chế hoạt động cũng như các tính năng mới:
  - Nó có thể nhận diện được các ứng dụng thay vì port, giao thức, SSL (1)
  - Nhận diện user thay vì IP (2)
  - Hiển thị chi tiết và kiểm soát chính sách quyền truy cập/chức năng của ứng dụng. (3) VD: cho phép truy cập facebook để đọc, không đc post 
  - Bảo vệ trong thời gian thực chống lại mối đe dọa được nhúng trên các ứng dụng. (4) VD: Detect đc version ứng dụng, kiểm tra xem version đó có bị lỗ hổng nào không dựa vào signature trong database của ứng dụng cập nhật theo thời gian thực.
  - Multigigabit, triển khai in-line mà không làm giảm hiệu suất. (5) VD: không phải xử lí gói tin tuần tự như traditional firewall(network -> web -> antivirus) mà NGFW sẽ kiểm tra song song cùng lúc, chỉ cần encapsulation và decapsulation 1 lần (network & web & anti virus).
  - Mở API để các hệ thống security như là IDS/IPS, sanbox giao tiếp qua lại để tạo thành 1 giải pháp tổng thể cho toàn bộ hệ thống.
  - Tích hợp antivirus, IDS/ IPS
- Protect phía server:
  - NAT: hidden IP của server 
  - chặn 1 phần được DOS, DDOS
  - ACL: kiểm tra truy cập ra vào của server, cho phép port cụ thể kêt nối ra ngoài internet 
- SSL offload - Decryption HTTPS->HTTP ra thành 2 phần payload(detect anti virus, dung lượng bất thường chặn đc ddos dos nhờ database pattern attack - signature để detect) và header(kiểm tra được url, ip, application đưa ra các ACL chặn ip, port nào đó, C&C server).


<br>

### 2. Trình bày sự khác biệt giữa IDS/IPS ( mô hình và tính năng)?

- Intrusion Detection System: 
  - Giám sát hoạt động trên hệ thống mạng và phân tích và phát hiện hoạt động đáng ngờ
  - Cảnh báo xâm nhập cho đội cũ quản trị mạng
  - Phối hợp với tường lửa, các phần mềm diệt virus tạo nên hệ thống bảo mật hoàn chỉnh.

- Intrusion Prevention System:  
  - Có các tính năng như IDS 
  - Có thêm tính năng phản ứng, ngăn chặn các xâm nhập trái phép 

<br>

Nên đặt sau FW để ghi nhớ các cuộc tấn công vượt FW, đặt trược dex bị Ddos attack.

<br>

sensor, control, alert, reaction 

<br>

Ngoài giám sát, IPS thực hiện phân tích, kết nối nhiều sensor để học xem malicous trafic có xuất hiện trong toàn mang không, 
sau đó đưa về Management Console để quyết định xem có cảnh báo không. Sau khi cảnh báo sẽ đưa ra phản ứng như block, ghi log, alert, 
cho qua nhưng vẫn log hoặc alert...


![image](https://user-images.githubusercontent.com/62002485/147706065-0d42d6ad-f643-4414-a8b8-1df61276cb7b.png)

![image](https://user-images.githubusercontent.com/62002485/147706570-7c18073d-51a7-422c-a489-33f2ea7efeb4.png)



<br>

### 3. Trình bày cơ chế hoạt động của của Web Application Firewall? Mô tả sự khác biệt giữa WAF với NG-FW?


Client muốn kết nối tới server phải đi thông qua WAF, WAF can thiệp vào luồng nói chuyện giữa client và server
khi đó WAF decryption https ra http cleartext, thực hiện giao thức data normalization, parsing dữ liệu htai thành ctruc de cac funtion secure của WAF co the thuận tiện đưa vào template xuli. Tất ca các bước lien quan den url accl, app .. se được triển khai in-line mà không là giảm hiệu suất, 
xem xét cac van de này co liên quan đến authentication và authorization hay không, đây là giai đoạn xu li header, nếu ổn thỏa(như ip allow, trafic gởi tới là normally trafic ...) thì chuyển sang bước tiếp theo, ko thì drop gói tin, 
Công việc tiếp theo là kiểm tra payload để xem có phải cuoc tân cong sql, .... hay ko, nếu trafic này ổn sẽ cân bang tải đưa xuống web server, web server trả lời về 
WAF can thiep vao http response, inspect vào payload detect xem có day phai dl hop le dua ra ben ngoài hay ko, ko thi block, hợp lệ cho qua, tiep theo ẩn information server 
đưa vào bộ đẹm, nén lại, mã hóa trả vè cho client 


![image](https://user-images.githubusercontent.com/62002485/175879767-a6a340d5-0de5-4187-be3a-867d467036ea.png)

![image](https://user-images.githubusercontent.com/62002485/175992196-3afd92ab-3b9f-499c-91f5-063108058c42.png)


- Next Generation Firewall:
  - SSL offload - Decryption HTTPS->HTTP ra thành 2 phần payload(detect anti virus, dung lượng bất thường chặn đc ddos dos nhờ database pattern attack - signature để detect) và header(kiểm tra được url, ip, application đưa ra các ACL chặn ip, port nào đó, C&C server).
  - Malware: client download về sẽ kiểm tra nếu ok thì chuyển xuống cho client (forward proxy)
  - Public dịch vụ web port 80,443, firewall thường ko có pattern về các cuộc tấn công web nên ko detect ra đc.
<br>

- Web application firewall:
  - Tường lửa ứng dụng web (hoặc WAF) lọc, giám sát và chặn lưu lượng truy cập HTTP / HTTPS đến và đi từ một ứng dụng web.
  - WAF được phân biệt với tường lửa thông thường ở chỗ WAF có thể lọc nội dung của các ứng dụng web cụ thể trong khi tường lửa thông thường đóng vai trò như một cổng an toàn giữa các máy chủ.
  - Bằng cách kiểm tra lưu lượng HTTP, nó có thể ngăn chặn các cuộc tấn công bắt nguồn từ các lỗi bảo mật ứng dụng web, chẳng hạn như chèn SQL, tập lệnh trang web chéo (XSS), bao gồm tệp và cấu hình sai bảo mật
  - Malware: up file lên thì kiểm tra nếu ok thì chuyển lên cho server (Đóng vai trò là reverse proxy)

<br>

### 4. Trình bày cơ chế hoạt động của của Database Firewall? Mô tả sự khác biệt giữa DBF với WAF?

![image](https://user-images.githubusercontent.com/62002485/175992432-1e0b2125-ca1f-4c31-888b-605da8eb3c94.png)



<br>

### 9. Trong các đồ án môn học, bạn hãy trình bày mô hình và cách thức hoạt động của đồ án kết hợp giữa Cuckoo Sandbox & ClamAV?

![image](https://user-images.githubusercontent.com/62002485/175892691-ad5a092e-62de-4a3c-80fc-12a47e8e3b8e.png)

![image](https://user-images.githubusercontent.com/62002485/175894360-b2aedfaa-edaa-4723-bc6c-0155120b5e39.png)



<br>

### 10. Trong các đồ án môn học, bạn hãy trình bày mô hình và cách thức hoạt động của tính năng network security trong môi trường Docker?

![image](https://user-images.githubusercontent.com/62002485/175892060-eaa8b69e-3fae-4f61-a00a-244abca88eb9.png)

![image](https://user-images.githubusercontent.com/62002485/175892179-a819a9cd-af0f-41d5-9c0b-55892b13bd60.png)

<br>

7. Trong các đồ án môn học, bạn hãy trình bày mô hình và cách thức hoạt động của đồ án kết hợp giữa NGINX & ModSecurity?

![image](https://user-images.githubusercontent.com/62002485/175991489-f61a51f3-17e6-40aa-b665-7a3eedd55cb7.png)

proxy nó pass hết traffic qua modsec nó xử lí, xử lí theo rule, rồi nó trả lại traffic hoặc là nó block, hoặc là nó drop

<br>

5. Trình bày cơ chế hoạt động của giải pháp Advance Persistent Threat? Mô tả sự khác biệt giữa APT với IDS/IPS?

fireeye nghe bảo là có tích hợp sandbox để chạy thử, phân tích bla bla, còn ids hình như là chỉ theo signature thôi

Kiểu như khi client down file về, file sẽ copy 1 bản qua sandbox, nếu sandbox phát hiện ra có vấn đề nó sẽ báo lên firewall r firewall bắt user đó xóa






