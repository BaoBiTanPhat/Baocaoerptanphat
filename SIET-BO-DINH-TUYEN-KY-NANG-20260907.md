# SIẾT BỘ ĐỊNH TUYẾN KỸ NĂNG — RÀ NGỮ NGHĨA TOÀN BỘ 128 KỸ NĂNG — 07/09/2026

**Gói việc:** `ERP-SKILL-ROUTING-HARDENING-CLOSEOUT-008`
**Phạm vi:** CHỈ hệ kỹ năng — không đụng mã sản phẩm · không đụng cơ sở dữ liệu · không triển khai
**Trạng thái:** `PARTIAL` — **không** dùng chữ "hoàn tất"

> Vì sao `PARTIAL`: mọi hạng mục trong phạm vi thi hành được đều đạt và có kiểm ngược chứng minh,
> nhưng **hai điều không thể đóng trong gói này** — bộ kiểm trên công cụ Cursor chưa chạy được,
> và sáu quyết định của Chủ dự án vẫn còn phần mở.

---

## 1. VIỆC LỚN NHẤT: RÀ NGỮ NGHĨA ĐỦ 128 KỸ NĂNG

Trước đây, "điều kiện để **không chọn** một kỹ năng" được máy rút ra bằng cách **dò chữ** —
thấy chữ "không", "cấm", "không kích hoạt" thì lấy. Cách đó sai về bản chất, và lần này được
thay bằng cách đọc **từng thân kỹ năng, toàn phần**, có **tầng phản biện đối kháng**.

**Cách làm:** một tác nhân đọc và phân loại → một tác nhân khác đọc lại **cùng tệp** và
**cố bác bỏ**. Bất đồng thì lấy bản phản biện (nghiêng về an toàn).

**Quy mô:** 128/128 kỹ năng · hai đợt · **251 tác nhân** · 0 lỗi · 123 mục có phản biện.

**Phản biện lật ngược 68 phán quyết** (63 về ngữ nghĩa, 6 về mức rủi ro). Đây không phải nghi thức —
tầng phản biện thật sự sửa được kết luận sai.

| Phân loại | Số kỹ năng |
|---|---|
| Điều kiện hợp lệ | 78 |
| Thân không có điều kiện nào | 39 |
| **Ghi sai — không phải điều kiện không-chọn** | **8** |
| Mơ hồ, cần Chủ dự án phân xử | 3 |

> **Phát hiện đáng chú ý:** **96/128** thân kỹ năng **có** điều kiện không-nên-dùng thật sự,
> trong khi sổ đăng ký chỉ khai **32**. Máy sinh bỏ sót phần lớn.

---

## 2. MỘT KẾT LUẬN CŨ BỊ LẬT NGƯỢC BẰNG SỐ ĐO

Bộ định tuyến đang suy mức rủi ro bằng **mẫu dò văn bản**. Đối chiếu với kết quả **đọc thân thật**:

| Cách đo | Chỉ đọc | Sửa mã | Chạm dữ liệu/quyền | Phát hành/vận hành |
|---|---|---|---|---|
| Mẫu dò (cũ) | 101 | 10 | 9 | 8 |
| **Sau khi lấy giá trị lớn nhất** | **6** | **96** | **15** | **11** |

**Lệch 109/128 kỹ năng, trong đó 97 ca cách đo cũ xếp THẤP HƠN thực tế.**

⇒ Mẫu dò **đánh giá thấp rủi ro một cách hệ thống**: nó bỏ sót mọi kỹ năng dạy sửa mã bằng
**văn xuôi** mà không có lệnh nào trong khối mã. Quy tắc "lấy giá trị lớn nhất trong ba nguồn,
cấm hạ" là thứ duy nhất giữ cho con số không bị kéo xuống.

---

## 3. NĂM LỖI CỦA CHÍNH BỘ ĐỊNH TUYẾN — TỰ PHÁT HIỆN, ĐÃ SỬA

Cả năm đều lộ ra khi **chạy trên dữ liệu thật** hoặc khi **kiểm ngược**, không phải khi đọc lại mã.

