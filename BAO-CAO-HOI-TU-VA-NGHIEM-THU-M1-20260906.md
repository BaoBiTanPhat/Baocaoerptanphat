# BÁO CÁO — KIỂM HỘI TỤ BA NƠI · DỌN TÀI LIỆU LỖI THỜI · ĐO NGHIỆM THU M1 (06/09/2026)

> **Kho:** báo cáo công khai (bản đã lọc an toàn) · **Ngày lập:** 06/09/2026
> **Phạm vi quyền của đợt này:** đo đạc và cập nhật tài liệu. **KHÔNG triển khai · KHÔNG đổi mã nghiệp vụ · KHÔNG đổi lược đồ/dữ liệu.**
> **Lớp bằng chứng:** `RUNTIME_PROVEN` (máy vận hành) · `DB_PROVEN` (đọc dữ liệu) · `CODE_PROVEN` · `FILE_PROVEN`.

---

## 1. KẾT LUẬN ĐIỀU HÀNH

**a) Mã đã triển khai đủ chưa? → CHƯA ĐỦ.** Máy vận hành **đang chạy tốt** bản `V1.00.369` (đo lại: dịch vụ sống, **7/7 tuyến trọng yếu trả 200**), nhưng kho mã đã đi thêm **9 lượt commit** sau đợt phát hành 04/09 **mà không tăng số phiên bản**.

**b) Ba nơi có đồng bộ không? → HAI ĐỒNG BỘ, MỘT LỆCH.**

| Nơi | Trạng thái |
|---|---|
| Máy phát triển ↔ kho riêng | ✅ **TRÙNG KHỚP TUYỆT ĐỐI** (0 trước, 0 sau) |
| Kho riêng ↔ máy vận hành | ⚠️ **LỆCH 9 commit** — cùng số `V1.00.369` nhưng **khác mã nguồn** |

**c) M1 nghiệm thu tới đâu? → ĐO ĐƯỢC, CHƯA CHẠY ĐƯỢC.** Phần đo dữ liệu và tài liệu đã xong; phần chạy bài kiểm T1–T9 và chụp ảnh **bị chặn** vì hai lý do độc lập (mục 6).

> 🔴 **Điểm quan trọng nhất:** *"cùng số phiên bản"* **KHÔNG** đồng nghĩa *"cùng mã nguồn"*. Chính cổng kiểm định danh phát hành của dự án đã bắt được và **CẤM TRIỂN KHAI** cho tới khi tăng số phiên bản.

---

## 2. PHÂN XỬ MÂU THUẪN GIỮA CÁC BÁO CÁO CŨ

Trước đợt này tồn tại hai lời khai đối nghịch về `V1.00.369`:

| Lời khai cũ | Phân xử bằng đo đạc 06/09 |
|---|---|
| *"V1.00.369 mới đẩy mã, đang bị chặn triển khai"* | ❌ **BỊ THAY THẾ** — hồ sơ triển khai trên máy vận hành ghi rõ ngày **04/09/2026**, và dịch vụ đang phục vụ thật |
| *"V1.00.369 đã phát hành sau khi vá hai lỗi công cụ triển khai"* | ✅ **ĐÚNG** — có hồ sơ triển khai, có mốc dựng, 7/7 tuyến trả 200 |

⇒ Mọi tài liệu còn ghi `V1.00.369 = DEPLOY_BLOCKED` **đều đã lỗi thời** kể từ 04/09.

---

## 3. BẢNG HỘI TỤ — BA NƠI

| Hạng mục | Máy phát triển | Kho riêng | Máy vận hành | Nhãn |
|---|---|---|---|---|
| Số phiên bản | `V1.00.369` | `V1.00.369` | `V1.00.369` | trùng |
| Mã nguồn (commit) | X | X | **Y (cũ hơn)** | ⚠️ **LỆCH THẬT** |
| Cây làm việc | sạch | — | chỉ khác **bit thực thi** của một kịch bản | `METADATA_DIFF` |
| Số bảng cơ sở dữ liệu | **101** | — | **101** | ✅ khớp |
| Tệp di trú trong phần lệch | **0** | | | ✅ không có rủi ro lược đồ |
| Tuyến trọng yếu | — | — | **7/7 trả 200** | ✅ khoẻ |
| Artifact đang chạy | — | — | mốc sửa **trùng khít** mốc dựng | ✅ không bị can thiệp sau triển khai |

### Phân loại phần lệch (theo bản chất, không theo số lượng)

