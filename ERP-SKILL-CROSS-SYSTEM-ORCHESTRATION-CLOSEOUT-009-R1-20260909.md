# ĐÍNH CHÍNH VÀ THAY THẾ — ĐÓNG CHUẨN HỆ ĐIỀU PHỐI KỸ NĂNG (BẢN R1) — 09/09/2026

**Gói việc:** `ERP-SKILL-CROSS-SYSTEM-ORCHESTRATION-CLOSEOUT-009-R1`
**Thay thế:** `ERP-SKILL-CROSS-SYSTEM-ORCHESTRATION-CLOSEOUT-009` (cùng ngày, phát hành trước đó)
**Phạm vi:** CHỈ hệ kỹ năng — không đụng mã sản phẩm · cơ sở dữ liệu · máy vận hành
**Trạng thái:** `PARTIAL` — **không** dùng chữ "hoàn tất", **không** dùng chữ "đạt" trần trụi

> ⚠️ **Bản 009 KHÔNG bị xoá và KHÔNG bị viết lại.** Nó còn nguyên trong lịch sử kho mã và
> vẫn tra được. Bản R1 chỉ **đính chính** những chỗ đo lại thấy sai, và mỗi chỗ đính chính
> đều giữ **nguyên văn** câu cũ để đối chiếu.
>
> **Nếu ai đang dùng bản 009 làm căn cứ: xin dừng và chuyển sang bản này.** Bốn khiếm
> khuyết dưới đây có thể dẫn tới quyết định sai nếu tiếp tục dùng bản cũ.

---

## 1. BỐN KHIẾM KHUYẾT CỦA CHÍNH BẢN 009 — ĐO ĐƯỢC, RỒI SỬA

Đây là phần quan trọng nhất. Cả bốn đều là lỗi **trong chính bản báo cáo và bộ mã mà chúng tôi
vừa phát hành hai giờ trước đó**. Chúng chỉ lộ ra khi **cố tình phá từng cơ chế một** để xem
cổng kiểm có thật sự bắt được không.

### E1 — Loại cứng **hỏng thì MỞ** (nghiêm trọng nhất)

Bộ định tuyến có một cơ chế "loại cứng": khi Chủ dự án đã quyết định rằng một kỹ năng
**không được đề xuất** cho một loại việc, thì nó bị loại thẳng.

Bản 009 kiểm tra điều đó bằng cách hỏi: *"ô căn cứ quyết định có phải là một chuỗi khác rỗng không?"*

**Đo được:** điền vào ô đó ba chữ bất kỳ — ví dụ `BAT KY CHUOI NAO` — là **loại cứng xảy ra**.
Nghĩa là bất kỳ ai gõ bất kỳ chữ gì cũng tạo ra được một **quyết định giả của Chủ dự án**.

Đây là **hỏng thì MỞ**, ngược hẳn nguyên tắc của dự án là **hỏng thì KHOÁ**.

**Đã sửa:** nay phải qua **mười hai cửa**, mỗi cửa hỏng thì khoá — thiếu, sai, hoặc
không tính được bất kỳ cửa nào đều **hạ xuống chỉ cảnh báo**, không bao giờ nới lên:

| # | Cửa | Hỏng thì |
|---|---|---|
| 1 | Trạng thái chính sách phải được **khai tường minh** | cảnh báo |
| 2 | Trạng thái đó phải nằm trong bảng hợp lệ | bỏ qua, không cưỡng chế |
| 3 | Phải **có** căn cứ quyết định | cảnh báo |
| 4 | Phải **đọc được** sổ quyết định | cảnh báo |
| 5 | Căn cứ phải **tra được** tới một mục **có thật** trong sổ | cảnh báo |
| 6 | Quyết định phải **đúng loại** (quyết định về bí danh hay rủi ro **không** bảo chứng cho điều kiện không-chọn) | cảnh báo |
| 7 | Quyết định phải **còn hiệu lực** (chưa thu hồi, chưa bị thay thế) | cảnh báo |
| 8 | Phải khớp **đúng định danh** kỹ năng | cảnh báo |
| 9 | Phải khớp **đúng điều kiện** đã được duyệt | cảnh báo |
| 10 | Ngày phải **hợp lệ** và **không ở tương lai** | cảnh báo |
| 11 | Quyết định phải **còn tươi** trong hạn công bố | cảnh báo |
| 12 | Phải khớp **cả ba phạm vi**: dự án · công cụ · đường dẫn | cảnh báo |

Kèm theo là một **sổ quyết định máy đọc được** — trước đây không có. Sổ này ghi rõ cả những
chỗ **chưa có quyết định**, để không ai tưởng nhầm là đã có.

