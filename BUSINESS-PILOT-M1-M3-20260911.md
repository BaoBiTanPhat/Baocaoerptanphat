# GÓI BUSINESS PILOT M1→M3 — BÁO CÁO

> **Cập nhật lần 2:** 11/09/2026 — sau gói bổ sung *"Hoàn tất Business Pilot ·
> Duyệt layout Báo Giá · Release V1.00.371"*.
> **Sổ Yêu Cầu Owner:** mục `#255` · `#256`

---

## ① KẾT LUẬN MỘT CÂU

> ## `READY_FOR_OWNER_LAYOUT_REVIEW`

Phần kỹ thuật đã xong và **chạy thật được** trên máy nội bộ: một Sales lập báo giá
cho khách được giao, tạo nhanh sản phẩm ngay trong form, gửi duyệt, Admin duyệt,
lên đơn hàng, xác nhận đơn — **có bản ghi thật trong cơ sở dữ liệu ở từng chặng**.
Bộ bản in đã dựng đủ để Owner nhìn bằng mắt.

**Còn đúng hai cổng Owner:** duyệt bố cục bản in (ngay bây giờ), rồi xác nhận
triển khai (sau).

| Nhãn | Trạng thái |
|---|---|
| `BUSINESS_PILOT_READY` | **BLOCKED** — chờ cổng Owner |
| `QUOTATION_LAYOUT_APPROVAL` | **PENDING** — bộ duyệt đã sẵn sàng |
| `PRODUCTION_DEPLOYMENT` | **NOT_APPROVED** — chưa trình biên nhận |

### 🔴 Hai lỗ chặn chỉ lộ ra khi chạy thật

Báo cáo lần trước kết luận *"bốn chặng đã thông"* dựa trên **có route và có nút**.
Khi bấm thật bằng trình duyệt thì chuỗi **đứt ở hai chỗ**, và cả hai đều nhìn mã
không thấy:

| Lỗ | Hiện tượng | Vì sao nhìn không ra |
|---|---|---|
| **1. Báo giá Nháp không gửi duyệt được** | Hàm gửi có tồn tại nhưng **không nơi nào gọi**. Nút Duyệt chỉ bật khi đã gửi. ⇒ báo giá mới lập nằm chết ở Nháp. | Thanh tiến trình trên màn **vẽ đủ bốn chặng** nên nhìn vào tưởng chạy được |
| **2. Báo giá đã duyệt không lên đơn được** | Hộp thoại tạo đơn **ghi lại lựa chọn phương án cho mọi dòng**, kể cả khi không đổi gì. Báo giá đã duyệt thì bị khoá sửa giá ⇒ lượt ghi thừa bị chặn | Thông báo lỗi đổ lỗi cho người dùng: *"Hãy huỷ duyệt rồi duyệt lại"* |

Cả hai đã vá. Lỗ 2 vá **đúng gốc**: cổng khoá giá không sai — nó có lý do thật;
cái sai là **ghi thừa**. Nay chỉ ghi những dòng thực sự khác. Người dùng *đổi*
phương án trên báo giá đã duyệt thì **vẫn bị chặn**, đúng thiết kế.

---

## ② DANH TÍNH BẢN KIỂM THỬ

| | Giá trị |
|---|---|
| Kho | `BaoBiTanPhat/erptanphat` · nhánh `main` |
| Phiên bản | **`V1.00.371`** *(số chưa từng dùng — đã tra toàn bộ lịch sử: 346→370 đều đã dùng)* |
| Mã nguồn ứng viên | **`«mã nguồn ứng viên — ghi ở kho riêng»`** |
| Mã nguồn dựng bộ bản in | **cùng một mã** — xem chứng minh ở mục ⑥ |
| Cây làm việc | sạch tại thời điểm chốt |
| Môi trường đã chạy | máy nội bộ · MariaDB 10.11 trong Docker · Chrome thật |
| Thời điểm | 11/09/2026 |

**Bộ bản in được dựng từ mã nguồn nào:** ghi rõ trong
[`docs/reports/ban-in-bao-gia-20260911/README.md`](ban-in-bao-gia-20260911/README.md).
Nếu mã nguồn đổi sau khi dựng, bộ đó **mất hiệu lực** và phải dựng lại.

---

## ③ BỘ DUYỆT BỐ CỤC BẢN IN

**Mở [`ban-in-bao-gia-20260911/README.md`](ban-in-bao-gia-20260911/README.md) là
thấy hết** — bảng liên kết từng tệp, chỗ cần nhìn kỹ, và những gì đã tự kiểm.

