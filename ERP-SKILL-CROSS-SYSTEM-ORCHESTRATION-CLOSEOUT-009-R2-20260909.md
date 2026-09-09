# ĐÍNH CHÍNH VÀ THAY THẾ — VÁ NHẤT QUÁN CUỐI CÙNG (BẢN R2) — 09/09/2026

**Gói việc:** `ERP-SKILL-CROSS-SYSTEM-ORCHESTRATION-CLOSEOUT-009-R2`
**Thay thế:** `…-009-R1` (cùng ngày, phát hành trước đó) — **không xoá, không viết lại**
**Phạm vi:** CHỈ hệ kỹ năng — không đụng mã sản phẩm · cơ sở dữ liệu · máy vận hành
**Trạng thái:** `PARTIAL_PENDING_NOTION_SYNC`

> ⚠️ **Nếu ai đang dùng bản 009-R1 làm căn cứ: xin dừng lại.**
> Bản R1 tuyên bố sáu hạng mục P0/P1 đều đạt, và kết luận đó **đã được ghi lên nền tảng
> tài liệu**. Bản R2 chứng minh bằng số đo rằng **một trong sáu lời khai đó là sai**, và
> tìm thêm **mười ba khiếm khuyết khác** — phần lớn nằm ngay trong thứ mà R1 vừa nói là
> đã xong. Bản 009-R1 vẫn còn nguyên trong lịch sử kho mã để đối chiếu.

---

## 1. CÁCH LÀM: RÀ ĐỘC LẬP, KHÔNG TIN BÁO CÁO TỰ KHAI

Yêu cầu đầu tiên của gói việc là *"đối soát độc lập bản trước với mã nguồn thật, không tin
báo cáo tự khai"*. Chúng tôi làm đúng như vậy:

- **Mười chiều rà song song**, mỗi chiều đọc **toàn phần** phần việc của mình: hợp đồng điều
  phối · ví dụ biên nhận · dòng dõi hiện vật · mã nguồn bộ định tuyến · chất lượng bộ kiểm ·
  tham chiếu chủ kho · đối soát định danh · nhất quán giá trị giữa các tệp · lời khai của báo
  cáo cũ · nhất quán ba sổ đăng ký.
- **Mỗi phát hiện bị một người phản biện đối kháng thẩm định**, với mệnh lệnh *"mặc định là
  BÁC BỎ nếu không tự chứng minh được"*. Người thẩm phải **tự mở tệp** và đối chiếu.
- Kết quả: **115 phát hiện · 83 đứng vững · 32 bị bác bỏ.** Tỉ lệ bác bỏ gần một phần ba cho
  thấy tầng phản biện có làm việc thật, không phải đóng dấu.

---

## 2. BỐN LỖI NẶNG NHẤT — ĐỀU NẰM TRONG THỨ VỪA ĐƯỢC TUYÊN BỐ LÀ XONG

### 2.1. Mã sản xuất tự phát ra nhãn **đã bị bỏ** vào **mọi** phiếu

Hệ thống có một mô hình bằng chứng gọi là **1 + 4**: một tín hiệu của **dự án**, tách hẳn
khỏi bốn trạng thái của **công cụ**. Nhãn cũ gộp hai loại đó làm một đã bị bỏ từ bản trước.

**Đo được:** chính bộ định tuyến vẫn ghi nhãn cũ ấy vào phần ghi chú của **từng phiếu quyết
định nó tạo ra**. Nghĩa là tài liệu nói một đằng, còn thứ chạy thật vẫn nói một nẻo — và mỗi
lần chạy lại phát tán cái nhãn sai đó thêm một lần.

### 2.2. Cổng canh đúng cái nhãn đó **rỗng nghĩa hoàn toàn**

Có một cổng kiểm được lập ra để bắt nhãn cũ. **Đo được: nó chưa từng bắt được gì.**

