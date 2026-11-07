# nguyen0xhieu — Design System v4 (Bento)

Nguồn chuẩn để thiết kế và code mọi sản phẩm của nguyen0xhieu. **Giữ bộ màu gốc**, dùng hai mật độ web theo mục đích và một tập component nhất quán. Cập nhật 2026-11-08: **v4 lấy Bento làm phong cách web mặc định** (mục ngay dưới). Các mục v3 phía sau vẫn đúng về màu, token và pattern dữ liệu, nhưng khi mâu thuẫn về bề mặt, bo góc, cỡ chữ, spacing thì **Bento thắng**.

## Dùng bộ này

1. Đọc tài liệu và `tokens.json` trước khi thiết kế.
2. Chọn **pattern**: editorial/landing, bảng dữ liệu hay danh sách công việc.
3. Chọn profile cho từng trang/vùng: `spacious` hoặc `compact`.
4. Dùng `web.css` xuất từ token; không tự tạo màu hay giảm spacing ngẫu nhiên.
5. Nếu có ngoại lệ đã duyệt, ghi vào `products` và tài liệu sản phẩm. Ngoại lệ sản phẩm ưu tiên trong đúng phạm vi đó.

| File | Vai trò |
|---|---|
| `tokens.json` | Màu Light/Dark, typography, spacing, component, hai profile và ngoại lệ sản phẩm |
| `web.css` | CSS variables được xuất tự động từ token, gồm màu/type/profile/product |
| `export_web.py` | Chạy `python export_web.py` để xuất lại CSS; không cần dependency |
| `README.md` | Quyết định thiết kế, cách chọn pattern và tiêu chí kiểm tra |

Trong HTML: `<body data-ds-product="0xhieu-xyz" data-ds-profile="compact">`. Theme dùng `data-ds-theme="dark"` khi sản phẩm có hỗ trợ. Profile đổi theo trang, không đổi tùy tiện chỉ vì viewport nhỏ.

## Bento v4 — phong cách web mặc định (chốt 2026-11-08)

Nguồn: giao diện 0xhieu.xyz được duyệt 07/11/2026. Token đầy đủ nằm ở `tokens.json → bento`, CSS ở `web.css` (`--ds-bento-*`).

### Bề mặt

| Thứ | Giá trị | Dùng cho |
|---|---|---|
| Canvas | `#F2F2F0` | Nền trang. Tiêu đề trang và nhãn nhóm nằm thẳng trên canvas, **không** có dải nền trắng. |
| Tile | `#FFFFFF` | Mọi nội dung đọc được nằm trong tile. Không viền, không bóng. |
| Hair | `#ECECEA` | Đường kẻ 1px giữa các hàng trong tile. |
| Tile tối | `#161616` | Ô tương phản (cảnh báo, khối quan trọng thứ hai). Chữ trắng, số dùng màu accent. |
| Tile accent | màu accent sản phẩm | Số liệu/khối chính. Chữ đen; nút trong đó nền đen chữ accent. |
| Chip | màu canvas | Thẻ, chip, ô icon, nút phụ bên trong tile trắng. |

- Mỗi màn **tối đa 1 tile accent và 1 tile tối**; còn lại là tile trắng.
- **Thẻ:** thẻ quan trọng nền đen chữ trắng/accent, thẻ thường nền canvas chữ đen. Không dùng thẻ viền.
- **Trạng thái:** việc kế tiếp là chip accent, quá giờ/nguy hiểm là chip `red-soft` chữ `red-text`, việc xong là chữ muted gạch ngang. Màu trạng thái luôn đi kèm chữ.
- **Bo góc chỉ 3 mức:**
  - **20** cho tile và popup.
  - **10** cho chip, thẻ, logo, ô icon, nút nhỏ, input.
  - **Pill** cho navbar, tab, toggle, ô đếm, nút nổi, avatar.
