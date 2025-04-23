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

VeXe (#MaVe,@Bienso, @MaNV,@MaGia,ThoiGianVao, ThoiGianRa, TrangThai) 

GiaVe (#MaGia, LoaiXe, GiaTien) 
## 1.Bảng KhachHang ( khách hàng )
MaKH(PK)
![image](https://github.com/user-attachments/assets/9bc76f27-00c2-46ff-a1a9-dcec52001154)
## 2.Bảng Xe ( thông tin xe )
BienSo(PK)
![image](https://github.com/user-attachments/assets/3d651d46-9c47-4011-9478-cf1a8bf86eb2)
MaKH(FK) Tham chiếu đến bảng KhachHang bằng cột MaKH của bảng Xe và bảng KhachHang 
![image](https://github.com/user-attachments/assets/54610dca-a8cd-449b-a3fb-212328911b2a)
## 3.Bảng NhanVien ( Nhân viên ) 
MaNV(PK)
![image](https://github.com/user-attachments/assets/2efbd7ca-a3bd-48e7-a657-6353c03e8fc5)
## 4.Bảng VeXe ( vé xe )
MaXe(PK)
![image](https://github.com/user-attachments/assets/d8811a51-7871-489f-ad73-245b9363ef66)
BienSo(FK) Tham chiếu đến bảng Xe bằng cột BienSo của bảng VeXe và bảng Xe
![image](https://github.com/user-attachments/assets/87eff472-0662-44e9-bf52-038b92bf323f)
MaNV(FK) Tham chiếu đến bảng NhanVien bằng cột BienSo của bảng VeXe và bảng Xe
![image](https://github.com/user-attachments/assets/b85628c4-98ba-4858-af23-c01d3cd88a4f)
MaGia(FK) Tham chiếu đến bảng GiaVe bằng cột MaGia của bảng VeXe và bảng GiaVe
![image](https://github.com/user-attachments/assets/c9c6b6f2-b8ff-4dd8-a01c-1260e7f882ae)
## 5. Bảng GiaVe ( giá vé )
MaGia(FK)
![image](https://github.com/user-attachments/assets/6ff8b053-9819-4ae5-b967-d1a7bdffb1c7)
# B. Nội dung Bài tập 05:
## 1. Thêm trường phi chuẩn TongTien cho bảng VeXe
![image](https://github.com/user-attachments/assets/de1f9105-236e-47a7-bd25-1403033660f1)
Bảng VeXe sau khi thêm trường phi chuẩn TongTien ( tổng tiền )
![image](https://github.com/user-attachments/assets/9844422b-aa5f-4e24-b697-7006743d2bad)
## 2. Nhập thông tin demo cho các bảng
Bảng KhachHang
![image](https://github.com/user-attachments/assets/f2b1f791-f7bd-4211-b065-b9c787120382)
Bảng NhanVien
![image](https://github.com/user-attachments/assets/1219166a-2d8f-43ed-a501-92ba12e562a2)
Bảng GiaVe
![image](https://github.com/user-attachments/assets/ab495ea0-fd2a-42d5-b16a-0e6772756183)
Bảng Xe
![image](https://github.com/user-attachments/assets/c61fe149-fd77-499a-9655-1ae0c9e925a2)
Bảng VeXe
![image](https://github.com/user-attachments/assets/d210c499-205c-4a1e-b6c5-d004406c50cb)
## 3. Viết trigger cho bảng VeXe
![image](https://github.com/user-attachments/assets/b3cf18f3-4512-4a0f-a662-84a3099c9a83)
code:
```
-- ================================================
-- Template generated from Template Explorer using:
-- Create Trigger (New Menu).SQL
--
-- Use the Specify Values for Template Parameters 
-- command (Ctrl-Shift-M) to fill in the parameter 
-- values below.
--
-- See additional Create Trigger templates for more
-- examples of different Trigger statements.
--
-- This block of comments will not be included in
-- the definition of the function.
-- ================================================
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
-- =============================================
-- Author:		<Lương Văn Học>
-- Create date: <23/4/2025>
-- Description:	<UpdateTongTien cho bảng VeXe>
-- =============================================
CREATE TRIGGER [dbo].[trg_UpdateTongTien]
ON [dbo].[VeXe]
AFTER UPDATE
AS
BEGIN
    SET NOCOUNT ON;

    -- Cập nhật TongTien cho các bản ghi có ThoiGianRa và MaGia hợp lệ
    UPDATE v
    SET v.TongTien = g.GiaTien * DATEDIFF(HOUR, v.ThoiGianVao, v.ThoiGianRa)
    FROM [dbo].[VeXe] v
    INNER JOIN inserted i ON v.MaVe = i.MaVe
    INNER JOIN [dbo].[GiaVe] g ON v.MaGia = g.MaGia
    WHERE i.ThoiGianRa IS NOT NULL
      AND i.ThoiGianRa >= i.ThoiGianVao
      AND i.MaGia IS NOT NULL;

    -- Đặt TongTien = NULL nếu ThoiGianRa hoặc MaGia không hợp lệ
    UPDATE v
    SET v.TongTien = NULL
    FROM [dbo].[VeXe] v
    INNER JOIN inserted i ON v.MaVe = i.MaVe
    WHERE i.ThoiGianRa IS NULL
       OR i.MaGia IS NULL;
END
GO
ALTER TABLE [dbo].[VeXe] ENABLE TRIGGER [trg_UpdateTongTien]
GO
```
## 4. Nhập dữ liệu để test

dòng có MaVe = VE004, ThoiGianVao = 2025-04-23 08:00:00, ThoiGianRa = NULL

thay đổi cột ThoiGianRa thành: 2025-04-23 14:00:00

và MaGia từ NULL->GIA002

Nhấn Enter hoặc di chuyển con trỏ ra ngoài ô để lưu thay đổi.
![image](https://github.com/user-attachments/assets/23b55723-4763-4e95-adf4-aac22a118fb2)
Kết quả sau khi thay đổi
Quan sát giá trị TongTien trong bảng VeXe. Nếu TongTien = 60.00, trigger hoạt động đúng.
![image](https://github.com/user-attachments/assets/78cdb64e-ba5d-4865-b9f4-282af789c76f)
## 5. Kết luận
Trigger trg_UpdateTongTien trong đồ án quản lý bãi gửi xe thông minh tại Đại học Kỹ thuật Công nghiệp Thái Nguyên mang lại các lợi ích chính:
- Tự động hóa: Tự tính TongTien dựa trên GiaTien và thời gian đỗ, giảm thao tác thủ công.
- Nhất quán dữ liệu: Đảm bảo TongTien chính xác, chỉ cập nhật khi ThoiGianRa và MaGia hợp lệ.
- Hiệu quả quản lý: Hỗ trợ thanh toán nhanh, báo cáo doanh thu, cải thiện trải nghiệm người dùng.
- Tiết kiệm chi phí: Giảm công sức lập trình, bảo trì, phù hợp với hệ thống IoT và Smart City.
- Thời gian thực: Tích hợp với cảm biến/camera, giảm tắc nghẽn giao thông.

