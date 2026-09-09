# ĐÓNG CHUẨN HỆ ĐIỀU PHỐI KỸ NĂNG LIÊN HỆ THỐNG — 09/09/2026

**Gói việc:** `ERP-SKILL-CROSS-SYSTEM-ORCHESTRATION-CLOSEOUT-009`
**Phạm vi:** CHỈ hệ kỹ năng — không đụng mã sản phẩm · cơ sở dữ liệu · máy vận hành
**Trạng thái:** `PARTIAL` — **không** dùng chữ "hoàn tất", **không** dùng chữ "đạt" trần trụi

> Vì sao `PARTIAL`: mọi hạng mục kỹ thuật trong phạm vi được cấp quyền đều xong và có kiểm ngược
> chứng minh. Hai điều **không thể** đóng trong gói này: ba phép đo trên công cụ Cursor đều
> **chưa chạy được**, và các quyết định của Chủ dự án vẫn còn phần mở.

---

## 1. TÁM LỖI TỰ PHÁT HIỆN — ĐỀU ĐÃ SỬA, ĐỀU CÓ PHÉP THỬ CHẶN

Đây là phần quan trọng nhất của gói này. Cả tám đều là lỗi **trong chính hệ thống chúng tôi vừa dựng**,
và cả tám chỉ lộ ra khi **chạy trên dữ liệu thật** hoặc khi **cố tình phá để xem cổng có bắt được không**.

| # | Lỗi | Vì sao nghiêm trọng |
|---|---|---|
| 1 | **Tên tệp thắng dữ liệu.** Một kỹ năng do Chủ dự án tự dựng, được quản lý trong kho, đang tạm nghỉ — vẫn bị xếp sang nhóm "của nhà cung cấp ngoài" chỉ vì **tên nó bắt đầu bằng một tiền tố** | Xếp nhầm quyền sở hữu. Tên tệp không phải giấy khai sinh |
| 2 | **Nhãn chung bị quy về một cái tên cụ thể.** Nhãn "của bên ngoài" bị tự động gán thành tên một nhà cung cấp nhất định | Gán sai nguồn gốc. Không biết là của ai thì phải nói **không biết** |
| 3 | **Kết quả do máy rà được dùng để LOẠI CỨNG.** Máy — dù có tầng phản biện — không phải Chủ dự án | Một phán quyết sai của máy làm người dùng **mất** kỹ năng lẽ ra phải được đề xuất, mà không biết vì sao |
| 4 | **Một trục bằng chứng bị suy ra từ trục khác.** "Công cụ không tự thấy" bị dùng làm căn cứ cho "công cụ cũng không đọc được" — hai việc khác nhau | Tạo ra một kết luận **chưa từng được đo**. Chính phép thử cũ cũng mã hoá đúng lỗi này |
| 5 | **Sổ ghi quá lời.** Ghi "cả năm mục đều có ghi chú hoàn tác" — đo thật chỉ **ba trên năm** | Phiên sau tin là đã có ranh giới gỡ bỏ, trong khi hai chỗ không có |
| 6 | **Trộn hai mẫu số.** Báo cáo trước viết "68 phán quyết (63 + 6)" — 63+6 = 69, không phải 68 | Hai con số đếm **hai thứ khác nhau**: một đếm theo mục, một đếm theo trục |
| 7 | **So chuỗi qua ranh giới chuẩn hoá.** Chuỗi trong nguồn cấu hình là nguyên văn, chuỗi trong sổ đã bị chuẩn hoá ⇒ so nguyên văn không bao giờ khớp | Chuỗi sai **âm thầm ở lại**, và cổng vẫn xanh vì không ai kiểm kết quả cuối |
| 8 | **Một nhánh mã không gánh việc gì.** Gỡ hẳn nó ra mà cổng vẫn xanh | Nhánh đó chỉ **trông như** đang bảo vệ. Kiểm ngược mới phát hiện |

---

## 2. BỐN TRỤC BẰNG CHỨNG — NAY THẬT SỰ ĐỘC LẬP

Trước đây ba khái niệm bị gộp dưới một nhãn mơ hồ. Nay tách hẳn thành **bốn trục**, mỗi trục
**một bằng chứng riêng**, và cấm suy trục này ra trục kia.

| Trục | Câu hỏi | Công cụ đang dùng | Công cụ Cursor |
|---|---|---|---|
| Bộ định tuyến có đề xuất được không | của **dự án**, không phải của công cụ | đang chạy | đang chạy |
| Công cụ có **tự thấy** kỹ năng không | | **chứng minh là KHÔNG** | **chưa đo được** |
| Nội dung có **tự vào** ngữ cảnh không | | **chưa đo** | **chưa đo được** |
| Agent có **tự làm theo** không | | **tắt theo thiết kế** | **tắt theo thiết kế** |

