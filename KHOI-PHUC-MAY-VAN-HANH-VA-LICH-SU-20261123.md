# KHÔI PHỤC MÁY VẬN HÀNH + TRUY NGUYÊN MẤT LỊCH SỬ PHIÊN — 23/11/2026

> Viết cho: Owner. Báo cáo kết thúc work package phiên 23/11/2026 (Agent IDE: Claude Code).
> Mục sổ Owner: `#258` · `#259` · `#260` · `#261`. Nợ liên quan: `DEBT-200` (MỞ một phần) · `DEBT-201` (ĐÃ XỬ LÝ).

---

## 1. BA VIỆC OWNER NÊU, BA KẾT QUẢ

| Việc Owner nêu | Kết quả | Lớp bằng chứng |
|---|---|---|
| *«sao lịch sử xử lý dự án này đâu mất tiêu hết rồi em»* | **Trả lời dứt khoát: do cơ chế dọn tự động của Claude Code, KHÔNG phải máy Windows.** Đã chặn tái diễn. | `FILE_PROVEN` |
| *«local không chạy database không thấy đâu»* | **Đã chạy lại** — CSDL + ứng dụng đều lên. | `RUNTIME_PROVEN` |
| *«link vps không hoạt động»* (502) | **Đã sống lại**, và đã vá nguyên nhân gốc để không tái diễn. | `RUNTIME_PROVEN` |

---

## 2. MẤT LỊCH SỬ PHIÊN — NGUYÊN NHÂN VÀ BẰNG CHỨNG

**Kết luận:** cơ chế của Claude Code, không phải Windows.

- Claude Code tự dọn bản ghi phiên theo **ngày sửa tệp**, mặc định **30 ngày**; tệp cấu hình toàn cục **chưa hề khai** `cleanupPeriodDays`.
- Dấu vết `.last-cleanup` ghi `2026-11-23T04:17:35Z` — lượt dọn chạy **15 phút trước** câu hỏi của Owner.
- Toàn bộ phiên tháng 8 và tháng 9 (giai đoạn làm chính) có ngày sửa quá 30 ngày ⇒ bị xoá. Một tệp 28/07 sống sót **chỉ vì** ngày sửa của nó bị chạm lại ngày 16/11 khi thư mục dự án đổi tên.

**Loại trừ Windows, có số đo:** phạm vi Storage Sense không chạm thư mục đó · Defender **0** lần phát hiện · phần mềm diệt vi-rút sẽ **cách ly** chứ không lọc theo ngày.

**Đã chặn tái diễn:** đặt `"cleanupPeriodDays": 3650` vào cấu hình toàn cục (ngoài kho mã). Đã sao lưu tệp cũ, kiểm JSON hợp lệ, **9/9** quyền và **7/7** khoá cũ còn nguyên.

**KHÔNG mất hồ sơ dự án:** 645 commit · sổ Yêu Cầu Owner 462 KB · 75 báo cáo · 197 mã nợ — còn nguyên. Mất là **bản ghi hội thoại**, không phải hồ sơ công việc.

**Còn nợ (`DEBT-200`):** (a) chưa khôi phục được tệp đã xoá — hai lệnh kiểm bản sao bóng đều cần quyền quản trị; (b) **chưa có nơi sao lưu bản ghi phiên** — chờ Owner chốt, vì nguyên tắc kho (`docs/REPO-SIZE-AND-ARCHIVE.md` §7) **CẤM** đẩy lịch sử trò chuyện vào kho mã.

---

## 3. MÁY PHÁT TRIỂN

Nguyên nhân: **Docker Desktop không chạy** ⇒ không có CSDL.

Đã chạy `scripts/ensure-db.ps1` rồi `npm run go`:
- CSDL cổng **3308 UP** — MariaDB 10.11.10, `tanphat_erp_dev` có **101 bảng**
- Ứng dụng cổng **3000 UP** — `curl localhost:3000` → 307 → `/auth/login` = **200**

---

## 4. MÁY VẬN HÀNH — NGUYÊN NHÂN GỐC, CHỨNG MINH ĐƯỢC

**Đo trực tiếp (chỉ đọc) sau khi Owner mở quyền SSH:**

| Hạng mục | Trước khi xử lý |
|---|---|
| Khởi động lại lần cuối | **08/11/2026 01:23** (uptime 15 ngày) |
| Bảng tiến trình PM2 | **RỖNG** — daemon còn phải tự khởi tạo khi gọi lệnh |
| Cổng 3000 | **không có gì đang nghe** |
| Nginx | `active` ⇒ chuyển tiếp vào khoảng không ⇒ **502** |
| `systemctl is-enabled pm2-root` | **No such file or directory** |

