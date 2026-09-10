# GÓI BUSINESS PILOT M1→M3 — BÁO CÁO KẾT THÚC

> **Ngày:** 11/09/2026 · **Gói:** `PROMPT TỔNG LỰC — MỞ BUSINESS PILOT M1→M3`
> **Sổ Yêu Cầu Owner:** mục `#255` · **Plan of Record:** `PL-ERP-SINGLE-TRACK-RECOVERY-20260825`
> **Bàn giao cho TanPhatAI:** xem mục ⑬ cuối trang.

---

## ① KẾT LUẬN ĐIỀU HÀNH

**Business Pilot đã sẵn sàng chưa?** — **CHƯA HOÀN TOÀN.** Bốn chặng nghiệp vụ đã thông
trên máy nội bộ, nhưng còn **hai cổng phải qua**, và cả hai đều là điểm mà chính Owner
cho phép dừng hỏi.

**Đã chạy thật chưa?** — **CÓ, trên máy nội bộ.** Đăng nhập thật bằng trình duyệt, đi hết
màn khách hàng và màn báo giá, chụp ảnh cả bản rộng lẫn bản 390px. **CHƯA** chạy trên
máy vận hành.

**Vướng đúng cổng nào?**

| # | Cổng | Vì sao dừng |
|---|---|---|
| 1 | **Owner duyệt bằng mắt bản in báo giá** | Mục ⑫ của chính gói này bắt: *"Sau khi có bản render cuối, DỪNG để Owner duyệt bằng mắt."* Bản render đã dựng xong, 4 bản, mỗi bản HTML + PDF A4 + ảnh chụp. |
| 2 | **Owner xác nhận triển khai** | Mục ⑮. Chưa trình biên nhận phát hành vì cổng 1 chưa qua — bản in là một phần của thứ sẽ phát hành. |

Ngoài hai cổng đó còn **ba việc cần Owner quyết**, đã ghi sổ nợ, không cái nào chặn
việc đang làm: `DEBT-195` (hai bài nghiệm thu T6·T7), `DEBT-196` (dữ liệu sai khách có
sẵn từ trước), và một điểm phân định về phạm vi lệnh cấm 24/07 (nêu ở mục ⑨).

---

## ② BIÊN NHẬN ĐẦU VÀ CUỐI

| | Đầu gói | Cuối gói |
|---|---|---|
| Nhánh | `main` | `main` |
| `HEAD` | *(mã nguồn kho riêng — tra ở bản nội bộ)* | *(xem mục ⑪)* |
| `origin/main` | *(cùng mã với HEAD)* | hội tụ |
| Cây làm việc | sạch | sạch |
| Phiên bản | `V1.00.370` | `V1.00.370` — **KHÔNG đổi** |
| Ahead/behind | 0 / 0 | 0 / 0 |

**Số phiên bản CỐ Ý KHÔNG tăng.** Mục ⑮ bắt phải trình biên nhận và xin xác nhận trước
khi phát hành; chưa tới đó thì chưa bump. Đã tra lịch sử: các số `V1.00.346` → `V1.00.370`
đều đã dùng, nên số chưa từng dùng kế tiếp là **`V1.00.371`** — đo được, không phỏng đoán.

---

## ③ NHỮNG NGUỒN ĐÃ ĐỌC

Đọc toàn bộ danh sách bắt buộc ở mục ⑤ của gói, chia mười một vùng, đọc song song.
Điều quan trọng nhất rút ra: **phân biệt được đâu là mã người dùng đang dùng thật, đâu là mã mồ côi.**

**Mã ĐANG DÙNG THẬT (đã lần theo `import`, không suy đoán):**
`src/app/m3/bao-gia/page.tsx` → `bao-gia-client.tsx` → `actions.ts` → `m3-store.ts`.
Đây là đường duy nhất; toàn bộ `src` chỉ có **một** nơi nhập `BaoGiaClient`.

**Mã MỒ CÔI (route còn sống nhưng đã gỡ khỏi menu, không ghi CSDL):**
`m3/bao-gia/item/*` và `m3/bao-gia/option/*` — cả hai mang banner *"TRANG KHÔNG DÙNG"*,
Owner gỡ khỏi menu 21/08/2026. Nút Lưu chỉ hiện thông báo, không gọi hàm ghi nào.
**Đã không sửa nhầm vào đây.**

