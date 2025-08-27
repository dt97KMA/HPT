> Tên tài liệu: _Kỹ thuật execution & privilege escalation trong ransomware_  
> Thực hiện: _Dat_  
> Cập nhật lần cuối: _25/08/2025_
## Mục lục:
1. [Execution](#a)
2. [Privilege Escalation](#b)

## Nội dung
<a name="a"></a>
### 1. Execution
#### 1.1 Mục tiêu
- Thiết lập foothold (chạy loader/beacon).
- Tải xuống payload thứ cấp (ransomware main).
- Triển khai hành vi ban đầu (disable AV, xóa shadow copies, tạo persistence).
#### 1.2 Kỹ thuật execution
##### Malicious Documents (MalDoc)
- Macro (VBA AutoOpen/Document_Open) trong .docm/.xlsm.
- HTML smuggling (file .html tạo payload trên client).
##### Command/Script-based execution
- PowerShell (encoded command, download-execute), WScript (VBScript), mshta, cscript.
##### Fileless / In-memory execution
- Loader tải mã vào bộ nhớ (Reflective DLL, Process Hollowing, RunPE).
##### Living-off-the-land binaries (LOLBins)
- Dùng rundll32, regsvr32, msbuild, wmic, certutil để tải/giải mã payload.
##### Executable drop & run
- Loader viết file .exe vào %APPDATA% hoặc C:\Windows\Temp rồi chạy.
##### Service/driver installation
- Cài đặt service tùy chỉnh hoặc driver (đặc biệt trên máy có quyền high).
##### Scripted scheduled tasks / Persistence
- schtasks /create hoặc Task Scheduler API để chạy payload lúc reboot.
##### DLL side-loading / signed binary abuse
- Đặt DLL độc hại cạnh executable tin cậy (sideloading).
- Abuse signed binaries to run unsigned payload.

<a name="b"></a>
### 2. Privilege Escalation 
#### 2.1 Mục tiêu
- Nâng quyền để phá bỏ giới hạn bảo vệ: thực hiện credential dumping, tắt AV, cài service, truy cập file server/DC.
- Lấy secrets (cleartext/password hashes/kerberos tickets) để lateral movement.
#### 2.2 Kỹ thuật
##### Credential theft / Harvesting
- LSASS memory dump → Mimikatz to extract NTLM/cleartext.
- Credential cache / Windows Vault, dpapi keys exfiltration.
- Web browser credential theft from Chrome/Edge/Firefox local stores.
##### Pass-the-Hash (PtH) / Pass-the-Ticket (PtT)
- Reuse LM/NTLM hashes or Kerberos tickets to authenticate to other hosts.
##### Overpass-the-Hash / Golden Ticket / Silver Ticket
- Forge Kerberos tickets if KRBTGT or service account hash obtained.
##### Exploitation of local vulnerabilities
- Exploit kernel or service vuln to escalate (e.g., local privilege escalation CVE on older Windows).
##### Abuse of misconfigurations / weak privileges
- Writable service binaries, weak ACLs on service executables, unquoted service path, DLL hijacking points.
##### Kerberoasting
- Request service ticket for SPN-bound accounts and offline crack TGS to retrieve plaintext passwords.
##### Token impersonation / Token kidnapping
- Create process with SYSTEM token via SeImpersonatePrivilege or abuse of service to spawn process as SYSTEM.
##### Credential reuse / Lateral credential reuse
- Use harvested credentials to authenticate to remote machines (RDP, SMB, WinRM).
