> Tên tài liệu: _Cơ chế infection ransomware_  
> Thực hiện: _Dat_  
> Cập nhật lần cuối: _25/08/2025_
## Mục lục:
1. [Tổng quan](#a)
2. [Reconnaissance](#b)

## Nội dung
<a name="a"></a>
1. Tổng quan
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
<a name="b"></a>  
## 2. Reconnaissance  

> Mục tiêu: Tìm điểm vào khả thi, xác định điểm yếu và thu thập dữ liệu chính về các hệ thống và lỗ hổng.  

**Các kỹ thuật sử dụng:**  
- Quét hạ tầng từ xa (IP, dịch vụ, RDP, VPN, firewall rule).  
- Thu thập thông tin nhân viên (OSINT, LinkedIn, email).  
- Dò tìm lỗ hổng chưa vá, mật khẩu yếu, dịch vụ RDP/SMB mở.  