**Lỗi truy xuất:** không có. Mọi tệp trong danh sách bắt buộc đều tồn tại.
Hai tệp `GOLIVE-PLAN.md` / `MODULE-PROGRESS.md` nằm trong `docs/golive/` chứ không phải gốc dự án.

**Một bộ test cạnh tranh đã phát hiện và CỐ Ý không chạy:** `S01–S10` trong
`docs/golive/P01-INTERNAL-PILOT-RUNBOOK-V0218.md` được `README.md:39` đánh dấu CURRENT.
Mục ⑬ của gói chỉ đích danh T1–T9 nên chạy đúng T1–T9. Ghi lại để không ai tưởng là bỏ sót.

---

## ④ ĐĂNG NHẬP

**Máy nội bộ: ĐÃ GỠ.** `LOCAL_LOGIN_PROVEN`.

Trước khi động vào bất cứ thứ gì, chứng minh đích là máy nội bộ — bốn điều, không điều nào là suy đoán:

1. Cấu hình trỏ `127.0.0.1`, cổng `3308`.
2. Cổng `3308` do một container Docker chiếm, gắn `127.0.0.1:3308->3306/tcp` — tức chỉ máy này vào được.
3. **Không** tiến trình `ssh` / `plink` / `putty` nào đang chạy ⇒ loại trừ khả năng cổng nội bộ là miệng một đường hầm ra máy vận hành. *(Dự án này để dành cổng 3307 cho đường hầm, nên đây là điều bắt buộc phải loại trừ.)*
4. Chốt chặn trong chính công cụ từ chối mọi máy chủ không phải nội bộ.

**Đo lại trước khi kết luận khoá hỏng:** đối chiếu `bcrypt` toàn bộ ứng viên rút từ hai sổ
bí mật với mọi tài khoản — **1.500 phép so, 0 trùng**. Không đoán mật khẩu, không thử đăng
nhập lặp (tránh ngưỡng khoá 5 lần).

**Sau khi đặt lại:** kiểm chứng lại — **1.590 phép so, 2 trùng đúng hai tài khoản pilot**.
Rồi đăng nhập thật qua trình duyệt: vào được.

**Máy vận hành: CHƯA KIỂM** — đúng luật gói này (`DEPLOYMENT` chưa mở).

*Không giá trị bí mật nào bị in ra màn hình, ghi vào tệp theo dõi, hay đưa vào báo cáo.*

---

## ⑤ CỔNG VÂN TAY

**Gốc canonical đã chọn:** thư mục bản chạy — vì đó là artifact **thực sự được chuyển và
chạy** (trình quản lý tiến trình lấy đúng thư mục đó làm thư mục làm việc).

**Ba khiếm khuyết sổ nợ ghi — tự kiểm chứng, cả ba ĐÚNG:**

| | Bệnh | Hậu quả đo được |
|---|---|---|
| 1 | Bên ghi băm một **thư mục con**, bên kiểm băm **cả thư mục** | Hai giá trị **không bao giờ** bằng nhau, kể cả khi máy hoàn toàn lành |
| 2 | Hàm phán định nhận **chuỗi rỗng** | Giá trị thật tính ra rồi **vứt đi** |
| 3 | Mẫu fail-**OPEN** | Một vế rỗng là bỏ qua **im lặng** |

**Bốn bẫy phát hiện thêm, nặng nhất:** thư mục **không tồn tại** và thư mục **rỗng** cho
**y hệt** một giá trị 32 ký tự trông như thật ⇒ cổng cũ báo **XANH cho một máy không có
bản chạy nào**.

**Vá gốc:** một hợp đồng vân tay **dùng chung, một bản cài đặt duy nhất**. Bên ghi gọi tại
chỗ, bên kiểm gửi đúng tệp đó sang chạy. *Sửa cho hai công thức giống nhau chỉ vá được hôm
nay — hai bản chép tay sẽ lệch lại vào lần sửa sau.*

**⭐ Lượt kiểm ngược đối kháng tìm ra lỗ THẬT mà bản đầu không khai:** dựng được đường
chiếm quyền **hoàn toàn vô hình** — thả mã vào vùng đệm rồi sửa tệp cấu hình bộ nạp trỏ vào
đó, **cả năm dòng đầu ra y hệt máy sạch**. Đã siết lên hợp đồng **VT-2**: bộ nạp nay được
băm, mọi vế loại trừ siết theo hình dạng tệp, và băm chế độ quyền đầy đủ thay vì một bit.