| # | Bản | Ảnh | PDF | HTML | Trang |
|---|---|---|---|---|---|
| 1 | 1 dòng | [ảnh](ban-in-bao-gia-20260911/01-minh-hoa-01-dong.png) | [PDF](ban-in-bao-gia-20260911/01-minh-hoa-01-dong.pdf) | [HTML](ban-in-bao-gia-20260911/01-minh-hoa-01-dong.html) | 1 |
| 2 | 5 dòng | [ảnh](ban-in-bao-gia-20260911/02-minh-hoa-05-dong.png) | [PDF](ban-in-bao-gia-20260911/02-minh-hoa-05-dong.pdf) | [HTML](ban-in-bao-gia-20260911/02-minh-hoa-05-dong.html) | 2 |
| 3 | 20 dòng | [ảnh](ban-in-bao-gia-20260911/03-minh-hoa-20-dong.png) | [PDF](ban-in-bao-gia-20260911/03-minh-hoa-20-dong.pdf) | [HTML](ban-in-bao-gia-20260911/03-minh-hoa-20-dong.html) | 4 |
| 4 | 30 dòng | [ảnh](ban-in-bao-gia-20260911/04-minh-hoa-30-dong.png) | [PDF](ban-in-bao-gia-20260911/04-minh-hoa-30-dong.pdf) | [HTML](ban-in-bao-gia-20260911/04-minh-hoa-30-dong.html) | 6 |
| 5 | **Bản NHÁP** có dấu chống gửi nhầm | [ảnh](ban-in-bao-gia-20260911/05-minh-hoa-ban-nhap-co-dau-chim.png) | [PDF](ban-in-bao-gia-20260911/05-minh-hoa-ban-nhap-co-dau-chim.pdf) | [HTML](ban-in-bao-gia-20260911/05-minh-hoa-ban-nhap-co-dau-chim.html) | 2 |

### Xem ngay tại đây — bốn bản chính

**Bản 1 dòng** — ngắn nhất, soi đầu trang và khối thông tin khách:

![Bản in báo giá 1 dòng](ban-in-bao-gia-20260911/01-minh-hoa-01-dong.png)

**Bản 5 dòng** — cỡ hay gặp nhất, soi bảng sản phẩm và tên rất dài:

![Bản in báo giá 5 dòng](ban-in-bao-gia-20260911/02-minh-hoa-05-dong.png)

**Bản 20 dòng** — soi chỗ chuyển trang, đầu bảng có lặp lại không:

![Bản in báo giá 20 dòng](ban-in-bao-gia-20260911/03-minh-hoa-20-dong.png)

**Bản 30 dòng** — báo giá dài nhất, sáu trang:

![Bản in báo giá 30 dòng](ban-in-bao-gia-20260911/04-minh-hoa-30-dong.png)

**Bản NHÁP** — thứ chặn việc gửi nhầm bản chưa duyệt cho khách:

![Bản in báo giá bản nháp có dấu chìm](ban-in-bao-gia-20260911/05-minh-hoa-ban-nhap-co-dau-chim.png)

---

### Bảng tự kiểm bố cục

| Điều | Kết quả | Điều | Kết quả |
|---|---|---|---|
| Nhận diện công ty (logo · tên · MST · hotline) | ✅ | Xuống dòng khi tên dài | ✅ |
| Thông tin khách (tên · mã · địa chỉ · MST · liên hệ) | ✅ | Chuyển trang không cắt đôi sản phẩm | ✅ |
| Bảng sản phẩm — hiện **mọi** phương án, đánh dấu cái được chọn | ✅ | Đầu bảng lặp khi sang trang | ✅ |
| Tổng tiền — ba dòng, dùng số của hệ thống | ✅ | Ghi chú | ✅ |
| Ngày `DD/MM/YYYY` · số kiểu Việt Nam | ✅ | Hai ô chữ ký | ✅ |
| Khổ A4 dọc, lề 1,5 cm | ✅ | **Không lộ chữ trạng thái nội bộ** | ✅ |
| Không có nút bấm lọt vào bản in | ✅ | Bản nháp / hết hiệu lực bị đóng dấu | ✅ |

### 🔴 Một điều mới vá trong đợt này: bản in từng lộ chữ nội bộ

Bản in cũ đóng **nhãn trạng thái quy trình** lên đầu **mọi** tờ giấy — *"Nháp"*,
*"Từ chối"*, *"Đã duyệt tạo đơn"*. Ba hậu quả đều thật:

1. Khách nhận tờ báo giá đóng dấu *"Từ chối"* thì không hiểu là gì, và nó làm
   hỏng quan hệ.