- **Bóng:** chỉ đồ vật **nổi** có `shadow-y2`: navbar dính, nút toolbar trang, nút nổi, popup. Tile và link/nút nằm trong tile thì phẳng.
- **Độ đậm chữ chỉ 3 mức:**
  - **400** cho chữ đọc.
  - **600** cho nhãn, tên, nút.
  - **800** cho tiêu đề và số lớn.
  - Không dùng 500 hay 700.

### Cỡ chữ — ít cỡ, không loạn

Chỉ dùng đúng các vai trò dưới đây. **Cấm** chế cỡ lẻ (13, 15, 17…) để nhét cho vừa. Không vừa thì rút gọn, xuống dòng hoặc ẩn bớt yếu tố. Chữ dữ liệu không bao giờ dưới 14.

| Vai trò | Mobile (≤640) | Desktop | Weight | Dùng cho |
|---|---|---|---|---|
| `bento-small` | 14/20 | 14/20 | 400 · 600 | Metadata, thẻ, chip, ô và tiêu đề bảng, chú thích |
| `bento-body` | 16/24 | 16/24 | 400 · 600 | Chữ hàng/task, đoạn văn, input (16 để iPhone không tự zoom), nút, menu |
| `bento-title` | 20/28 | 20/28 | 800 | Tiêu đề tile, tiêu đề dropdown, tiêu đề mục CV |
| `bento-page` | 20/28 | 28/36 | 800 | Một tiêu đề trang mỗi màn |
| `bento-display` | 32/36 | 48/52 | 800 | Số lớn trong tile accent/tối, tên trên CV. Tối đa 2 chỗ mỗi màn |
| `bento-hero` | 40/44 | 64/68 | 800 | **Chỉ trang spacious**, một dòng mỗi trang |

- **Mobile dùng 4 cỡ:** 14 · 16 · 20 · 32. Trang spacious thêm cỡ 40 cho hero.
- **Desktop dùng 5 cỡ:** 14 · 16 · 20 · 28 · 48. Trang spacious thêm cỡ 64 cho hero.
- Mọi con số dùng `tabular-nums`.

### Bố cục chung

- **Khung:** rộng tối đa 1280, lề ngang 24 trên desktop và 16 trên mobile.
- **Navbar:** viên trắng nổi, dính trên đầu. Logo bên trái, cụm tab bên phải; tab đang mở nền accent, chữ đen.
- **Đầu trang:** tiêu đề bên trái, nút điều khiển bên phải, đặt thẳng trên canvas. Nút điều khiển là viên trắng có bóng.
- **Lưới:** desktop 4 cột, ≤1024 còn 2 cột, mobile 2 cột cho ô số liệu và ô tính năng.
  - Danh sách, checklist và bảng chiếm trọn hàng.
  - Ô mở rộng được (`details`) khi mở ra chiếm 2 cột, trên mobile chiếm cả hàng.

### Trang dữ liệu — khít và sạch (`data-ds-profile="compact"`)

Gồm Valuation, Work, dashboard, admin, tracker, screener.

| | Desktop | Mobile |
|---|---|---|
| Khe giữa tile | 12 | 12 |
| Khe giữa các khối | 12 | 12 |
| Đệm trong tile | 20 | 16 |
| Hàng tối thiểu | 40 | 44 (vùng chạm) |
| Đệm dọc hàng | 10 | 10 |

- **Một khe 12 cho mọi thứ**, để cả trang đọc như một bảng liền.
- Hàng trong tile ngăn bằng đường hair. **Không đặt card trong card.**
- **Bảng trên mobile không bao giờ kéo ngang.** Theo thứ tự:
  1. Ẩn bớt cột phụ.
  2. Rút gọn giá trị ghép, chỉ giữ số chính (ví dụ ATH chỉ còn `đỉnh (×N)`).
  3. Không bao giờ thu nhỏ chữ.
- **Danh sách tham khảo** (danh sách dự án, hướng dẫn) gom vào **một tile dropdown, mặc định gập**. Nội dung dùng hằng ngày thì để mở sẵn.
- **Checklist:**
  - Gồm một tile hero (ngày, số việc, vòng tiến độ) và ngay dưới là một tile danh sách trắng.
  - Tick tự về 0 khi sang ngày hoặc tuần mới.
  - Việc có giờ hẹn hiện trong ô "Lịch hôm nay".
