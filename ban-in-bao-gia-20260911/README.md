# BỘ DUYỆT BỐ CỤC BẢN IN BÁO GIÁ — 11/09/2026

> **Để làm gì:** Owner nhìn trực tiếp rồi chốt bố cục, trước khi khoá bản phát hành.
> **Sinh từ:** mã nguồn của **bản phát hành ứng viên** (mã ghi ở kho riêng) · phiên bản `V1.00.371`
> **Dựng lại lúc:** 11/09/2026, ngay sau khi chốt bản phát hành — bộ cũ (dựng ở bản trước,
> mang `V1.00.370`) đã **hết hiệu lực** và được thay trọn. Giữa hai mã nguồn đó chỉ
> có **một** tệp đổi: `src/lib/version.ts` — tệp này **không** tham gia dựng bản in.
> **Bộ dựng:** `npx tsx scripts/dung-ban-xem-thu-bao-gia.mjs` — dùng **đúng hàm**
> mà ứng dụng dùng khi in thật (`generateBaoGiaPrintHtml`), không phải bản chép lại.

---

## Mở cái nào trước

**Xem nhanh nhất:** mở tệp `.png` — đó là ảnh chụp đúng chế độ in, nút bấm trên màn
đã tự ẩn. **Xem đúng như in ra giấy:** mở tệp `.pdf` (khổ A4, lề 1,5 cm).
**Xem để soi chi tiết:** mở tệp `.html` bằng trình duyệt rồi bấm Ctrl+P.

| # | Bản | Ảnh | PDF | HTML | Số trang | Cỡ PDF |
|---|---|---|---|---|---|---|
| 1 | **1 dòng** — báo giá ngắn nhất | [ảnh](01-minh-hoa-01-dong.png) | [PDF](01-minh-hoa-01-dong.pdf) | [HTML](01-minh-hoa-01-dong.html) | 1 | 366 KB |
| 2 | **5 dòng** — cỡ hay gặp nhất | [ảnh](02-minh-hoa-05-dong.png) | [PDF](02-minh-hoa-05-dong.pdf) | [HTML](02-minh-hoa-05-dong.html) | 2 | 376 KB |
| 3 | **20 dòng** — soi chuyển trang | [ảnh](03-minh-hoa-20-dong.png) | [PDF](03-minh-hoa-20-dong.pdf) | [HTML](03-minh-hoa-20-dong.html) | 4 | 390 KB |
| 4 | **30 dòng** — báo giá dài | [ảnh](04-minh-hoa-30-dong.png) | [PDF](04-minh-hoa-30-dong.pdf) | [HTML](04-minh-hoa-30-dong.html) | 6 | 400 KB |
| 5 | **Bản NHÁP** — có dấu chống gửi nhầm | [ảnh](05-minh-hoa-ban-nhap-co-dau-chim.png) | [PDF](05-minh-hoa-ban-nhap-co-dau-chim.pdf) | [HTML](05-minh-hoa-ban-nhap-co-dau-chim.html) | 2 | 389 KB |

> ⚠️ **Cả năm bản dùng DỮ LIỆU BỊA, có nhãn.** Đầu mỗi trang có dải vàng
> *"DỮ LIỆU MINH HOẠ — KHÔNG PHẢI BÁO GIÁ THẬT"*, mã khách là `KHMAU-0001`.
> Bản dựng từ **dữ liệu thật** cố ý **không** nằm ở đây vì nó chứa tên, địa chỉ và
> điện thoại khách thật — nó nằm ở `docs/anh-kiem-thu/` (thư mục bị git bỏ qua).

---

## Anh cần nhìn kỹ những chỗ này

| Chỗ | Nhìn gì | Bản nào rõ nhất |
|---|---|---|
| **Đầu trang** | Logo có méo không · tên công ty · địa chỉ trụ sở và nhà máy · mã số thuế · hotline | bản 1 dòng |
| **Thông tin khách** | Kính gửi · Mã KH · Địa chỉ · MST · Người liên hệ · NV phụ trách | bản 1 dòng |
| **Bảng sản phẩm** | Mọi phương án giá đều hiện, ô vuông cam đánh dấu cái được chọn | bản 5 dòng |
| **Tên dài** | Dòng cuối của bản 5/20/30 cố ý đặt tên **rất dài** để soi tràn chữ | bản 5 dòng |
| **Chuyển trang** | Một sản phẩm có bị cắt đôi giữa hai trang không · đầu bảng có lặp lại không | bản 20 và 30 dòng |
| **Tổng tiền** | Ba dòng: Tổng tiền hàng · Thuế GTGT · **TỔNG CỘNG** | mọi bản |
| **Thuế** | Ghi *"Thuế GTGT (nếu áp dụng) / Theo hóa đơn"* — **cố ý không có con số** | mọi bản |
| **Ghi chú** | Dòng ghi chú của báo giá + câu mời khách đánh dấu phương án | mọi bản |
| **Chữ ký** | Hai ô: *Người lập báo giá (Kinh doanh)* và *Khách hàng xác nhận* | mọi bản |
| **Dấu chống gửi nhầm** | Dấu chìm chéo trang + dải đỏ giải thích | **bản NHÁP** |

---

## Những gì đã tự kiểm trước khi trình

| Điều | Kết quả |
|---|---|
| Tiếng Việt có dấu hiển thị đúng | ✅ |
| Khổ A4 dọc, lề 1,5 cm | ✅ |
| Ngày theo `DD/MM/YYYY` | ✅ |
| Số tiền và số lượng theo cách viết Việt Nam | ✅ |
| Tên sản phẩm rất dài **không tràn** ra ngoài giấy | ✅ |
| Tên khách rất dài **không tràn** | ✅ |
| Không cắt đôi một sản phẩm giữa hai trang | ✅ |
| Đầu bảng lặp lại khi sang trang | ✅ |
| Không có nút bấm hay thanh cuộn lọt vào bản in | ✅ |
| **Không lộ chữ trạng thái nội bộ** (Nháp · Từ chối · Đã duyệt tạo đơn) | ✅ |
| Bản nháp / hết hiệu lực bị đóng dấu | ✅ |
| Không bịa thuế, điều khoản, số tài khoản, tên người ký | ✅ |
| Không có dữ liệu cá nhân thật trong bộ này | ✅ |

Bài kiểm tự động: `npm run test:ban-in-bao-gia` — **60/60 điều kiện đạt**, trong đó
nhóm `[14]` kiểm riêng từng trạng thái báo giá.

---

## Bốn thứ cố ý ĐỂ TRỐNG — chờ anh quyết

1. **Suất thuế GTGT** — mẫu anh đã duyệt ghi *"Theo hóa đơn"*, không có con số.
   Trong kho đang có hai số chọi nhau (8% và 10%) nên chọn bên nào cũng là đoán.
2. **Điều khoản thanh toán** — chưa có nguồn nào ghi, nên không in.
3. **Số tài khoản ngân hàng** — chưa có nguồn, không in.
4. **Tên người ký** — chỉ in chức danh và chừa ô trống để ký tay, đúng như mẫu.

Trường nào khách chưa khai thì bản in hiện dấu gạch `—`, không suy đoán, và tuyệt
đối không lấy thông tin công ty mình điền vào chỗ của khách.

---

*Nguồn bố cục: `docs/Form Mẫu Tham Khảo/01_Bao_Gia.html` — mẫu Owner đã duyệt,
chính là tệp mà trang Liên Hệ chỉ đích danh là letterhead chuẩn.*