Biểu thức tìm kiếm của nó bị hỏng khi viết vào tệp — các ký tự điều khiển đặc biệt bị vỏ
lệnh nuốt mất, biến biểu thức thành một mẫu **không khớp với bất cứ chuỗi nào**. Vì cách nó
kiểm là "nếu **không** tìm thấy thì đạt", một mẫu không khớp gì sẽ **luôn luôn đạt**.

Cổng ấy đã báo xanh suốt hai gói việc mà không kiểm một thứ gì.

Nó còn một khiếm khuyết thứ hai: nó chỉ soi **ba tệp tài liệu**, hoàn toàn **không nhìn mã
nguồn** — trong khi chỗ vi phạm thật lại nằm đúng ở mã nguồn.

> **Bài học ghi lại:** một cổng chưa từng bị phá là một cổng chưa từng được chứng minh.
> Bản R2 thêm một cổng canh **cả họ lỗi này** cho mọi kịch bản, và bắt cổng cũ phải **tự
> chứng minh** nó bắt được thứ nó khai là đang canh.

### 2.3. Trần an toàn **đảo ngược theo rủi ro**

Mỗi kỹ năng được cấp một "trần" — mức cao nhất mà nó được phép được dùng. Có một trần rất
chặt dành cho kỹ năng **chọi với chuẩn giao diện**: chỉ được đọc lấy bối cảnh, **cấm chép giá
trị**.

**Đo được:** khi một kỹ năng như vậy **đồng thời** có mức rủi ro cao, đoạn mã xét rủi ro
**ghi đè** trần chặt bằng một trần **lỏng hơn**. Tức là: **rủi ro càng cao thì ràng buộc càng
nới**.

Hai kỹ năng thật trong kho trúng đúng lỗi này, và cả hai đều mất ràng buộc "cấm chép giá trị"
**chính vì** rủi ro của chúng cao hơn các kỹ năng khác.

Điều đáng nói: hệ thống **đã có sẵn** một hàm "lấy trần nghiêm nhất" từ gói việc trước —
nhưng đoạn mã này chưa bao giờ dùng tới nó.

### 2.4. Hợp đồng điều phối **nói ngược** sổ bằng chứng của chính nó

Hợp đồng ghi rằng một phép đo về công cụ là **"chưa kiểm"**. Sổ bằng chứng — nguồn mà hợp
đồng viện dẫn — ghi rằng phép đo đó **đã chạy và cho kết quả âm**.

Ghi "chưa kiểm" vào chỗ đã có kết quả là **xoá mất một bằng chứng đã có**. Người đọc sẽ tưởng
vẫn còn cửa để công cụ tự nhận diện kỹ năng, trong khi thực tế đã đo và biết là không.

Cùng ô đó, phần dành cho công cụ thứ hai cũng ghi "chưa kiểm", trong khi trạng thái đúng là
**"bị chặn, chưa chạy được"** — hai điều hoàn toàn khác nhau. "Chưa ai chịu đo" hàm ý chỉ cần
bỏ công ra làm; "bị chặn" thì phải gỡ chặn trước, và cách gỡ đã được viết sẵn thành thủ tục.
Ghi nhầm là xoá luôn cả lý do chặn lẫn đường đi để gỡ.

---

## 3. MƯỜI KHIẾM KHUYẾT CÒN LẠI — ĐỀU ĐÃ SỬA

