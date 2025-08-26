> Tên tài liệu: _Vector lây lan_  
> Thực hiện: _Dat_  
> Cập nhật lần cuối: _25/08/2025_
## Mục lục:
1. [Phishing](#a)
2. [RDP Brute-force](#b)
3. [Supply Chain Attack](#c)
4. [So sánh các vector lây lan](#d)

## Nội dung
<a name="a"></a>
### 1. Phishing
#### Cơ chế kỹ thuật
- Kẻ tấn công gửi email giả mạo (spear-phishing hoặc mass-phishing).
- Đính kèm tài liệu chứa macro độc hại (Word, Excel) hoặc tệp thực thi nén (ZIP/RAR) → khi mở sẽ tải payload.
- Liên kết dẫn đến website giả mạo chứa exploit kit hoặc tải xuống dropper.
- Kỹ thuật phổ biến:
  - Macro AutoOpen() trong Office.
  - HTML Smuggling (ẩn mã độc trong file HTML đính kèm).
  - MalDoc + Living-off-the-land (sử dụng PowerShell, mshta, rundll32).

<a name="b"></a>
### 2. RDP Brute-Force / Credential Attack  
#### Cơ chế kỹ thuật
- Kẻ tấn công quét cổng RDP (3389/TCP) công khai hoặc nội bộ.
- Thử brute-force password hoặc dùng credential từ dump (Mimikatz, stealer).
- Nếu thành công → truy cập trực tiếp server bằng quyền user/administrator.
- Sau đó:
  - Triển khai ransomware thủ công.
  - Tắt dịch vụ backup, Shadow Copies.
  - Di chuyển ngang (lateral movement) qua SMB/WMI.

<a name="c"></a>
### 3. Supply Chain Attack 
#### Cơ chế kỹ thuật
- Thay vì nhắm trực tiếp nạn nhân, kẻ tấn công xâm nhập nhà cung cấp dịch vụ/phần mềm.
- Cấy mã độc vào bản update hoặc package phân phối.
- Khi khách hàng cập nhật phần mềm → payload ransomware cài đặt âm thầm.

<a name="d"></a>
### 4. So sánh các vector lây lan: phishing, RDP brute-force, supply chain

| Tiêu chí                         | Phishing Email                               | RDP Brute-force Attack                       | Supply Chain Attack                                    |
|----------------------------------|----------------------------------------------|----------------------------------------------|--------------------------------------------------------|
| **Cơ chế hoạt động**             | Gửi email chứa file đính kèm độc hại hoặc link dẫn đến payload. | Tấn công brute-force/mật khẩu yếu để truy cập trái phép Remote Desktop. | Cấy mã độc vào phần mềm/hệ thống của nhà cung cấp thứ ba. |
| **Mức độ phức tạp**              | Trung bình – dựa nhiều vào kỹ thuật social engineering. | Thấp đến trung bình – khai thác mật khẩu yếu hoặc RDP không bảo vệ. | Cao – yêu cầu xâm nhập vào hệ thống phát triển/phân phối phần mềm. |
| **Độ phổ biến**                  | Rất cao, chiếm phần lớn các chiến dịch ransomware. | Khá phổ biến với các tổ chức có RDP mở công khai. | Ít phổ biến hơn nhưng đang tăng, có tác động lớn. |
| **Tính hiệu quả**                 | Cao, vì người dùng dễ bị lừa mở email giả mạo. | Cao nếu quản trị viên không có bảo mật 2FA hoặc chính sách mật khẩu mạnh. | Rất cao, có thể lây lan hàng loạt đến nhiều nạn nhân cùng lúc. |
| **Rủi ro đối với nạn nhân**      | Nhanh chóng bị lây nhiễm sau khi tải/mở file. | Toàn bộ hệ thống bị kiểm soát trực tiếp. | Chuỗi cung ứng bị xâm nhập => lây nhiễm diện rộng, khó kiểm soát. |
| **Khả năng phát hiện**           | Có thể bị phát hiện bởi email filter, sandbox. | Có thể phát hiện qua log sự kiện, IDS/IPS. | Rất khó phát hiện trước khi phần mềm bị phát hành. |
| **Ví dụ thực tế**                 | Ryuk, Locky, Emotet (qua email).             | Dharma, SamSam.                              | SolarWinds Orion (2020), Kaseya VSA (2021). |
| **Chi phí cho attacker**          | Thấp – cần gửi hàng loạt email spam.         | Trung bình – cần công cụ brute-force, server scan. | Rất cao – cần năng lực kỹ thuật và tài chính lớn. |
| **Mức độ thiệt hại tiềm ẩn**      | Trung bình – phụ thuộc số lượng user click.  | Cao – kiểm soát hoàn toàn hệ thống nạn nhân. | Rất cao – ảnh hưởng đến nhiều tổ chức/khách hàng cùng lúc. |