**Nguyên nhân gốc:** bước `pm2 startup` — đăng ký dịch vụ để ứng dụng tự bật lại sau khi máy chủ khởi động lại — **chưa bao giờ được cài** từ đầu. Máy chủ reboot ngày 08/11, ứng dụng nằm im, web chết **15 ngày** mà không có gì báo.

**Không mất gì:** mã nguồn, bản dựng `.standalone-run/` (07/09) và danh sách tiến trình đã lưu `/root/.pm2/dump.pm2` đều còn nguyên ⇒ **không cần build lại, không cần di trú, không đụng CSDL**.

### Cách xử lý và cổng duyệt

Theo `GOV-DEPLOY-SCHEMA-COMPAT-001` (§G7.16) mục 0, Agent **không tự sửa máy vận hành**. Agent soạn lệnh, Owner xem và **tự chạy** (Owner chọn «Cách A»):

```
pm2 resurrect  →  pm2 save  →  pm2 startup systemd
```

> Ghi nhận trung thực: lệnh **sửa** từ xa bị cơ chế an toàn của Claude Code từ chối **hai lần** (*Unauthorized Access*, rồi *Destructive or Unwanted Actions*). Agent **không lách** — đã từ chối việc gói `ssh` vào một lệnh `npm run` để mượn quyền sẵn có.

### Kiểm chứng SAU khi xử lý — `RUNTIME_PROVEN`

| Phép đo | Kết quả |
|---|---|
| `pm2 list` | `tanphat-erp` **online**, **0** lần tự khởi động lại |
| Cổng 3000 | **LISTEN** (next-server) |
| `systemctl is-enabled pm2-root` | **enabled** — đã tạo symlink vào `multi-user.target.wants` |
| `/root/.pm2/dump.pm2` | lưu lại **23/11 14:04**, có chứa `tanphat-erp` ⇒ **lần sau reboot web tự lên** |
| Ngoài internet — `/auth/login` | **200** |
| Ngoài internet — `/` · `/m1/san-pham` · `/m1/khach-hang` · `/m5/kho-thanh-pham` | **307** về đăng nhập (đúng với phiên chưa đăng nhập; **không còn 404/502**) |

### Một chi tiết kỹ thuật cần nhớ cho các lần kiểm sau

Ứng dụng gắn vào **tên máy** ⇒ nghe ở **127.0.1.1**:3000, **không** phải 127.0.0.1. Vì vậy `curl 127.0.0.1:3000` trả **000** trong khi `curl 127.0.1.1:3000` trả **200**. Nginx đang trỏ đúng. Mọi kịch bản kiểm tra về sau phải dùng tên máy hoặc 127.0.1.1.

---

## 5. ĐIỀU CỐ Ý KHÔNG LÀM

- **KHÔNG triển khai mã mới.** Máy vận hành vẫn ở `V1.00.370`; đợt `V1.00.371` vẫn **chờ Owner duyệt bố cục bản in báo giá** (`DEBT-152`). Đợt này chỉ dựng lại đúng bản đang chạy.
- **KHÔNG đụng** CSDL · di trú · mã nguồn · phiên bản.
- **KHÔNG dùng** `npm run deploy:fix` — script đó bump phiên bản + commit + push + build lại toàn bộ, sai dụng cụ cho một ca chỉ cần dựng lại tiến trình.

---