- **Toolbar** một hàng. Control nào hết công dụng thì **bỏ hẳn**, không để nổi lơ lửng.
- Không dùng cỡ `bento-hero`.

### Trang trình bày — có khoảng thở (`data-ds-profile="spacious"`)

Gồm CV, portfolio, landing, marketing, giới thiệu.

| | Desktop | Mobile |
|---|---|---|
| Khe giữa tile | 16 | 12 |
| Khe giữa các mục | 48 | 32 |
| Đệm trong tile | 32 | 20 |
| Tile hero | chiếm 2/4 cột, cao tối thiểu 320, đệm 40 | đệm 24 |

- Một hero mạnh duy nhất, đứng cạnh tile số liệu accent và tile liên hệ.
- Các mục cách nhau bằng khe lớn; tile trong cùng một mục dùng khe tile.
- Đoạn văn rộng tối đa 680.
- Ảnh nằm trong tile riêng, có chú thích, không đè chữ lên ảnh.
- Nút liên hệ là chip canvas phẳng.

### Component mẫu

- **Tile số liệu:**
  - Nền accent hoặc nền tối.
  - Nhãn nhỏ đậm 600 ở trên, số cỡ display ở giữa, chú thích nhỏ ở dưới.
- **Tile danh sách:**
  - Hàng tiêu đề gồm tiêu đề và ô đếm dạng pill nền canvas.
  - Các hàng ngăn bằng đường hair.
- **Tile dropdown:**
  - Hàng tóm tắt gồm tiêu đề (`bento-title`), ô đếm và mũi tên.
  - Mở ra là các nhóm hàng.
- **Hàng:**
  - Đầu hàng: logo hoặc ô check 36.
  - Giữa: chữ chính (body) và dòng meta (small, xám).
  - Cuối hàng: nút icon 32 nền canvas, bo 10.
- **Checkbox:**
  - Hình tròn 24, viền xám 2px.
  - Khi tick: nền đen, dấu check trắng; chữ đổi sang muted và gạch ngang.
- **Vòng tiến độ:**
  - Cỡ 92 trên desktop, 80 trên mobile.
  - Trên tile accent: vòng đen. Trên tile tối: vòng accent.
  - Giữa vòng là `n/tổng`.
- **Nút viên:**
  - Màu trắng, có bóng.
  - Cao 40 trên desktop. Trên toolbar mobile cao 32 nhưng vùng chạm vẫn đủ 44.
- **Bảng:**
  - Nằm trong tile trắng.
  - Tiêu đề bảng chữ xám nhỏ, đậm 600.
  - Các hàng ngăn bằng đường hair; số canh phải.

### Kiểm tra trước khi giao

1. **Đếm cỡ chữ** trên trang:
   - Mobile chỉ dùng {14, 16, 20, 32}, cộng 40 nếu là trang spacious.
   - Desktop chỉ dùng {14, 16, 20, 28, 48}, cộng 64 nếu là trang spacious.
2. **Đếm bo góc:** chỉ có 20, 10 và pill.
3. **Ở khổ 390, 360 và 320:**
   - Không có gì phải kéo ngang.
   - Không chữ nào dưới 14.
4. **Màu tile:** mỗi màn tối đa 1 tile accent và 1 tile tối.
5. **Chụp ảnh thật** để xem, không chỉ dựa vào lint.

## Nền tảng và nguồn tham khảo

Đây là **bộ quy tắc tổng hợp cho sản phẩm của mình**, không giả vờ một thư viện quy định toàn bộ các con số:

- [Radix spacing](https://www.radix-ui.com/themes/docs/theme/spacing): scale 4/8/12/16/24…, density thay đổi có hệ thống.
- [Radix Table — mã nguồn](https://github.com/radix-ui/themes/blob/main/packages/radix-ui-themes/src/components/table.css): compact cell padding 8px, canh nội dung, dùng kẻ phân cách và một bề mặt chung.
- [shadcn Tasks — mã nguồn](https://github.com/shadcn-ui/ui/blob/main/apps/v4/app/%28app%29/examples/tasks/components/data-table.tsx): workspace công việc tổ chức theo dòng/bảng với thao tác chung; không biến mỗi thông tin thành một card.
- [Carbon data table](https://www.carbondesignsystem.com/building-blocks/core/components/data-table/guidelines): nhiều mức mật độ, 32px cho dense desktop và 40px mặc định. Header Valuation 56px là yêu cầu riêng của sản phẩm, **không phải** thông số suy ra từ Carbon.

## Hai profile web

| | `spacious` — trình bày | `compact` — công việc/dữ liệu |
|---|---|---|
| Dùng cho | CV, portfolio, landing, trang giới thiệu | Valuation, Work/Airdrop, dashboard, Admin, bảng dữ liệu |
| Mục tiêu | Đọc và hiểu câu chuyện, CTA rõ | Quét, so sánh và thao tác nhanh |
| Nhịp chính | 8px | 4px |
| Lề mobile | 16px | 16px |
| Lề desktop | Theo khung 1200px, lề tối thiểu 48px | 24px; không bắt buộc khung 1200 |
| Nhóm nội dung | 64px desktop / 32px mobile | 16px |
| Panel | Đệm 16–32px, khoảng giữa 16–24px | Cell/đệm chính 8px, panel phụ 8–12px |
| Nội dung | Body 16/24, lead 18/28 | Body 16/24; số/task/metadata 14/20 |
| Header panel | 20/28 khi cần nhấn | 16/24, mobile có thể 14/20 |
| Dòng | Theo nội dung, list min 56 | Mặc định 40; dense desktop 32; touch 44 |
| Chiều cao | Theo nội dung | Theo nội dung, trừ panel cố định đã được yêu cầu |
| Bề mặt | Khối nội dung rõ; whitespace có chủ đích | Một bề mặt theo nhóm, ít lớp nền/viền; kẻ hàng thay card lồng card |

Không lấy spacing section của landing áp vào workspace. Không lấy chữ native-app 22px áp cho bảng web. Một trang có thể có hero spacious và vùng dữ liệu compact, nhưng ranh giới phải rõ.

## Bộ màu — giữ nguyên

- Global brand: **0x Blue `#1E6DF7`** ở cả Light/Dark. Primary dùng `blue` + `on-blue`; small text trên nền tint dùng `blue-strong`.
- Văn bản chỉ ba cấp: `ink` (chính), `grey` (phụ), `muted` (metadata/disabled). Không dùng muted cho việc người dùng cần đọc để hành động.
- Nền `ground`, nhóm `mist`, kẻ `line`. Không tự pha xám thứ tư.
- Mỗi màu trạng thái có base / `-text` / `-soft`: green thành công, red lỗi/nguy hiểm, yellow chờ/cảnh báo, orange chú ý, cyan thông tin, purple chuỗi phụ/tính năng mới. Màu trạng thái phải kèm chữ hoặc ký hiệu rõ nghĩa.
- Chữ trên yellow luôn đen. Nền solid là mặc định; tối đa một gradient lớn/màn, không dùng gradient cho chữ, icon nhỏ hay bảng dữ liệu.
- Disabled: nền line, chữ muted, không shadow, không giảm opacity.
- Sản phẩm 0xhieu.xyz giữ primary đen và vàng mắt mèo `#FFA111`; đó là override đã duyệt trong `products.0xhieu-xyz`, không đổi palette global.

## Typography

Inter cho thiết kế/Figma/slide; system Apple/SF Pro với fallback system cho code web/app. Giá trị đầy đủ và letter-spacing nằm trong `type.groups`.

| Vai trò web | Style | Thông số |
|---|---|---|
| Metadata/data | web-caption | 14/20, 400 |
| Nhãn | web-label | 14/20, 600 |
| Nội dung | web-body | 16/24, 400 |
| Panel/toolbar | web-nav-button | 16/24, 600 |
| Lead | web-lead | 18/28, 400 |
| Tiêu đề nhỏ | web-h4 | 20/28, 600 |
| Tiêu đề màn/mục | web-h3 | 24/32, 600 |
| Display | web-h2/h1/hero | 40/48, 56/64, 72/80, 700; mobile theo style riêng |

Chữ dữ liệu không dưới 14. Số dùng `tabular-nums`; nhãn canh trái, số theo cột. Task/tên/tag được xuống dòng, không mất chữ. Không đổi weight làm nhích layout khi hover. Chữ body có thể giới hạn 680px; bảng không chịu giới hạn này.

## Component và bề mặt

- Radius: panel 16, control nhỏ 8, data row 0, pill/circle 9999. Không bọc từng nhãn/số bằng thẻ bo góc.
- Flat/border line là mặc định. `shadow-y2` chỉ cho overlay, menu nổi hoặc bề mặt nổi có lý do; không phủ bóng mọi nút/card.
- Nút thường 40px compact, toolbar nhìn thấy 32; spacious 48. Trên thiết bị cảm ứng đảm bảo mục bấm chung tối thiểu 44, không chồng nhau. Ngoại lệ toolbar sản phẩm phải ghi rõ.
- Ô nhập compact 40, touch 44; chữ input mobile 16 để tránh tự zoom. Form có label, focus 2px và error text.
- Focus nhìn rõ, offset 2px. Hover dùng màu/chỉ báo ổn định; không nâng card hay thay độ rộng chữ. Không bổ sung chuyển động trang trí.
- Popup theo nội dung, có max-height trong viewport và cuộn; khóa nền khi mở. Escape/backdrop theo hành vi đã định, form nhập dài không tự mất khi bấm nhầm.
- Icon dùng Lucide 1.59.0, stroke 2, size 16/20/24/32. Không dùng emoji làm icon thao tác.

## Pattern: bảng dữ liệu

Một bề mặt bảng, header và thân thẳng cột. Độ rộng theo nội dung, dành chỗ cho trường dài; không chia đều mọi cột bằng phần trăm. Header và body có cùng quy tắc đo, cùng hướng cuộn. Bảng cuộn nội bộ khi tổng minimum width vượt viewport; không tràn toàn trang hoặc đè cột.

Không ngắt một giá trị ghép cần đọc cùng nhau chỉ để giữ cột hẹp. Không thu nhỏ font để che lỗi width. Chỉ vùng danh sách dài mới cần giới hạn cao. Không thêm dòng rỗng để lấp box. Các header cùng vai trò dùng token chung, không sửa độc lập.

## Pattern: workspace công việc

Mỗi nhóm có một bề mặt chung; mỗi dự án là một hàng. Desktop tách vùng thông tin dự án và vùng việc. **Phase là cột nhãn cạnh task**, không phải một tiêu đề lớn chiếm thêm hàng trên từng task. Mobile chuyển thông tin dự án lên trên, nhưng phase và việc vẫn cạnh nhau.

Giữ toàn bộ task/link, không tự thêm điểm số/checklist/tính năng AI. Không dùng dải màu Daily lặp xen kẽ; màu chỉ cho nhóm/trạng thái có nghĩa. Rank có thể là metadata; không tạo nhiều lớp nhãn, separator và badge cho cùng một ý.

## Pattern: CV/landing

Chọn một trục căn lề và phân cấp nội dung. CV là editorial portfolio: avatar, tên và thông điệp nhận diện thành một hero rõ; nội dung kinh nghiệm dễ đọc, hình ảnh có caption. CTA vừa đủ và không cạnh tranh với tiêu đề. Landing marketing có thể dùng display lớn hơn; không bắt CV phải có hero 72px.

## Quy tắc riêng của 0xhieu.xyz

- `/` spacious; `/valuation` và `/work` compact. `/airdrop` chuyển 301 sang `/work` và có fallback client.
- Brand đen/vàng cũ. Navbar căn theo khung của profile đang mở.
- Valuation: 8 token trên cả desktop/mobile; dòng 40, header bảng/popup/box **56**; chữ header desktop16/24, mobile14/20, 600. Ba box **328px cố định**, nội dung dài cuộn; mobile tất cả dùng 2 cột bằng nhau, không tự cho một box span cả hàng.
- Nhãn/giá trị trong box trái/phải, min-height 56, cho phép tăng để hiện đủ chữ. Ticker dưới $300M đậm đen; từ $300M đậm cam, không chấm. ATH `đầu → cuối (×N)` một dòng, tỷ số tính từ số gốc và cam đậm.
- Work: project column240 desktop; phase104; padding8; task40 desktop/44 touch; groupgap16. Những kích thước này phục vụ pattern, không dùng làm spacing chung cho mọi thành phần.
- CV: khung1200; hero trên96/48, khối cách64/32; portrait112/72. Nội dung CV vẫn tiếng Anh, tagline giữ nguyên văn.
- Toolbar mobile một hàng là yêu cầu riêng: title20/18/16/14, control nhìn thấy32. Không biến ngoại lệ này thành chuẩn touch cho mọi nơi.

## Native app và slide

Giữ nguyên token chuyên biệt hiện có: app scale14/16/18/22/28/34/48, body22/28, input/button48; safe-area theo thiết bị. Slide1920×1080 giữ lề128, rãnh64 và type slide riêng. Chúng không bị thay bằng geometry web compact. Các bảng grid/type trong `tokens.json` là nguồn chính xác.

## Export, kiểm tra và thay đổi

Chạy `python export_web.py`; commit token và CSS xuất cùng nhau. Hash dùng JSON canonical (sort key, bỏ whitespace), không phụ thuộc CRLF/LF của Windows/Linux. Website phải đồng bộ bản CSS và ghi phiên bản, không đọc remote CSS runtime. Dùng nguồn JSON để kiểm tra màu không bị đổi ngoài scope.

QA tối thiểu: desktop1440/1024/768 và mobile640/390/360/320; các ngôn ngữ; dữ liệu rỗng/dài; không cắt chữ/tràn cột; đủ link/action; hover/focus; vùng chạm; popup; navbar và back/forward. Xem ảnh thật, không chỉ báo lint. Test component phải kiểm tra vai trò/layout, không chỉ khớp một con số rời rạc.

Figma gốc: https://www.figma.com/design/IPyKVg7ylGw1mjMRyYVrL7/hieu. Token v3 và pattern mới **chưa được đồng bộ sang Figma**; không tuyên bố file Figma đã chứa thay đổi này.

## 0xhieu.xyz — workspace alignment approved 2026-11-01

Valuation and Work share the product workspace tokens: max frame1280px including padding, radius8, neutral white card headers, line border, horizontal card padding12, section padding8 and card gap12. Work uses independent cards: desktop2 columns, mobile1 (<=900px), DAILY yellow-soft with orange-text label. Reference chosen by user: [Linear Board](https://linear.app/docs/board-layout). Valuation retains 8 visible rows, 56px headers, fixed328px panels and its existing panel column counts. These product decisions supersede earlier product list/fluid-layout guidance; do not apply them to unrelated products without approval.

### Shared component identity across all three pages

For 0xhieu.xyz, `sharedComponents` applies to CV as well as Valuation and Work: card/control/badge radius8, white surface, line border, no decorative card shadow. Spacious and compact control spacing/type density, not separate card styles. CV keeps its spacious hero, section gaps and 16px body text. Circular avatars/language switches and radius16 overlays retain their distinct roles. CV social buttons, Highlights and Available-for labels must consume the same product component tokens; do not leave legacy radius16/pill surfaces in those components.

### Approved action elevation

User requires drop shadow on clickable button surfaces across CV/Valuation/Work: existing black32%, y2px, blur8px token. Read-only cards/badges/content and disabled controls stay flat. Text navigation/inline links keep their text treatment. This supersedes the earlier overlay-only shadow restriction.

### Approved orange headers

User overrides neutral header surfaces: Work card headers, Valuation panel/table headers and matching table popup headers use solid product accent #FFA111 with ink/black text. Bodies remain white; DAILY remains soft yellow. Source: product workspace/headerSurface=accent. This supersedes earlier white-header guidance; dimensions stay unchanged.

### Approved accent text

0xhieu.xyz accent text uses the same product orange #FFA111, weight600. Do not substitute earth-orange #B84A0C for emphasis. Orange header backgrounds use black text. Global palette tokens for other products remain unchanged.

## Current 0xhieu.xyz blue theme — user decision 2026-11-01

Supersedes previous orange rules: black normal text, grey secondary text, blue important text. Use existing cobalt #1E6DF7 for primary actions/header fills and blue-strong #0F3DB2 for small important text on grey/tinted surfaces. White page, grey mist card/popup bodies, cobalt headers with on-blue/white text, blue-soft DAILY. Header interactive text remains white on hover; use underline instead of same-color blue text. Cards/labels remain flat, buttons keep approved drop shadows. Red is only semantic danger/destructive feedback. Preserve approved geometry, all source data/formulas, and original logo/photo artwork.

## Current product decision: black/orange + stronger DAILY + single language switch

Supersedes blue product theme: regular orange #FFA111 for button/header fills, black text on those fills, dark orange #B84A0C for important text, normal text black, secondary grey, card bodies grey. DAILY uses yellow-soft with a4px orange left border and dark-orange bold task text. VI/EN is one native accessible switch with a single translating thumb and two labels, not two circular buttons. Dimensions/data/formulas remain unchanged.

## 2026-11-02: softer headers and continuous rank slider

User requires pale orange `orange-soft` box/table headers with black text. Keep saturated orange for smaller buttons/selection highlights rather than large header fills. Work rank is one continuous bar with one sliding orange selected region, native range keyboard/drag support and scroll-spy synchronization; five independent circular buttons are prohibited.

## 2026-11-02: header matches DAILY

Supersedes the pale orange header rule: product box/table headers use the exact DAILY background `yellow-soft` #FEF5D9, black text.

## 2026-11-02: shared horizontal frame

CV, Work, Valuation and navigation/footer share max1280 border-box, horizontal inset24 desktop/16 mobile. CV spacious density does not change the common horizontal frame.

## Current 0xhieu.xyz tone — user decision 2026-11-04

Supersedes every earlier orange/blue/cream rule above for this product. White-grey-black: white page and card bodies, mist `#ECF0F8` table/box headers and popups, black text, grey secondary text. Orange `#FFA111` only on buttons, selected controls and highlights (accent text weight 600; black text on orange fills). Button hover is black with white text; input focus is black. Earth orange `#B84A0C` and cream `#FEF5D9` are banned on this product; the global palette for other products is unchanged. Red stays semantic danger only.

## 0xhieu.xyz DAILY and rank label — user decision 2026-11-04

Supersedes earlier DAILY rules: DAILY stands out through a mist section surface, without an orange border. Task text is black weight 400 at rest and weight 600 on hover, the same as every clickable item. The Work-to-Earn position in the rank bar is labelled `w2e`, because `$` looked like `S`.

## 0xhieu.xyz neutral surface, marker highlight and Work tags — user decision 2026-11-06

Supersedes the mist and orange-text rules above for this product. Headers, popups and DAILY use the product token `--ds-color-surface` `#E5E5E5` (neutral, slightly darker than mist); the global `mist` for other products is unchanged. Highlighted text is a marker: black text weight 600 on an `#FFA111` fill, never orange text on white. Work header tags: rank w2e/S, high-potential and narratives in the Valuation Trending Narratives top 5 are black fill with white text; rank A/B/C, low-potential and other narratives are white with a line border and black text. Hero or Zero values use the same marker; red stays for danger badges (table ×ATM≥15) only.