2. Bản **nháp** in ra rồi gửi đi mà **không có gì cản** — nó trông y hệt bản chính thức.
3. Bản **hết hiệu lực** cũng vậy: khách có thể cầm tờ giá cũ đi đặt hàng.

Nay: nhãn đó **gỡ hẳn**. Trạng thái chỉ dùng để quyết định bản in có được gửi
khách không, và biểu hiện ra ngoài là **dấu chìm chéo trang** — xem bản số 5.
Trạng thái lạ (ai đó thêm mới mà quên cập nhật) cũng bị đóng dấu, không mặc định
cho gửi.

### Điểm thẩm mỹ còn muốn Owner để mắt

- Độ đậm của dấu chìm: hiện để nhạt (16% đỏ) để không át chữ. Anh thấy cần đậm hơn?
- Dòng "Nhà máy" trong khối công ty: giữ hay bỏ cho gọn?
- Khoảng trống chừa ký tay: hiện 70px. Đủ chưa?

---

## ④ BẰNG CHỨNG NGHIỆP VỤ — CHẠY THẬT, KHÔNG PHẢI ĐỌC MÃ

Chạy bằng Chrome thật, đăng nhập thật, 32 bước — **31 đạt · 0 hỏng**.
Lệnh: `npm run test:pilot-m1-m3`.

| Điều phải chứng minh | Cách đo | Kết quả |
|---|---|---|
| Sales chỉ thấy khách được giao | màn Khách Hàng hiện *Tổng: 3* trong khi danh mục khách của công ty lớn hơn hàng trăm lần | ✅ `UI_PROVEN` |
| Chưa chọn khách thì không chọn được sản phẩm | ô sản phẩm mờ, ghi *"Chọn khách hàng trước"* | ✅ `UI_PROVEN` |
| Sản phẩm đúng khách | ô chỉ hiện 3 sản phẩm của khách đó; sản phẩm gắn mã khách không tồn tại **nằm ngoài** | ✅ `UI_PROVEN` |
| Tạo nhanh — khách bị khoá | form hiện đúng tên khách + *"đã khoá theo báo giá đang lập"* | ✅ `UI_PROVEN` |
| Tạo nhanh — **bản nháp còn nguyên** | ngày hiệu lực đang gõ vẫn còn; dòng sản phẩm thêm trước vẫn còn | ✅ `UI_PROVEN` |
| Tạo nhanh — tự chọn vào báo giá | sản phẩm mới xuất hiện ngay trong danh sách dòng | ✅ `UI_PROVEN` |
| Khách **giữ nguyên** qua hai lần mở tạo nhanh | so tên khách lần 1 và lần 2 | ✅ `UI_PROVEN` |
| Mã sản phẩm do **máy chủ** cấp, gắn **đúng khách** | đọc thẳng CSDL: mã sinh tự động · `ma_khach_hang` đúng · `nguoi_tao` = tài khoản Sales | ✅ `DB_PROVEN` |
| Chống trùng tên | gõ lại cùng tên **viết thường không dấu chuẩn** → vẫn bị bắt, bày sản phẩm cũ ra để chọn | ✅ `UI_PROVEN` |
| Không tạo trùng | đếm trong CSDL: **1 bản ghi**, không phải 2 | ✅ `DB_PROVEN` |
| **Không còn chữ tự do** | mọi dòng báo giá mới đều có định danh sản phẩm | ✅ `DB_PROVEN` |
| Sales **không tự duyệt** báo giá của mình | nút Duyệt khoá với vai Kinh doanh | ✅ `UI_PROVEN` |
| Báo giá thật được lập | bản ghi mới trong CSDL, có mã, có tổng tiền, người tạo = Sales | ✅ `DB_PROVEN` |
| Admin duyệt được | trạng thái chuyển sang *duyệt tạo đơn* | ✅ `DB_PROVEN` |
| **Đơn hàng thật** được tạo | bản ghi đơn mới, tổng tiền khớp báo giá | ✅ `DB_PROVEN` |
| **Ghi chú người dùng được lưu** | `ghi_chu` = dòng truy vết hệ thống **+** ghi chú người dùng | ✅ `DB_PROVEN` |
| Ngày giao dự kiến được lưu | đúng ngày đã chọn trong hộp thoại | ✅ `DB_PROVEN` |
| **Đơn hàng được xác nhận** | trạng thái *đã xác nhận* — chặng cuối của pilot | ✅ `DB_PROVEN` |
| **Cảnh báo vàng hiện ra thật** | ảnh chụp: *"Đã chuyển trạng thái — nhưng CHƯA trọn… hãy tự liên hệ khách nếu cần"* | ✅ `UI_PROVEN` |

