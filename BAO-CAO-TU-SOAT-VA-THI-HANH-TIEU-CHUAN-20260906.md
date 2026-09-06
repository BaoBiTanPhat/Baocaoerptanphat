# BÁO CÁO — TỰ SOÁT ĐỐI KHÁNG & THI HÀNH TIÊU CHUẨN ĐÃ KHOÁ (06/09/2026)

> **Kho:** báo cáo công khai (bản đã lọc an toàn) · **Ngày lập:** 06/09/2026
> **Lớp bằng chứng:** `CODE_PROVEN` + `FILE_PROVEN`. **KHÔNG** có `UI_PROVEN` — lý do ở mục 6.
> **Loại phiên:** tự soát (không có lượt Owner bác kết quả). Chủ dự án chỉ thị: *"xử lý tiếp các vấn đề trong khả năng đã rõ ràng đi"* và *"nhớ báo cáo đầy đủ"*.

---

## 1. Vì sao có phiên này

Sau chuỗi việc 03–05/09, chủ dự án yêu cầu rà xem **còn vấn đề tiềm ẩn nào chưa soi thấy**. Đợt rà chạy **7 hướng độc lập** (bộ luật · tài liệu chuẩn · mã bảng danh mục · mã panel/định danh · sổ nợ · sổ yêu cầu & nghĩa vụ quản trị · dây chuyền phát hành · độ đúng của báo cáo công khai), mỗi phát hiện đều đưa qua **vòng phản biện cố bác bỏ**.

Kết quả đáng chú ý nhất: **phần lớn lỗi tìm được là do chính các lượt vá trước đó của tôi để sót** — không phải lỗi mới của hệ thống.

---

## 2. Ba lỗi nghiêm trọng nhất — đều là "vá xong nhưng bỏ sót chỗ cùng chủ đề"

### 2.1 Bản vá luật 05/09 vi phạm chính điều luật nó đang sửa

Quy tắc sửa-bảo-toàn bắt: *"trước khi sửa, quét toàn file tìm MỌI vị trí nói về cùng đối tượng, sửa hết trong cùng một lượt"*. Lượt 05/09 sửa điều luật về nơi lưu thông tin rủi ro nhưng **bỏ sót bảng chỉ mục** — tức **chỗ mà mọi phiên đọc TRƯỚC TIÊN** — nơi vẫn ghi giới hạn cũ đã bị bãi bỏ. Phiên sau tra bảng chỉ mục sẽ nhận thông tin sai.

Đã khép **10 điểm** trong một lượt trên cả năm bản luật (đồng nhất từng byte), mỗi dòng thay đều giữ nguyên văn ở mục lịch sử.

### 2.2 Bộ tiêu chí nghiệm thu vẫn dạy đúng tổ hợp gây lỗi

Tiêu chí nghiệm thu "đầu bảng phải ghim" còn ghi **"BA điều kiện"** và điều kiện (1) là đặt thuộc tính ghim lên **ô tiêu đề** — đúng tổ hợp mà tài liệu chuẩn đã CẤM từ 04/09. Nghĩa là: **ai nghiệm thu theo đúng bộ tiêu chí sẽ tái tạo y nguyên lỗi "ghim nhưng trong suốt"** mà chủ dự án đã báo.

Tài liệu chuẩn được vá ngày 05/09 nhưng **bộ tiêu chí thì bị quên**. Nay đã sửa thành **bốn điều kiện**, khớp tài liệu chuẩn.

### 2.3 Số đo "0" trong báo cáo 04/09 là **0 giả**

Báo cáo 04/09 khẳng định *"quét toàn hệ, số chỗ đặt ghim sai = 0"*. Phép dò khi đó giả định thẻ mở và danh sách thuộc tính nằm **cùng một dòng**; mã dự án viết **nhiều dòng**, nên phép dò trả về 0 mà thực tế **một trang còn 4 ô tiêu đề đặt ghim sai**.

Về hiển thị thì **vẫn đúng** (vì hàng tiêu đề mới là hộp mang nền và được ghim) ⇒ **lỗi chủ dự án báo đã thật sự hết**. Nhưng lời khai "0" thì sai — và chính tài liệu chuẩn đã ghi **"CẤM nghiệm thu bằng phép dò chuỗi"**. Đã đính chính công khai trong tài liệu chuẩn, kèm **cách đo đúng** để phiên sau không dính lại.