### E2 — Cảnh báo và quan sát **chưa hề tồn tại**

Bản 009 công bố cơ chế "giữ kỹ năng lại nhưng gắn cảnh báo". **Đo được:** có 25 ứng viên
khớp điều kiện, mà phiếu quyết định xuất ra **không một cảnh báo nào, không một quan sát nào**.
Cơ chế được mô tả trong báo cáo nhưng **không có trong mã**.

**Đã sửa:** nay cảnh báo thật sự được phát ra, mỗi cảnh báo mang đủ tám thông tin (kỹ năng nào ·
trạng thái chính sách nào · khớp điều kiện nào · căn cứ từ đâu · vì sao · phạm vi có khớp không ·
còn tươi không · hành động là **giữ lại kèm cảnh báo**).

### E3 — Gộp tín hiệu **của dự án** với trạng thái **của công cụ**

Bản 009 xếp bốn mục ngang hàng nhau và dùng chung một nhãn cho hai khẳng định khác nhau:

- *"bộ định tuyến không tự nạp nội dung"* — đây là **bất biến theo thiết kế**, luôn đúng;
- *"công cụ không nạp nội dung"* — đây là điều **phải đo mới biết**.

Gộp hai thứ đó vào một nhãn chính là chỗ sinh ra một kết luận **chưa từng được đo**.

**Đã sửa** thành mô hình **1 + 4**:

| Loại | Tên | Nghĩa |
|---|---|---|
| Tín hiệu **của dự án** | bộ định tuyến có đề xuất được không | script của dự án, chạy được ở mọi vỏ lệnh — **không** phải năng lực của công cụ nào |
| Trạng thái **của công cụ** ① | công cụ có **tự thấy** kỹ năng không | phải đo trên chính công cụ đó |
| Trạng thái **của công cụ** ② | công cụ có **tự nạp** nội dung không | phải đo riêng, **cấm** suy từ ① |
| Trạng thái **của công cụ** ③ | công cụ có **tự làm theo** quy trình không | phải đo riêng |
| Trạng thái **của công cụ** ④ | công cụ có **quyền tự thi hành** không | tắt theo thiết kế |

Cộng thêm **một bất biến** ghi riêng: *bộ định tuyến không tự nạp nội dung — theo thiết kế*.
Bất biến này **cấm** được viết lại thành "công cụ không nạp".

### E4 — Hai con số **chọi nhau trong cùng một tệp**

Bản 009 có một ô tự tính ra **6**, còn câu ghi chú ngay bên cạnh viết cứng chữ **"Bảy"**.

**Đo lại:** 8 tổng − 2 đã gỡ = **6 còn lại**. Nhãn cũ giữ nguyên văn trong khối đính chính,
và nay có cổng kiểm canh để nhãn chữ không trôi khỏi con số đo được nữa.

---

## 2. SÁU HẠNG MỤC ĐƯỢC GIAO — LÀM GÌ VÀ CHỨNG MINH RA SAO

| Mã | Hạng mục | Chứng minh |
|---|---|---|
| P0-A | Sửa cách phân loại **quyền sở hữu** kỹ năng, **xuyên suốt** từ sổ vào đường sản xuất | Bốn bậc ưu tiên, trên thắng dưới. Phép thử gọi **chính đường sản xuất**, không chỉ gọi hàm phụ trợ rời |
| P0-B | Loại cứng phải **hỏng thì khoá** | 12 cửa · 16 ca âm đều **không** loại cứng · một đối chứng dương duy nhất thì **có** loại cứng |
| P0-C | Cảnh báo và quan sát phải **có thật** | Mọi phép thử đều đòi **số lượng lớn hơn không**; cấm dạng "lọc rồi mọi" vốn luôn đúng trên tập rỗng |
| P1-A | Chuẩn hoá mô hình bằng chứng **1 + 4** | Cùng một giá trị ở sổ năng lực · hợp đồng · bộ kiểm · ví dụ phiếu · đề xuất đồng bộ · báo cáo này |
| P1-B | Sửa lược đồ phiếu, ghi chú và tiêu đề tệp mã | **Đo** lược đồ thật trên phiếu do đường sản xuất tạo ra, không chép con số cũ |
| P1-C | Sinh lại **toàn bộ** hiện vật hiện hành | Sinh từ nguồn cuối, **không sửa tay để ép khớp**; cổng tính lại và so **từng** mã băm |

### Về hạng mục P1-B

