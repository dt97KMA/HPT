> Tên tài liệu: _AES_  
> Thực hiện: _Dat_  
> Cập nhật lần cuối: _25/08/2025_
## Mục lục:
1. [RSA](#a)
2. [Type of RSA](#b)

## Nội dung
<a name="a"></a>
### 1. RSA
#### Asymmetric ( mã hóa bất đối xứng)
- Mã hóa bất đối xứng sử dụng hai khóa khác nhau, một khóa công khai và một khóa riêng tư. Khóa công khai được chia sẻ với mọi người, trong khi khóa riêng tư được giữ bí mật bởi người sở hữu. Mã hóa bất đối xứng thường được sử dụng cho các ứng dụng yêu cầu tính bảo mật cao, chẳng hạn như xác thực và ký điện tử. Vd: RSA (Rivest–Shamir–Adleman),...
- Đặc điểm:
    - Khóa: Mã hóa bất đối xứng sử dụng hai khóa khác nhau, một khóa công khai và một khóa riêng tư. Khóa công khai được chia sẻ với mọi người, trong khi khóa riêng tư được giữ bí mật bởi người sở hữu.
    - Tính bảo mật: Tính bảo mật của mã hóa bất đối xứng phụ thuộc vào độ phức tạp của thuật toán mã hóa và độ dài của khóa. Khóa càng dài và thuật toán mã hóa càng phức tạp thì càng khó để bẻ khóa.
    - Tốc độ: Mã hóa bất đối xứng thường chậm hơn mã hóa đối xứng. Điều này là do mã hóa bất đối xứng cần sử dụng hai khóa, trong khi mã hóa đối xứng chỉ cần sử dụng một khóa.
    - Ứng dụng: Mã hóa bất đối xứng thường được sử dụng cho các ứng dụng yêu cầu tính bảo mật cao, chẳng hạn như xác thực và ký điện tử.
- Ưu điểm:
  - Tính bảo mật cao.
  - Không cần chia sẻ khóa.
  - Có thể sử dụng cho các ứng dụng yêu cầu xác thực và ký điện tử.
- Nhược điểm:
  - Tốc độ chậm.
  - Yêu cầu phần cứng và phần mềm mạnh mẽ hơn.

 #### RSA
 ##### Khái niệm
- RSA là một thuật toán mật mã hóa khóa công khai. Đây là thuật toán đầu tiên phù hợp với việc tạo ra chữ ký điện tử đồng thời với việc mã hóa. Nó đánh dấu một sự tiến bộ vượt bậc của lĩnh vực mật mã học trong việc sử dụng khóa công cộng. RSA đang được sử dụng phổ biến trong thương mại điện tử và được cho là đảm bảo an toàn với điều kiện độ dài khóa đủ lớn. RSA là một thuật toán mã hóa bất đối xứng, nó sử dụng hai khóa riêng biệt để mã hóa và giải mã dữ liệu. Khóa công khai được chia sẻ với công chúng, trong khi khóa bí mật được giữ bí mật.
##### Cách hoạt động:
- Chọn Số Nguyên Tố:
  - Chọn hai số nguyên tố lớn ngẫu nhiên, đặt chúng là p và q.
  - Tính n = pxq. n là một số nguyên dương lớn và được sử dụng làm phần công khai của khóa.
- Tính Hàm Euler:
  - Tính hàm Euler của n, ký hiệu là φ(n) . Đối với n = p.q , φ(n) = (p − 1) (q − 1).
- Chọn Số E:
  - Chọn một số nguyên dương e sao cho 1 < e < φ(n) và d(e, φ(n))= 1. Số e được chọn làm phần công khai của khóa.
- Tính Số D:
  - Tìm số nguyên d sao cho d.e = 1 mod (φ(n)). Số d được chọn làm phần bí mật của khóa.
- Tạo Khóa Công Khai và Bí Mật:
  - Khóa công khai là cặp (n, e).
  - Khóa bí mật là cặp (n, d).
- Mã Hóa và Giải Mã:
  - Mã hóa: Tìm c từ m thông qua công thức c ≡ m^e (mod n).
  - Giải mã: Tìm m từ c thông qua công thức m ≡ c^d (mod n).
