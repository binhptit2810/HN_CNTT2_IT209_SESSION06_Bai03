\# IT209 - Session 06 - Exercise 3



\## 1. Mục tiêu



Cấu hình tường lửa UFW trên Ubuntu VPS và kiểm tra các cổng mạng đang lắng nghe.



Yêu cầu:

\- Mặc định từ chối kết nối vào (deny incoming).

\- Cho phép kết nối ra ngoài (allow outgoing).

\- Cho phép SSH qua port 22/tcp.

\- Cho phép ứng dụng web qua port 8080/tcp.

\- Kiểm tra trạng thái UFW.

\- Kiểm tra các port đang LISTEN bằng `ss`.



\---



\## 2. Cấu hình UFW



\### Đặt chính sách mặc định



```bash

sudo ufw default deny incoming

sudo ufw default allow outgoing

Cho phép SSH port 22

sudo ufw allow 22/tcp

Cho phép Web Application port 8080

sudo ufw allow 8080/tcp

Bật UFW

sudo ufw enable



Kết quả:



Firewall is active and enabled on system startup

3\. Kiểm tra trạng thái UFW



Lệnh:



sudo ufw status verbose



Kết quả:



Status: active

Logging: on (low)

Default: deny (incoming), allow (outgoing), disabled (routed)

New profiles: skip



To                         Action      From

\--                         ------      ----

22/tcp                     ALLOW IN    Anywhere

8080/tcp                   ALLOW IN    Anywhere

22/tcp (v6)                ALLOW IN    Anywhere (v6)

8080/tcp                   ALLOW IN    Anywhere (v6)

Nhận xét

UFW đang ở trạng thái active.

Kết nối vào mặc định bị từ chối.

Kết nối ra ngoài được cho phép.

Port 22/tcp được phép để duy trì kết nối SSH.

Port 8080/tcp được phép cho ứng dụng web.

4\. Kiểm tra các port đang LISTEN



Lệnh:



ss -tlnp



Kết quả:



State    Recv-Q   Send-Q       Local Address:Port       Peer Address:Port   Process

LISTEN   0        4096            127.0.0.54:53              0.0.0.0:\*       users:(("systemd-resolve",pid=761,fd=17))

LISTEN   0        4096         127.0.0.53%lo:53              0.0.0.0:\*       users:(("systemd-resolve",pid=761,fd=15))

LISTEN   0        5                  0.0.0.0:8080            0.0.0.0:\*       users:(("python3",pid=2165,fd=3))

LISTEN   0        4096                     \*:22                    \*:\*       users:(("sshd",pid=1173,fd=3),("systemd",pid=1,fd=87))

Nhận xét

Port 22 đang LISTEN bởi sshd, phục vụ kết nối SSH.

Port 8080 đang LISTEN bởi python3, phục vụ ứng dụng web.

Port 53 được sử dụng bởi systemd-resolved cho DNS.

5\. Kiểm tra Web Application



Lệnh:



curl http://localhost:8080



Kết quả:



IT209 - Session 06 - Exercise 3

Nhận xét



Ứng dụng web trên port 8080 hoạt động bình thường và có thể truy cập từ localhost.



6\. Kết luận



Đã hoàn thành cấu hình và kiểm tra UFW:



&#x20;UFW được cài đặt.

&#x20;Default incoming: DENY.

&#x20;Default outgoing: ALLOW.

&#x20;SSH port 22/tcp được phép.

&#x20;Web application port 8080/tcp được phép.

&#x20;UFW đang ACTIVE.

&#x20;Port 22 đang LISTEN.

&#x20;Port 8080 đang LISTEN.

&#x20;Web application hoạt động trên port 8080.

