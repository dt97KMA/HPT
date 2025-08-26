> Tên tài liệu: _Cơ chế infection ransomware_  
> Thực hiện: _Dat_  
> Cập nhật lần cuối: _25/08/2025_
## Mục lục:
1. [Tổng quan](#a)
2. [Reconnaissance](#b)
3. [Initial compromise](#c)
4. [Persistence](#d)
5. [Information gathering](#e)
6. [Privilege escalation](#f)
7. [Lateral movement](#g)
8. [Staging (prior to the attack launch)](#h)
9. [End-stage impact (the result)](#i) 

## Nội dung
<a name="a"></a>
### 1. Tổng quan
> Cơ chế infection (nhiễm) của ransomware là cách mà mã độc này xâm nhập vào hệ thống nạn nhân để bắt đầu hoạt động - đây là con đường và kỹ thuật mà ransomware sử dụng để lây nhiễm.

> Infection chain:
- Reconnaissance
- Initial compromise
- Persistence
- Information gathering
- Privilege escalation
- Lateral movement
- Staging (prior to the attack launch)
- End-stage impact (the result) 
<img width="1272" height="165" alt="image" src="https://github.com/user-attachments/assets/1b08a80d-f8e8-4c10-8ea3-9a2b6c76511f" />

<a name="b"></a>
### 2. Reconnaissance  
- Quét hạ tầng từ xa (IP, dịch vụ, RDP, VPN, firewall rule).  
- Thu thập thông tin nhân viên (OSINT, LinkedIn, email).  
- Dò tìm lỗ hổng chưa vá, mật khẩu yếu, dịch vụ RDP/SMB mở.  

### 3. Initial Compromise
- Phishing email chứa macro, link tải file độc.
- Lợi dụng lỗ hổng (VPN, Exchange, SMB, RDP brute force).
- Trojan / malicious update (supply chain).

### 4. Persistence 
- Tạo Scheduled Task, Registry Run key.
- Implant backdoor (webshell, reverse shell).
- Cài đặt C2 agent để giữ quyền truy cập.

### 5. Information Gathering
- Liệt kê người dùng, nhóm, máy chủ AD.
- Quét network để xem chia sẻ file, domain controller.
- Dùng whoami, ipconfig, net user, net group, nltest.

### 6. Privilege Escalation
- Khai thác lỗ hổng hệ điều hành (PrintNightmare, Zerologon…).
- Móc password/NTLM hash từ LSASS (Mimikatz).
- Trộm quyền admin/domain admin.

### 7. Lateral Movement 
- Sử dụng RDP, SMB, PsExec, WMI để lây sang máy khác.
- Di chuyển từ workstation → file server → domain controller.

### 8. Staging
- Upload ransomware binary vào các host.
- Vô hiệu hóa antivirus, backup, EDR.
- Exfiltration: trộm dữ liệu ra ngoài (double extortion).

### 9. End-stage Impact
- Triển khai ransomware → mã hóa dữ liệu.
- Ghi ransom note, yêu cầu Bitcoin/Monero.
- Có thể: DDoS, xóa bản backup, leak dữ liệu nếu không trả tiền.
