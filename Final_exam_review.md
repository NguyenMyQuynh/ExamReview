# Proxy 

- Proxy Server là máy chủ đóng vai trò trung gian để xử lý yêu cầu giữa client và máy chủ khác.

- Giao thức hỗ trợ: `HTTP, HTTPS`(đa số), FTP, P2P,
Telnet, SOCKS, DNS, TCP-Tunnel, IM (AIM,
MSN, Yahoo!), MMS, RTSP, QuickTime.

<br>

### Mục đích: 
Proxy Server (Forward) được sử dụng với 2 mục đích chính:
  -  Tăng tốc độ truy cấp internet cho người dùng
trong mạng LAN.
  - Quản lý được nội dung truy cập internet của
người dùng.

<br>

### Lợi ích của Proxy Server?
  - Content Filtering (filtering content của user, VD: ko cho truy cập face, ko cho truy cập web có 1 key word ...), Content Security (tích hợp antiVirus down file về và sẽ scan), Spyware
Prevention (phát hiện có Spyware bên trong file và drop) 
  - IM Control, P2P Blocking, Phishing & Pop-up
Blocking
  - Virus Scanning
  - Streaming Control
  - Compression (HTTP & TCP/SOCKS)
  - Bandwidth Management
  - SSL Termination & Acceleration

<br>

### Phân loại Proxy Server: 
Phân loại theo `cơ chế hoạt động` của Proxy có: Forward Proxy và Reverse Proxy.


#### Forward Proxy:
- Caching data cho user: file ở sever down về thì sẽ được caching để trả lời cho các client khác. Việc caching loại file hay page nào do chúng ta quyết định.
- Filter request cho user cả luồng traffic ra và vào, request gửi đến kiểm tra xem hợp lệ không, nếu không drop.
- Tốc độ ra Internet là một vấn đề vì vậy forward proxy hỗ trợ tốc độ nhanh hơn.
- Content Filtering 

#### Reverse Proxy:
- Caching data cho user: Những user ngoài Internet yêu cầu file sẽ caching và trả lời cho user.
- Filter request cho user cả luồng traffic ra và vào, request gửi đến kiểm tra xem hợp lệ không, nếu không drop.
- Hidden IP của server: ip của sever nếu không có phải để IP public, nhưng nếu có rồi thì ip public proxy và tất cả các server sẽ để ip private. Bảo vệ server, ẩn IP kkhông phát sinh ra ngoài Internet.

