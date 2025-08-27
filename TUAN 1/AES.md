> Tên tài liệu: _AES_  
> Thực hiện: _Dat_  
> Cập nhật lần cuối: _25/08/2025_
## Mục lục:
1. [AES](#a)
2. [Type of AES](#b)

## Nội dung
<a name="a"></a>
### 1. AES
#### Symmetric ( mã hóa đối xứng)
- Mã hóa đối xứng sử dụng cùng một khóa để mã hóa và giải mã thông tin. Khóa này được chia sẻ giữa người gửi và người nhận. Mã hóa đối xứng thường được sử dụng cho các ứng dụng yêu cầu tốc độ cao, chẳng hạn như mã hóa dữ liệu lưu trữ hoặc mã hóa kết nối mạng.
- Đặc điểm:
  - Khóa: Mã hóa đối xứng sử dụng cùng một khóa để mã hóa và giải mã thông tin. Khóa này được chia sẻ giữa người gửi và người nhận.
  - Tính bảo mật: Tính bảo mật của mã hóa đối xứng phụ thuộc vào độ dài của khóa. Khóa càng dài thì càng khó để bẻ khóa.
  - Tốc độ: Mã hóa đối xứng thường nhanh hơn mã hóa bất đối xứng. Điều này là do mã hóa đối xứng chỉ cần sử dụng một khóa, trong khi mã hóa bất đối xứng cần sử dụng hai khóa.
  - Ứng dụng: Mã hóa đối xứng thường được sử dụng cho các ứng dụng yêu cầu tốc độ cao, chẳng hạn như mã hóa dữ liệu lưu trữ hoặc mã hóa kết nối mạng.
- Ưu điểm:
  - Tốc độ nhanh.
  - Dễ triển khai.
  - Yêu cầu phần cứng và phần mềm đơn giản.
- Nhược điểm:
  - Tính bảo mật thấp hơn mã hóa bất đối xứng.
  - Yêu cầu chia sẻ khóa giữa người gửi và người nhận.

#### Block Cipher 
- Block cipher là thuật toán mã hóa chia nhỏ dữ liệu thành các khối cố định kích thước và mã hóa từng khối một. Kích thước khối thường là 64 hoặc 128 bit.
- Đặc điểm của block cipher:
  - Cách thức mã hóa dữ liệu: Block cipher chia dữ liệu thành các khối cố định kích thước, thường là 64 hoặc 128 bit. Mỗi khối được mã hóa độc lập với các khối khác.
  - Kích thước khối: Kích thước khối là một thông số quan trọng của thuật toán block cipher. Kích thước khối càng lớn thì khả năng kháng lại tấn công bằng lực brute càng cao. Tuy nhiên, kích thước khối lớn cũng làm giảm tốc độ mã hóa.
  - Tốc độ: Block cipher thường chậm hơn stream cipher. Điều này là do block cipher cần xử lý từng khối dữ liệu một, trong khi stream cipher có thể mã hóa từng bit dữ liệu một.
  - Ứng dụng: Block cipher thường được sử dụng cho các ứng dụng yêu cầu tính bảo mật cao, chẳng hạn như mã hóa dữ liệu lưu trữ và truyền tải.
- Các bước mã hóa dữ liệu bằng block cipher:
  - Chia dữ liệu thành các khối cố định kích thước.
  - Sử dụng khóa để mã hóa từng khối dữ liệu.
  - Ghép các khối dữ liệu đã được mã hóa lại với nhau để tạo thành bản mã.
- Các bước giải mã dữ liệu bằng block cipher:
  - Chia bản mã thành các khối cố định kích thước.
  - Sử dụng khóa để giải mã từng khối dữ liệu.
  - Ghép các khối dữ liệu đã được giải mã lại với nhau để tạo thành bản rõ.
- Ưu điểm của block cipher:
  - Tính bảo mật cao.
  - Có thể chống lại các tấn công bằng brute.
  - Có thể được sử dụng cho các ứng dụng yêu cầu tính bảo mật cao.
- Nhược điểm của block cipher:
  - Tốc độ chậm hơn stream cipher.
  - Yêu cầu phần cứng và phần mềm mạnh mẽ.

 #### AES
- Trong mật mã học, Advanced Encryption Standard( nghĩa là tiêu chuẩn mã hóa tiên tiến) là một thuật toán mã hóa khối. AES sử dụng mạng thay thế- hoán vị.
- Số vòng trong AES có thể thay đổi và phụ thuộc vào độ dài của khóa. AES sử dụng 10 vòng cho các phím 128 bit, 12 vòng cho các phím 192 bit và 14 vòng cho các phím 256 bit. Mỗi vòng này sử dụng một khóa tròn 128 bit khác nhau, được tính từ khóa AES ban đầu.
- Sơ đồ cấu trúc của AES được miêu tả như sau:

<img width="794" height="543" alt="68747470733a2f2f6861636b6d642e696f2f5f75706c6f6164732f4831366f41527639612e706e67" src="https://github.com/user-attachments/assets/0d7c6e32-b6b1-4089-a09d-46db6b0b495d" />

##### Mã hóa
- AES sẽ lấy khối dữ liệu 128 bits từ plaintext thành 16 bytes để xếp thành ma trận 4x4.
- 1.Khởi động vòng lặp
  - AddRoundKey — Mỗi cột của trạng thái đầu tiên lần lượt được kết hợp với một khóa con theo thứ tự từ đầu dãy khóa.
- 2.Vòng lặp
  - SubBytes — đây là phép thế (phi tuyến) trong đó mỗi byte trong trạng thái sẽ được thế bằng một byte khác theo bảng tra (Rijndael S-box).
  - ShiftRows — dịch chuyển, các hàng trong trạng thái được dịch vòng theo số bước khác nhau.
  - MixColumns — quá trình trộn làm việc theo các cột trong khối theo một phép biến đổi tuyến tính.
  - AddRoundKey
- 3.Vòng lặp cuối
  - SubBytes
  - ShiftRows
  - AddRoundKey
- Tại chu trình cuối thì bước MixColumns không thực hiện.
##### Mô tả chi tiết 
- AES sẽ lấy khối dữ liệu 128 bits từ plaintext thành 16 bytes để xếp thành ma trận 4x4.

<img width="854" height="549" alt="68747470733a2f2f6861636b6d642e696f2f5f75706c6f6164732f536b75682d315f63702e706e67" src="https://github.com/user-attachments/assets/6585c4cc-a243-4e16-b8f7-5560560f3656" />

- Quá trình mã hóa của một vòng gồm 4 quy trình SubBytes, ShiftRows, MixColumns, AddRoundKey.

<img width="521" height="391" alt="68747470733a2f2f6861636b6d642e696f2f5f75706c6f6164732f423131566b796439542e706e67" src="https://github.com/user-attachments/assets/0f21241a-4228-42eb-b59e-bdfa8c9aefe6" />

- SubBytes: 16 bytes đầu vào được thay thế bằng cách tra cứu một bảng cố định (hộp S) được đưa ra trong thiết kế.

<img width="480" height="233" alt="68747470733a2f2f6861636b6d642e696f2f5f75706c6f6164732f424a636c474a6463362e706e67" src="https://github.com/user-attachments/assets/23915ed3-6132-4d71-bc1d-90b1bb499303" />

<img width="640" height="600" alt="68747470733a2f2f6861636b6d642e696f2f5f75706c6f6164732f724a7362554a7563612e706e67" src="https://github.com/user-attachments/assets/66da74e3-d10e-4ae8-88b5-d73806258540" />

- Shiftrows
  - Mỗi hàng trong số bốn hàng của ma trận được chuyển sang trái. Bất kỳ mục nào 'rơi ra' sẽ được chèn lại ở phía bên phải của hàng.
  - Hàng đầu tiên không bị dịch chuyển.
  - Hàng thứ hai được dịch chuyển một (byte) vị trí sang trái.
  - Hàng thứ ba được chuyển hai vị trí sang trái.
  - Hàng thứ tư được chuyển ba vị trí sang trái.
  - Kết quả là một ma trận mới bao gồm 16 byte giống nhau nhưng được dịch chuyển đối với nhau.

<img width="480" height="178" alt="68747470733a2f2f6861636b6d642e696f2f5f75706c6f6164732f726b386b514a4f71362e706e67" src="https://github.com/user-attachments/assets/5f061ccc-b2e4-486e-a050-a0e2f01b7f8c" />

- MixColumns: Bước này về cơ bản là phép nhân ma trận. Mỗi cột được nhân với một ma trận cụ thể và do đó vị trí của mỗi byte trong cột được thay đổi. Bước này được bỏ qua ở vòng cuối cùng.

<img width="480" height="255" alt="68747470733a2f2f6861636b6d642e696f2f5f75706c6f6164732f5331655f496b6471702e706e67" src="https://github.com/user-attachments/assets/ddf940f3-a0ce-4bf1-81d4-8f037d793ca5" />

- Addroundkey: Trong thao tác AddRoundKey, 128 bit của ma trận state sẽ được XOR với 128 bit của khóa con của từng vòng. Vì sử dụng phép XOR nên phép biến đổi ngược của AddRoundKey trong cấu trúc giải mã cũng chính là AddRoundKey. Việc kết hợp với khóa bí mật tạo ra tính làm rối (confusion) của mã hóa. Sự phức tạp của thao tác mở rộng khóa (KeySchedule) giúp gia tăng tính làm rối này.

<img width="512" height="398" alt="68747470733a2f2f6861636b6d642e696f2f5f75706c6f6164732f486b6c646e614f71702e706e67" src="https://github.com/user-attachments/assets/6bbf1e3d-ab45-45db-979b-68a6f4f06900" />

##### Giải mã 
- Quá trình giải mã của một bản mã AES tương tự như quá trình mã hóa theo thứ tự ngược lại. Mỗi vòng bao gồm bốn quy trình được tiến hành theo thứ tự ngược lại:
  - AddRoundKey.
  - Inverse MixColumns.
  - ShiftRows.
  - Inverse SubBytes.

<img width="418" height="640" alt="68747470733a2f2f6861636b6d642e696f2f5f75706c6f6164732f7279347652545f71542e706e67" src="https://github.com/user-attachments/assets/7c54bcd3-3cc7-432e-b8d6-9fd9a1e34c44" />

<a name="b"></a>
### 2. Type of AES
#### ECB
<img width="975" height="937" alt="image" src="https://github.com/user-attachments/assets/33a328fc-cec1-4ffb-8ba2-bdcd56d44238" />

#### CBC
<img width="975" height="950" alt="image" src="https://github.com/user-attachments/assets/09ba353e-3bfc-4545-bc0a-1a4414d39346" />
