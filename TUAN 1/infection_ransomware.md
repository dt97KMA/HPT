> Tên tài liệu: _Cơ chế infection ransomware_  
> Thực hiện: _Dat_  
> Cập nhật lần cuối: _25/08/2025_
## Mục lục:
1. [Tổng quan](#a)
2. [Các phương thức lây lan ransomware](#b)
3. [Infection chain](#c)

## Nội dung
<a name="a"></a>
### 1. Tổng quan
> Cơ chế infection (nhiễm) của ransomware là cách mà mã độc này xâm nhập vào hệ thống nạn nhân để bắt đầu hoạt động - đây là con đường và kỹ thuật mà ransomware sử dụng để lây nhiễm.

<a name="b"></a>
### 2. Các phương thức lây lan ransomware
- Phishing qua email và kỹ thuật xã hội
  - Kẻ tấn công giả mạo email từ giám đốc điều hành hoặc các đối tượng tin cậy để lừa nạn nhân nhấp vào liên kết hoặc tải tệp đính kèm độc hại.
  - Phương thức này dựa trên nghiên cứu kỹ lưỡng về tổ chức và nhân viên mục tiêu (social engineering).
- Quảng cáo độc hại (Malvertising) và bộ công cụ khai thác lỗi (Exploit Kits)
  - Quảng cáo trực tuyến có chứa mã độc, dẫn đến các trang web khai thác lỗ hổng hệ thống.
  - Khi khai thác thành công, ransomware được tải xuống thiết bị của nạn nhân.
- Tấn công không dùng tệp (Fileless attacks)
  - Sử dụng công cụ hợp pháp của hệ thống, ví dụ PowerShell hoặc Windows Management Instrumentation (WMI), để thực hiện hành vi độc hại mà không cần tệp thực thi.
  - Phương thức này giúp tránh được các cơ chế phát hiện truyền thống.
- Remote Desktop Protocol (RDP)
  - Kẻ tấn công quét mạng Internet để tìm các cổng RDP dễ bị tấn công, từ đó xâm nhập trực tiếp vào hệ thống.
  - Phương thức này phổ biến với các doanh nghiệp có RDP chưa được bảo mật tốt.
- Lợi dụng nhà cung cấp dịch vụ quản lý (MSPs) và phần mềm quản lý từ xa (RMMs)
  - Kẻ tấn công xâm nhập vào hạ tầng MSP hoặc RMM, từ đó phát tán ransomware đến nhiều khách hàng cùng lúc.
  - Đây là phương thức lây lan nhanh và ảnh hưởng lớn đến chuỗi cung ứng.
- Tải xuống tự động (Drive-By Downloads)
  - Ransomware được tải xuống thiết bị của người dùng khi họ truy cập các trang web bị nhiễm mà không nhận ra.
- Phần mềm bản quyền lậu
  - Phần mềm cài đặt từ các nguồn không chính thức hoặc bẻ khóa có thể chứa ransomware.
  - Khi người dùng cài đặt, ransomware được kích hoạt.
- Phát tán qua mạng (Network Propagation)
  - Ransomware có khả năng tự lây lan qua các kết nối mạng nội bộ, ảnh hưởng đồng thời đến nhiều thiết bị trong cùng hệ thống.
- Ransomware-as-a-Service (RaaS)
  - RaaS là mô hình kinh doanh cho phép những kẻ tấn công thuê ransomware từ các nhóm tội phạm mà không cần có kỹ năng kỹ thuật cao.
  - Phương thức này làm gia tăng số lượng các cuộc tấn công ransomware trên toàn cầu.

<a name="c"></a>
### 3. Infection chain
- Reconnaissance
- Initial compromise
- Persistence
- Information gathering
- Privilege escalation
- Lateral movement
- Staging (prior to the attack launch)
- End-stage impact (the result) 
<img width="1272" height="165" alt="image" src="https://github.com/user-attachments/assets/1b08a80d-f8e8-4c10-8ea3-9a2b6c76511f" />

#### Reconnaissance  
- Quét hạ tầng từ xa (IP, dịch vụ, RDP, VPN, firewall rule).  
- Thu thập thông tin nhân viên (OSINT, LinkedIn, email).  
- Dò tìm lỗ hổng chưa vá, mật khẩu yếu, dịch vụ RDP/SMB mở.  

#### Initial Compromise
- Phishing email chứa macro, link tải file độc.
- Lợi dụng lỗ hổng (VPN, Exchange, SMB, RDP brute force).
- Trojan / malicious update (supply chain).

#### Persistence 
- Tạo Scheduled Task, Registry Run key.
- Implant backdoor (webshell, reverse shell).
- Cài đặt C2 agent để giữ quyền truy cập.

#### Information Gathering
- Liệt kê người dùng, nhóm, máy chủ AD.
- Quét network để xem chia sẻ file, domain controller.
- Dùng whoami, ipconfig, net user, net group, nltest.

#### Privilege Escalation
- Khai thác lỗ hổng hệ điều hành (PrintNightmare, Zerologon…).
- Móc password/NTLM hash từ LSASS (Mimikatz).
- Trộm quyền admin/domain admin.

#### Lateral Movement 
- Sử dụng RDP, SMB, PsExec, WMI để lây sang máy khác.
- Di chuyển từ workstation → file server → domain controller.

#### Staging
- Upload ransomware binary vào các host.
- Vô hiệu hóa antivirus, backup, EDR.
- Exfiltration: trộm dữ liệu ra ngoài (double extortion).

#### End-stage Impact
- Triển khai ransomware → mã hóa dữ liệu.
- Ghi ransom note, yêu cầu Bitcoin/Monero.
- Có thể: DDoS, xóa bản backup, leak dữ liệu nếu không trả tiền.