**Bảy biểu hiện đã đo, đạt cả bảy** — gồm cả hai chiều đối nghịch: đổi thứ được nạp thì
**phải** phát hiện, mà dời chỗ đặt thì **không được** đổi giá trị.

⚠️ **Một điều đã thử rồi RÚT LẠI ngay trong phiên, ghi ra để không ai làm lại:** băm số tệp
trong vùng đệm vào vân tay là **sai** — vân tay chốt trước khi chạy ứng dụng, còn bên kiểm
chạy sau khi máy đã phục vụ và tự ghi đầy đệm ⇒ **cổng đỏ vĩnh viễn**, đúng căn bệnh đã sinh
ra nợ này. Đường chặn thật nằm ở chỗ khác và đã đóng.

**Bằng chứng production: CHƯA CÓ.** Cao nhất mới là RUNTIME trong container Linux.
`DEBT-189` **chưa đóng**.

---

## ⑥ KHÔNG BÁO XANH GIẢ

**Trước:** duyệt báo giá hoặc chốt đơn có kèm gửi thông báo/email cho khách — gửi **thất
bại** vẫn hiện **toast XANH**. Người kinh doanh tin là khách đã nhận.

**Chuỗi mất thông tin, có HAI điểm chứ không phải một:**

```
executePostActions()  ✅ trả đủ: đã chạy / chưa hỗ trợ / lỗi
        ↓
transitionState()     ❌ ĐIỂM 1 — gọi xong VỨT kết quả, không gán biến
                      ❌ ĐIỂM 2 — kiểu trả về KHÔNG có chỗ nào chứa cảnh báo
        ↓
server action         → không có gì để truyền
        ↓
màn hình              → chỉ thấy đúng/sai → bắn TOAST XANH
```

Sửa mỗi điểm 1 là **chưa đủ** — đó là lý do bản vá trước đó không tới được người dùng.

**Sau:** trạng thái vẫn đổi thật (nên **không** dùng màu đỏ — đỏ nghĩa là hỏng, sai sự
thật), nhưng hiện **cảnh báo màu vàng** nói rõ *"Đã chuyển trạng thái. Nhưng thông báo và
email CHƯA được gửi — hãy tự liên hệ khách nếu cần."*
Câu chữ cố ý **không hứa "sẽ gửi sau"** vì hiện không có hàng đợi nào cả.

**Bài kiểm mới: 18 điều kiện, gọi thật hàm.**
**Kiểm ngược đã chạy:** tái tạo đúng lỗi cũ → 4 điều kiện ĐỎ; khôi phục → 18/18 xanh.

⚠️ **Bản ĐẦU của bài kiểm là CỔNG GIẢ** — nó dựa vào kiểu dữ liệu, mà bộ chạy chỉ lột kiểu
chứ không kiểm kiểu, nên kiểm ngược **vẫn xanh 15/15** dù lỗi đã quay lại. Đã viết lại thành
phép gọi thật. Bẫy này ghi thẳng trong chú thích bài kiểm.

**Đo trên dữ liệu thật:** 7 bước chuyển trạng thái đang khai hành động chưa nối dịch vụ,
gồm **cả ba chặng của pilot** ⇒ bản vá không phải lý thuyết.

---

## ⑦ SẢN PHẨM TRONG BÁO GIÁ

**Bệnh đo được — ba đường đều sinh dòng không neo danh mục:**

| Đường | Hành vi cũ |
|---|---|
| Ô chọn nhanh | Gõ tên không khớp → tạo dòng với định danh **rỗng**, cố ý **không** ghi vào danh mục |
| Sheet "thêm sản phẩm mới" | Cùng vậy |
| Sheet sửa dòng | Không chọn danh mục thì tên gõ tay vẫn được nhận, định danh **rỗng** |

Và: **ô chọn sản phẩm KHÔNG lọc theo khách đang chọn** — người lập báo giá cho khách A vẫn
chọn được sản phẩm riêng của khách B. Ô "người liên hệ" ngay phía trên thì **đã lọc đúng từ
trước** — chỉ ô sản phẩm bị bỏ sót.

**Đã làm:**

- Lọc sản phẩm theo khách đang chọn, dùng **đúng khuôn mẫu** mà ô người liên hệ đang dùng.
  Mỗi dòng hiện đủ bốn thứ: tên đầy đủ · mã · quy cách · đơn vị tính.
  Chưa chọn khách thì ô mờ đi và hiện *"Chọn khách hàng trước"*.
