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

# Access control list:

- ACL là một danh sách các điều kiện mà Router/Switch L3 dùng để kiểm tra khi gói tin đi qua một cổng của Router/Switch L3. ACL áp lên interface của thiết bị.
- Danh sách các điều kiện này cho Router biết loại gói tin nào được chấp nhận hay từ chối dựa trên các điều kiện cụ thể
- Các điều kiện của ACL :
  - Địa chỉ Nguồn
  - Địa chỉ Đích
  - Giao thức
  - Port


- Cơ chế hoạt động của ACL:
Khi gói tin đi vào hay đi ra 1 cổng nào đó trên Router. Router sẽ
dựa vào ACL để kiểm tra gói tin đó để quyết định cho qua hay
drop gói tin. Gói tin sẽ được kiểm tra theo thứ tự của các điều kiện. 
Khi kiểm tra phù hợp các thông số : Địa chỉ IP, Giao thức, Port
sau đó Router kiểm tra tới điều kiện cho phép hay hủy bỏ gói tin. 
Luôn luôn tồn tại 1 điều kiện cấm tất cả ở cuối danh sách điều
kiện

![image](https://user-images.githubusercontent.com/62002485/159100853-1d6448a6-f9e9-4d11-bbb6-d384492d38f1.png)

![image](https://user-images.githubusercontent.com/62002485/159100863-215991e0-4eff-44f9-9ab1-87bce5a5a526.png)

![image](https://user-images.githubusercontent.com/62002485/159100898-926a4846-f2df-4484-8fd5-13884e035dda.png)

![image](https://user-images.githubusercontent.com/62002485/159100889-cfc6d3a1-d417-4ebf-8f0c-96f318903f5b.png)


<br>
<br>

<hr>

# Firewall

- Được đặt ở vị trí giao thương giữa các mạng với nhau, đặc biệt là mạng private và public. Trong mạng private, muốn bảo vệ vùng nào thì đặt firewall trước vùng đó.
- Firewall hay còn được còn là Tường Lửa. Là thiết
bị, ỏa hóa hay phần mềm bảo mật được sử dụng
để quản lý luồng gói tin qua nó : cho phép
(permit) hay cấm (deny). Xét chiều đi phải xét chiều về, nếu không vd khhi gửi request thì sẽ không nhận được reponse.
- Antivirus: focus vào file, phân tích behaviour về mặt system, phát hiện đối tượng file run trên hệ thống có an toàn không
- Filewall có nhiều function: và Network Security là function chính: protect đc host, tính năng NAT, ẩn địa chỉ IP của server, cho phép thiết lập rule cho phép kiểm soát cho máy này ra internet ở những port nào...



<br>

### Phân loại tường lửa
- Phần cứng: Thiết bị mạng (có hardware của thiết bị, có formware có hdh tối ưu hóa lại và install software firewall lên)
  - Checkpoint, Cisco ASA, Astaro, Cyberoam,…
- Phần mềm : Ứng dụng bảo mật được cài trên
máy tính (Chúng ta phải có 1 con server vật lí RAM, CPU, cài hdh, cài software firewall lên và tiến hành sdung: cài các rules... ==> hdh chưa đc tối ưu hóa và khi xảy ra lỗi ở mức hdh thi ta phải tự xử lí)
  - ISA Server, IPCop, Smoothwall, Pfsense,…
- Ảo hóa (nhà cung cấp sẽ cung cấp 1 file để ta import vào hạ tầng ảo hóa và nó sẽ bung ra cho chúng ta máy virtual client đã có hdh và phần mềm security và chúng ta chỉ cần bật máy lên và sử dụng)
  - SOPHOS, Palo Alto,...

Cả Personal Firewall và Network Firewall
được chia làm 3 loại chính :
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
- Không hỗ trợ authentication, không ngăn chặn ddos, tcp/ip.
- Log dạng text chứ không hiện lên darkbroad.

<br>

###  Stateful Packet Filter Firewalls

Chức năng tương tự Simple Packet Filter nhưng thêm tính năng lưu được trạng thái của gói tin đi trước, so sánh với gói đi sau để lưu lại quấ trình đi của gói tin.

![image](https://user-images.githubusercontent.com/62002485/147690843-6c2c5f54-0fa8-446a-93e0-268cd48768cc.png)

- Simple: A communication với B cần thiết lập rule 2 chiều, còn Stateful chỉ cần  xét từ A đến B thì connection sẽ được cập nhật trong stateful table 

![image](https://user-images.githubusercontent.com/62002485/159025511-ec0d177f-ec4b-4b9c-803b-d351db3f33c8.png)

Điểm yếu 
- Chiếm nhiều tài nguyên hơn.
- Footprint được nên giảm được attack.
- Ít giả mạo được hơn vì FW sẽ phát hiện IP Spoofing nhờ stateful table.

<br>

### Application Level Firewalls:
- Còn được gọi Application-Proxy Gateways.
- Có thể inspect sâu bên trong gói HTTP header, SMTP header, có khả
năng điểu khiển truy cập từ Layer 2 đến Layer 7
- Deep Packet Inspection : kiểm tra chi tiết gói tin
nên có khả ngăn chặn các ứng dụng Instant
Message, Peer to Peer,…
- Hoạt động ở Layer 7

<br>

- Cơ chế Buffering: vd khi download gom tất cả các mẫu nhỏ và discapsulation thành 1 file và scan nó, nếu ok cho qua.
- Inspect sâu bên trong protocol hiển thị các application đang chạy ở các port cụ thể, băng thông và người dùng.
==> Giám sát mạng chạy ntn, nhắc nhở ai đang sdung giao thức quá ngưỡng...

<br>

- Tích hợp được LDAP, active directory để xác thực user password.
- Tích hợp VPN xác thực Token
- Biometric: one time password - xác thực vân tay.
- Log rất chi tiết.
- Authentication
- Có khả năng tạo rule ngăn cản gói tin đã mã hóa (file ko đọc được FW sẽ block luôn)

Next Generation Firewall:
- Protect phía client:
  - Tích hợp anti virus, IDS/ IPS
  - Nó có thể xác thực được các ứng dụng qua port, giao thức, SSL
  - Xác định user qua IP
  - chặn đc giao thức, chặn đc các chức năng cụ thể
  - detect đc version ứng dụng 
  - kiểm tra song song (network, web, anti virus) không phải tuần tự như traditional firewall 
- Protect phía server:
  - NAT: hidden IP của server 
  - chặn 1 phần được DOS, DDOS
  - ACL: kiểm tra truy cập ra vào của server, cho phép port cụ thể kêt nối ra ngoài internet 


### Injection: sql, command
- sql: dùng các câu truy vấn để khai thác ô input để bypass authentication, lấy thông tin database.
- command: kết nối vào đc server, dùng command khai thác vulnerability trên server từ đó leo thang đặc quyền(với những quyền user đang có khai thác để lấy được quyền cao hơn).
Broken authentication:
  - sd tool attack web, crack password (hiện challenge page, hiện option yêu cần điền challenge character)
Sensitive data:
  - Client gửi request lấy sensitive data, can thiệp http response detect sensitive key word và block lại và ko để truyền ra bên ngoài. 
  
<br>

### HTTP/HTTPS:
- Next Generation Firewall:
  - Decryption HTTPS->HTTP ra thành 2 phần payload(detect anti virus, dung lượng bất thường chặn đc ddos dos nhờ database pattern attack - signature để detect) và header(kiểm tra được url, ip, application đưa ra các ACL chặn ip, port nào đó, C&C server).
  - Malware: client download về sẽ kiểm tra nếu ok thì chuyển xuống cho client (forward proxy)
- Web application firewall (hoạt động trên nền giao thức http/https, lọc nội dung của ứng dụng web trong khi tường lửa thông thường đóng vai trò như cổng an toàn giữa các máy chủ):
  - Public dịch vụ web port 80,443, firewall thường ko có pattern về các cuộc tấn công web nên ko detect ra đc.
  - Decryption HTTPS->HTTP ra thành 2 phần payload( bằng cách kiểm tra lưu lượng HTTP, xem có các pattern liên quan đến các cuộc tấn công như sql injection, buffer oveflow, command injection,broken authentication và các attack liên quan đến web app khác) và header(xem ip, url xem hợp lệ hay không).
  - Malware: up file lên thì kiểm tra nếu ok thì chuyển lên cho server (preverse proxy - HTTP POST)

<br>

- Web server tương tác với người dùng
![image](https://user-images.githubusercontent.com/62002485/160228407-47e8f94e-db03-4ffc-adda-58981bb1687c.png)

![image](https://user-images.githubusercontent.com/62002485/160228514-6d9bf1a7-d52b-4072-b259-71c21ee253ab.png)

![image](https://user-images.githubusercontent.com/62002485/160228593-acd6d996-3fd3-4513-a1c5-a7030e6cdb8f.png)

![image](https://user-images.githubusercontent.com/62002485/160228695-48567968-da83-4b33-b536-a596b77341a9.png)


<br>

###  Mô hình triển khai tường lửa

#### Gateway Mode: 
FW là nơi giao tiếp giữa 3 mạng, kết nôi các mạng với nhau, filter trafic đi qua các mạng (client ra I, client qua server, DMZ ra I)

![image](https://user-images.githubusercontent.com/62002485/147693402-c34419c8-bfaf-4c3b-bc3e-f54fbcca3313.png)

#### Bridge Mode: 
không phá vỡ kiến trúc network của hệ thống hiện tại, chỉ cần cắt dây ra ra nhét FW vào và thiết lập FW đó ở chế độ Bridge mode là xong.

![image](https://user-images.githubusercontent.com/62002485/147694017-0e50e948-8188-44b0-8f65-4631ce29cad0.png)

<br>
<br>

<hr>

Các giao thức chạy trên IPv4: HTTP, Telnet,...

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

- 2 tinh năng chính: Authentication(mutual) và Encryption (layer3).
- Để thực hiện được chức năng chính của mình là bảo mật dữ liệu trong VPN, IPSec cung cấp những tính năng sau:
  - Bảo vệ IPv4 khỏi những cuộc tấn công basic vd như spoofing sẽ có authentication...

  - Sự bảo mật dữ liệu (Data Confidentiality): Đảm bảo dữ liệu được an toàn, tránh những kẻ tấn công phá hoại bằng cách thay đổi nội dung hoặc đánh cắp dữ liệu quan trọng. Việc bảo vệ dữ liệu được thực hiện bằng các thuật toán mã hóa như DES, 3DES và AES. Tuy nhiên, đây là một tính năng tùy chọn trong IPSec.

  - Sự toàn vẹn dữ liệu (Data Integrity): Đảm bảo rằng dữ liệu không bị thay đổi trong suốt quá trình trao đổi. Data Integrity bản thân nó không cung cấp sự an toàn dữ liệu. Nó sử dụng thuật toán băm (hash) để kiểm tra dữ liệu bên trong gói tin có bị thay đổi hay không. Những gói tin nào bị phát hiện là đã bị thay đổi thì sẽ bị loại bỏ. Những thuật toán băm: MD5 hoặc SHA-1.

  - Chứng thực nguồn dữ liệu (Data Origin Authentication): Mỗi điểm cuối của VPN dùng tính năng này để xác định đầu phía bên kia có thực sự là người muốn kết nối đến mình hay không. Lưu ý là tính năng này không tồn tại một mình mà phụ thuộc vào tính năng toàn vẹn dữ liệu. Việc chứng thực dựa vào những kĩ thuật: Pre-shared key, certificate, RSA-encryption, RSA-signature.

  - Tránh trùng lặp (Anti-replay): Đảm bảo gói tin không bị trùng lặp bằng việc đánh số thứ tự. Gói tin nào trùng sẽ bị loại bỏ, đây cũng là tính năng tùy chọn.

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

### Cơ chế hoạt động:

![image](https://user-images.githubusercontent.com/62002485/147646097-0f8cf27c-dac9-49f3-a3ea-521012a61dca.png)

- P1: thỏa thuận cơ chế trao đổi khóa và sử dụng cơ chế đó để xác thực. Một khi các giải thuật và các thông số được lựa chọn,
IPsec thiết lập sự kết hợp bảo mật (Security Association - SA) (Pre-shared key đảm bảo tính xác thực)
- P2: client đóng gói dữ liệu theo SA đã thỏa thuận và gửi đến server. (ÍPec header mã hóa, toàn vẹn)
- P3: data tranfer.

<br>

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

### Định dạng AH:

![image](https://user-images.githubusercontent.com/62002485/147662928-56fff433-fe45-4b39-a6f6-7892cdae0de4.png)

Authentication Header (AH) bao gồm các vùng:
- Next Header (8 bits): xác định header kế tiếp.
- Payload Length (8 bits): chiều dài của Authentication
Header theo từ 32-bit, trừ 2.
- Reserved (16 bits): sử dụng cho tương lai.
- Security Parameters Index (32 bits): xác định một SA.
- Sequence Number (32 bits): một giá trị tăng đơn điệu.
- Authentication Data (variable): Một vùng có chiều dài biến
đổi (phải là một số nguyên của từ 32 bits) chứa giá trị kiểm
tra tính toàn vẹn (Integrity Check Value - ICV) đối với gói
tin này.

Authentication Header
- Xác thực (SA, Pre-shared key)
- Toàn vẹn (Hash)
- Tránh tấn công Replay-Attack (Sequence Number)

<i>Data gốc bao gồm header + payload được hash và cho vào phần Authentication data trong AH IPSec header. Tiến hành gắn cả AH IPSec header vào data gốc và gửi đi. Client nhận được tách data gốc ra tiến hành hash theo thuật toán đã thỏa hiệp trước đó và so sánh với chuỗi hash trong phần Authentication data trong AH IPSec header.</i>

<br>

### Định dạng ESP:

![image](https://user-images.githubusercontent.com/62002485/147662957-192ca97e-0891-4ca6-a8d3-155bf16cfb6e.png)

Một gói ESP chứa các vùng sau:
- Security Parameters Index (32 bits): xác định một SA.
- Sequence Number (32 bits): một giá trị đếm tăng đơn
điệu, cung cấp chức năng anti-replay (giống AH).
- Payload Data (variable): đây là một segment ở
transport-level (transport mode) hoặc gói IP (tunnel
mode) được bảo vệ bởi việc mã hoá.
- Padding (0255 bytes)
- Pad Length (8 bits): chỉ ra số byte vùng đứng ngay
trước vùng này.
- Next Header (8 bits): chỉ ra kiểu dữ liệu chứa trong
vùng payload data bằng cách chỉ ra header đầu tiên
của vùng payload này.
- Authentication Data (variable): một vùng có chiều dài
biến đổi (phải là một số nguyên của từ 32-bit) chứa
ICV được tính bằng cách gói ESP trừ vùng
Authentication Data.

Encapsulating Security Payload (ESP)
- Xác thực (SA, Pre-shared key)
- Toàn vẹn (Hash)
- Bảo mật (mã hóa luôn phần dữ liệu gốc)
- Tránh tấn công Replay-Attack (Sequence Number)

<i>Data gốc bao gồm header + payload được hash và cho vào phần Authentication data trong AH IPSec header, đồng thời data gốc cũng được mã hóa và cho vào payload của IPSec header. Tiến hành gửi đi. Client nhận được giải mã phần payload header theo thuật toán đã thỏa hiệp trước đó thu được data gốc, tiến hành hash data gốc (vừa thu được sau giải mã) theo thuật toán đã thỏa hiệp trước đó và so sánh với chuỗi hash trong phần Authentication data trong AH IPSec header.</i>

<br>

### Các phương thức hoạt động của IPsec:
IPSec gửi dữ liệu bằng cách sử dụng chế độ Tunnel hoặc Transport. Các chế độ này có liên quan chặt chẽ đến loại giao thức được sử dụng, AH hoặc ESP.

Chế độ Tunnel: Trong chế độ Tunnel, toàn bộ gói tin được bảo vệ. IPSec gói gói dữ liệu trong một packet mới, mã hóa nó và thêm một IP header mới. Nó thường được sử dụng trong thiết lập VPN site-to-site. Chế độ Tunnel trong IPsec được sử dụng giữa hai router chuyên dụng, với mỗi router hoạt động như một đầu của "đường hầm" ảo thông qua mạng công cộng. Trong chế độ Tunnel, IP header ban đầu chứa đích cuối cùng của gói được mã hóa, cùng với payload gói. Để cho những router trung gian biết nơi chuyển tiếp các gói tin, IPsec thêm một IP header mới. Tại mỗi đầu của đường hầm, những router giải mã những IP header để chuyển các gói đến đích của chúng.

![image](https://user-images.githubusercontent.com/62002485/147666675-5faaf896-4689-4ac2-ad0b-4e17f9dbf5b8.png)


Chế độ Transport: Trong chế độ Transport, IP header gốc vẫn còn và không được mã hóa. Chỉ có payload và ESP trailer được mã hóa mà thôi. Chế độ Transport thường được sử dụng trong thiết lập VPN client-to-site. Trong chế độ Transport, payload của mỗi gói được mã hóa, nhưng IP header ban đầu thì không. Do đó, các router trung gian có thể xem đích cuối cùng của mỗi gói - trừ khi sử dụng một giao thức tunnel riêng biệt (chẳng hạn như GRE).

![image](https://user-images.githubusercontent.com/62002485/147666651-6c872b04-b184-4970-b3a4-053806919749.png)


<br>
<br>

<hr>

# SSL/TLS: 

HTTPS (Hypertext Transfer Protocol Secure) là giao thức truyền tải siêu văn bản an toàn. Thực chất, đây chính là giao thức HTTP nhưng tích hợp thêm Chứng chỉ bảo mật SSL nhằm mã hóa các thông điệp giao tiếp để tăng tính bảo mật. 

- Giao thức SSL (Secure Socket Layer Protocol)
và giao thức TLS (Transport Layer Security
Protocol) là những giao thức bảo mật tại lớp vận
chuyển được dùng chủ yếu trong thực tế.
- TLS là một phiên bản sửa đổi của SSL v3.
- Khi cấu hình liên quan SSL, lưu ý VD: A & B cấu hình SSL với nhau thì phải hỗ trợ version với nhau, web browser và web server 2 đầu SSL cần match version. 

![image](https://user-images.githubusercontent.com/62002485/147627060-76f392fd-1b7e-4369-9969-106071183edd.png)

- 2 tinh năng: Authentication(mutual) và Encryption (layer7).
- Client ko có certificate thì server không xác thực được là client có phải đúng là client hợp lệ hay ko. (client anonymous)

<br>

### Cấu trúc của SSL

Giao thức SSL bao gồm 2 thành phần:
- Thành phần thứ nhất được gọi là record protocol, được 
đặt trên đỉnh của các giao thức lớp vận chuyển. 
- Thành phần thứ hai được đặt giữa các giao thức tầng 
ứng dụng (như HTTP) và record protocol , bao gồm các 
giao thức:
  - Handshake protocol
  - Change-cipher-spec protocol
  - Alert protocol
  
![image](https://user-images.githubusercontent.com/62002485/147700916-bee50897-d19f-43d8-8317-48886e138458.png)

<br>

### Record protocol của SSL

Gỉả sử dữ liệu là file M, máy A gửi cho B thì từ tầng 7 máy A đi xuống 6,5,... và đến B 1,2,...7.
Khi đi xuông ở tầng 6 bắt đầu cắt và compress M. Nếu có SSL, tiến hành hash ...... (như hình)
Sau đó chuyển xuống tầng dưới đóng thêm header tầng 4, 3 vào.
==> Dữ liệu vừa toàn vẹn vừa an toàn.

![image](https://user-images.githubusercontent.com/62002485/147701676-aec30b28-8fbf-47ad-b8bf-55391f62695c.png)

<br>

### Các giao thức của SSL

- Giao thức bắt tay (handshake protocol) thành lập các
giải thuật mã hóa, giải thuật nén, và các thông số sẽ
được sử dụng bởi cả hai bên trong việc trao đổi dữ liệu
được mã hóa. Sau đó, các giao thức bản ghi (record
protocol) chịu trách nhiệm phân chia thông điệp vào các
khối, nén mỗi khối, chứng thực chúng, mã hóa chúng,
thêm header vào mỗi khối, và sau đó truyền đi các khối
kết quả.
- Các giao thức đổi mật mã (change-cipher-spec
protocol) cho phép các bên giao tiếp có thể thay đổi các
giải thuật hoặc các thông số trong một phiên truyền
thông.
- Các giao thức cảnh báo (alert protocol) là một giao
thức quản lý, nó thông báo cho các bên tham gia truyền
thông khi có vấn đề xảy ra. VD: Bị drop gói 3 lần đưa ra alert 

<br>

### Quá trình thiết lập kết nối SSL

![image](https://user-images.githubusercontent.com/62002485/147705218-3759bd03-2f21-4339-9f1c-38f4c90b790a.png)

- B1: Client gõ https://..., gửi request đến server.
- B2: Server nhận request và gửi client thông báo đã nhận.
- B3: Server gửi certificate của mình (có chứa public key của server) cho client.
- B4: Server yêu cầu certificate của client.
- B5: Client gửi certificate của mình cho server. //or not
- B6: Client generate ra 1 sesion key, sau đó sử dụng public key của server để mã hóa(confidetial - bảo mật) và gửi sesion key đã được mã hóa cho server. Server dùng private key của mình để giải mã.
- B7: Client dùng private key cảu nó mã hóa (authentication) sesion key. Server dùng public key của client để giải mã và compare (toàn vẹn) 2 session key với nhau. //or not

<i>Dùng session key mã hóa dữ liệu => tăng performance.</i>

<br>
<br>

<hr>

# PGP (giao thức bảo mật email): 
Là giao thưc hỗ trợ bảo mật cho giao thức email POP3
Mã hóa nằm ở phía client.
Bảo mật, xác thực và toàn vẹn.

![image](https://user-images.githubusercontent.com/62002485/147709421-d0854d87-8cea-4b19-a450-04fe94210f37.png)


<br>
<br>

<hr>

# SSH 
Là giao thức bảo mật cho giao thức telnet để kết nối vào server để quản trị bằng command.

<br>
<br>

<hr>

# IDS/IPS

<br>

### IDS

Intrusion Detection: qui trình theo dõi các sự kiện
xuất hiện trong `hệ thống máy tính` và `mạng`. Sau đó
phân tích chúng có dấu hiệu của sự xâm nhập hay
không?

Intrusion Detection
System: là một hệ
thống tự động giám
sát hoạt động trên hệ
thống mạng và phân
tích để tìm ra các dấu
hiệu vi phạm đến các
quy định bảo mật máy
tính,chính sách sử
dụng và các tiêu chuẩn
an toàn thông tin.

![image](https://user-images.githubusercontent.com/62002485/147706065-0d42d6ad-f643-4414-a8b8-1df61276cb7b.png)

<br>

### IPS:

Intrusion Prevention
System: là một hệ
thống bao gồm cả
chức năng phát hiện
xâm nhập (Intrusion
Detection – ID) và
khả năng ngăn chặn
các xâm nhập trái
phép vào tài nguyên
của hệ thống mạng

Ngoài giám sát, IPS thực hiện phân tích, kết nối nhiều sensor để học xem malicous trafic có xuất hiện trong toàn mjang không, sau đó đưa về Management 
Console để quyết định xem có cảnh báo không. 
Sau khi cảnh báo sẽ đưa ra phản ứng như block, ghi log, alert, cho qua nhưng vẫn log hoặc alert...

![image](https://user-images.githubusercontent.com/62002485/147706570-7c18073d-51a7-422c-a489-33f2ea7efeb4.png)

<br>

### Thành phần chính của IDS/IPS

Nên đặt sau FW để ghi nhớ các cuộc tấn công vượt FW, đặt trược dex bị Ddos attack.

![image](https://user-images.githubusercontent.com/62002485/147706636-9c4669e4-89db-488b-b9ec-d352ddf2cf25.png)

![image](https://user-images.githubusercontent.com/62002485/147706653-3d07c190-ebfc-4711-9a61-772caabadc21.png)

### Phân loại IDS/IPS

Network–based (NIDS/NIPS) và Host–based IDS (HIDS/HIPS)

![image](https://user-images.githubusercontent.com/62002485/147706993-d911d383-3737-43c9-9402-cfbe8fd70c7c.png)

![image](https://user-images.githubusercontent.com/62002485/147707000-e4579a30-2c46-415a-b31a-07e35dcacf47.png)

Cài HIDS/HIPS, NIDS/NIPS cho server. Trên Core-switch cài IDS monitor tất cả trafic đi qua đi lại client.
<br>
Không cài HIPS trên client vì tốn chi phí và make noisy (chặn liên tục, user không sử dụng được).

![image](https://user-images.githubusercontent.com/62002485/147707624-48b0614f-37bb-4791-baf2-2f768f52af63.png)



