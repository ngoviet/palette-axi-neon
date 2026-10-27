# Palette AXI Neon

<!-- readme-axi type=card -->

[![HACS Custom](https://img.shields.io/badge/HACS-Custom-41BDF5.svg)](https://hacs.xyz/docs/faq/custom_repositories)
[![GitHub release](https://img.shields.io/github/v/release/ngoviet/palette-axi-neon)](https://github.com/ngoviet/palette-axi-neon/releases)
[![HACS validation](https://github.com/ngoviet/palette-axi-neon/actions/workflows/validate.yml/badge.svg)](https://github.com/ngoviet/palette-axi-neon/actions/workflows/validate.yml)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

[English](README.md) · **Tiếng Việt**

Theme tối phong cách neon cho Home Assistant: nền xanh đêm, màu nhấn neon, chữ đọc rõ ở mọi nơi, kể cả các ô
nhập liệu và bộ chọn mà nhiều theme tối vẫn để màu sáng.

> 🇻🇳 Dự án do một người Việt tự xây dựng và duy trì — nếu nó giúp ích cho bạn, hãy
> [ủng hộ dự án](#ủng-hộ-dự-án).

![Bảng màu Palette AXI Neon](https://raw.githubusercontent.com/ngoviet/palette-axi-neon/main/images/palette.png)

## Tính năng

- **Xanh đêm, không phải đen.** Nền trang là xanh đậm (OKLCH L 0.18), card sáng hơn một bậc, và một quầng sáng
  nhẹ nâng góc trên bên trái. Viền và các màu xám dùng chung sắc độ với nền, nên không chỗ nào xám chết.
- **Màu nhấn cùng một dải sáng.** Mọi màu nhấn (L 0.70–0.84) có độ nặng thị giác gần như nhau, nên không màu nào
  lấn át màu nào. Mỗi màu một nghĩa: xanh lá = tốt, hổ phách = cần chú ý, đỏ = lỗi, xanh dương = thông tin,
  cyan = màu chính.
- **Độ tương phản đo thật.** Chữ chính đạt 14.99:1 trên card, chữ phụ 8.66:1 (WCAG AAA). Mọi màu trạng thái đạt
  ít nhất 6.5:1.
- **Ô nhập liệu đọc rõ.** Theme khai báo rõ chế độ tối, nên ô tìm kiếm, bộ chọn và trường form dùng nền tối (xem
  [Vì sao khối `modes` quan trọng](#vì-sao-khối-modes-quan-trọng)).
- **Hợp với Mushroom.** Các màu có tên của HA (`red-color`, `amber-color`, `teal-color`, …) được ánh xạ lại vào
  cùng bảng màu, nên chip Mushroom và `icon_color` khớp với theme.

## Cài đặt

### HACS (khuyên dùng)

1. Mở **HACS** trong Home Assistant.
2. Mở menu (⋮, góc trên bên phải) → **Custom repositories**.
3. Thêm `https://github.com/ngoviet/palette-axi-neon` và chọn loại **Theme**.
4. Tìm **Palette AXI Neon**, mở ra và chọn **Download**.
5. Tải lại theme: **Developer tools → Actions → `frontend.reload_themes`**, hoặc khởi động lại Home Assistant.

### Cài tay

1. Bảo đảm `configuration.yaml` nạp theme từ một thư mục:

   ```yaml
   frontend:
     themes: !include_dir_merge_named themes
   ```

2. Chép [`themes/palette_axi_neon.yaml`](themes/palette_axi_neon.yaml) vào `/config/themes/`.
3. Gọi action `frontend.reload_themes` (hoặc khởi động lại Home Assistant).

## Cách dùng

- **Toàn bộ giao diện (theo từng người dùng):** mở **Hồ sơ** (Profile) → **Theme** và chọn `palette-axi-neon`.
- **Một dashboard hoặc một view:** đặt `theme: palette-axi-neon` cho view trong trình sửa cấu hình thô (raw
  configuration editor).
- **Làm mặc định cho mọi người:** gọi `frontend.set_theme` với `name: palette-axi-neon`.

## Vì sao khối `modes` quan trọng

Theme kết thúc bằng khối `modes: dark:`. Đừng xoá nó.

Khi theme không có khoá `modes`, frontend Home Assistant ép theme đó sang **chế độ sáng**. Ô nhập liệu, bộ chọn
theme và các điều khiển form khác khi đó dùng nền sáng mặc định (`#f5f5f5`), trong khi chữ lại kế thừa
`primary-text-color` màu sáng của theme. Kết quả là chữ sáng trên ô sáng, gần như không nhìn thấy.

Theme khai báo `dark` mà không có `light` thì frontend ép sang **chế độ tối**. Mọi giá trị theme không đặt sẽ lấy
theo mặc định tối của Home Assistant, và khối này cũng chỉnh màu ô nhập cho khớp bảng màu:

```yaml
  modes:
    dark:
      input-fill-color: "#142443"
      input-ink-color: "#e6edf7"
      input-label-ink-color: "#a2b7d7"
      # …
```

Cùng mẹo này sửa được mọi theme tối tự làm có ô nhập liệu khó đọc.

## Bảng màu

| Vai trò | Biến | Màu | Tương phản trên card |
|------|----------|--------|------------------|
| Nền trang | `primary-background-color` | `#0a1122` | — |
| Card | `card-background-color` | `#0e182e` | — |
| Thanh bên / tiêu đề | `sidebar-background-color` | `#060a14` | — |
| Ô nhập liệu | `input-fill-color` | `#142443` | chữ 13.07:1 |
| Viền / đường chia | `divider-color` | `#1e2b4a` | — |
| Chữ chính | `primary-text-color` | `#e6edf7` | 14.99:1 |
| Chữ phụ | `secondary-text-color` | `#a2b7d7` | 8.66:1 |
| Chữ vô hiệu | `disabled-text-color` | `#6b7fa3` | 4.37:1 |
| Màu chính / nhấn | `primary-color` | `#22d3ee` | 9.77:1 |
| Thành công | `success-color` | `#22c55e` | 7.75:1 |
| Cảnh báo | `warning-color` / `amber-color` | `#f59e0b` / `#fbbf24` | — / 10.58:1 |
| Lỗi | `error-color` | `#ff716a` | 6.58:1 |
| Thông tin | `info-color` | `#6ca4ff` | 7.06:1 |
| Tím | `purple-color` | `#a78bfa` | 6.49:1 |
| Cam | `orange-color` | `#fb923c` | 7.81:1 |
| Hồng | `pink-color` | `#f472b6` | 6.67:1 |

Chữ trên nút chính màu cyan (`text-primary-color` `#0a1122`) đạt 10.41:1. Số tương phản là tỉ lệ WCAG 2, đo bằng
[palette-axi](#ghi-công).

### Biến bổ sung cho card tự làm

Theme còn định nghĩa các biến `--nv-*` (`nv-cyan`, `nv-blue`, `nv-green`, `nv-amber`, `nv-red`, `nv-purple`,
`nv-orange`, `nv-pink`, `nv-metric`, `nv-surface`) cho custom card và style `card-mod`. Luôn ghi giá trị dự phòng
để card vẫn chạy được với theme khác:

```css
color: var(--nv-blue, #448aff);
```

## Tương thích

- Đã thử trên Home Assistant **2026.10**.
- Chỉ có bản tối: không có biến thể sáng, và theme vẫn tối ngay cả khi hồ sơ của bạn đặt sáng hoặc tự động.

## Ghi công

Bảng màu được tạo và kiểm tra bằng **palette-axi** (OKLCH, `generate --preset neon-dark`), một CLI nhỏ chuyên
kiểm tra màu giao diện: màu trung tính pha sắc, màu nhấn cùng một dải sáng, độ tương phản APCA và WCAG, gam màu sRGB.

<!-- support:start -->
## Ủng hộ dự án

<p align="center">
  <img src="https://raw.githubusercontent.com/ngoviet/.github/main/assets/support/banner.svg" width="720" alt="Built and maintained by one person in Việt Nam">
</p>

<p align="center">
  <a href="https://buymeacoffee.com/ngoviet"><img src="https://raw.githubusercontent.com/ngoviet/.github/main/assets/support/btn-coffee.svg" height="56" alt="Buy me a coffee"></a>
  &nbsp;
  <a href="https://github.com/sponsors/ngoviet"><img src="https://raw.githubusercontent.com/ngoviet/.github/main/assets/support/btn-sponsors.svg" height="56" alt="GitHub Sponsors"></a>
</p>

<p align="center">
  <img src="https://raw.githubusercontent.com/ngoviet/.github/main/assets/support/vietqr-card.svg" width="300" alt="VietQR — MB Bank — NGO DUC VIET — 911051212">
  &nbsp;
  <img src="https://raw.githubusercontent.com/ngoviet/.github/main/assets/support/crypto-card.svg" width="300" alt="Crypto — BNB Smart Chain (BEP20) — 0xcbf0402b232cb24b4d998f09a4884f87b5f74750">
</p>

<p align="center"><b>Ví tiền mã hoá, chỉ gửi qua mạng BNB Smart Chain (BEP20):</b><br><code>0xcbf0402b232cb24b4d998f09a4884f87b5f74750</code></p>

<p align="center"><sub>🇻🇳 VietQR: quét bằng app ngân hàng bất kỳ, nội dung <code>Ung ho palette-axi-neon</code>. Cảm ơn bạn đã giúp dự án tiếp tục phát triển!</sub></p>
<!-- support:end -->

## Giấy phép

[MIT](LICENSE) © Ngô Đức Việt.