- **Cổng máy chủ** chặn dòng mới thiếu định danh và chặn sản phẩm chéo khách — áp cho **cả**
  đường tạo lẫn đường lưu. Lọc phía màn hình là để dễ dùng; máy chủ mới là nơi phân xử.
- Trong Sheet sửa dòng: ô tên sản phẩm nay **chỉ đọc** khi đã chọn từ danh mục.

**Dòng lịch sử được MIỄN — có chủ đích.** Dòng đã có trong cơ sở dữ liệu mà đang thiếu định
danh thì vẫn đọc được, vẫn hiện ra, **không bị viết lại**. Sửa ngầm dữ liệu cũ là làm hỏng
bằng chứng nghiệp vụ. Nhưng miễn trừ **chỉ áp cho THIẾU định danh, KHÔNG áp cho SAI khách**.

**Bằng chứng lớp giao diện:** tài khoản kinh doanh đăng nhập thấy **đúng phần khách được
phân công**, không thấy phần còn lại.

---

## ⑧ TẠO NHANH VÀ TÊN SẢN PHẨM

**Nút "Tạo Nhanh Sản Phẩm"** đặt ngay trong form báo giá đang dùng thật.
Khách hàng **bị khoá** theo báo giá đang lập, không đổi được trong hộp thoại.
Tạo xong: tự chọn vào đúng dòng, **bản nháp giữ nguyên** — không tải lại trang, vì tải lại là
mất trắng thứ đang gõ.

**Trùng tên:** không tạo trùng, cũng không im lặng — bày ra sản phẩm đã có (kèm mã · quy
cách · đơn vị tính) để người dùng chọn lại hoặc đổi tên.

**Chống trùng theo TỪNG khách:** bỏ dấu · gộp khoảng trắng · không phân biệt hoa thường.
**Cố ý KHÔNG gộp** sản phẩm trùng tên của **hai khách khác nhau** — hai khách cùng đặt
"Hộp Quà Tết" là chuyện bình thường và đó là hai sản phẩm khác nhau.

### 🔴 Một giả định của gói cần đính chính

Mục ⑪ giả định có sẵn công thức tính **tên đầy đủ cho sản phẩm**. Đo được: công thức ghép
nhiều mảnh thành một chuỗi thuộc về **VẬT TƯ**, không phải sản phẩm. Với sản phẩm, dự án chỉ
có chuẩn hoá **Title Case**.

Nên đã **tái dùng đúng cái đang có** — tuyệt đối không tự chế công thức mới (mục ⑪ cấm).
Điểm cải thiện thật: tên đầy đủ nay **tính lại ở máy chủ**, và **mã sản phẩm do máy chủ cấp**
(bản cũ để màn hình cấp — không an toàn khi hai người lập báo giá cùng lúc).

**Không thêm cột, không thêm di trú lược đồ.** Bảng sản phẩm không có ràng buộc duy nhất cho
cặp (khách, tên) nên chống trùng làm ở máy chủ; **rủi ro còn lại**: hai người bấm cùng một
phần giây vẫn lọt — đã ghi sổ nợ, không giấu.

---

## ⑨ BẢN IN BÁO GIÁ

**Bệnh:** đếm chuỗi trên chính tệp bản in — «tên khách» **0 lần** · «Tân Phát» **0 lần** ·
«mã số thuế» **0 lần** · «thuế» **0 lần** · khối ký **0**. Bản in ra một chuỗi ghép từ **số
thứ tự trong cơ sở dữ liệu**, không phải mã khách thật, càng không phải tên khách.

**Gốc rễ:** hàm nạp dữ liệu chạy `SELECT` trên **một bảng duy nhất**, **không hề nối** sang
bảng khách hàng ⇒ bản in không có tên khách trong tay.
**Nghịch lý:** chính màn hình **đang** hiển thị tên khách — chỉ bản in là không dùng.

**Nguồn layout đã truy được:** mẫu Owner duyệt trong `docs/Form Mẫu Tham Khảo/` — chính là
tệp mà trang Liên Hệ chỉ đích danh là letterhead chuẩn, và **có sẵn chú thích tên cột cho
từng ô**. Không phải làm lại từ đầu.

### Bốn thứ CỐ Ý KHÔNG BỊA