**Ảnh nghiệm thu:** desktop và 390px, ở `docs/anh-kiem-thu/pilot-m1-m3-20260911/`
— thư mục **bị git bỏ qua** vì ảnh có dữ liệu khách thật.

**Dữ liệu thử:** mọi bản ghi mang tiền tố `PILOT-20260911`, truy vết được, dọn
được bằng `scripts` đi kèm. Không đụng dữ liệu của những khách còn lại.

### Ba lần bài kiểm báo HỎNG mà ứng dụng thì ĐÚNG

Ghi ra để người sau không mất công đo lại — cả ba đều là lỗi của **bài kiểm**:

1. Bấm bằng `element.click()` trong mã trang gửi sự kiện **không đáng tin**, khung
   giao diện lúc nhận lúc không → đổi sang phép bấm thật của công cụ.
2. Đếm **số phần tử** thay vì đếm **số mã khách phân biệt** → đếm nhầm cả phần tử
   bọc lồng nhau, báo 4 khách trong khi màn hình hiện đúng 3.
3. Chờ 5 giây rồi mới đọc thông báo nổi — nó **tự tắt sau ~4 giây** → báo "không
   bắt được cảnh báo" trong khi cảnh báo có hiện.

Nếu tin ngay lượt chạy đầu, tôi đã báo với Owner rằng hệ thống hỏng ba chỗ trong
khi nó hoàn toàn bình thường.

---

## ⑤ NỢ KỸ THUẬT

| Nợ | Trạng thái | Căn cứ |
|---|---|---|
| `DEBT-152` bản in | 🔶 **ĐANG XỬ LÝ** | Mã xong · render xong · **chờ Owner duyệt bằng mắt** |
| `DEBT-173` báo xanh giả | ✅ **ĐÃ XỬ LÝ — nay có `UI_PROVEN`** | Đã **nhìn thấy** cảnh báo vàng thật khi xác nhận đơn, có ảnh |
| `DEBT-185` đăng nhập | 🔶 **ĐANG XỬ LÝ** | Máy nội bộ đã gỡ và đã dùng thật · **máy vận hành chưa kiểm — tách riêng, không gộp** |
| `DEBT-189` vân tay | 🔶 **ĐANG XỬ LÝ** | Vá gốc + siết sau kiểm ngược · **chưa chạy trên máy vận hành nên chưa đóng** |
| `DEBT-193` cổng PII mù | 🔶 **ĐANG XỬ LÝ** | Bộ công khai đợt này **chỉ dùng dữ liệu bịa** (mã `KHMAU-0001`); bản dữ liệu thật để ngoài kho. Cổng vẫn chưa tự bắt được tên+địa chỉ — còn nợ |
| `DEBT-194` bốn lỗ vân tay | 🔶 **ĐANG XỬ LÝ** | Đã phân loại — xem bảng dưới |
| `DEBT-195` T6·T7 | ⏸️ **HOÃN CÓ CHỦ ĐÍCH** | Giữ `NOT_CHECKED`, **không ghi PASS giả**. Không chặn pilot một Admin + một Sales |
| `DEBT-196` dữ liệu sai khách | 🔶 **ĐÃ CÁCH LY** | Sản phẩm gắn mã khách không tồn tại **tự nằm ngoài** tập pilot vì bộ lọc theo khách. **Không xoá, không đoán chủ** |
| `DEBT-197` ô nhập trang trí | ✅ **ĐÃ XỬ LÝ** | Ba ô là bản trùng → gỡ; ô Ghi chú → **lưu thật**, có bằng chứng CSDL |

### `DEBT-194` — bốn lỗ vân tay, phân loại theo đường phát hành chuẩn

| Lỗ | Nằm trên đường phát hành chuẩn? | Xử lý |
|---|---|---|
| 1. Tệp môi trường riêng máy không được băm | **CÓ** | **Giới hạn cố hữu** — không băm được vì mỗi máy một khác. Phải nói thẳng, không được để câu *"vân tay chứng minh toàn vẹn"* bị hiểu quá tầm |
| 2. Ba công thức vân tay song song còn lại | **KHÔNG** — thuộc công cụ tiền kiểm | Ghi nợ. Riêng một cái luôn băm thư mục **đã bị xoá** ⇒ luôn cho vân tay của hư không |
| 3. Không đường triển khai nào **tự động** gọi cổng | **CÓ** | Cơ chế đúng mà không ai bấm thì giá trị thi hành bằng 0. Cần nối vào bước tiền-triển-khai |
| 4. Bản kê nằm ngay trên máy vận hành | **CÓ** | Giới hạn cố hữu của mọi cơ chế tự chứng thực. Muốn chặt hơn thì bản kê phải ký hoặc để nơi máy vận hành không ghi được |

