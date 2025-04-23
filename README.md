# Họ và tên sinh viên: Lương Văn Học - MSSV: K225480106025
# BÀI TẬP VỀ NHÀ 05, Môn Hệ quản trị csdl.
# SUBJECT: Trigger on mssql
# A. Trình bày lại đầu bài của đồ án PT&TKHT:
1. Mô tả bài toán của đồ án PT&TKHT, 
   đưa ra yêu cầu của bài toán đó
2. Cơ sở dữ liệu của Đồ án PT&TKHT :
   Có database với các bảng dữ liệu cần thiết (3nf),
   Các bảng này đã có PK, FK, CK cần thiết
   
# B. Nội dung Bài tập 05:
1. Dựa trên cơ sở là csdl của Đồ án
2. Tìm cách bổ xung thêm 1 (hoặc vài) trường phi chuẩn
   (là trường tính toán đc, nhưng thêm vào thì ok hơn,
    ok hơn theo 1 logic nào đó, vd ok hơn về speed)
   => Nêu rõ logic này!
3. Viết trigger cho 1 bảng nào đó, 
   mà có sử dụng trường phi chuẩn này,
   nhằm đạt được 1 vài mục tiêu nào đó.
   => Nêu rõ các mục tiêu 
4. Nhập dữ liệu có kiểm soát, 
   nhằm để test sự hiệu quả của việc trigger auto run.
5. Kết luận về Trigger đã giúp gì cho đồ án của em.
# Bài làm: 
# A. Phân tích và thiết kế hệ thống quản lý bãi gửi xe thông minh tại trường Đại học kỹ thuật Công nghiệp Thái Nguyên
## 1. Mô tả bài toán
Hệ thống quản lý bãi gửi xe thông minh được thiết kế nhằm tự động hóa và tối ưu hóa quy trình quản lý bãi gửi xe tại trường Đại học Kỹ thuật Công nghiệp Thái Nguyên. Hiện tại, việc quản lý bãi gửi xe thường được thực hiện thủ công (ghi vé giấy, kiểm tra bằng tay), dẫn đến các vấn đề như mất thời gian, sai sót, khó kiểm soát lượng xe ra vào, và thiếu thông tin thống kê. Hệ thống thông minh sẽ sử dụng công nghệ hiện đại (như nhận diện biển số, thẻ RFID, cảm biến, hoặc ứng dụng di động) để quản lý việc ra vào của xe, lưu trữ thông tin, và cung cấp báo cáo chi tiết.
## 2. Yêu cầu bài toán
Hệ thống quản lý bãi gửi xe thông minh tại trường Đại học Kỹ thuật Công nghiệp Thái Nguyên nhằm tự động hóa quy trình, thay thế phương pháp thủ công, đảm bảo an toàn, chính xác và nâng cao trải nghiệm người dùng. Yêu cầu chức năng: Nhận diện xe tự động (biển số, RFID), quản lý vé điện tử, theo dõi chỗ trống, quản lý người dùng, thống kê, báo cáo, tích hợp ứng dụng di động. Yêu cầu phi chức năng: Xử lý nhanh (<5 giây), hoạt động 24/7, bảo mật, dễ mở rộng, giao diện thân thiện. Yêu cầu kỹ thuật: Camera, cảm biến, máy chủ, cơ sở dữ liệu, kết nối mạng ổn định. Hệ thống triển khai trong 3-6 tháng, chi phí hợp lý, kèm đào tạo và bảo trì.
# B. Cơ sở dữ liệu của hệ thống quản lý bãi gửi xe thông minh 
Bảng 3NF:
KhachHang(#MaKH, HoTen, SoDienThoai, DiaChi) 
Xe(#BienSo, @MaKH,LoaiXe) 
NhanVien (#MaNV,HoTen,SoDienThoai) 
VeXe (#MaVe,@Bienso, @MaNV,ThoiGianVao, ThoiGianRa, TrangThai) 
GiaVe (#MaGia, LoaiXe, GiaTien) 
## 1.Bảng KhachHang ( khách hàng )
MaKH(PK)
![image](https://github.com/user-attachments/assets/9bc76f27-00c2-46ff-a1a9-dcec52001154)
## 2.Bảng Xe ( thông tin xe )
BienSo(PK)
![image](https://github.com/user-attachments/assets/3d651d46-9c47-4011-9478-cf1a8bf86eb2)
MaKH(FK) 
![image](https://github.com/user-attachments/assets/54610dca-a8cd-449b-a3fb-212328911b2a)