| Trường | Vì sao không in |
|---|---|
| **Suất thuế** | Mẫu Owner duyệt ghi *"Thuế GTGT (nếu áp dụng)" / "Theo hóa đơn"* — **không có con số**. Trong kho đang có **hai số chọi nhau**; chọn bên nào cũng là đoán. |
| Điều khoản thanh toán | Không có nguồn |
| Tài khoản ngân hàng | Không có nguồn |
| Tên người ký | Chỉ in **chức danh** + ô trống để ký tay, đúng như mẫu |

Trường nào khách chưa khai thì in dấu gạch, **không suy đoán**, không lấy thông tin công ty
mình điền vào chỗ của khách.

**Thêm một cảnh báo mới:** nếu tổng tiền lưu trong hệ thống **lệch** tổng cộng lại từ các
phương án đã chọn thì bản in **nói thẳng ra** thay vì che. *(Bản nháp đầu của lượt này tự
tính lại tổng — sai hướng, đó là dựng nguồn sự thật thứ hai. Đã sửa: in đúng số của hệ thống,
lệch thì lộ ra.)*

**Bản render để Owner xem:** `docs/reports/ban-in-bao-gia-20260911/` — **4 bản** minh hoạ
1 / 5 / 20 / 30 dòng, mỗi bản **HTML + PDF khổ A4 + ảnh chụp**. Số trang PDF: 1 / 2 / 4 / 6.
Cả bốn mang dải nhãn **"DỮ LIỆU MINH HOẠ — KHÔNG PHẢI BÁO GIÁ THẬT"**.

Đã soi: tên sản phẩm rất dài **không tràn** ra ngoài giấy · tên khách rất dài **không tràn** ·
không cắt ngang một sản phẩm giữa hai trang · đầu bảng lặp lại khi sang trang · ngày đúng
`DD/MM/YYYY` · số phân nhóm nghìn kiểu Việt Nam · tổng tiền đúng.

**Bản dựng từ dữ liệu thật CỐ Ý không vào kho** — nó chứa tên, địa chỉ, điện thoại khách
thật. Nó nằm ở nơi đã chứng minh bị git bỏ qua.

### ⚠️ Cần Owner phân định một điểm

Lệnh cấm khoá 24/07/2026 mở đầu bằng chữ **"ĐƠN HÀNG:"** — đọc nguyên văn thì nó cấm chép bố
cục Báo Giá **SANG** mẫu Đơn Hàng, **không** nói cấm sửa chính bản in Báo Giá. Sổ nợ đang
viện dẫn dòng đó làm cớ chặn. Hai cách hiểu khác nhau.
Dù hiểu cách nào thì kết quả lượt này **giống nhau**: dựng xong rồi **dừng chờ Owner duyệt**.

---

## ⑩ T1–T9 VÀ CHUỖI PILOT

Chạy bằng **trình duyệt thật**, trên máy nội bộ, đăng nhập thật. Ma trận lấy **nguyên văn**
từ kế hoạch go-live — **không** soạn bộ mới cạnh tranh.

| # | Bài | Vai | Kết quả | Lớp |
|---|---|---|---|---|
| T1 | Quản trị đăng nhập → thấy tất cả menu | Quản trị | ✅ **ĐẠT** — vào được, thấy đủ 7 vùng | `UI_PROVEN` |
| T2 | Kinh doanh đăng nhập → thanh bên đã lọc | Kinh doanh | ✅ **ĐẠT** — **không** vùng cấm nào lọt ra | `UI_PROVEN` |
| T3 | Kinh doanh gõ thẳng URL màn quản trị | Kinh doanh | ✅ **ĐẠT** — bị đẩy sang trang 403 | `UI_PROVEN` |
| T4 | Kinh doanh tạo khách hàng | Kinh doanh | ✅ **ĐẠT** — có đường tạo | `UI_PROVEN` |
| T5 | Kinh doanh xoá khách hàng | Kinh doanh | ✅ **ĐẠT** — bị chặn | `UI_PROVEN` |
| T6 | Thiết kế đăng nhập (chỉ xem) | Thiết kế | ⚪ **CHƯA ĐO** | `NOT_CHECKED` |
| T7 | Thiết kế gõ URL wizard | Thiết kế | ⚪ **CHƯA ĐO** | `NOT_CHECKED` |
| T8 | Kinh doanh tạo Báo Giá | Kinh doanh | ✅ **ĐẠT** — có đường tạo | `UI_PROVEN` |
| T9 | Kinh doanh xoá Báo Giá | Kinh doanh | ✅ **ĐẠT** — bị chặn | `UI_PROVEN` |