> **Bài học chung của cả ba:** vá đúng chỗ được chỉ ra thì dễ; **quét hết chỗ cùng chủ đề** mới là phần hay hỏng.

---

## 3. Bẫy còn sót trong dây chuyền phát hành

| Điểm | Tình trạng trước | Đã xử lý |
|---|---|---|
| Chuỗi lệnh nhiều dòng gửi sang máy vận hành | Bản vá 04/09 chỉ chuẩn hoá **một** biến; còn **một biến khác** cũng nhiều dòng vẫn gửi thô ⇒ cùng gốc lỗi từng làm đứng đợt phát hành | ✅ Đã chuẩn hoá |
| Kiểm tuyến sau khi khởi động lại | Chỉ **in** dòng trạng thái rồi đi tiếp ⇒ lỗi máy chủ **vẫn trót lọt âm thầm** | ✅ Nay **đọc mã trạng thái thật** và **chặn** khi hỏng |
| Cổng "đợt này không cần nạp dữ liệu" | **Tin ngay lời khai**, không đối chứng gì | ✅ Nay đối chứng bằng máy: nếu lượt kéo mã có đụng vùng cơ sở dữ liệu thì lời khai bị **bác** |

**Hai báo động đã được kiểm và BÁC BỎ** (nêu ra để không ai đuổi lại): các tệp kịch bản mang ký tự xuống dòng kiểu Windows trên máy phát triển là **vô hại** (bản lưu trong kho đã chuẩn, máy vận hành nhận đúng); và một biến bị nghi thiếu chuẩn hoá thực ra là chuỗi **một dòng**, không có rủi ro.

---

## 4. Thi hành tiêu chuẩn đã khoá — phần mã nguồn

Chủ dự án đã chốt từ 03/09 rằng bốn điều là **tiêu chuẩn thiết kế**, và chấn chỉnh 04/09: *"đã là tiêu chuẩn thì áp hết, không hỏi từng trang"*.

- **Cấm để lộ khoá nội bộ ra màn hình — vá 11 chỗ.** Trong đó **hai chỗ nằm ngay trên trang mà chủ dự án đã bác một lần**: ô chọn người phụ trách khi **chuyển khách hàng**, và ô chọn ở **luồng tạo mới nhiều bước** — cả hai vẫn in số khoá nội bộ cạnh tên người, đúng kịch bản đã bị bác. Lượt vá 03/09 chỉ sửa panel chi tiết nên bỏ sót.
- **Gỡ một cái bẫy:** một hàm trợ giúp **không còn nơi nào gọi** nhưng thân hàm vẫn là đúng hai mẫu bị cấm — để nguyên là đặt sẵn bẫy cho phiên sau nhặt lên (cùng loại bẫy như họ component mang tên "chuẩn" nhưng chọi chuẩn). Đã cho uỷ quyền sang hàm an toàn.
- **Số dòng mặc định 25** cho trang danh mục còn sót và cho màn công cụ tính giá (4 bảng).
- **Dọn nốt đầu bảng** ở ba trang: gỡ thuộc tính ghim thừa, đưa chiều cao ô tiêu đề về chuẩn, đổi chữ tiêu đề cột từ tối sang trắng cho dễ đọc trên dải cam.

Toàn bộ có **bộ tiêu chí nghiệm thu chốt ra file TRƯỚC khi sửa dòng mã đầu tiên** — nghĩa vụ này trước đây bị bỏ qua. Trình biên dịch kiểm lại: **0 lỗi**.

---

## 5. Một quyết định CỐ Ý KHÔNG LÀM

Có đề xuất sửa **component bảng dùng chung**. Chủ dự án đã duyệt, nhưng đo kỹ thì trong **21 tệp** dùng nó chỉ **2** là trang danh mục; **19 tệp còn lại là hộp thoại, bảng con, luồng nhiều bước, cửa sổ bật lên** — nơi chuẩn đầu bảng **không áp**. Sửa mặc định của component sẽ **đổi giao diện 19 bề mặt cùng lúc**, đúng loại thay đổi mà quy trình bắt phải **dựng bản xem thử cho chủ dự án duyệt trước**. Cộng thêm: lượt này **không xác minh được bằng mắt** (mục 6) nên sửa component dùng chung là làm mù.

⇒ **Không đụng vào.** Việc đúng là dựng đầu bảng theo chuẩn **tại chính hai trang đó** khi có dịp đụng vào chúng vì lý do chức năng.