**Lỗ 1 và 4 là giới hạn bản chất**, không vá được trong phạm vi gói này — đã ghi
rõ để không ai hiểu nhầm. **Lỗ 3 là việc làm được** và nên làm cùng lượt đóng
`DEBT-189`. **Lỗ 2 nằm ngoài đường chuẩn** nên ghi nợ, có bằng chứng cách ly.

---

## ⑥ KIỂM THỬ VÀ PHÁT HÀNH

| Cổng | Kết quả |
|---|---|
| Kiểm kiểu toàn dự án | **sạch** |
| Bài kiểm bản in (60 điều kiện, có nhóm riêng cho từng trạng thái) | **60/60** |
| Bài kiểm không-báo-xanh-giả (18 điều kiện, gọi hàm thật) | **đạt** |
| Bài kiểm sản phẩm trong báo giá (26 điều kiện) | **đạt** |
| Bài kiểm vân tay bản dựng (52 điều kiện) | **đạt** |
| Bộ chạy pilot thật (32 bước, trình duyệt thật) | **31 đạt / 0 hỏng** |
| Nhóm bài kiểm nhanh | **đạt** |
| Nhóm bài kiểm cần cơ sở dữ liệu | **đạt** |
| Cổng quét bí mật · quét dữ liệu cá nhân | **đạt** |
| Cổng cổng-mồ-côi | **3/3** |
| Lint | **không tăng** ở bất kỳ tệp nào đợt này sửa *(xem ghi chú)* |

> **Ghi chú về lint:** toàn dự án đang có sẵn 843 cảnh báo/lỗi từ trước.
> Đã đối chiếu từng tệp đợt này sửa với bản trước gói: **không tệp nào tăng**,
> một tệp còn **giảm**. Các tệp mới thêm: **sạch**. Việc dọn 843 mục đó nằm ngoài
> phạm vi gói này.

### Biên nhận bản phát hành ứng viên

| Điều | Giá trị |
|---|---|
| Phiên bản | **`V1.00.371`** |
| Mã nguồn ứng viên (đầy đủ) | **`«mã nguồn ứng viên — ghi ở kho riêng»`** |
| Nhánh | `main` |
| Trên đĩa = HEAD = | `V1.00.371` *(đã chạy `npm run release:status` xác nhận)* |
| Cây làm việc | sạch sau khi chốt |
| Cổng tăng phiên bản | tự động kiểm: **đúng +1 bậc**, cho qua |
| Vân tay bản dựng | **`«vân tay — ghi ở kho riêng»`** · **2.832 tệp** · hợp đồng `VT-2` |

> ⚠️ **Vân tay trên đo bản dựng NỘI BỘ**, không phải thư mục chạy trên máy vận
> hành (`.standalone-run` — chỉ tồn tại sau khi kích hoạt trên máy vận hành).
> Nó chứng minh **cơ chế chạy được và cho giá trị thật**, chưa chứng minh bản
> trên máy vận hành. Đây chính là lý do `DEBT-189` **chưa đóng**.

### Bốn commit của gói này

| Mã | Nội dung |
|---|---|
| gói 1 | `DEBT-197` ô nhập thật + bảo vệ trạng thái bản in (không lộ chữ nội bộ) |
| gói 2 | vá **HAI lỗ chặn** làm đứt chuỗi nghiệp vụ + bộ chạy pilot thật |
| gói 3 | bộ duyệt bố cục bản in — 5 bản + tệp chỉ mục |
| **bản phát hành** | **bản phát hành `V1.00.371`** |

**27 tệp đổi · 1.517 dòng thêm · 67 dòng bớt.** Mã nguồn chạm đúng 7 tệp:
`bao-gia-client.tsx` · `bao-gia-print-content.ts` · `actions.ts` ·
`SelectOptionForOrderDialog.tsx` · `m3-store.ts` · `ban-in-bao-gia-policy.ts` (mới) ·
`version.ts`. Còn lại là bài kiểm, bộ dựng và tài liệu.

### Bộ bản in được dựng từ ĐÚNG mã nguồn nào

Bộ cũ dựng ở gói 2 khi hệ thống còn mang `V1.00.370` ⇒ theo đúng luật đã chốt,
bộ đó **hết hiệu lực** khi mã nguồn đổi. Đã **dựng lại trọn bộ** tại
`«mã nguồn ứng viên — ghi ở kho riêng»`.

Giữa hai mã nguồn ấy git báo **đúng một tệp đổi: `src/lib/version.ts`** — và tệp đó
không tham gia dựng bản in (đã tìm trong bộ dựng: không chỗ nào gọi tới). Nên bộ mới
và bộ cũ khác nhau ở chỗ nào cũng chỉ là dữ liệu bên trong tệp PDF, không phải bố cục.