![image](https://user-images.githubusercontent.com/62002485/147618791-3fd154b1-02b6-4728-b9cc-55dd2b7b63e7.png)



Đối với luồng traffic đi ra bên ngoài của client (luồng Forward): client -> CoreSwitch -> Proxy Forward (nếu có trả lời client) ----không có----> CoreSwitch -> Firewall -> I -> Server -> I -> FW -> CoreSwitch -> Forward -> CSwitch -> Client.

Đối với luồng reverse, mình có một vài con server public ra Internet: Client -> FW ----NAT----> Rerverse kiểm tra -> Server ...
![image](https://user-images.githubusercontent.com/62002485/147619390-affdb545-c94b-42ab-9fd4-6d63508052a0.png)

<br>

### Cơ chế hoạt động của Proxy Server(Forward):

![image](https://user-images.githubusercontent.com/62002485/147620935-0770074b-3686-4a31-9892-5b84ad649512.png)

![image](https://user-images.githubusercontent.com/62002485/147620916-d2b0035e-320c-44db-b3e0-04a800daf5f0.png)

<br>

### Mô hình triển khai Proxy:

Can thiệp vào kết nối giữa mạng lan và internet và proxy đứng sau Firewall. Ở mô hình này, khi proxy có sự cố mạng (ví dụ như treo )thì cả mạng sẽ bị sập luôn và user sẽ không vào mạng được.

![image](https://user-images.githubusercontent.com/62002485/147621151-1361fbda-0953-4888-8b8c-6261efc34d64.png)

<i> Solution: </i> Dựng proxy có vai trò như là một PC, kết nối vào lớp mạng và cài proxy server lên đó, trỏ các proxy client về proxy sever . Khi đó khi proxy sever có sự cố chỉ cần set policy bỏ phần proxy client trong các client thì user sẽ truy cập được internet.

![image](https://user-images.githubusercontent.com/62002485/147621172-b2f63fbd-14fb-4157-9379-7cb7f5356c6f.png)

<br>
<br>

<hr>

Những cuộc tấn công có thể xảy ra với IPv4
- Eavesdropping =>  Mã hóa dữ liệu.
- Data modification => IP sử dụng thuật toán hàm băm
- Identity spoofing (IP address spoofing) => IP sử dụng thuật toán hàm băm
- Denial-of-service attack => Cho phép firewall block traffic
- Man-in-the-middle attack => Sử dụng cơ chế xác thực lẫn nhau + Shared Key: vừa xác thực vừa mã hóa

IPv4 không có bảo mật chạy trong OSI được add on:
- NetworkL: IPSec 
- Application: HTTPS, SLL, Secure Shell, PGP, Kerberos
- Transport Layer: Transport Layer Security (TLS)

![image](https://user-images.githubusercontent.com/62002485/147626957-edf833ba-a34c-41a5-b72d-7122419bc0de.png)

<br>
<br>

<hr>


# IP Security

- 2 tinh năng: Authentication(mutual) và Encryption (layer3).
- Ứng dụng trong:
  - LAN: Authentication: Server xác thực client(hợp lệ hay không) khi client kết nối vào và client xác thực server(server hợp lí) khi server trả kết quả về(2 chiêu).
  - WAN: VPN (Remote Asscess và Site To Site), kênh truyền sử dụng tích hợp tính năng IPPec. 

![image](https://user-images.githubusercontent.com/62002485/147626281-860641d3-cc4e-4fe5-960e-44e702331444.png)

- Là một giao thức bảo mật chính tại lớp Mạng (Network Layer –
OSI) hoặc lớp Internet (Internet Layer – TCP/IP).
- IPsec là yếu tố quan trọng để xây dựng mạng riêng ảo (VPN –
Virtual Private Networks).
- Bao gồm các giao thức chứng thực, các giao thức mã hoá, các
giao thức trao đổi khoá:
  - AH (Authentication header): được sử dụng để xác định
nguồn gốc gói tin IP và đảm bảo tính toàn vẹn của nó.
  - ESP (Encapsulating Security Payload): được sử dụng để
chứng thực và mã hoá gói tin IP (phần payload hoặc cả gói
tin).
  - IKE (Internet key exchange): được sử dụng để thiết lập khoá
bí mật cho người gởi và người nhận.

<br>

### Ứng dụng của IPsec:
- Bảo mật kết nối giữa các chi nhánh văn phòng qua
Internet.
- Bảo mật truy cập từ xa qua Internet.
- Thực hiện những kết nối Intranet và Extranet với các
đối tác (Partners).
- Nâng cao tính bảo mật trong thương mại điện tử.


<br>
  
### Security Association - SA:
Là cách thức để hai bên tham gia vào kết nối IPSec đưa ra những thống nhất với nhau về mặt thuật toán.
Một SA cung cấp các thông tin sau:
  - Chỉ mục các thông số bảo mật (SPI - Security
parameters index): là một chuỗi nhị phân 32 bit được
sử dụng để xác định một tập cụ thể của các giải thuật
và thông số dùng trong phiên truyền thông. SPI được
bao gồm trong cả AH và ESP để chắc chắn rằng cả
hai đều sử dụng cùng các giải thuật và thông số.
  - Địa chỉ IP đích.
  - Giao thức bảo mật: AH hay ESP. IPsec không cho
phép AH hay ESP sử dụng đồng thời trong cùng một
SA

#### Trao đổi thông tin về giải thuật và các thông số:
THÔNG BÁO -> CHẤP NHẬN hoặc THƯƠNG LƯỢNG ..... ALL OK IPsec thiết lập sự kết hợp bảo mật (Security Association - SA) cho phần còn lại của phiên làm việc.

VD: B đã enable IPSec. A muốn thiêt lập IPSec với B. A gửi request đến B. B thông báo cho A sd hash md5 mã hóa aes. Nếu A chưa enable tính năng IPSec thì ko hiểu và gửi lại gói request, đến lần thứ 3 B drop gói tin đó. Nếu A enable rồi thì báo lại hash md5 OK, aes ko hỗ trợ chỉ hỗ trợ des ... tiếp tục trao đổi các thông tin cần thiết để thống nhát để làm việc với nhau.

<br>

### Cơ chế hoạt động:

![image](https://user-images.githubusercontent.com/62002485/147646097-0f8cf27c-dac9-49f3-a3ea-521012a61dca.png)

- P1: trao đổi khóa, SA.
- P2: Cơ chế IPSec chạy theo kiểu gì, AH hay ESP, data được truyền trên kênh IPSec đó.
- P3: data tranfer.

#### IKE là cơ chế trao đổi key
- Được sử dụng để thiết lập phiên làm việc của IPSec
- Có 5 giá trị được thỏa thuận:
- 2 modes (main mode và aggressive mode)
- 3 phương thức xác thực (Preshared-Key {A kết nối đến B, B yêu cầu secret key, A cung cấp và bắt đầu phiên làm việc}; Kerberos {phân vùng tính năng active directory add máy vào và triển khai IPSec và
Certification {đưa certification của chúng ta cho partner để họ import vào}) 


<br>

![image](https://user-images.githubusercontent.com/62002485/147649926-64ca758e-2726-4565-95d0-44a4a841574f.png)

- MSG 1: client gửi gói tin có IP đích đến server, đề xuất thuật toán encryption(aes or RSA) và authentication (md5).
- MSG 2: server phản hồi đồng ý (or không)
- MSG 3: gửi key thông qua cơ chế Diffie-Hellman(thông tin đẻ tạo ra key chứ ko phải key thực sự ... @@) để ko bị lộ key trên đường truyền. Ngoài ra còn đính kèm thêm một giá trị random Nonce khi mã hóa chèn mã đó vào tránh trường hợp bị phá mã.
- MSG 4: gửi key thông qua cơ chế Diffie-Hellman. Sau buiwsc này thống nhất key và hai bên có nonce của nhau.
- MSG 5: initiator tiến hành việc sign lên và sử dụng key(random nên có thể trùng giữa các client) đã thống nhất + nounce (ko trùng do được tạo ra mỗi khi 1client kết nói vô -server) để encrypt.
- MSG 6: server trích lục trong hệ quản trị(có 1 loạt các key và nounce) key và nonce nào giải mã ra được thì biết chắc chắn là initiator đó gửi chứ ko phải nào khác, tiến hành reponse signature mã hóa và gửi lại cho initiator. 

<i>Initiator nhận và sử dụng key + nounce đã đượuc nhận từ server để giải mã và xác nhận đsung server đó.</i>

<br>

### Các phương thức hoạt động của IPsec:
IPSec gửi dữ liệu bằng cách sử dụng chế độ Tunnel hoặc Transport. Các chế độ này có liên quan chặt chẽ đến loại giao thức được sử dụng, AH hoặc ESP.

Chế độ Tunnel: Trong chế độ Tunnel, toàn bộ gói tin được bảo vệ. IPSec gói gói dữ liệu trong một packet mới, mã hóa nó và thêm một IP header mới. Nó thường được sử dụng trong thiết lập VPN site-to-site. Chế độ Tunnel trong IPsec được sử dụng giữa hai router chuyên dụng, với mỗi router hoạt động như một đầu của "đường hầm" ảo thông qua mạng công cộng. Trong chế độ Tunnel, IP header ban đầu chứa đích cuối cùng của gói được mã hóa, cùng với payload gói. Để cho những router trung gian biết nơi chuyển tiếp các gói tin, IPsec thêm một IP header mới. Tại mỗi đầu của đường hầm, những router giải mã những IP header để chuyển các gói đến đích của chúng.

Chế độ Transport: Trong chế độ Transport, IP header gốc vẫn còn và không được mã hóa. Chỉ có payload và ESP trailer được mã hóa mà thôi. Chế độ Transport thường được sử dụng trong thiết lập VPN client-to-site. Trong chế độ Transport, payload của mỗi gói được mã hóa, nhưng IP header ban đầu thì không. Do đó, các router trung gian có thể xem đích cuối cùng của mỗi gói - trừ khi sử dụng một giao thức tunnel riêng biệt (chẳng hạn như GRE).

<br>
<br>

<hr>

# SSL

- 2 tinh năng: Authentication(mutual) và Encryption (layer7).
- Client ko có certificate thì server không xác thực được là client có phải đúng là client hợp lệ hay ko.

![image](https://user-images.githubusercontent.com/62002485/147627060-76f392fd-1b7e-4369-9969-106071183edd.png)




