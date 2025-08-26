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
- Artifact: Office MRU, RecentDocs, Prefetch của WINWORD/EXCEL, created temp files (C:\Users\<user>\AppData\Local\Temp\*).
##### Command/Script-based execution
- PowerShell (encoded command, download-execute), WScript (VBScript), mshta, cscript.
- Artifact: PowerShell operational logs, ScriptBlock logging, Sysmon EventID 1 with suspicious commandline.
##### Fileless / In-memory execution
- Loader tải mã vào bộ nhớ (Reflective DLL, Process Hollowing, RunPE).
- Artifact: Ít file trên disk; cần memory dump, Volatility/rekall analysis; anomalous remote thread creation, unusual module loads via Sysmon EventID 8/10.
##### Living-off-the-land binaries (LOLBins)
- Dùng rundll32, regsvr32, msbuild, wmic, certutil để tải/giải mã payload.
- Artifact: rundll32.exe / certutil.exe spawn với network I/O; check commandline for base64, -encoded, download URL.
##### Executable drop & run
- Loader viết file .exe vào %APPDATA% hoặc C:\Windows\Temp rồi chạy.
- Artifact: new executable hash, MFT records, Prefetch, Windows Defender events.
##### Service/driver installation
- Cài đặt service tùy chỉnh hoặc driver (đặc biệt trên máy có quyền high).
- Artifact: sc create, Service Control Manager logs, service binary path info.
##### Scripted scheduled tasks / Persistence
- schtasks /create hoặc Task Scheduler API để chạy payload lúc reboot.
- Artifact: Task XML in C:\Windows\System32\Tasks, TaskScheduler logs.
##### DLL side-loading / signed binary abuse
- Đặt DLL độc hại cạnh executable tin cậy (sideloading).
- Abuse signed binaries to run unsigned payload.
- Artifact: unusual DLL search order loads, signed exe spawning unsigned child.

<a name="b"></a>
### 2. Privilege Escalation 
#### 2.1 Mục tiêu
- Nâng quyền để phá bỏ giới hạn bảo vệ: thực hiện credential dumping, tắt AV, cài service, truy cập file server/DC.
- Lấy secrets (cleartext/password hashes/kerberos tickets) để lateral movement.
#### 2.2 Kỹ thuật
##### Credential theft / Harvesting
- LSASS memory dump → Mimikatz to extract NTLM/cleartext.
  - Artifact: procdump.exe or comsvcs.dll usage; Sysmon EventID 10 ProcessAccess where LSASS accessed.
- Credential cache / Windows Vault, dpapi keys exfiltration.
- Web browser credential theft from Chrome/Edge/Firefox local stores.
##### Pass-the-Hash (PtH) / Pass-the-Ticket (PtT)
- Reuse LM/NTLM hashes or Kerberos tickets to authenticate to other hosts.
- Artifact: EventID 4624 with Logon Type 3 (network) using NTLM where service account used atypically; unusual Kerberos TGT requests.
##### Overpass-the-Hash / Golden Ticket / Silver Ticket
- Forge Kerberos tickets if KRBTGT or service account hash obtained.
- Artifact: Unusual TGT lifetime, anomalies in Kerberos authentication logs, suspicious ticket properties.
##### Exploitation of local vulnerabilities
- Exploit kernel or service vuln to escalate (e.g., local privilege escalation CVE on older Windows).
- Artifact: Crash logs, new unsigned driver loads, suspicious kernel-mode drivers.
##### Abuse of misconfigurations / weak privileges
- Writable service binaries, weak ACLs on service executables, unquoted service path, DLL hijacking points.
- Artifact: Service configuration showing ImagePath pointing to suspicious path; file ACLs changed.
##### Kerberoasting
- Request service ticket for SPN-bound accounts and offline crack TGS to retrieve plaintext passwords.
- Artifact: High volume of TGS requests for service accounts, tickets with RC4 encryption.
##### Token impersonation / Token kidnapping
- Create process with SYSTEM token via SeImpersonatePrivilege or abuse of service to spawn process as SYSTEM.
- Artifact: Process creation events with elevated token but no corresponding logon event.
##### Credential reuse / Lateral credential reuse
- Use harvested credentials to authenticate to remote machines (RDP, SMB, WinRM).
- Artifact: Successful logons from unusual source hosts/accounts, event sequences: credential dump → remote logon.
