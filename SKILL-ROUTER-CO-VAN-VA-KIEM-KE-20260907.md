# BỘ ĐỊNH TUYẾN KỸ NĂNG CỐ VẤN + KIỂM KÊ TOÀN KHO — 07/09/2026

**Gói việc:** `ERP-SKILL-CONTINUOUS-EVOLUTION-ROUTING-007`
**Phạm vi:** CHỈ hệ kỹ năng — không đụng mã chức năng ERP · không đụng cơ sở dữ liệu · không triển khai
**Trạng thái chung:** `PASS` cho phần đã làm · **6 việc chờ Chủ dự án quyết**

---

## 1. LÀM ĐƯỢC GÌ

### 1.1 Quét trước khi tạo — điều kiện bắt buộc
Lệnh giao việc cấm tạo bộ định tuyến mới **trước khi** quét thành phần tương đương.
Đã quét: **0** tệp định tuyến/phân giải tương đương tồn tại trong kho ⇒ được phép tạo mới.
Ba cổng kiểm kỹ năng đã có từ trước vẫn giữ nguyên, không bị thay thế.

### 1.2 Bộ định tuyến — **CỐ VẤN**, không phải người quyết
Nó **đề xuất** tuyến cho một việc, kèm lý do đo được. Nó **không** nạp kỹ năng,
**không** thi hành, **không** ghi tệp, **không** gọi mạng, **không** chạm cơ sở dữ liệu,
và **không cấp thêm quyền cho bất kỳ ai**.

Bốn điều kiện của cổng chứng minh điều này bằng cách **đọc chính mã nguồn** của nó,
chứ không tin lời tự khai.

### 1.3 Trần an toàn — theo **bằng chứng**, không theo nhãn
Chế độ "công cụ tự chọn kỹ năng" hiện **không cấp cho bất kỳ kỹ năng nào**.
Lý do đo được: **0/128** kỹ năng ở trạng thái nội dung `ACTIVE` (127 chưa soát · 1 ngủ đông).
Theo luật hiện hành, "chưa soát" **không phải** là "còn hiệu lực".

Trần này **tự nâng lên** khi Chủ dự án soát và gắn hiệu lực cho kỹ năng — **không cần sửa mã**.

### 1.4 Cổng kiểm — 41 điều kiện, đọc đầu vào thật
Bốn nhóm: hành vi · chặn hồi quy · trần an toàn · cấu trúc mã nguồn.
Đã nối vào bộ cổng quản trị; cổng chống-lệnh-mồ-côi xác nhận **124/124** lệnh đều có bộ gộp gọi tới.
Toàn bộ chuỗi cổng quản trị: **mã thoát 0**.

---

## 2. TỰ SOÁT — HAI LỖI CỦA CHÍNH BẢN NHÁP ĐẦU

Cả hai đều do **đo bằng vật thế thân** thay vì đo tác động — **cùng loại sai** với gói việc trước,
chỉ lật ngược chiều.

| # | Lỗi | Hậu quả |
|---|---|---|
| a | Một lớp trình bày giao diện trùng tên với một lệnh cơ sở dữ liệu, bị bắt nhầm | Kỹ năng giao diện bị đẩy lên lớp rủi ro dữ liệu/quyền |
| b | Kỹ năng có nhiệm vụ **CẤM** chạm thông tin nhạy cảm bị đẩy lên lớp rủi ro cao nhất, chỉ vì thân nó **nhắc tên** những thứ nó cấm | Cổng lọc bảo vệ lại bị xếp nguy hiểm hơn thứ nó bảo vệ |

**Bài học ghi lại trong mã:** *nhắc một việc không phải là làm việc đó*.
Cả hai lỗi nay đều có phép thử chặn hồi quy, kèm **đối chứng dương** (lệnh thật vẫn phải bị bắt).

### Lỗi thứ ba — lộ ra nhờ kiểm ngược
Bộ lọc "bỏ qua khi nằm trong ngữ cảnh cấm" **không hề chạy**: bản đầu **cắt rời** khối lệnh khỏi văn xuôi
rồi mới dò chữ "CẤM" — mà chữ đó đã bị cắt mất.
Sửa bằng cách **đánh dấu vùng trên chuỗi gốc** thay vì cắt chuỗi.

