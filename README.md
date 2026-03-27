# 💧 Hệ Thống Giám Sát Mực Nước
### *Water Level Monitoring System*

<div align="center">

![Status](https://img.shields.io/badge/Trạng%20thái-Đang%20phát%20triển-yellow?style=for-the-badge)
![Platform](https://img.shields.io/badge/Nền%20tảng-_%5BVĐK%5D_-blue?style=for-the-badge)
![Language](https://img.shields.io/badge/Ngôn%20ngữ-C%2FC%2B%2B-brightgreen?style=for-the-badge)
![License](https://img.shields.io/badge/License-MIT-red?style=for-the-badge)

</div>

---

## 📋 Mục Lục

- [Giới thiệu](#-giới-thiệu)
- [Tính năng](#-tính-năng)
- [Phần cứng](#-phần-cứng)
- [Sơ đồ kết nối](#-sơ-đồ-kết-nối)
- [Cấu trúc thư mục](#-cấu-trúc-thư-mục)
- [Cài đặt & Nạp code](#-cài-đặt--nạp-code)
- [Hướng dẫn sử dụng](#-hướng-dẫn-sử-dụng)
- [Lưu đồ thuật toán](#-lưu-đồ-thuật-toán)
- [Nhóm thực hiện](#-nhóm-thực-hiện)
- [Giấy phép](#-giấy-phép)

---

## 🎯 Giới Thiệu

Đây là đồ án môn học **Vi xử lý – Vi điều khiển**, thực hiện xây dựng một hệ thống nhúng có khả năng **giám sát và cảnh báo mực nước theo thời gian thực**.

Hệ thống ứng dụng thực tế trong các bài toán:
- Giám sát bể chứa nước sinh hoạt
- Cảnh báo lũ lụt / ngập úng
- Kiểm soát mực nước trong hệ thống tưới tiêu tự động

> **Môn học:** Vi xử lý – Vi điều khiển  
> **Học kỳ:** `[Học kỳ X – Năm học XXXX–XXXX]`  
> **Trường:** `[Tên trường đại học]`  
> **Khoa/Bộ môn:** `[Tên khoa]`  
> **Giáo viên hướng dẫn:** `[Tên GVHD]`

---

## ✨ Tính Năng

| # | Tính năng | Mô tả | Trạng thái |
|---|-----------|-------|------------|
| 1 | 📏 **Đo mực nước** | Đọc dữ liệu từ cảm biến, tính toán mực nước hiện tại | ✅ |
| 2 | 🖥️ **Hiển thị real-time** | Hiển thị mực nước lên màn hình/thiết bị đầu ra | ✅ |
| 3 | 🚨 **Cảnh báo tràn** | Kích hoạt cảnh báo khi mực nước vượt ngưỡng cài đặt | ✅ |
| 4 | 💾 **Lưu EEPROM** | Lưu ngưỡng cảnh báo vào EEPROM, khôi phục khi mất điện | ✅ |

---

## 🔧 Phần Cứng

### Danh sách linh kiện

| Linh kiện | Mô tả | Số lượng |
|-----------|-------|----------|
| `[Tên vi điều khiển]` | Vi điều khiển trung tâm | 1 |
| `[Tên cảm biến]` | Cảm biến đo mực nước | 1 |
| `[Màn hình/LED]` | Thiết bị hiển thị | 1 |
| Buzzer | Còi cảnh báo | 1 |
| EEPROM (tích hợp / ngoài) | Lưu trữ dữ liệu | 1 |
| Nguồn DC | Cấp nguồn hệ thống | 1 |
| Điện trở, tụ điện, dây nối | Linh kiện bổ trợ | — |

> 📌 **Ghi chú:** Cập nhật bảng linh kiện chi tiết sau khi phần cứng được chốt.

---

## 🔌 Sơ Đồ Kết Nối

```
┌─────────────────────────────────────────────────┐
│                                                 │
│   [Cảm biến]  ──────►  [Vi điều khiển]          │
│                              │                  │
│                    ┌─────────┼──────────┐        │
│                    │         │          │        │
│               [Màn hình]  [Buzzer]  [EEPROM]    │
│                                                 │
└─────────────────────────────────────────────────┘
```

> 📐 *Sơ đồ nguyên lý (schematic) và sơ đồ mạch in (PCB/breadboard) chi tiết xem tại thư mục [`/hardware`](./hardware/).*

---

## 📁 Cấu Trúc Thư Mục

```
water-level-monitoring/
│
├── 📂 src/                        # Source code chính
│   ├── main.c / main.ino          # Chương trình chính
│   ├── sensor.c / sensor.h        # Driver đọc cảm biến
│   ├── display.c / display.h      # Điều khiển hiển thị
│   ├── eeprom.c / eeprom.h        # Đọc/ghi EEPROM
│   └── alert.c / alert.h          # Xử lý cảnh báo
│
├── 📂 hardware/                   # Tài liệu phần cứng
│   ├── schematic.pdf              # Sơ đồ nguyên lý
│   ├── breadboard_layout.png      # Sơ đồ kết nối thực tế
│   └── components_list.xlsx       # Danh sách linh kiện
│
├── 📂 docs/                       # Tài liệu đề tài
│   ├── baocao.pdf                 # Báo cáo đồ án
│   ├── thuyet_minh.docx           # Thuyết minh đề tài
│   └── flowchart.png              # Lưu đồ thuật toán
│
├── 📂 images/                     # Ảnh demo / mô hình
│   ├── hardware_photo.jpg         # Ảnh mô hình thực tế
│   └── demo_screenshot.jpg        # Ảnh màn hình demo
│
├── 📄 README.md                   # File này
└── 📄 LICENSE                     # Giấy phép
```

---

## 🚀 Cài Đặt & Nạp Code

### Yêu cầu môi trường

- **IDE:** `[Arduino IDE / Keil uVision / STM32CubeIDE / MPLAB X]` *(cập nhật sau)*
- **Compiler/Toolchain:** `[Phiên bản]`
- **Thư viện phụ thuộc:**
  - `[Tên thư viện 1]` — `[Mục đích]`
  - `[Tên thư viện 2]` — `[Mục đích]`

### Các bước thực hiện

**Bước 1 — Clone repository**
```bash
git clone https://github.com/[username]/water-level-monitoring.git
cd water-level-monitoring
```

**Bước 2 — Mở project**
```
Mở file src/main.c (hoặc main.ino) bằng IDE phù hợp
```

**Bước 3 — Cấu hình thông số** *(trong file `src/main.c`)*
```c
#define WATER_LEVEL_MAX   100   // Chiều cao bể (cm)
#define THRESHOLD_ALERT   80    // Ngưỡng cảnh báo tràn (%)
#define EEPROM_ADDR       0x00  // Địa chỉ EEPROM lưu cấu hình
```

**Bước 4 — Build & Nạp code**
```
1. Kết nối vi điều khiển với máy tính qua cáp nạp
2. Chọn đúng cổng COM / giao thức nạp
3. Build → Flash vào vi điều khiển
```

---

## 📖 Hướng Dẫn Sử Dụng

```
1. Cấp nguồn cho hệ thống
   → Vi điều khiển khởi động, đọc cấu hình từ EEPROM

2. Hệ thống tự động đo mực nước định kỳ
   → Kết quả hiển thị trên [màn hình]

3. Khi mực nước ≥ ngưỡng cảnh báo:
   → Buzzer kêu / đèn LED cảnh báo sáng

4. Khi mất điện và khởi động lại:
   → Hệ thống tự động phục hồi cấu hình từ EEPROM
   → Hoạt động bình thường, không cần cài đặt lại
```

---

## 🔄 Lưu Đồ Thuật Toán

```
        ┌──────────────┐
        │   Khởi động  │
        └──────┬───────┘
               │
        ┌──────▼───────────────┐
        │  Đọc cấu hình EEPROM │
        └──────┬───────────────┘
               │
        ┌──────▼───────────────┐
        │   Đọc cảm biến       │◄──────────────┐
        └──────┬───────────────┘               │
               │                               │
        ┌──────▼───────────────┐               │
        │  Tính toán mực nước  │               │
        └──────┬───────────────┘               │
               │                               │
        ┌──────▼───────────────┐               │
        │   Hiển thị kết quả   │               │
        └──────┬───────────────┘               │
               │                               │
        ┌──────▼────────────┐                  │
        │ Mực nước ≥ ngưỡng?│                  │
        └──┬────────────┬───┘                  │
           │ CÓ         │ KHÔNG                │
    ┌──────▼──────┐     └──────────────────────┘
    │ Kích hoạt   │
    │ cảnh báo    │
    └──────┬──────┘
           │
    ┌──────▼──────────────┐
    │ Lưu trạng thái      │
    │ vào EEPROM          │
    └──────┬──────────────┘
           │
           └──────────────────────────────────►(Lặp lại)
```

> 📄 *Lưu đồ chi tiết đầy đủ xem tại [`/docs/flowchart.png`](./docs/flowchart.png)*

---

## 👥 Nhóm Thực Hiện

| STT | Họ và tên | MSSV | Vai trò |
|-----|-----------|------|---------|
| 1 | `Dương Gia Bảo` | `23520097` | Nhóm trưởng – `[Phân công]` |
| 2 | `Huỳnh Trịnh Ý` | `21522817` | Thành viên – `[Phân công]` |
| 3 | `Lê Phan Thanh Bình` | `23520154` | Thành viên – `[Phân công]` |

> 📌 *Điền đầy đủ thông tin nhóm trước khi nộp / public repo.*

---

## 📅 Tiến Độ Dự Án

- [x] Lên ý tưởng & xác định yêu cầu
- [ ] Chốt phần cứng & sơ đồ kết nối
- [ ] Lập trình driver cảm biến
- [ ] Lập trình hiển thị
- [ ] Lập trình cảnh báo
- [ ] Lập trình lưu/đọc EEPROM
- [ ] Tích hợp & kiểm thử toàn hệ thống
- [ ] Viết báo cáo & hoàn thiện tài liệu

---

## 📝 Ghi Chú Phát Triển

> Dùng phần này để ghi lại các quyết định kỹ thuật quan trọng trong quá trình làm đồ án.

- `[DD/MM/YYYY]` — Khởi tạo repo, xác định đề tài
- `[DD/MM/YYYY]` — *(Cập nhật tiếp theo)*

---

## 📄 Giấy Phép

Dự án sử dụng giấy phép [MIT](./LICENSE) — tự do sử dụng cho mục đích học thuật và phi thương mại với điều kiện ghi rõ nguồn gốc.

---

<div align="center">

**Đồ án môn Vi xử lý – Vi điều khiển**  
`[Tên trường]` • `[Học kỳ X – XXXX]`

*Made with ❤️ by `[Tên nhóm]`*

</div>