| # | Vấn đề | Vì sao đáng kể |
|---|---|---|
| 5 | **So khớp phạm vi hỏng thì MỞ.** Mọi giá trị sai kiểu đều bị coi là "không giới hạn" và khớp mọi thứ | Một quyết định gõ sai kiểu dữ liệu sẽ áp cho cả những chỗ nó không được phép áp |
| 6 | **Vòng duyệt dừng ở cảnh báo đầu tiên** | Một điều kiện loại-cứng đứng sau sẽ **không bao giờ được xét**; kết quả phụ thuộc thứ tự danh sách |
| 7 | **Suy đoán lấn lượt khai tường minh.** Nguồn gốc được *suy* từ một tín hiệu phụ rồi truyền đi **như thể đã được khai** | Một mục có khai đích danh nhà cung cấp vẫn bị xếp nhầm sang nhóm nội bộ |
| 8 | **Trường cảnh báo trên ứng viên rơi mất.** Nó được tính rồi không bao giờ được gắn vào kết quả | Hợp đồng hứa có, người đọc không thấy. Phép thử canh nó lại chạy trên tập rỗng nên im lặng |
| 9 | **Mười sáu trên hai mươi mốt căn cứ quyết định không tra được** — dùng dạng chữ tự do thay vì mã tra cứu | Chính tệp đó tự khai nguyên tắc "mỗi mục phải có căn cứ tra được" |
| 10 | **Bốn phép thử xanh vì sai cửa hoặc vì tập rỗng** | Tên phép thử khai canh điều A, thân nó thực ra dừng ở điều B — hoặc chạy trên tập không bao giờ có phần tử |
| 11 | **Dòng dõi hiện vật dùng một trường mơ hồ** gánh hai nghĩa khác nhau | Người đọc không biết con số đó nói về mốc nào |
| 12 | **Bản in ra màn hình hiện chữ "không xác định"** ở hai dòng | Nó đọc hai trường đã bị bỏ tên |
| 13 | **Ký tự điều khiển lạc trong bộ sinh sổ** làm chết một nhánh dò | Cùng nguyên nhân với lỗi số 2 |
| 14 | **Hai bộ sinh cùng ghi một tệp**, một bản đã lỗi thời hai gói | Chạy nhầm thứ tự là ghi đè bằng dữ liệu cũ |

---

## 4. DÒNG DÕI BẰNG CHỨNG — KHÔNG TỰ THAM CHIẾU

Gói việc yêu cầu phân biệt tường minh các vai trò của một mốc, và **không** tạo bài toán
"tệp chứa mã kiểm tra của chính nó".

**Câu đố đã giải:** năm hiện vật khai thuộc gói R1, nhưng cùng trỏ về một mốc của gói **trước
đó**. Đọc kỹ thì hoá ra mốc ấy **đúng** — nhưng đúng cho một nghĩa khác. Nó là mốc **nội dung
kỹ năng** (lần cuối nội dung đó thay đổi), chứ không phải mốc **sinh ra hiện vật**. Một trường
đang gánh hai nghĩa, nên đọc kiểu nào cũng thấy sai.

Bản R2 tách thành **năm vai trò riêng biệt**, mỗi vai một phép đo:

| Vai trò | Nghĩa | Cách lấy |
|---|---|---|
| Mốc nội dung kỹ năng | lần cuối nội dung kỹ năng thật sự đổi | đo bằng lịch sử kho |
| Mốc sinh hiện vật | trạng thái kho lúc chạy bộ sinh | đo lúc chạy |
| Mốc đã kiểm | nơi cổng **đã thật sự chạy** | điền **sau** khi mốc đó tồn tại |
| Mốc hồ sơ | chỉ chứa biên nhận, trỏ về mốc đã kiểm | bước hai |
| Mốc báo cáo | kho báo cáo công khai | bước cuối |

Ba vai trò cuối **không được khai trước khi chúng tồn tại**. Hiện vật ghi thẳng là "chưa có"
thay vì đoán — đó là lý do quy trình đi **hai bước** thay vì một.

---

## 5. ĐỐI SOÁT MỘT CON SỐ BỊ HIỂU NHẦM SUỐT HAI GÓI

Có hai con số bị đọc như thể mâu thuẫn: nơi này ghi ba mươi hai, nơi kia ghi ba mươi mốt.

**Kết luận: không hề mâu thuẫn.** Có **hai cách chia khác hẳn nhau**, và **cả hai cùng cho ra
ba mươi mốt**:

- chia theo **bản chất**: một nhóm chuyên biệt + một nhóm cơ bản + một trang cá nhân được bảo vệ;
- chia theo **trạng thái chuẩn hoá**: phần đã đưa vào danh mục chung + phần chưa đưa.

Hai cách chia độc lập nhau và **trùng hợp cùng ra một con số**. Lỗi thật không nằm ở con số —
nó nằm ở chỗ bản trước ghi con số ấy **trần trụi**, không nói nó thuộc cách chia nào.

Chúng tôi đã đọc trực tiếp nguồn để phân định dứt điểm: con số "một" trong danh mục thuộc
**cách chia thứ hai**, không phải trang cá nhân của cách chia thứ nhất.

> **Nguyên tắc rút ra:** một con số không kèm **tiêu chí đếm** là một con số chết. Từ nay mọi
> con số trong tài liệu điều phối phải nêu cả **mốc** lẫn **cách đếm**.

---

## 6. CỔNG KIỂM VÀ KIỂM NGƯỢC

| Phép | Trước (R1) | Sau (R2) |
|---|---|---|
| Số điều kiện cổng | 185 | **244** |
| Kết quả | 185 đạt / 0 hỏng | **244 đạt / 0 hỏng** |
| Bảng chân trị chính sách | 21 ca | **24 ca** |
| Nhóm điều kiện | A–G (7 nhóm) | **A–H (8 nhóm)** |

**Nhóm H mới — mười ba cổng chống tái phát**, mỗi cổng chặn **đúng một** loại sai lệch **đã đo
được trên kho thật**, không phải phòng xa chung chung. Trong đó có:

- một cổng chặn **cả họ lỗi nuốt ký tự** cho mọi kịch bản — thứ đã làm cổng cũ rỗng nghĩa;
- một cổng bắt **chính cổng cũ phải tự chứng minh** nó bắt được thứ nó khai là đang canh;
- một cổng so **từng ô** giữa hợp đồng và sổ bằng chứng — lệch một ô là đỏ;
- một cổng cấm **rủi ro cao làm trần lỏng**;
- một cổng cấm **phép thử chạy trên tập rỗng** — đúng thứ gói việc cấm đích danh.

### Vòng kiểm ngược đầu **thất bại** — và đây là phần đáng giá nhất

Gói việc yêu cầu: *"nếu có lỗ mù thì sửa, chạy lại toàn bộ, và **báo cả vòng thất bại đầu,
không che**."* Chúng tôi báo đúng như vậy.

**Vòng một: 18 đạt · 8 lỗ mù · 1 không kết luận / 27 lần phá.**

Tám lỗ mù ấy **không** nằm ở phần đã sửa — chúng nằm ở **chính các cổng mới**. Cụ thể:

1. Bảng kiểm chỉ có dữ liệu **đúng dạng**, nên gỡ hẳn nhánh xử lý dữ liệu **sai dạng** mà cổng
   vẫn xanh. *Một nhánh chưa từng được cho thứ nó cần lọc là một nhánh chưa từng được đo.*
2. Không có ca nào đặt **cảnh báo đứng trước loại-cứng** trên cùng một kỹ năng, nên khôi phục
   lệnh dừng sớm mà không ai thấy.
3. Bộ đối chiếu giá trị hợp lệ không có gì để bắt, vì **mọi dữ liệu trong kho đều hợp lệ** —
   phải **tiêm** một giá trị sai vào mới đo được.
4. Một cổng chỉ so hai nơi, còn chỗ vi phạm nằm ở **nơi thứ ba**.
5. Một cổng dò chuỗi ở **bất kỳ đâu** trong tệp, nên đổi tiêu đề mục mà nó vẫn xanh.
6. Một cổng đọc trường A trong khi phép phá đổi trường B — hai trường **không ai buộc phải
   khớp nhau**.

Cả tám đã được vá bằng điều kiện thật, rồi chạy lại toàn bộ.

---

## 7. CHẾ ĐỘ VẬN HÀNH SAU GÓI NÀY