Bản 009 công bố lược đồ phiếu theo một con số cũ. Yêu cầu là *"đo lược đồ thật; không chép
con số cũ nếu nguồn đã thay đổi"*.

**Nguồn đã thay đổi.** Đo lại trên phiếu do đường sản xuất tạo ra: **35 trường = 29 bắt buộc + 6 bổ trợ**.
Nay có ba điều kiện cổng khoá con số công bố vào chính phiếu — tổng phải bằng tổng hai danh sách,
không được có trường lạ, và hai danh sách không được giao nhau.

Một câu sai trong hợp đồng cũ (*"26 là tập con của 30"* — tự mâu thuẫn vì cùng chỗ đó nêu tổng là 32)
**đã gỡ**, nguyên văn giữ trong khối đính chính.

---

## 3. ĐỐI CHỨNG DƯƠNG — CHỨNG MINH CƠ CHẾ **CÒN CHẠY**, KHÔNG PHẢI CHỈ BỊ KHOÁ CHẶT

Siết chặt một cơ chế mà không chứng minh nó **vẫn hoạt động** thì chỉ là làm nó chết.

Đo qua **chính đường sản xuất**, với một việc thật:

> *"ô chọn tìm kiếm, chọn nhiều giá trị cùng lúc, hiển thị các thẻ đã chọn"*

Kết quả: kỹ năng **chọn một giá trị** bị loại cứng — đúng như Chủ dự án đã quyết định — với
lý do ghi rõ: đúng định danh · đúng điều kiện · còn hiệu lực · **còn tươi 0 trên 180 ngày** ·
đúng cả ba phạm vi. Kỹ năng **chọn nhiều giá trị** vẫn ở lại danh sách đề xuất, đúng như mong đợi.

Ngược lại, **mười sáu** ca thiếu hoặc sai (thiếu trạng thái · trạng thái lạ · thiếu căn cứ ·
căn cứ không tồn tại · sai định danh · sai điều kiện · quyết định bị thu hồi · quyết định bị
thay thế · hết tươi · ngày không hợp lệ · ngày soát ở tương lai · thiếu ngày hiện tại ·
lệch dự án · lệch công cụ · lệch đường dẫn · thiếu thông tin bắt buộc) — **không ca nào** loại cứng.

---

## 4. KIỂM NGƯỢC — PHÁ ĐỂ XEM CỔNG CÓ THẬT SỰ BẮT ĐƯỢC KHÔNG

Cổng kiểm xanh **không** chứng minh điều gì, nếu chưa ai thử phá.

**48 lần phá · 48 lần cổng đỏ đúng chỗ · 0 lỗ mù.**

Nguyên tắc bắt buộc: **trước khi kết luận, phải xác nhận mã băm của tệp đã thật sự đổi.**
Nếu lệnh phá không ăn mà ta lại kết luận "cổng vẫn xanh nên cơ chế yếu", đó là kết luận sai
từ một phép thử chưa từng chạy. Phá xong khôi phục, rồi đối chiếu lại mã băm để chứng minh
tệp trở về **đúng nguyên trạng từng byte**.

### Ba lỗ mù ở vòng chạy đầu — và cả ba nằm ở **bộ kiểm**, không phải mã sản xuất

Vòng đầu ra **45 đạt · 3 lỗ mù**. Đây là phần đáng giá nhất của cả gói việc:

1. **Hai dòng trong bảng chân trị dùng điều kiện "hoặc".** Khi gỡ cửa *"ngày hiện tại phải hợp lệ"*,
   giá trị rỗng bị ép về số không, luồng **rơi sang cửa khác** và vẫn khớp vế thứ hai của điều kiện
   "hoặc" ⇒ **cổng vẫn xanh dù cửa đã mất**. Đúng cái bẫy mà chính chú thích phía trên bảng đó
   đã cảnh báo — mà vẫn vướng.
2. **Bảng chân trị thiếu hẳn một ca.** Có ca "ngày quyết định ở tương lai" nhưng **không** có ca
   "ngày soát lại ở tương lai" — nên cửa thứ hai chưa từng được đo.
3. **Một lần phá làm cổng sập** bằng ngoại lệ chưa bắt. Cổng đỏ thật, nhưng không hiện tên điều
   kiện nào ⇒ máy chấm điểm không nhận ra. Nay được phân loại riêng.

Sau khi vá cả ba: **48 trên 48, không còn lỗ mù**.

---

## 5. CÁC MẶC ĐỊNH AN TOÀN ĐỂ **ĐÓNG** LUỒNG KỸ NĂNG

Luồng kỹ năng nay đóng ở chế độ **cố vấn — thủ công**. Không mặc định nào phá huỷ thứ gì,
và không chờ quyết định phá huỷ nào.