**Bản kê bộ duyệt bố cục** — 16 tệp (5 HTML · 5 PDF · 5 ảnh · tệp chỉ mục), mỗi tệp
có mã băm SHA-256 và cỡ tệp ghi trong **bản nội bộ**. Mã băm bị che ở bản công khai
vì luật của dự án xếp chuỗi băm vào nhóm dấu vết hạ tầng nội bộ.
### Sao lưu và cách lùi lại — chuẩn bị trước, chưa dùng

**Trước khi triển khai** (chỉ chạy sau khi Owner xác nhận ở cổng thứ hai):

1. Sao lưu cơ sở dữ liệu máy vận hành, ghi lại tên tệp sao lưu và cỡ tệp.
2. Ghi lại mã nguồn **đang chạy** trên máy vận hành trước khi đổi — đó là mốc lùi về.
3. Ghi lại vân tay thư mục chạy hiện tại, để sau khi đổi còn đối chiếu.

**Nếu phải lùi lại:** đưa mã nguồn về đúng mốc đã ghi ở bước 2, dựng lại, kích hoạt
lại, rồi đối chiếu vân tay với giá trị đã ghi ở bước 3.

> ⚠️ Gói này **KHÔNG có di trú cơ sở dữ liệu** — không thêm, không xoá, không đổi
> bảng hay cột nào. Cái cần lùi chỉ là mã nguồn. Sao lưu cơ sở dữ liệu vẫn làm, theo
> nguyên tắc, chứ không phải vì gói này chạm vào dữ liệu.

**Đã đẩy lên kho riêng. CHƯA triển khai, CHƯA kích hoạt trên máy vận hành** — chờ
Owner duyệt bố cục trước, vì bản in là một phần của thứ sẽ phát hành.

---

## ⑦ VIỆC OWNER CẦN XÁC NHẬN

**Bây giờ — chỉ một việc:** duyệt bố cục bản in báo giá.
Mở [`ban-in-bao-gia-20260911/README.md`](ban-in-bao-gia-20260911/README.md), xem
ảnh/PDF/HTML của cả năm bản.

**Sau đó** mới tới việc xác nhận triển khai — tôi sẽ trình biên nhận phát hành đầy
đủ (phiên bản · mã nguồn chính xác · danh sách tệp đổi · bản kê · vân tay · sao lưu
· cách lùi lại) rồi hỏi đúng một câu.

---

## ⑧ SỰ CỐ TRONG PHIÊN — TỰ BÁO

Khi đang đo lint, tôi chạy `git stash pop` mà **không có stash nào của mình**.
Lệnh đó mở nhầm **stash của phiên làm việc khác** (`DEBT-049` — thứ chính prompt
ghi là không được đụng) và tạo xung đột ở 9 tệp, trong đó có cả 5 tệp quản trị.

**Đã khắc phục ngay và kiểm chứng đủ:** đưa cây làm việc về đúng mốc đã commit ·
**cả hai stash còn nguyên** · 5 tệp quản trị đồng bộ trở lại · mọi bản vá của gói
còn đủ · kiểm kiểu sạch. Không mất gì.

**Bài học đã ghi:** trong kho có stash của phiên khác thì `git stash pop` là lệnh
nguy hiểm — phải kiểm tra lệnh `push` của mình có thật sự tạo stash hay không
trước khi `pop`.

---

### Sự cố thứ hai — tôi đẩy bản công khai chưa che, cổng bắt được

Tôi đẩy bản công khai lần đầu mà **chưa chạy cổng an toàn báo cáo công khai**. Cổng
chạy sau đó bắt **hai điều**: bản đó có mã nguồn của kho riêng, vân tay bản dựng, mã
băm bản kê — và **số lượng khách chính xác**. (Bản anh đang đọc đã che cả hai.)

Tôi đã tự lý luận rằng số lượng khách chỉ là "số lượng kỹ thuật" nên công khai được.
**Cổng đúng, tôi sai** — trong chính mã của cổng có ghi sẵn bài học ngày 03/09 về
đúng lỗi này: *"báo cáo từng tự ghi «công khai-an toàn vì chỉ nêu số lượng» — SAI.
Chính con số đó LÀ dữ liệu kinh doanh."*

**Đã khắc phục đúng cách cổng chỉ định:** che bằng **một commit mới**
(`«lần đẩy 2 — mã ghi ở bản nội bộ»`), **không viết lại lịch sử, không đẩy ép**
— đúng chỉ thị Owner sổ `#224`. Cổng nay **7/7 sạch** trên toàn bộ 147 tệp báo cáo.