---

## 6. Điều CHƯA chứng minh được — và một đính chính về chính tôi

**Vẫn không có ảnh nghiệm thu ở lớp người dùng nhìn thấy.** Nguyên nhân: khoá đăng nhập không dùng được trên cơ sở dữ liệu phát triển.

**Đính chính quan trọng:** ở phiên trước tôi kết luận *"sổ bí mật thiếu giá trị"*. **Kết luận đó SAI.** Đo lại kỹ hơn cho thấy:

- lỗi nằm ở **chính bộ trích của tôi** — nó cắt nhầm một ký tự dẫn đầu trong ô giá trị, nên **chưa từng thử đúng chuỗi**;
- sửa lại rồi thử **giữ nguyên từng ký tự**, đủ biến thể, đối chiếu với **toàn bộ tài khoản** trong cơ sở dữ liệu ⇒ vẫn không khớp;
- cơ chế xác thực **không có lớp muối bổ sung**, cơ sở dữ liệu **đúng cái đang dùng**, và **không phải** bản phục hồi từ tệp sao lưu cũ;
- chỉ **một** tài khoản từng đổi mật khẩu, đúng ngày **26/08/2026**.

⇒ **Sổ không thiếu giá trị; cơ sở dữ liệu phát triển mới là bên lệch.** Chính cuốn sổ tự khai *"máy nội bộ trùng máy vận hành — đã đối chiếu 23/08"*; câu đó đúng ngày 23/08 nhưng **lần đổi 26/08 đã phá nó mà không ai cập nhật sổ**.

Việc đồng bộ lại đã được chủ dự án đồng ý, nhưng **công cụ phát triển chặn** mọi thao tác tác nhân ghi mật khẩu vào bảng tài khoản — đây là chốt an toàn của công cụ, **không phải quy định nội bộ**. Cần chủ dự án chạy giúp đúng một lệnh.

---

## 7. Nghĩa vụ quản trị bị bỏ quên — đã khép

- **Gói bàn giao** cho bên quản lý tài liệu: quy định bắt buộc phải có khi kết thúc đợt việc có quyết định mới; từ gói gần nhất tới nay đã dồn **22 mục** mà **không có gói nào**. Đã lập gói đầy đủ, ghi bù nhưng **giữ đúng mốc thật** của từng sự việc, kèm mục **"những điều chưa chứng minh được"** để bên nhận không hiểu nhầm thành sự thật hiện hành.
- **Sổ theo dõi phiên bản** đứng yên ở một mốc từ 23/08 trong khi mã đã đi thêm **14 đợt**. Đã cập nhật theo đúng **ba lớp bằng chứng**, và **không** khai mức "đã quan sát trên máy vận hành" vì lượt này không đo trực tiếp.
- **Sổ nợ:** đóng 4 nợ đã trả (có bằng chứng đo lại), mở rộng 2 nợ kèm toạ độ chính xác, thêm 2 nợ mới.
- **Sổ yêu cầu:** bổ sung trường đếm lượt cho hai lượt bị bác trước đây còn thiếu, và cập nhật bốn mục ghi sai trạng thái.

---

## 8. Trạng thái thật

| Việc | Trạng thái |
|---|---|
| Rà 7 hướng + phản biện | ✅ XONG |
| Khép các chỗ bản vá trước bỏ sót (luật · tiêu chí nghiệm thu · tài liệu chuẩn) | ✅ XONG |
| Vá bẫy còn sót trong dây chuyền phát hành (3 điểm) | ✅ XONG — **chưa chạy phát hành** |
| Thi hành tiêu chuẩn trên mã nguồn (11 chỗ lộ khoá · số dòng · đầu bảng) | ✅ XONG — trình biên dịch 0 lỗi |
| Gói bàn giao + các sổ | ✅ XONG |
| Component bảng dùng chung | ⏸️ **CỐ Ý KHÔNG LÀM** — lý do ở mục 5 |
| **Ảnh nghiệm thu ở lớp người dùng** | ❌ **CHẶN** — mục 6 |

**Cổng kiểm toàn bộ:** chạy hết, **không cổng nào đỏ**.

---

*Bản công khai đã lọc: không mã đăng nhập, không dữ liệu cá nhân, không số liệu kinh doanh, không dấu vết hạ tầng. Mã commit của kho mã nguồn nằm ở sổ nội bộ, không đưa ra kho công khai.*