| Nhãn | Nội dung |
|---|---|
| **`REAL_CODE_DRIFT`** | **10 tệp giao diện** — các bản vá tiêu chuẩn ngày 06/09 (hết lộ khoá nội bộ · số dòng mặc định · dọn đầu bảng). Thuần trình bày, **không đụng nghiệp vụ** |
| **`REAL_CODE_DRIFT` (công cụ)** | **3 kịch bản triển khai** — trong đó **2 kịch bản chạy TRÊN máy vận hành**: bản siết kiểm tuyến và bản siết cổng nạp dữ liệu. Máy vận hành **vẫn đang dùng bản cũ** của hai kịch bản này |
| **`REPORT_ONLY_DELTA`** | 12 tệp tài liệu · sổ · năm bản luật |
| **`SCHEMA_OR_MIGRATION_DRIFT`** | **KHÔNG CÓ** |
| **`METADATA_DIFF`** | bit thực thi của một kịch bản trên máy vận hành (0 dòng thay đổi) |
| **`GENERATED_OR_RUNTIME_ONLY`** | thư mục chạy và hồ sơ triển khai (bình thường) |

---

## 4. HỒ SƠ BAO PHỦ TRIỂN KHAI

| Mục | Kết quả |
|---|---|
| Nguồn số phiên bản | tệp phiên bản trong mã — `V1.00.369` |
| Hồ sơ triển khai trên máy vận hành | **CÓ** — ghi mã nguồn 40 ký tự, số phiên bản, mốc dựng, mốc triển khai, vân tay bản dựng |
| Cổng kiểm định danh phát hành | **3 ĐẠT / 1 HỎNG** — hỏng đúng ở điều *"không đụng độ định danh"* |
| Bài kiểm nhanh sau triển khai | **7/7 tuyến trả 200** |
| Di trú / lược đồ | **101 ≡ 101 bảng**, phần lệch **không chứa tệp di trú** |
| Dấu "đã nạp dữ liệu" | **KHÔNG có** trên máy vận hành ⇒ đợt 04/09 đi qua cổng bằng đường khai *"đợt này không cần nạp dữ liệu"* |

### 🔴 Ba khiếm khuyết của chính cơ chế vân tay bản dựng (phát hiện mới)

1. **Đo hai thư mục khác nhau.** Lúc triển khai, vân tay tính trên thư mục bản dựng máy chủ; lúc kiểm, lại tính trên thư mục chạy. **Hai tập tệp khác nhau ⇒ không bao giờ khớp được**, kể cả khi mọi thứ đều đúng.
2. **Phụ thuộc đường dẫn.** Phép băm bao gồm cả tên tệp, nên chạy bằng đường dẫn tuyệt đối và tương đối cho **hai kết quả khác nhau** trên cùng một artifact. Đo thực tế: ba cách tính cho **ba giá trị khác nhau**.
3. **Luật bắt lệch vân tay không bao giờ chạy.** Cổng có sẵn luật *"vân tay lệch"*, nhưng lúc gọi lại truyền vào **hai chuỗi rỗng**, nên luật đó **chỉ sống trong bài tự kiểm**, không hề canh lượt thật.

⇒ Vân tay hiện **không dùng để kết luận được**. Kết luận "artifact không bị can thiệp" ở mục 3 dựa trên **mốc thời gian tệp**, không dựa vào vân tay. Đã ghi vào sổ nợ; **không sửa trong đợt này** vì quyền được cấp là *kiểm tra*, không phải sửa công cụ.

---

## 5. DỌN TÀI LIỆU LỖI THỜI

**Nguyên tắc áp dụng:** không xoá tệp nào. Không tệp nào hội đủ điều kiện xoá an toàn (đều còn chứa quyết định, bằng chứng hoặc dấu vết truy xuất). Tất cả xử lý bằng **gắn nhãn + con trỏ**.

| Tệp | Nhãn | Xử lý |
|---|---|---|
| `README.md` (kho công khai) | `CURRENT_CANONICAL` — **đã lỗi thời** | ✅ **CẬP NHẬT**: số phiên bản `V1.00.355` → `V1.00.369`; ngày cập nhật 24/08 → 06/09; số bảng đo lại; **thêm cảnh báo cùng-số-khác-mã-nguồn** |
| `GOLIVE-PLAN.md` (**cả hai kho**) | `HISTORICAL_REFERENCE` | ✅ **GẮN NHÃN** mốc nền 14/06; giữ **T1–T9** làm tài sản dùng lại; nêu rõ dòng *"Chờ Owner xác nhận"* là trạng thái **của bản 14/06, đã hết hiệu lực** |
| `MODULE-PROGRESS.md` (**cả hai kho**) | `HISTORICAL_REFERENCE` · **từng `CONFLICT`** | ✅ **GẮN NHÃN cho bản trong kho mã** |
| `GOVERNANCE-LOG.md` | `CURRENT_REFERENCE` — dừng ở 25/08 | ✅ **THÊM KHỐI CON TRỎ** tới 5 báo cáo 03–06/09 + số bản luật hiện hành. Không chép lại log cũ |

### ⚠️ Phát hiện đáng kể: bản nguy hiểm lại là bản KHÔNG có cảnh báo

`GOLIVE-PLAN.md` và `MODULE-PROGRESS.md` tồn tại ở **cả hai kho**. Bản ở kho công khai **đã** mang nhãn lịch sử từ trước — nhưng **bản nằm trong kho mã, tức bản mà tác nhân đọc trực tiếp, thì CHƯA có nhãn nào**. Đo được: hai bản lệch nhau đúng bằng khối nhãn còn thiếu.