| # | Lỗi | Vì sao nguy hiểm |
|---|---|---|
| 1 | **Đảo cực.** Điều kiện *"việc KHÔNG đụng tới giao diện"* chứa chính chữ "giao diện", nên một việc **giao diện** lại **khớp** điều kiện loại-bỏ | Loại đúng thứ đáng lẽ phải chọn — sai **ngược chiều** |
| 2 | **Khớp vào từ vựng chung.** Hai kỹ năng chọn-một và chọn-nhiều dùng chung từ "chọn giá trị", nên kỹ năng chọn-nhiều bị loại bởi điều kiện chọn-một | Ranh giới giữa hai kỹ năng bị xoá sạch |
| 3 | **Chặn quá tay.** Chữ "CẤM" ở mệnh đề trước nuốt luôn lệnh thật ở mệnh đề *"thay vào đó, chạy…"* | Giấu đi đúng thứ cần thấy — nguy hơn không chặn |
| 4 | **Ba phép thử rỗng nghĩa.** Chúng xanh vì **không có ca nào để xét**, chứ không phải vì cơ chế chạy đúng | Cổng xanh mà cơ chế không được bảo vệ |
| 5 | **Đánh giá thấp rủi ro** (mục 2 ở trên) | Việc nguy hiểm bị xếp nhẹ |

Cả năm nay đều có phép thử chặn tái diễn, kèm **đối chứng dương** (ca thật vẫn phải bị bắt).

---

## 4. NHỮNG THỨ ĐÃ SIẾT

- **Bốn trục trạng thái độc lập** thay cho một nhãn mơ hồ gộp chung. Nhận diện được ≠ nạp vào ≠ làm theo.
- **Chế độ tự động: tắt toàn bộ.** Không nhánh mã nào mở được, và giá trị đó **không nằm trong**
  danh sách hợp lệ của nguồn cấu hình. Muốn mở phải sửa **cả** mã, **cả** cấu hình, **cả** cổng kiểm —
  không thể mở bằng một dòng dữ liệu.
- **Trần số kỹ năng hỗ trợ là cứng** — người gọi truyền số lớn hơn cũng không vượt được.
- **Tuyến cuối lấy mức chặt nhất** của toàn bộ kỹ năng chính và hỗ trợ, không phải của riêng cái chính.
- **Mã băm đầy đủ** trong biên nhận — bản rút gọn không đủ làm bằng chứng.
- **Nguồn cấp quyền phải do người gọi nêu đích danh.** Không nêu thì biên nhận ghi thẳng "chưa nêu",
  tuyệt đối không tự bịa một cái chung chung.
- **Hoà điểm thì hỏi Chủ dự án**, cấm chọn theo thứ tự tệp.
- **Số đo năng lực công cụ đọc từ tệp**, quá hạn 30 ngày thì tự cảnh báo — vì công cụ **tự cập nhật**
  liên tục, viết cứng trong mã nghĩa là biến số đo hôm nay thành "sự thật vĩnh viễn" của mai.
- **Năm không gian định danh tách bạch.** Một cái tên giống nhau ở hai hệ khác nhau là **hai thứ khác nhau**.

---

## 5. CỔNG KIỂM VÀ KIỂM NGƯỢC

Cổng kiểm mở rộng từ **41 lên 95 điều kiện**, đã nối vào bộ cổng quản trị (mã thoát 0;
cổng chống-lệnh-mồ-côi xác nhận mọi lệnh đều có bộ gộp gọi tới).

**Kiểm ngược: phá 20 chỗ có chủ đích — 20/20 làm cổng đỏ đúng cơ chế tương ứng.**

> **Quy tắc rút ra từ lần trước, lần này thi hành nghiêm:** mỗi lần phá đều **đối chiếu mã băm tệp**
> trước khi kết luận. Không xác nhận tệp đã thật sự đổi thì kết quả "cổng vẫn xanh" là vô nghĩa.
> Sau khi chạy xong, mã băm được đối chiếu lại để chứng minh mọi thứ **trở về đúng nguyên trạng**.

Nhờ làm đúng cách, kiểm ngược phát hiện thêm **ba phép thử rỗng nghĩa** đã nêu ở mục 3.

---

## 6. SÁU QUYẾT ĐỊNH — ĐÃ LÀM GÌ, CÒN GÌ