**Thứ đã lộ trong lịch sử kho công khai:** mã commit của kho riêng, vân tay một bản
dựng trên máy phát triển, mã băm các tệp bản in, và hai con số đếm khách.
**KHÔNG lộ:** mật khẩu, khoá, địa chỉ máy chủ, tên hay địa chỉ khách hàng nào.

**Bài học đã ghi:** chạy cổng công khai **TRƯỚC** khi đẩy, không phải sau.

---

## ⑨ CHƯA XÁC MINH ĐƯỢC

| Điều | Vì sao | Ai xác minh được |
|---|---|---|
| Toàn bộ hành vi trên **máy vận hành** | Gói này chưa mở quyền triển khai | Sau khi Owner xác nhận |
| Vân tay bản dựng trên máy vận hành thật | Cùng lý do — bằng chứng cao nhất hiện có là chạy trong Linux máy ảo | Lần kích hoạt kế tiếp |
| Ứng dụng có tự ghi thêm gì vào thư mục bản chạy sau khi khởi động không | Chỉ đo được trên máy vận hành thật | Quyết định cổng vân tay ổn định hay đỏ vĩnh viễn |
| T6·T7 vai Thiết Kế | Không tài khoản nào mang vai đó; gán thêm là vượt phạm vi Owner khoá | Cần Owner quyết |

---