Gói việc yêu cầu tách bạch **cấu hình đang bật/tắt** khỏi **kết quả đo năng lực** — hai loại
thông tin khác hẳn nhau và trước đây bị trộn.

**Cấu hình vận hành** — điều đang được bật hay tắt:
- chế độ: **cố vấn — thủ công**
- không móc tự động · không tự cài · không tự cập nhật
- quyền thi hành: **tắt theo thiết kế**

**Bằng chứng năng lực** — điều đã đo được:
- công cụ đang dùng: **đã đo và xác nhận là không** tự nhận diện được kỹ năng dự án; hai trục
  còn lại **chưa đo**; quyền thi hành **tắt theo thiết kế**
- công cụ thứ hai: cả ba phép đo **bị chặn, chưa chạy được** — không phải "trượt"

> ⛔ **Ba điều tuyệt đối không được suy:** "chưa đo" **không phải** "đã đo và không có";
> "bị chặn" **không phải** "trượt"; "tắt theo thiết kế" **không phải** một kết quả đo.

---

## 8. NHỮNG GÌ **KHÔNG** ĐỘNG TỚI

- Không đụng mã sản phẩm, giao diện nghiệp vụ, lược đồ hay dữ liệu thật
- Không đụng máy vận hành, không triển khai, không nâng số phiên bản
- Không xoá, gộp, đổi tên hay thay thế bất kỳ kỹ năng nào — **toàn bộ định danh còn nguyên**
- Không sửa nội dung của bất kỳ kỹ năng nào
- Không cài, không cập nhật thư viện kỹ năng bên ngoài
- Không bật móc tự động, không bật tự nhận diện, không bật tự nạp, không bật tự thi hành
- **Không gọi giao diện lập trình để sửa nền tảng tài liệu.** Kết nối chỉ được dùng để **đọc**,
  và đã dùng để lấy **nguyên văn** hiện trạng làm căn cứ cho đề xuất

---

## 9. CÒN LẠI — VÌ SAO CHƯA ĐÓNG HẲN

1. **Nền tảng tài liệu chưa được đồng bộ.** Nó đang ghi kết luận của bản trước, mà bản đó đã
   bị bác bỏ một phần. Đề xuất sửa đã soạn xong cho **tám trang**, mỗi mục có nguyên văn trước
   và sau — nhưng **chưa áp**, và sẽ không áp cho tới khi có xác nhận mới.
2. **Xác nhận cũ không tự động áp cho bản mới.** Chủ dự án đã duyệt bản trước dựa trên hồ sơ
   bản trước. Bản này bác bỏ một phần hồ sơ ấy, nên trạng thái đồng bộ quay về **đề xuất**.
3. **Ba phép đo trên công cụ thứ hai vẫn bị chặn** — cần một phiên đúng công cụ đó. Việc này
   là **bảo trì**, **không** chặn chế độ cố vấn — thủ công và **không** chặn quay lại làm ERP.
4. **Hai trục năng lực chưa được đo trên bất kỳ công cụ nào.**
5. **Các quyết định còn mở** vẫn giữ mặc định an toàn, không phá huỷ gì.
6. **Sáu trong tám trang đề xuất chưa được đọc trực tiếp** trong gói này. Với những trang đó,
   số hiệu bản gốc ghi thẳng là **"chưa đo được"** thay vì đoán.

---

## 10. VỀ TÍNH ĐỘC LẬP CỦA BẰNG CHỨNG

Các mã kiểm tra tính toàn vẹn trong hồ sơ là **do chính phiên này tính**. Chúng chứng minh
tệp **không đổi giữa hai thời điểm** — **không** phải xác nhận độc lập của bên thứ ba.

Việc đối soát độc lập thuộc bước sau.

---

*Báo cáo này an toàn để công khai: không chứa địa chỉ máy chủ, đường dẫn máy vận hành, khoá,
mật khẩu, thông tin định danh cá nhân, số liệu kinh doanh hay số tiền.*