**TỔNG: 7 ĐẠT · 0 HỎNG · 2 CHƯA ĐO.** Chạy hai lượt liên tiếp, kết quả **giống nhau**.

**T6·T7 vì sao chưa đo:** trên cơ sở dữ liệu nội bộ **không tài khoản nào mang vai trò Thiết
Kế**. Vai trò đó **có tồn tại** nhưng chưa gán cho ai. Gán thêm là đổi cấu hình phân quyền,
**vượt ra ngoài tập người dùng mà chính Owner đã khoá** cho gói này (đúng một Quản trị + một
Kinh doanh). Ghi **CHƯA ĐO**, tuyệt đối không ghi là đạt. → `DEBT-195`, cần Owner quyết.

**Bằng chứng lớp giao diện:** ảnh chụp bản rộng **và** bản 390px, đều **sau khi đã đăng
nhập**. Ảnh nằm ở nơi bị git bỏ qua vì chứa dữ liệu khách hàng thật.

### Hai lần bài kiểm của tôi báo sai — và cách phát hiện

Lượt đầu T1·T2 báo **HỎNG** *"không vào được"*, trong khi T3·T5·T8·T9 **chạy được bằng chính
phiên đăng nhập đó** — T3 còn vào tới trang 403, tức máy chủ **đã nhận ra người dùng**.
Mâu thuẫn đó chứng minh lỗi nằm ở **bài kiểm**, không phải ứng dụng.

Nguyên nhân thật: trang đăng nhập đặt xong phiên nhưng **không tự rời khỏi** trang đó, nên
phép đo theo địa chỉ trang luôn kết luận sai. Đã sửa thành **chờ đúng cookie phiên** rồi tự
đi tới trang chủ xem có bị đá ngược ra không.

Lần thứ hai: T4 báo hỏng vì tôi dò nút bằng chữ *"thêm / tạo mới"*, còn nút thật ghi
**"+ Tạo KH"**. Ảnh chụp cho thấy ngay.

**Ghi lại vì đây là bài học:** nếu tin ngay lượt chạy đầu, tôi đã báo với Owner rằng hệ thống
hỏng ba chỗ trong khi nó **hoàn toàn bình thường**.

**Dữ liệu thử:** không tạo bản ghi nghiệp vụ mới nào. Việc dựng nền pilot chỉ gồm nối tài
khoản với nhân sự và phân công **một tập nhỏ** khách hàng — trạng thái trước đã lưu lại để
đảo ngược được. **Không chạm** dữ liệu của phần còn lại.

---

## ⑪ PHÁT HÀNH

**CHƯA PHÁT HÀNH.** Chưa trình biên nhận, chưa xin xác nhận triển khai, chưa tăng số phiên bản.

**Lý do:** cổng ⑫ (Owner duyệt bản in) chưa qua, mà bản in là một phần của thứ sẽ phát hành.
Trình biên nhận lúc này là trình một gói chưa chốt.

**Đã đo sẵn để lúc trình không phải đoán:** số phiên bản chưa từng dùng kế tiếp là
**`V1.00.371`** (tra lịch sử, không mặc định số kế tiếp).

**Cổng chất lượng đã chạy:**

| Cổng | Kết quả |
|---|---|
| Kiểm kiểu toàn dự án | **sạch** |
| Cổng quản trị | **đạt** |
| Nhóm bài kiểm nhanh | **1.048 điều kiện đạt** |
| Nhóm bài kiểm cần cơ sở dữ liệu | **đạt** |
| Cổng quét bí mật · quét dữ liệu cá nhân | **đạt** |
| Cổng cổng-mồ-côi | **2/1 → 3/0** *(xem dưới)* |

**Bốn bài kiểm mới từng MỒ CÔI** — viết xong mà không bộ gộp nào gọi, tức **giá trị thi hành
bằng 0**. Đã nối vào đúng nhóm theo điều kiện chạy.

---

## ⑫ NỢ ĐÓNG VÀ CÒN MỞ

**Chỉ đổi trạng thái theo bằng chứng thật:**