> **Đính chính quan trọng:** báo cáo trước ghi ô thứ ba là "chứng minh là không". Con số đó
> **chưa hề được đo riêng** — nó chỉ bám theo ô thứ hai. Nay hạ về **"chưa đo"**, đúng mức bằng chứng thật.

> **Phiên bản công cụ đã đổi** kể từ báo cáo trước (chỉ trong hai ngày). Kết luận cũ vì vậy chỉ còn
> hiệu lực cho **đúng phiên bản cũ**; bản hiện tại được đo lại từ đầu.

---

## 3. VÒNG ĐỜI CHÍNH SÁCH — AI RÀ KHÔNG PHẢI NGƯỜI DUYỆT

Bốn trạng thái, và **chỉ một** trong bốn được phép loại bỏ một kỹ năng khỏi danh sách đề xuất:

| Trạng thái | Được làm gì |
|---|---|
| Chỉ quan sát | ghi nhận, không can thiệp |
| **Máy đã rà** | **chỉ được cảnh báo** |
| **Chủ dự án đã duyệt** | **được loại cứng** — nhưng phải có căn cứ tra được, còn hiệu lực, và đúng phạm vi |
| Đã bị bác | giữ làm lịch sử, không dùng để cưỡng chế |

Thiếu bất kỳ vế nào trong ba vế của dòng thứ ba ⇒ **tự động hạ xuống cảnh báo**. Không có đường tắt.

⇒ Hệ quả thực tế: **bảy chuỗi ghi sai còn lại không gây hại ngay**, vì chúng chỉ ở mức "máy đã rà"
nên không loại cứng được ai.

---

## 4. SÁU MẶT PHẲNG NĂNG LỰC — CẤM CỘNG GỘP

| Mặt phẳng | Số lượng | Thẩm quyền |
|---|---|---|
| Kỹ năng do Chủ dự án dựng | 118 | Chủ dự án |
| Kỹ năng nhà cung cấp đang cách ly | 10 | bên ngoài — **đang khoá** |
| Tham chiếu nhà cung cấp | 37 | bên ngoài — **chưa cài**, chỉ đọc tham khảo |
| Kỹ năng của trợ lý Notion | 32 | Chủ dự án, ở lớp Notion — **không phải kỹ năng công cụ lập trình** |
| Năng lực dựng sẵn của công cụ | **đếm theo từng công cụ và phiên bản** | nhà cung cấp công cụ |
| Năng lực trình kết nối ngoài | theo từng trình kết nối | bên thứ ba |

⛔ **Không có con số "tổng thư viện".** Cộng bốn mặt phẳng lại rồi tuyên bố "đã làm chủ toàn bộ"
là gộp **bốn thẩm quyền khác nhau** thành một lời khẳng định sai.

⛔ Một cái tên giống nhau ở hai mặt phẳng là **hai thứ khác nhau**.

---

## 5. ĐỐI SOÁT SỐ LIỆU — TÍNH LẠI TỪ DỮ LIỆU, KHÔNG CHÉP

Báo cáo trước viết *"phản biện lật 68 phán quyết (63 ngữ nghĩa + 6 rủi ro)"*. Cộng lại ra 69.

Đếm lại trực tiếp trên dữ liệu:

| Ký hiệu | Nghĩa | Giá trị |
|---|---|---|
| A | số **mục** bị sửa phán quyết về ý nghĩa | 63 |
| B | số **mục** bị sửa phán quyết về mức rủi ro | 6 |
| **C** | số **MỤC** bị sửa **ít nhất một** trục | **68** |
| **D** | tổng số **TRỤC** bị sửa | **69** |
| E | số mục bị sửa **cả hai** trục | 1 |

**C = A + B − E → 68 = 63 + 6 − 1.** Khớp.

⇒ Cách viết **đúng**: *"68 trên 123 mục đã thẩm định bị sửa ít nhất một trục; tổng 69 trục;
đúng một mục bị sửa cả hai."* Hai con số 63/6 đếm theo **trục**, con số 68 đếm theo **mục** —
đặt cạnh nhau mà không nói mẫu số thì trông như phép cộng sai.

---

## 6. BẢO TOÀN KỸ NĂNG — ĐO, KHÔNG KHAI

Năm kỹ năng được sửa ở đợt trước, kiểm chứng lại toàn bộ:

- **0 dòng bị xoá** trên cả năm tệp; tổng **+158 dòng thêm**. Không nội dung cũ nào mất.
- Nội dung trên đĩa **y hệt** bản trong kho — chưa ai đụng thêm sau đợt trước.
- **128/128 định danh còn nguyên.** Không kỹ năng nào bị xoá, gộp, đổi tên hay thay thế.

> **Đính chính:** sổ ghi "mỗi mục đều có ghi chú hoàn tác" — đo thật chỉ **3/5**.
> Nay đã bù cho hai chỗ thiếu, và có một điều kiện cổng canh để câu khai đó không sai lần nữa.