| Nhóm | Số lượng | Mặc định |
|---|---|---|
| Mục cần Chủ dự án phân xử | 3 | **chỉ quan sát** — không cảnh báo, không loại cứng |
| Sai-dương còn lại | 6 | **chỉ cảnh báo** — giữ kỹ năng trong danh sách đề xuất |
| Mục thiếu điều kiện không-chọn | 39 | chỉ quan sát; xếp việc theo rủi ro từ cao xuống thấp |
| Kỹ năng của nhà cung cấp ngoài | 10 | giữ **cách ly** và **khoá tuyến** |
| Định danh bên trợ lý tài liệu | 31 | giữ nguyên, **không** chuẩn hoá hàng loạt |
| Kỹ năng đã rà trong các gói trước | 13 | giữ đủ 13 — **không** gộp, **không** xoá, **không** thay thế |

Điểm mới của bản R1: những mặc định này trước đây **ngầm định** — để trống thì hệ thống vẫn
xử lý an toàn, nhưng không ai kiểm toán được. Nay cả chín mục đều **khai tường minh**.

Chứng minh qua đường sản xuất: việc *"chỉ đọc hoặc phân tích, không đổi gì"* làm kỹ năng
triển khai xuất ra **hai quan sát**, hành động là **giữ lại và ghi nhận**, **không** loại cứng.

Và với sáu chuỗi sai-dương: dùng **chính chuỗi sai** làm việc cần làm — cả tám hàng đều
**không** bị loại cứng. Chuỗi sai bị chặn ngay ở khâu lọc nên không những không loại cứng
mà còn không khớp được.

---

## 6. NHỮNG GÌ **KHÔNG** ĐỘNG TỚI

- Không đụng mã sản phẩm, giao diện nghiệp vụ, API nghiệp vụ, lược đồ hay dữ liệu thật
- Không đụng máy vận hành, không triển khai, không nâng số phiên bản
- Không xoá, gộp, đổi tên hay thay thế bất kỳ kỹ năng nào — **toàn bộ định danh còn nguyên**
- Không sửa thêm thân kỹ năng nào ngoài hai ghi chú hoàn tác đã có từ gói trước
- Không cài, không cập nhật bất kỳ thư viện kỹ năng bên ngoài nào
- Không bật móc tự động, không bật nhận diện tự động, không bật tự nạp, không bật tự thi hành
- **Không gọi giao diện lập trình để sửa tài liệu trên nền tảng ghi chép** — chỉ tạo **đề xuất**

---

## 7. CÒN LẠI — VÌ SAO VẪN LÀ `PARTIAL`

1. **Ba phép đo trên công cụ Cursor vẫn chưa chạy được.** Phiên làm việc này là một công cụ
   dòng lệnh chạy **bên trong** cửa sổ Cursor. **Ở trong Cursor không phải là Cursor.**
   Chúng tôi **không** điền kết quả thay, và **không** dùng phép đo bị chặn để che lỗi mã nguồn.
   Quy trình và câu hỏi thử đã soạn sẵn để chạy trên đúng công cụ.
2. **Trục "công cụ có tự nạp nội dung không" và "có tự làm theo quy trình không" chưa đo
   trên bất kỳ công cụ nào.**
3. **Các quyết định của Chủ dự án còn mở** — ba mục cần phân xử, sáu điều kiện thay thế cho
   sai-dương, và 39 mục thiếu điều kiện.
4. **Điểm khớp việc với kỹ năng vẫn là đo thô theo từ khoá**, chưa phải hiểu ngữ nghĩa.
5. **Mức rủi ro vẫn là suy đoán** — nguồn mạnh nhất hiện có là bản rà đọc thân kỹ năng có
   tầng phản biện, chưa có người soát từng dòng.

---

## 8. VỀ TÍNH ĐỘC LẬP CỦA BẰNG CHỨNG

Các mã băm trong hồ sơ nội bộ là **do chính phiên này tính**. Chúng chứng minh **tính toàn vẹn**
(tệp không đổi giữa hai thời điểm), **không** phải là xác nhận độc lập của bên thứ ba.

Việc đối soát độc lập thuộc về bước sau: đối chiếu hồ sơ đã công bố với kho mã, rồi trình
Chủ dự án xác nhận lần cuối.

---

*Báo cáo này an toàn để công khai: không chứa địa chỉ máy chủ, đường dẫn máy vận hành, khoá,
mật khẩu, thông tin định danh cá nhân, số liệu kinh doanh hay số tiền.*