| Nợ | Trước | Sau | Vì sao |
|---|---|---|---|
| `DEBT-173` | MỞ | ✅ **ĐÃ XỬ LÝ** | Vá **hai** điểm mất thông tin; bài kiểm hành vi 18/18; kiểm ngược đạt |
| `DEBT-152` | MỞ · CHẶN GO-LIVE | 🔶 **ĐANG XỬ LÝ** | Mã xong, render xong — **chờ Owner duyệt bằng mắt** |
| `DEBT-185` | MỞ | 🔶 **ĐANG XỬ LÝ** | Máy nội bộ đã gỡ; **máy vận hành chưa kiểm** |
| `DEBT-189` | MỞ | 🔶 **ĐANG XỬ LÝ** | Vá gốc + siết VT-2; **chưa chạy trên máy vận hành** |

**Năm nợ MỚI ghi trong phiên:**

| Nợ | Nội dung |
|---|---|
| `DEBT-193` | 🔴 Cổng quét dữ liệu cá nhân **mù** với tên + địa chỉ khách trong tệp báo cáo — hôm nay tuân luật vì **người làm nhớ luật**, không phải vì máy canh |
| `DEBT-194` | 🟠 Cơ chế vân tay còn **bốn lỗ đã biết**, gồm một công thức luôn băm **hư không** |
| `DEBT-195` | 🟠 T6·T7 chưa đo — cần Owner quyết có gán vai Thiết Kế không |
| `DEBT-196` | 🟠 Dữ liệu **có sẵn** bị sai khách — không tự sửa vì phải **đoán** |
| `DEBT-197` | 🟡 Bốn ô nhập **trang trí** ở bước tạo đơn — gõ vào rồi mất trắng |

**Các nợ hoãn: KHÔNG tuyên bố đóng cái nào.** Không đụng tới Pricing, M4, M5, MF, M9,
`DEBT-190`, hay các nợ động cơ quy trình ngoài phạm vi hẹp đã nêu.

---

## ⑬ BÀN GIAO TanPhatAI

```
FINAL_SYNC_CONFIRMATION
```

| Mục | Giá trị |
|---|---|
| Phiên bản hiện hành | `V1.00.370` — **không đổi trong gói này** |
| Phiên bản kế tiếp chưa dùng | `V1.00.371` *(đã tra lịch sử)* |
| Mã nguồn phát hành | **chưa có** — chưa phát hành |
| Mã nguồn máy vận hành | **chưa đo lại trong gói này** |
| Vân tay bản dựng | hợp đồng **VT-2**; **chưa có bằng chứng trên máy vận hành** |
| Nợ đã đóng | `DEBT-173` |
| Nợ đang xử lý | `DEBT-152` · `DEBT-185` · `DEBT-189` |
| Nợ mới mở | `DEBT-193` · `DEBT-194` · `DEBT-195` · `DEBT-196` · `DEBT-197` |
| Trạng thái pilot | **CHƯA SẴN SÀNG** — chờ 2 cổng Owner |
| Đường dẫn báo cáo | `docs/reports/BUSINESS-PILOT-M1-M3-20260911.md` |
| Bản in để duyệt | `docs/reports/ban-in-bao-gia-20260911/` |
| Sổ Yêu Cầu Owner | mục `#255` |

**Tài liệu Notion cần đồng bộ:**

1. Trạng thái `DEBT-152` — từ *chặn go-live* sang *chờ Owner duyệt mẫu giấy*.
2. Chuỗi nghiệp vụ M1→M3: dòng báo giá **mới** nay **bắt buộc** neo vào danh mục sản phẩm,
   và sản phẩm phải **đúng khách của báo giá**.
3. Có thêm chức năng **Tạo Nhanh Sản Phẩm** ngay trong form báo giá.
4. Hành vi thông báo: chuyển trạng thái có kèm gửi thông báo/email nay hiện **cảnh báo vàng**
   khi chưa gửi được — **không còn báo xanh giả**.
5. Đính chính một giả định: **không** có công thức tên đầy đủ cho *sản phẩm*; công thức đó
   thuộc về *vật tư*.
6. Ghi nhận: bộ nghiệm thu T1–T9 đạt **7/9**, hai bài còn lại **chưa đo** chứ không phải hỏng.

```
NOTION_MUTATION: NONE
```

---

## ⑭ NHÃN KẾT LUẬN — TỪNG DÒNG MỘT