---

## 7. KIỂM CHỨNG

| Phép kiểm | Kết quả |
|---|---|
| Cổng bộ định tuyến | **136 điều kiện, 136 đạt, 0 hỏng** (đợt trước: 95) |
| Kiểm ngược có chủ đích | **31 lần phá — 31 lần cổng đỏ đúng cơ chế** |
| Sinh lại tất định | 3 lần liên tiếp → **cùng một mã băm** |
| Chuỗi cổng quản trị | **mã thoát 0** |
| Cổng chống lệnh mồ côi | **124/124** lệnh đều có bộ gộp gọi tới |

> **Cách làm kiểm ngược:** mỗi lần phá đều **đối chiếu mã băm tệp trước khi kết luận** — không xác nhận
> tệp đã thật sự đổi thì kết quả "cổng vẫn xanh" là vô nghĩa. Sau khi chạy xong, đối chiếu lại
> để chứng minh mọi thứ **trở về đúng nguyên trạng**.
>
> Chính cách này phát hiện lỗi thứ 8: một nhánh mã gỡ ra mà cổng vẫn xanh — tức nó **chỉ trông như**
> đang bảo vệ. Đã sửa để nhánh đó thật sự quyết định, và phép thử tương ứng cũng được sửa
> để **không có nhánh khác đỡ lưng**.

---

## 8. CHƯA CHỨNG MINH ĐƯỢC

| Điều | Vì sao | Ai xác minh được |
|---|---|---|
| Công cụ Cursor có tự thấy kỹ năng dự án không | Phiên thi hành là **công cụ khác chạy bên trong vỏ Cursor**. Ở trong nó không phải là nó | Một phiên Cursor thật |
| Nội dung kỹ năng có tự vào ngữ cảnh không | **Chưa đo trên bất kỳ công cụ nào** | Phép đo B trong thủ tục đã soạn |
| Công cụ có làm theo ràng buộc trong kỹ năng không | **Chưa đo trên bất kỳ công cụ nào** | Phép đo C trong thủ tục đã soạn |
| Danh mục năng lực dựng sẵn của Cursor | Không quan sát được từ bên ngoài | Nhà cung cấp công cụ |
| Mức rủi ro từng kỹ năng | Vẫn là **suy đoán** — nguồn mạnh nhất hiện nay là bản đọc nội dung có phản biện, chưa có người soát từng dòng | Chủ dự án soát mẫu |

**Ba phép đo trên Cursor đã được tách riêng** thay vì gộp làm một, vì trả lời được câu này
**không** trả lời được câu kia: thấy tên khác hẳn đọc được nội dung; đọc được khác hẳn làm đúng theo.

---

## 9. CHỜ CHỦ DỰ ÁN QUYẾT — MỖI DÒNG CÓ MỘT MẶC ĐỊNH AN TOÀN

| Việc | Mặc định an toàn khi chưa quyết |
|---|---|
| Ba mục cần phân xử về ý nghĩa | chỉ quan sát, không cưỡng chế |
| Sáu chuỗi ghi sai còn lại | giữ nguyên — chỉ ở mức cảnh báo nên không loại cứng được ai |
| 39 kỹ năng thiếu điều kiện | chỉ quan sát; xếp ưu tiên theo rủi ro |
| 10 kỹ năng nhà cung cấp cách ly | **giữ khoá** — không xoá, không cài lại |
| 31 định danh trợ lý Notion | giữ nguyên, chỉ ghi số lượng |
| Cặp kỹ năng gần nhau | **giữ riêng** |

⇒ Chưa quyết thì hệ thống **không tự làm gì**. Đó là điểm của cột bên phải.

---

## 10. NHỮNG ĐIỀU **KHÔNG** LÀM

- Không sửa mã sản phẩm · cơ sở dữ liệu · máy vận hành — **0 tệp sản phẩm bị đụng**
- Không xoá, gộp, đổi tên, thay thế hay lưu trữ bất kỳ kỹ năng nào
- Không sửa hàng loạt tệp kỹ năng chỉ để lấp trường trống
- Không cài, cập nhật hay tự chạy bất kỳ thư viện bên ngoài nào
- Không bật móc tự chạy, không đổi cài đặt công cụ
- **Không sửa tài liệu trên nền tảng ngoài** — chỉ lập **đề xuất** để bộ phận phụ trách đối soát
- Không tăng số phiên bản, không triển khai

---

## 11. BƯỚC KẾ TIẾP — ĐÚNG MỘT VIỆC

Gửi hồ sơ bàn giao này cho bộ phận phụ trách tài liệu để đối soát với kho công khai,
rồi trình Chủ dự án xác nhận lần cuối trước khi cập nhật tài liệu.

---

*Mã commit, mã băm nội bộ và đường dẫn riêng tư không đưa vào báo cáo công khai theo quy tắc an toàn; đã bàn giao riêng.*
