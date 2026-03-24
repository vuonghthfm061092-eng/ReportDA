[Xem báo cáo](https://vuonghthfm061092-eng.github.io/ReportDA/)
# Báo Cáo Pipeline 4 Kênh — CEO Report

Báo cáo tĩnh dạng single-file HTML, trình bày hiệu suất pipeline tháng 02/2026 cho 4 kênh khai thác: **ET**, **DVOL**, **Digital**, **CD**. Thiết kế theo chuẩn CEO-level — đọc trên màn hình từ mobile đến 32 inch đều hiển thị đúng.

---

## Mở file

Không cần server, không cần cài đặt. Chỉ cần:

```
Mở file index.html bằng bất kỳ trình duyệt nào
```

> Cần kết nối internet để tải font (Google Fonts) và thư viện chart (Chart.js CDN). Nếu offline, font sẽ fallback về system font nhưng nội dung vẫn hiển thị đầy đủ.

---

## Cấu trúc file

File duy nhất `report_pipeline_ceo.html` bao gồm tất cả — CSS, HTML, JavaScript — không phụ thuộc file ngoài nào khác ngoài CDN.

```
report_pipeline_ceo.html
├── <style>          CSS + CSS Variables + Responsive Media Queries
├── <body>
│   ├── <nav>        Sticky navigation, scroll spy tự động
│   ├── #cover       Trang bìa + KPI tổng quan 4 kênh
│   ├── #executive   Executive Summary + Alert cards
│   ├── #funnel      Funnel Analysis — 5 tầng chuyển đổi
│   ├── #channels    Channel Deep Dive — phân tích từng kênh
│   ├── #financial   Tài chính, scheme sản phẩm, địa lý
│   ├── #team        Hiệu suất đội ngũ — Supervisor / DSO Team / Cá nhân
│   ├── #root-cause  Phân tích nguyên nhân gốc rễ
│   └── #decisions   Ma trận quyết định 8 hành động ưu tiên
└── <script>         Chart.js render (13 charts) + Scroll Spy
```

---

## Thư viện sử dụng

| Thư viện | Phiên bản | Mục đích |
|---|---|---|
| [Chart.js](https://www.chartjs.org/) | 4.4.1 | Render 13 biểu đồ (bar, line, radar, doughnut, bubble) |
| [Playfair Display](https://fonts.google.com/specimen/Playfair+Display) | — | Font tiêu đề |
| [DM Sans](https://fonts.google.com/specimen/DM+Sans) | — | Font nội dung |
| [DM Mono](https://fonts.google.com/specimen/DM+Mono) | — | Font số liệu |

---

## Responsive

File hỗ trợ 5 breakpoint theo chiến lược **PC-first → thu dần**:

| Breakpoint | Target |
|---|---|
| `≥ 1920px` | Màn hình 32 inch / 4K |
| `≤ 1280px` | Laptop 13–15 inch |
| `≤ 1024px` | Tablet nằm / Laptop nhỏ |
| `≤ 768px` | Tablet đứng / Mobile lớn |
| `≤ 480px` | Mobile nhỏ |

Tất cả kích thước (chart height, padding, font, grid) được kiểm soát qua **CSS custom properties** trong `:root` — media query chỉ cần override variable, không ghi đè từng property rời.

```css
/* Ví dụ: thay đổi chart height cho mobile */
@media (max-width: 768px) {
  :root {
    --chart-sm: 180px;
    --chart-md: 210px;
    --chart-lg: 230px;
  }
}
```

---

## CSS Variables quan trọng

Muốn tùy chỉnh giao diện, chỉ cần sửa trong khối `:root`:

```css
:root {
  /* Màu nền */
  --bg: #f8f7f5;
  --bg2: #ffffff;

  /* Màu kênh — đổi ở đây là đổi toàn bộ */
  --et:      #16a34a;   /* xanh lá */
  --dvol:    #2563eb;   /* xanh dương */
  --digital: #7c3aed;   /* tím */
  --cd:      #dc2626;   /* đỏ */

  /* Layout */
  --nav-h:    52px;     /* chiều cao nav — scroll-margin tự theo */
  --page-max: 1280px;   /* max-width trang */
  --page-px:  2rem;     /* padding ngang */

  /* Chart heights */
  --chart-sm: 220px;
  --chart-md: 280px;
  --chart-lg: 320px;
}
```

---

## Cập nhật dữ liệu

Toàn bộ số liệu nằm trong khối `<script>` cuối file. Để cập nhật báo cáo tháng mới:

1. **Số liệu chart** — tìm comment `// ── 1. FUNNEL OVERALL ──` đến `// ── 13. QUADRANT MATRIX ──`, sửa mảng `data: [...]` tương ứng.
2. **KPI trang bìa** — tìm `class="cover-kpi"`, sửa nội dung trong `.cover-kpi-value` và `.cover-kpi-sub`.
3. **Tiêu đề kỳ báo cáo** — tìm `Tháng 02/2026` và thay bằng tháng mới (xuất hiện ở nhiều chỗ — nên dùng Find & Replace).
4. **Bảng Top DSO** — tìm `class="data-table"` trong section `#team`, cập nhật các dòng `<tr>`.

---

## Tính năng

- **Sticky navigation** với scroll spy — nav tự highlight đúng section khi cuộn trang
- **Smooth scroll** khi click nav link, tính đúng offset của nav (không bị che)
- **13 biểu đồ** tương tác: hover tooltip, legend click ẩn/hiện dataset
- **Print-friendly** — nav ẩn khi in, section không bị cắt ngang trang
- **Light theme** chuẩn báo cáo tài chính nội bộ

---

## Phân loại nội dung

> ⚠️ **Bảo mật — Nội bộ.** File này chứa số liệu kinh doanh thực tế của HD Saison. Chỉ chia sẻ trong phạm vi cấp quản lý được phép.

---

## Liên hệ

Thuộc team **SCL-Coor** — HD Saison.