---

## 3. KIỂM NGƯỢC — VÀ MỘT BÀI HỌC VỀ CHÍNH VIỆC KIỂM NGƯỢC

Cổng xanh **không** chứng minh cơ chế chạy. Chỉ kiểm ngược mới chứng minh.
Đã phá **7 chỗ**, mỗi lần một chỗ, rồi phục hồi — **7/7 lần cổng đỏ đúng điều kiện tương ứng**.

> ⚠️ **Bài học riêng:** ở lần kiểm ngược đầu, **ba lệnh phá không hề có tác dụng** (sai dấu thoát),
> nhưng kết quả hiện ra y như "cổng vẫn xanh" — suýt nữa thành một kết luận sai.
> ⇒ Kiểm ngược **phải xác nhận tệp đã thật sự đổi** trước khi kết luận.
> Điều này đã được ghi thành quy tắc trong hợp đồng điều phối.

Nhờ kiểm ngược đúng cách, phát hiện **ba cơ chế không có phép thử nào bảo vệ** —
và **một phép thử xanh vì lý do khác với điều nó khai**. Cả bốn đã được vá.

---

## 4. SỐ ĐO MỚI TRÊN TOÀN KHO 128 KỸ NĂNG

### 4.1 Rủi ro theo **tác động tối đa nếu làm theo nội dung**
| Lớp | Số kỹ năng |
|---|---|
| Chỉ đọc | 101 |
| Chạm mã nguồn | 10 |
| Chạm dữ liệu hoặc quyền | 9 |
| Chạm phát hành / vận hành | 8 |

### 4.2 Nguồn gốc — phát hiện đáng chú ý nhất
**10/128** kỹ năng **không được Git theo dõi**. Cả 10 đều thuộc **một họ kỹ năng của nhà cung cấp
bên ngoài**, nằm **cùng thư mục** với kỹ năng của dự án nên rất dễ bị tưởng là đã được quản.
Đối chiếu bằng lệnh Git: khớp **10/10**.

Không lịch sử · không nguồn gốc kiểm được · chưa kiểm giấy phép ⇒ bộ định tuyến **khoá sẵn**.
**Không xoá cái nào** — chờ Chủ dự án quyết.

### 4.3 Trùng lặp — kết quả **trái với giả định ban đầu**
Đo toàn bộ **8.128 cặp**:

| Ngưỡng trùng | Số cặp |
|---|---|
| ≥ 0,20 | 3 |
| ≥ 0,15 | 13 |
| ≥ 0,10 | 33 |
| trùng hoàn toàn | **0** |

Trung vị độ trùng: **0,0000**.
Trong 33 cặp ≥ 0,10: **32 cặp** nằm trong họ nhà cung cấp, **đúng 1 cặp** là kỹ năng do Chủ dự án dựng.

> **Kết luận:** giả định "kho kỹ năng phình ra vì trùng lặp" **không đúng** với phần Chủ dự án tự dựng.
> Trùng lặp tập trung ở họ nhà cung cấp. ⇒ **Không gộp** phần Chủ dự án tự dựng.

### 4.4 Rào cản ngôn ngữ — cản trở việc tra cứu theo triệu chứng
**0/128** kỹ năng có chữ **"giao diện"** ở tên · mô tả · lĩnh vực. Toàn bộ viết tắt bằng tiếng Anh.
Trong khi Chủ dự án **và chính bộ luật** đều viết tiếng Việt, và có **61** kỹ năng thuộc lĩnh vực giao diện.

⇒ Mọi lần tra kỹ năng theo triệu chứng bằng tiếng Việt đều **trượt hoàn toàn**.
Đã bắc **cầu từ vựng Việt→Anh** trong bộ định tuyến, khai rõ là **bảng do người dựng, còn thiếu** —
thiếu một lối vào chỉ làm bộ định tuyến im lặng, **không** làm nó chọn bừa.