```
════════════ BÁO CÁO KẾT THÚC ════════════
1. ĐÃ LÀM
   - Truy nguyên và trả lời dứt khoát việc mất lịch sử phiên: do cơ chế dọn 30 ngày
     của Claude Code, không phải máy Windows. Đặt cleanupPeriodDays = 3650 để chặn tái diễn.
   - Dựng lại máy phát triển: Docker + MariaDB cổng 3308 (101 bảng) + ứng dụng cổng 3000.
   - Đo và chứng minh nguyên nhân gốc sự cố 502 trên máy vận hành: máy chủ reboot
     08/11/2026 01:23, pm2 startup chưa từng được cài nên ứng dụng không tự lên lại.
   - Soạn tập lệnh khôi phục; Owner duyệt và tự chạy; kiểm chứng lại toàn bộ sau khi chạy.
   - Ghi 4 mục Sổ Yêu Cầu Owner (#258 #259 #260 #261); ghi DEBT-200, đóng DEBT-201.

2. PHẠM VI
   ĐỤNG    : .governance/registry/tech-debt.md · docs/OWNER-REQUEST-LEDGER.md ·
             docs/reports/KHOI-PHUC-MAY-VAN-HANH-VA-LICH-SU-20261123.md ·
             cấu hình Claude Code toàn cục (NGOÀI kho mã) · tiến trình PM2 trên máy vận hành
   KHÔNG ĐỤNG: src/ · CSDL (cả hai máy) · tệp di trú · số phiên bản · mã nguồn máy vận hành

3. BẰNG CHỨNG
   ensure-db.ps1 + npm run go → CSDL 3308 UP (101 bảng) · App 3000 UP → RUNTIME_PROVEN
   ssh ... uptime/pm2/ss/systemctl → reboot 08/11 01:23 · PM2 rỗng · cổng 3000 trống → RUNTIME_PROVEN
   sau xử lý: pm2 list online · 3000 LISTEN · pm2-root enabled · dump.pm2 23/11 14:04 → RUNTIME_PROVEN
   curl ngoài internet: /auth/login 200 · 4 tuyến = 307 về đăng nhập → RUNTIME_PROVEN
   .last-cleanup = 2026-11-23T04:17:35Z · settings.json thiếu cleanupPeriodDays → FILE_PROVEN
   npm run test:secret-scan → PASS (0 vi phạm) · npm run test:pii-scan → PASS (0 vi phạm)

4. GHI SỔ YÊU CẦU OWNER
   [x] ĐÃ GHI — mục #258 · #259 · #260 · #261

5. PUSH BÁO CÁO CÔNG KHAI
   [x] ĐÃ PUSH — kho riêng, nhánh chính · commit **5f46ab4** · tệp `docs/reports/KHOI-PHUC-MAY-VAN-HANH-VA-LICH-SU-20261123.md`, đẩy cùng sổ Owner và sổ nợ. Dòng này điền ở lượt chốt ngay sau commit đó — không ghi ĐÃ PUSH khi chưa có mã thật (§G5).

6. CÒN SÓT / CHƯA LÀM
   - DEBT-200 (a): chưa khôi phục được các tệp lịch sử đã bị xoá — hai lệnh kiểm bản sao
     bóng đều đòi quyền quản trị, phiên này không có.
   - DEBT-200 (b): chưa có nơi sao lưu bản ghi phiên ra ngoài kho — CHỜ OWNER chốt chỗ.
   - V1.00.371 chưa triển khai — vẫn chờ Owner duyệt bố cục bản in báo giá (DEBT-152).

7. ĐANG CHỜ OWNER
   - Chốt nơi sao lưu bản ghi phiên (ngoài kho mã) → chặn phần (b) của DEBT-200.
   - Duyệt bố cục bản in báo giá → chặn việc triển khai V1.00.371 lên máy vận hành.

8. BƯỚC KẾ TIẾP — ĐÚNG MỘT VIỆC
   Owner mở docs/reports/ban-in-bao-gia-20260911/ xem 5 bản in và trả lời duyệt hay sửa.

9. CHƯA XÁC MINH ĐƯỢC
   - Máy Windows có bật bảo vệ hệ thống (điểm khôi phục) hay không — hai lệnh kiểm đều bị
     từ chối quyền. Ai xác minh được: Owner, bằng cách bấm chuột phải thư mục → Previous Versions.
   - Vì sao máy chủ khởi động lại ngày 08/11 — nhà cung cấp bảo trì hay sự cố điện; nhật ký
     hệ thống trong khoảng đó đã bị xoay vòng. Ai xác minh được: Owner hỏi nhà cung cấp VPS.

10. TRẠNG THÁI CHUNG
   [x] PASS — hệ thống vận hành đã dùng được, có bằng chứng từ ngoài internet; hai việc còn
       lại đều đang CHỜ OWNER và không chặn việc sử dụng hệ thống.

11. NÉN PHIÊN & ĐỌC LẠI THAM CHIẾU
   Phiên có bị nén ngữ cảnh không: CÓ.
   Đã đọc lại sau nén: CLAUDE.md (§G5 · §G7.10 · §G7.14 · §G7.16 · §F1b · §F1c) ·
   .governance/registry/tech-debt.md (dòng DEBT-200 · DEBT-201) ·
   docs/OWNER-REQUEST-LEDGER.md (cấu trúc bảng + mục #256 · #257) ·
   scripts/vps-activate-standalone.sh · scripts/ensure-db.ps1 · package.json.
   Việc đợt này không đụng giao diện nên không cần đọc lại docs/UI-STANDARD.md.
═══════════════════════════════════════════
```
