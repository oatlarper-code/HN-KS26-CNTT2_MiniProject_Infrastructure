# Bài làm
1. Mô hình IPO (Input – Process – Output):
- Input: Tệp log-he-thong.log phát sinh liên tục từ máy chủ, bảng mã linh kiện, bảng dữ liệu thực địa trạm cảm biến.
- Process: Script auto_report.bat lọc các dòng CRITICAL / ERROR bằng Pipe, lắp đầy khoảng trống (Trim), tự động tìm kiếm thông tin (Vlookup).
- Output: Tệp bao-cao-su-co.txt trong thư mục backup/ dùng để báo cáo.
2. Mô hình DIKW (Data – Information – Knowledge – Wisdom):
- Data: Hàng triệu dòng log thô, chưa có ý nghĩa khi đứng riêng lẻ.
- Information: Các dòng log đã được lọc theo từ khóa lỗi (ERROR 404, TIMEOUT).
- Knowledge: Nhận biết mẫu lỗi lặp lại, trạm nào có tần suất sự cố cao.
- Wisdom: Ra quyết định vận hành — nâng cấp thiết bị, điều chỉnh cấu hình mạng.
3. Kiến trúc cây thư mục 4 trụ cột:

- docs/ — Trụ cột Tài liệu: README, đặc tả kỹ thuật.
- scripts/ — Trụ cột Xử lý: các tệp tự động hóa .bat/.sh.
- data/ — Trụ cột Dữ liệu: log hệ thống, bảng đối soát thiết bị.
- backup/ — Trụ cột Lưu trữ: bản sao báo cáo, phục vụ truy vết.

Thư mục|Nội dung
|-|-|
docs/README.md,srs-he-thong.docx|(Render chuẩn trên GitHub)(Chuẩn Styles & Auto TOC)
scripts/auto_report.bat|(Chạy thành công, không lỗi)
data/quan-ly-thiet-bi.xlxs|(VLOOKUP chạy đúng, không lỗi #N/A)
.env|(File ẩn chứa cấu hình giả định)



- Quy tắc đặt tên
- Sử dụng kebab-case cho tên thư mục và tệp (VD: log-he-thong.log).
- Không sử dụng Tiếng Việt có dấu.
- Không sử dụng khoảng trắng trong tên thư mục/tệp.
- Tệp cấu hình nhạy cảm (.env) phải là tệp ẩn, không commit lên GitHub công khai.


Module 1: Thiết lập "Căn cứ số" (Terminal)
- mkdir docs, scripts, data; ni docs/README.md, docs/srs-he-thong.docs; ni scripts/auto_report.bat; ni data/quan-ly-thiet-bi.xlsx
- cd .; $key=123; $key >> .env
- SSet-ItemProperty .\.env -Name Attributes -Value Hidden

Module 2: Robot lọc Log tự động (Advanced Terminal & Scripting)
```
@echo off
if not exist "..\backup" mkdir "..\backup"
echo ========== > "..\backup\bao-cao-su-co.txt"
echo Hệ thống báo lỗi >> "..\backup\bao-cao-su-co.txt"
echo ========== >> "..\backup\bao-cao-su-co.txt"
echo . >> "..\backup\bao-cao-su-co.txt"
type "..\data\log-he-thong.log" | findstr /I /C:"CRITICAL" /C:"ERROR" >> "..\backup\bao-cao-su-co.txt"
echo Hoàn tất! Kết quả lưu tại: backup\bao-cao-su-co.txt
```

5. Ràng buộc dữ liệu & Bẫy dữ liệu

- Giải pháp Terminal: toàn bộ cấu trúc tuân thủ theo kebab-case
- Giải pháp Script: Áp dụng lệnh điều kiện trước khi thực thi lệnh và dùng cơ chế ghi đè để đảm bảo dữ liệu vẫn còn trước đó lưu tiếp tục vào tài liệu mới
- Giải pháp Excel: Mỗi cột là dữ liệu (Field) còn mỗi hàng là (Record), vùng dữ liệu chứa hàng trống hoặc ô Merge Cell sẽ làm AutoFilter hoạt động sai, kết hợp hàm lệnh Trim và VLookup để đảm bảo các khoảng trống được lắp đầy và có thông tin chuẩn xác rõ ràng
- Giải pháp Hardware: 1 byte = 8 bits, 1 MB = 1024B, Tốc độ truyền tải (MB/s)=Tốc độ mạng(Mbps)/8 