### 4.5 Điều kiện không-kích-hoạt
**96/128** kỹ năng **chưa khai** điều kiện không-kích-hoạt ⇒ phép kiểm âm **không thể đạt**
⇒ những kỹ năng này **không bao giờ** được chọn tự động.

---

## 5. BỐN HỆ KỸ NĂNG CÙNG TỒN TẠI — CHỈ **MỘT** ĐƯỢC QUẢN

| Hệ | Có sổ đăng ký | Có cổng kiểm |
|---|---|---|
| Kỹ năng dự án | ✅ | ✅ |
| Kỹ năng nhà cung cấp (nằm cùng thư mục) | ✅ | một phần |
| Kỹ năng dựng sẵn của công cụ | ❌ | ❌ |
| Kỹ năng của trình kết nối ngoài | ❌ | ❌ |

Hai hệ cuối nằm **hoàn toàn ngoài** vòng quản trị của dự án và **thay đổi theo bản cập nhật của công cụ**
mà dự án không hay biết. Cả hai công cụ đang dùng đều đã **tự cập nhật nhiều lần** trong chuỗi rà soát này.

---

## 6. NHỮNG ĐIỀU **KHÔNG** LÀM (đúng lệnh cấm)

- Không sửa mã chức năng ERP · không sửa cơ sở dữ liệu · không triển khai
- Không sửa năm bản luật quản trị chỉ để gắn bộ định tuyến
- Không tạo móc tự chạy — đã quét, không có thư mục móc và không tệp cài đặt nào khai khoá móc
- **Không xoá cứng kỹ năng nào**, kể cả kỹ năng ngủ đông và kỹ năng không rõ nguồn gốc
- Không chép nội dung nhà cung cấp vào kỹ năng dự án
- **Không tự nâng kỹ năng nào lên trạng thái còn hiệu lực** — đó là quyền của Chủ dự án

---

## 7. CHƯA CHỨNG MINH ĐƯỢC

| Điều | Vì sao | Ai xác minh được |
|---|---|---|
| Cursor có tự nhận diện kỹ năng dự án hay không | Chưa có phiên Cursor nào tự báo danh sách kỹ năng được cấp. **Cấm suy kết quả từ công cụ khác** | Một phiên Cursor chạy bộ kiểm đã soạn ở gói việc trước |
| Kỹ năng dựng sẵn của từng công cụ theo từng bản | Công cụ không công bố dạng máy đọc | Nhà cung cấp công cụ |
| Chất lượng khớp việc↔kỹ năng ngoài các ca đã thử | Cầu từ vựng do người dựng, chưa phủ hết | Dùng thật rồi ghi ca trượt |

---

## 8. CHỜ CHỦ DỰ ÁN QUYẾT — 6 VIỆC

1. **Mười kỹ năng nhà cung cấp không rõ nguồn gốc**: giữ khoá · tách khỏi thư mục kỹ năng dự án · hay kiểm giấy phép rồi nhận nuôi?
2. **Bổ sung bí danh tiếng Việt** vào sổ đăng ký kỹ năng, để tra theo triệu chứng bằng tiếng Việt không trượt?
3. **Một cặp kỹ năng trùng nhau** do Chủ dự án dựng — gộp hay giữ cả hai?
4. **96 kỹ năng chưa khai điều kiện không-kích-hoạt** — có làm đợt bổ sung không?
5. **Kỹ năng dựng sẵn của công cụ** — có lập sổ đăng ký để biết khi nào chúng đổi không?
6. **Hợp đồng điều phối** đang ở trạng thái *đề xuất* — có nâng thành luật để các phiên sau bắt buộc theo không?

---

## 9. BƯỚC KẾ TIẾP — ĐÚNG MỘT VIỆC

Chạy bộ kiểm trên **một phiên Cursor thật** để trả lời dứt điểm câu hỏi
"công cụ có tự nhận diện kỹ năng dự án không" — đây là điều duy nhất chặn việc
quyết định giữa hai đường điều phối.

---

*Mã commit và mã băm nội bộ không đưa vào báo cáo công khai theo quy tắc an toàn báo cáo; đã bàn giao riêng.*