Nghĩa là suốt thời gian qua, **tác nhân đọc kho mã vẫn thấy một kế hoạch 14/06 tự xưng "Chờ Owner xác nhận"** và một bảng tiến độ 14/06 không cảnh báo gì — đúng cơ chế khiến việc bị làm lại. Đã gắn nhãn cho cả hai bản trong kho mã.

**Không tệp nào bị xoá ⇒ không có hồ sơ xoá.** Mọi thay đổi đều là thêm khối cảnh báo hoặc sửa số liệu, phục hồi được bằng lịch sử phiên bản.

---

## 6. NGHIỆM THU M1 — ĐO ĐƯỢC GÌ, CHẶN Ở ĐÂU

### 6.1 Đã đo được (không cần đăng nhập)

**Câu hỏi của chủ dự án: năm sản phẩm là danh mục chết hay đang dùng thật?**

| Phép đo trên máy vận hành | Kết quả |
|---|---|
| Dòng báo giá **trỏ vào danh mục sản phẩm** | **5/7** |
| Dòng báo giá **gõ tự do** (không trỏ danh mục) | **2/7** |
| Dòng trỏ vào bản ghi **không còn tồn tại** | **0** — không có dữ liệu mồ côi |
| Sản phẩm trong danh mục **đã từng được dùng** | **3/5** |
| Đơn hàng | **chưa có đơn nào** |

**Kết luận:** danh mục **đang được dùng thật**, dữ liệu **sạch** (không mồ côi), nhưng **mỏng** — và **đường gõ tự do vẫn đang mở**, chiếm khoảng **một phần ba** số dòng.

⇒ Đúng như chủ dự án đã chốt: đây là **tín hiệu cần đo**, **không phải lệnh nhập hàng loạt**. Việc đáng làm tiếp là **quyết định có ràng buộc dòng báo giá phải trỏ danh mục hay không**, chứ không phải đổ thêm sản phẩm vào.

Dữ liệu khách hàng đã có ở quy mô vận hành thật; đơn hàng thì chưa phát sinh — phù hợp với giai đoạn **nghiệm thu/đưa người dùng vào**, không phải giai đoạn xây màn hình.

### 6.2 Bị chặn — hai lý do độc lập

| Việc | Bị chặn bởi |
|---|---|
| Chạy **T1–T9** trên máy vận hành | **Lệch mã nguồn** — quy định nội bộ cấm chạy nghiệm thu vận hành khi ba nơi chưa hội tụ |
| Chạy **T1–T9** trên máy nội bộ · chụp ảnh nghiệm thu | **Không đăng nhập được** — khoá trong sổ bí mật không khớp cơ sở dữ liệu phát triển |

**Bộ T1–T9 đã sẵn sàng**, không cần soạn lại: ma trận quyền **Quản trị / Kinh doanh / Thiết kế** nằm trong kế hoạch 14/06 (nay đã gắn nhãn lịch sử nhưng **phần này giữ nguyên giá trị**).

---

## 7. TRẠNG THÁI THẬT

| Việc | Trạng thái |
|---|---|
| Đóng băng mốc đo trước khi sửa | ✅ XONG |
| Đo hội tụ ba nơi | ✅ XONG — **phát hiện lệch thật** |
| Hồ sơ bao phủ triển khai + cổng phát hành | ✅ XONG — cổng bắt đúng đụng độ định danh |
| Ba khiếm khuyết cơ chế vân tay | ✅ **PHÁT HIỆN & GHI NỢ** — không sửa (ngoài quyền đợt này) |
| Dọn tài liệu lỗi thời | ✅ XONG — 4 nhóm tệp, **0 tệp bị xoá** |
| Đo dùng thật danh mục sản phẩm | ✅ XONG |
| Chạy T1–T9 · ảnh nghiệm thu | ❌ **CHẶN** — mục 6.2 |
| Triển khai | ⛔ **KHÔNG THỰC HIỆN** — ngoài quyền, và cổng đang cấm |

---

## 8. VIỆC KẾ TIẾP — ĐÚNG MỘT VIỆC

**Tăng số phiên bản lên một số chưa dùng rồi phát hành gói bổ sung**, để ba nơi hội tụ. Gói đó **không chứa thay đổi lược đồ**, gồm các bản vá giao diện và **hai kịch bản triển khai đã được siết** — riêng hai kịch bản này còn có tác dụng làm chính lần phát hành sau **an toàn hơn** (kiểm tuyến biết chặn khi hỏng, cổng dữ liệu biết đối chứng).

Việc này **cần chủ dự án duyệt** — đợt này chỉ được cấp quyền kiểm tra.

---

*Bản công khai đã lọc: không mã đăng nhập, không dữ liệu cá nhân, không số liệu kinh doanh tuyệt đối, không dấu vết hạ tầng, không mã commit kho riêng.*
