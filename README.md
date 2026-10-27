# 1. Terminal (Khởi tạo dự án)
### DOS
:: Tạo toàn bộ cây thư mục lồng nhau trong 01 dòng lệnh
mkdir greentech-system\docs greentech-system\scripts greentech-system\data greentech-system\backup

:: Di chuyển tương đối và tạo file ẩn .env
cd greentech-system
echo DB_PASSWORD=SecretGreenTech2026! > .env
attrib +h .env
# 2. Script lọc Log (scripts/auto_report.bat)
### DOS
@echo off
chcp 65001 > nul
echo ==================================================== > ..\backup\bao-cao-su-co.txt
echo          BAO CAO SU CO HE THONG GREENTECH          >> ..\backup\bao-cao-su-co.txt
echo          Thoi gian: %DATE% %TIME%                  >> ..\backup\bao-cao-su-co.txt
echo ==================================================== >> ..\backup\bao-cao-su-co.txt
echo. >> ..\backup\bao-cao-su-co.txt

:: Dùng Pipe (|) lọc log 500MB trực tiếp, không tràn RAM
type ..\data\log-he-thong.log | findstr /i "CRITICAL ERROR TIMEOUT" >> ..\backup\bao-cao-su-co.txt

:: Audit: An toàn hệ thống (KHÔNG dùng: del /f /s /q)
echo. >> ..\backup\bao-cao-su-co.txt
echo [AUDIT SUCCESS]: Hoan tat trich xuat log. >> ..\backup\bao-cao-su-co.txt
# 3. Tài liệu Kỹ thuật
File docs/README.md
Markdown
# Hệ Thống Quản Trị Hạ Tầng GreenTech

## Hướng dẫn vận hành
```cmd
cd scripts
auto_report.bat
Checklist kiểm tra trạm IoT
•	[ ] Kiểm tra kết nối mạng (3G/4G/LoRa)
•	[ ] Xác thực dung lượng RAM và SSD
•	[ ] Kiểm tra báo cáo lỗi tại backup/bao-cao-su-co.txt
Bảng thông số phần cứng
Mã Linh Kiện	Tên Thiết Bị	Loại Storage	Đơn Giá (VNĐ)
CPU-I7-GEN13	Intel Core i7 13700K	N/A	9,500,000
SSD-NVME-1TB	Samsung 980 Pro 1TB	SSD	2,200,000

#### **Quy chuẩn `docs/srs-he-thong.docx`**
* **Heading Styles:** Gán **Heading 1** (Chương), **Heading 2** (Mục lớn), **Heading 3** (Mục nhỏ).
* **Auto TOC:** Trang 1 $\rightarrow$ **References** $\rightarrow$ **Table of Contents** $\rightarrow$ **Automatic Table 1**.

---

### **4. Công thức Excel (`data/quan-ly-thiet-bi.xlsx`)**

Tại Sheet `trang-thai-tram`, nhập công thức điền `ten_thiet_bi`:

$$=VLOOKUP(TRIM(B2), 'danh-muc-linh-kien'!$A$2:$D$100, 2, FALSE)$$

* **TRIM(B2):** Loại bỏ khoảng trắng thừa gây lỗi `#N/A`.
* **`$A$2:$D$100`:** Khóa cố định vùng tra cứu.
* **Bẫy Excel:** Không để hàng trống, không dùng **Merge Cell** để **AutoFilter** hoạt động đúng.

---

### **5. Bẫy Hardware (Thời gian tải Log)**

File log **500 MB**, mạng **100 Mbps**:
* Tốc độ thực tế: $\frac{100 \text{ Mbps}}{8} = 12.5 \text{ MB/s}$
* Thời gian tải: $\frac{500 \text{ MB}}{12.5 \text{ MB/s}} = 40 \text{ giây}$

---

### **6. Cấu trúc GitHub Repository**

```text
[TênLớp]_[MônHọc]_MiniProject_GreenTech/
├── docs/
│   ├── README.md
│   └── srs-he-thong.docx
├── scripts/
│   └── auto_report.bat
├── data/
│   ├── log-he-thong.log
│   └── quan-ly-thiet-bi.xlsx
├── backup/
│   └── bao-cao-su-co.txt
└── .env