```
════════════ BÁO CÁO KẾT THÚC ════════════
1. ĐÃ LÀM
   - Vá DEBT-197: ba ô nhập trang trí gỡ bỏ, ô Ghi chú lưu thật xuyên ba tầng
   - Vá ⑤B: bản in không còn lộ chữ trạng thái nội bộ; thêm dấu chìm fail-closed
   - Vá HAI lỗ chặn làm đứt chuỗi nghiệp vụ (gửi duyệt · tạo đơn từ báo giá đã duyệt)
   - Viết bộ chạy pilot thật bằng trình duyệt: 32 bước, 31 đạt / 0 hỏng
   - Dựng bộ duyệt bố cục: 5 bản × (HTML + PDF A4 + ảnh) + tệp chỉ mục
   - Tăng phiên bản lên V1.00.371 (đã tra là số chưa từng dùng)
   - Cập nhật báo cáo private + public; ghi sổ Owner và sổ nợ

2. PHẠM VI
   ĐỤNG      : src/app/m3/bao-gia/{bao-gia-client,bao-gia-print-content,actions} ·
               src/components/m3/SelectOptionForOrderDialog.tsx · src/lib/m3-store.ts ·
               src/lib/m3/ban-in-bao-gia-policy.ts (mới) · src/lib/version.ts ·
               scripts/tests/{chay-pilot-m1-m3.mjs (mới), bao-gia-print-parity.test.ts} ·
               scripts/dung-ban-xem-thu-bao-gia.mjs · package.json ·
               docs/reports/ · sổ Owner · sổ nợ
               CSDL nội bộ: bản ghi thử mang tiền tố PILOT-20260911
   KHÔNG ĐỤNG: máy vận hành · Notion · lược đồ CSDL · Pricing · M4/M5/MF/M9 ·
               scripts/skill-router.mjs · dữ liệu những khách còn lại ·
               hai stash của phiên khác (đã kiểm chứng còn nguyên sau sự cố)

3. BẰNG CHỨNG
   npm run test:pilot-m1-m3     → 31 đạt / 0 hỏng / 32 bước   → UI_PROVEN + DB_PROVEN
   npm run test:ban-in-bao-gia  → 60/60                        → CODE_PROVEN
   npm run test:bao-xanh-gia    → đạt                          → CODE_PROVEN + DB_PROVEN
   npm run test:san-pham-bao-gia→ đạt                          → CODE_PROVEN + DB_PROVEN
   npm run test:van-tay-ban-dung→ 52/52                        → CODE_PROVEN
   npm run test:nhom-nhanh      → đạt                          → CODE_PROVEN
   npm run test:nhom-csdl       → đạt                          → DB_PROVEN
   npm run test:cong-mo-coi     → 3/3                          → CODE_PROVEN
   npx tsc --noEmit             → sạch                          → CODE_PROVEN
   ảnh nghiệm thu desktop + 390px ở docs/anh-kiem-thu/          → UI_PROVEN

4. GHI SỔ YÊU CẦU OWNER
   [x] ĐÃ GHI — mục #256 (gói bổ sung); mục #255 là gói trước

5. PUSH BÁO CÁO CÔNG KHAI
   [x] ĐÃ PUSH — kho Baocaoerptanphat
       commit «lần đẩy 1 — mã ghi ở bản nội bộ»  (đẩy lần 1)
       commit «lần đẩy 2 — mã ghi ở bản nội bộ»  (che nội dung — xem mục ⑧)
       file   BUSINESS-PILOT-M1-M3-20260911.md
              + ban-in-bao-gia-20260911/ (16 tệp: 5 HTML · 5 PDF · 5 ảnh · README)
       Bản công khai ĐÃ CHE: mã nguồn kho riêng · vân tay bản dựng · mã băm
       bản kê · số lượng khách chính xác. Nội dung nghiệp vụ giữ nguyên.
       Cổng `npm run test:bao-cao-cong-khai` → 7/7 PASS trên 147 tệp.

6. CÒN SÓT / CHƯA LÀM
   - Chưa commit bản phát hành V1.00.371, chưa đẩy, chưa triển khai (đúng luật gói)
   - T6·T7 giữ NOT_CHECKED (DEBT-195)
   - DEBT-193: cổng PII vẫn chưa tự bắt được tên+địa chỉ trong tệp báo cáo
   - DEBT-194 lỗ 3 (không đường triển khai nào tự gọi cổng vân tay) chưa nối
   - 843 mục lint có sẵn của dự án — ngoài phạm vi gói này

7. ĐANG CHỜ OWNER
   - Duyệt bố cục bản in → chặn đóng DEBT-152 và toàn bộ bước phát hành
   - (sau đó) Xác nhận triển khai → chặn mọi bằng chứng trên máy vận hành

8. BƯỚC KẾ TIẾP — ĐÚNG MỘT VIỆC
   Owner mở docs/reports/ban-in-bao-gia-20260911/README.md, xem năm bản
   (ảnh + PDF + HTML), rồi trả lời câu hỏi duyệt bố cục ở cuối báo cáo này.

9. CHƯA XÁC MINH ĐƯỢC
   - Mọi hành vi trên máy vận hành — gói này chưa mở quyền triển khai
   - Vân tay bản dựng trên máy vận hành thật
   - Ứng dụng có tự ghi thêm vào thư mục bản chạy sau khi khởi động không

10. TRẠNG THÁI CHUNG
   [x] PROVISIONAL — READY_FOR_OWNER_LAYOUT_REVIEW.
       Điều kiện lên PASS: Owner duyệt bố cục → trình biên nhận phát hành →
       Owner xác nhận triển khai → chạy nghiệm thu trên máy vận hành.

11. NÉN PHIÊN & ĐỌC LẠI THAM CHIẾU
   Phiên có bị nén ngữ cảnh không: CÓ (nén ở đầu phiên trước)
   Đã đọc lại sau nén, đọc thật từ đĩa:
     - CLAUDE.md (tự tiêm lại) · .governance/registry/tech-debt.md
     - docs/golive/GOLIVE-PLAN.md (ma trận T1–T9) · docs/PLAN-OF-RECORD.md
     - docs/UI-STANDARD.md · docs/UI-ACCEPTANCE-CHECKLIST.md
     - docs/Form Mẫu Tham Khảo/01_Bao_Gia.html (mẫu Owner duyệt)
     - toàn bộ src/app/m3/bao-gia/ · src/lib/m3-store.ts · workflow-service.ts
     - src/components/m3/SelectOptionForOrderDialog.tsx
     - scripts/van-tay-artifact.sh · scripts/tests/kiem-dinh-danh-phat-hanh.mjs
   Không dùng trí nhớ từ trước nén cho bất kỳ kết luận nào.
═══════════════════════════════════════════
```

---

*Báo cáo đã qua cổng công khai: không địa chỉ máy chủ · không đường dẫn tuyệt đối của
máy vận hành · không địa chỉ thư của người thật · không khoá hay mật khẩu · không tên,
địa chỉ hay điện thoại của khách hàng · không số tiền của giao dịch nào.*

> ⚠️ **Bản này là BẢN NỘI BỘ.** Nó có mã nguồn, vân tay bản dựng và số lượng khách
> chính xác — ba thứ mà luật công khai của dự án **xếp vào nhóm chặn**. **Bản đưa lên
> kho công khai đã che cả ba**, nội dung nghiệp vụ giữ nguyên.
>
> Tôi đã định giữ nguyên số lượng khách trong bản công khai với lý do "đó chỉ là số
> lượng kỹ thuật". **Cổng của dự án chặn lại và cổng đúng** — chính con số đó là dữ
> liệu kinh doanh, và trong mã cổng còn ghi sẵn bài học ngày 03/09 về đúng lỗi này.