| Nhãn | Trạng thái | Ghi chú |
|---|---|---|
| `LOCAL_LOGIN_PROVEN` | ✅ `UI_PROVEN` | Đăng nhập thật qua trình duyệt, hai vai |
| `CUSTOMER_SCOPE_PROVEN` | ✅ `UI_PROVEN` + `DB_PROVEN` | Kinh doanh chỉ thấy phần được phân công |
| `PRODUCT_MASTER_PROVEN` | ✅ `CODE_PROVEN` + `DB_PROVEN` | Cổng máy chủ chặn dòng thiếu định danh; 26 điều kiện đạt |
| `QUICK_CREATE_PROVEN` | 🟡 `CODE_PROVEN` | Mã xong, kiểm kiểu sạch — **chưa** bấm tay từng bước trên màn |
| `PRODUCT_NAME_UNIQUENESS_PROVEN` | ✅ `CODE_PROVEN` | 7 điều kiện chống trùng, gồm khác dấu / khác hoa thường |
| `NO_FREE_TEXT_IDENTITY_PROVEN` | ✅ `CODE_PROVEN` | Chặn cả ba đường; dòng lịch sử được miễn có chủ đích |
| `POST_ACTION_STATUS_PROVEN` | ✅ `CODE_PROVEN` + `DB_PROVEN` | 18/18; kiểm ngược đạt; 7 bước thật trong cấu hình |
| `QUOTATION_PRINT_PROVEN` | 🔶 `BLOCKED` | **Chờ Owner duyệt bằng mắt** — đúng điểm dừng gói cho phép |
| `ARTIFACT_FINGERPRINT_PROVEN` | 🔶 `BLOCKED` | 52/52 + 7/7 biểu hiện, nhưng **chưa chạy trên máy vận hành** |
| `SYNCED_EXACT_RELEASE` | ⚪ `NOT_CHECKED` | Chưa phát hành |
| `RELEASE_CONVERGED` | ⚪ `NOT_CHECKED` | Chưa phát hành |
| `UI_PROVEN` | 🟡 một phần | Máy nội bộ có ảnh; **máy vận hành chưa** |
| `BUSINESS_PILOT_READY` | 🔶 `BLOCKED` | Chờ 2 cổng Owner + `DEBT-195` |

---

## ⑮ ĐANG CHỜ OWNER — ĐÚNG NĂM VIỆC

1. **Duyệt bằng mắt bản in báo giá** → mở `docs/reports/ban-in-bao-gia-20260911/`.
   *Chặn:* đóng `DEBT-152` và toàn bộ bước phát hành.
2. **Suất thuế trên báo giá** — mẫu duyệt ghi *"Theo hóa đơn"*, nhưng trong kho có hai số
   chọi nhau. Giữ như mẫu, hay chốt một suất?
   *Chặn:* nếu Owner muốn in số thuế.
3. **Vai Thiết Kế cho T6·T7** — cho gán vai để đo nốt, hay đóng pilot ở 7/9?
   *Chặn:* tuyên bố nghiệm thu đầy đủ.
4. **Dữ liệu sai khách có sẵn** (`DEBT-196`) — sản phẩm mồ côi thật ra thuộc khách nào, hay
   xoá hẳn? *Chặn:* đưa dữ liệu đó vào vận hành thật.
5. **Xác nhận triển khai** — chỉ xin **sau khi** việc 1 xong và biên nhận phát hành đã trình.

---

## ⑯ CHƯA XÁC MINH ĐƯỢC

| Điều | Vì sao | Ai xác minh được |
|---|---|---|
| Toàn bộ hành vi trên **máy vận hành** | Gói này không mở quyền triển khai | Sau khi Owner xác nhận, Agent tự chạy |
| Vân tay bản dựng trên máy vận hành thật | Cùng lý do | Chạy cổng định danh sau lần kích hoạt kế tiếp |
| Từng bước bấm tay của **Tạo Nhanh Sản Phẩm** | Đã kiểm mã và kiểu, chưa dựng kịch bản bấm tay | Agent, phiên sau — hoặc Owner bấm thử |
| Ứng dụng có tự ghi thêm gì vào thư mục bản chạy sau khi khởi động không | Chỉ đo được trên máy vận hành thật | Quyết định cổng vân tay có ổn định hay đỏ vĩnh viễn |

---

*Báo cáo này đã qua cổng công khai: không địa chỉ máy chủ, không đường dẫn tuyệt đối của máy
vận hành, không địa chỉ thư người thật, không khoá/mã băm, không số lượng khách hàng chính
xác, không số tiền giao dịch cụ thể.*