| Quyết định | Đã thi hành | Còn mở |
|---|---|---|
| Cách ly nhóm kỹ năng nhà cung cấp | Khoá tuyến, không lọt vào ứng viên, **không xoá cái nào** | Rà giấy phép và nguồn gốc thật |
| Bí danh tiếng Việt | Nguồn cấu hình bền vững, sinh lại hai lần cho kết quả giống hệt, tên gốc bất biến | Mới phủ phần hay dùng nhất |
| Giữ riêng cặp kỹ năng gần nhau | Hai mục tách riêng, mỗi cái có ranh giới trỏ sang cái kia | — |
| Rà ngữ nghĩa điều kiện | 128/128, không sửa hàng loạt tệp nào | 39 thiếu · 3 mơ hồ · 7 ghi sai chưa xử |
| Sổ năng lực công cụ | Tách riêng, đọc từ tệp, có cảnh báo dữ liệu cũ | Chưa liệt kê đầy đủ được |
| Hợp đồng điều phối | Đã đính chính một câu sai, giữ nguyên văn câu cũ | Vẫn ở trạng thái **đề xuất** |

---

## 7. MỘT CÂU SAI TRONG BÁO CÁO TRƯỚC — ĐÃ ĐÍNH CHÍNH

Báo cáo ngày 06/09 viết: *"Trần này **tự nâng lên** khi có kỹ năng được soát và gắn hiệu lực;
**không cần sửa mã**."*

**Câu đó SAI.** Gắn nhãn hiệu lực cho một kỹ năng **không** tự mở chế độ tự động. Theo hợp đồng
điều phối đã có, trạng thái đó nhiều nhất chỉ **có thể được xét** sau một phép thử kích hoạt riêng.

Câu cũ được **giữ nguyên văn** trong khối đính chính, theo đúng luật cấm ghi đè im lặng.

---

## 8. CHƯA CHỨNG MINH ĐƯỢC

| Điều | Vì sao | Ai xác minh được |
|---|---|---|
| Công cụ Cursor có tự nhìn thấy kỹ năng dự án không | Phiên thi hành là **công cụ khác chạy bên trong vỏ Cursor** — ở trong nó không phải là nó. Gọi đây là phép đo Cursor sẽ tạo ra một kết quả ĐẠT giả | Một phiên Cursor thật; bộ kiểm hai câu hỏi đã soạn sẵn |
| Danh sách đầy đủ kỹ năng dựng sẵn của từng công cụ | Nhà cung cấp không công bố dạng máy đọc | Nhà cung cấp công cụ |
| Chất lượng khớp việc↔kỹ năng ngoài các ca đã thử | Phép khớp là **đo thô theo từ khoá**, không phải hiểu ngữ nghĩa | Dùng thật rồi ghi lại ca trượt |
| Mức rủi ro từng kỹ năng | Vẫn là **suy đoán** — mạnh nhất hiện nay là bản đọc thân có phản biện, nhưng chưa có người soát từng dòng | Chủ dự án soát mẫu |

---

## 9. NHỮNG ĐIỀU **KHÔNG** LÀM

- Không xoá, gộp, thay thế hay lưu trữ bất kỳ kỹ năng nào của Chủ dự án — **128/128 còn nguyên**
- Không sửa hàng loạt tệp kỹ năng chỉ để lấp trường trống
- Không cài, cập nhật hay tải bất kỳ thư viện bên ngoài nào
- Không sửa mã sản phẩm · cơ sở dữ liệu · máy vận hành · không triển khai · không tăng số phiên bản
- Không sửa các bản luật quản trị — chưa có đối chiếu đầy đủ
- Không tự cập nhật tài liệu trên nền tảng ngoài; gói bàn giao lập riêng để bộ phận phụ trách nhận

---

## 10. BƯỚC KẾ TIẾP — ĐÚNG MỘT VIỆC

Chạy bộ kiểm hai câu hỏi trên **một phiên Cursor thật**, rồi ghi kết quả vào sổ năng lực công cụ.
Đây là điều duy nhất còn chặn việc chọn giữa hai đường điều phối — và bộ định tuyến **đọc thẳng
tệp đó**, nên cập nhật xong là có hiệu lực ngay, **không cần sửa mã**.

---

*Mã commit, mã băm nội bộ và đường dẫn riêng tư không đưa vào báo cáo công khai theo quy tắc an toàn; đã bàn giao riêng.*
