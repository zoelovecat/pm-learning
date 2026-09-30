---
title: Checklist việc cần làm khi onboarding thành viên mới theo vai trò
source: Onboarding todo (Ch5·03)
stage: Cross-cutting
level: cơ bản
prerequisites: [Ch5·02]
---
# Checklist việc cần làm khi onboarding thành viên mới theo vai trò

## Mục tiêu học xong bạn làm được gì
- Lập danh sách "việc để LÀM" cho thành viên mới join giữa dự án, cá nhân hóa theo vai trò BE/FE/QA/BrSE/PM.
- Mô tả mỗi việc đủ 12 trường (cho ai, ở đâu, ưu tiên, hạn, trạng thái...).
- Chia checklist thành 4 nhóm A/B/C/D và gán ưu tiên, hạn hợp lý.
- Xử lý onboarding nhiều người (mỗi người một file riêng) và chọn định dạng Markdown/Excel.

## Khi nào dùng (thời điểm, ai kích hoạt, điều kiện đầu vào)
- Khi thành viên mới vào dự án đang chạy, ngay sau khi có brief onboarding (brief = để ĐỌC bối cảnh; checklist = để LÀM).
- PM (hoặc TL) kích hoạt và duyệt bản nháp trước khi giao.
- Đầu vào bắt buộc: mã + tên dự án; tên + vai trò thành viên (1 hoặc nhiều người); định dạng xuất (`md`, `excel` hoặc `both`).
- Đầu vào tùy chọn: link tài liệu (overview/SRS/spec/onboarding doc), URL môi trường/server/DB/repo (DEV/STG), task đã giao, ngày hạn cụ thể, người hỗ trợ từng nhóm.
- Vai trò ngoài catalog (Infra, Designer, Comtor...): PM khai bộ việc nhóm B/C, khung A/D giữ nguyên, ghi chú "custom role".
- Không làm: tạo task Jira mới, gửi thông báo, viết brief tổng quan.

## Khái niệm cốt lõi (định nghĩa, thuật ngữ, vì sao quan trọng)
- **Checklist hành động**: khác brief, mỗi dòng là một việc kèm ai làm, làm ở đâu, gấp đến mức nào, hạn khi nào, đã xong chưa.
- **4 nhóm việc**: A. Chung (mọi vai trò), B và C (theo vai trò), D. Ngày đầu và hòa nhập (mọi vai trò).
- **Hạn tương đối**: D1 (ngày đầu), D2 (ngày thứ 2), W1 (tuần 1); có thể dùng ngày cụ thể. Dn = ngày thứ n, Wn = tuần n.
- **Ưu tiên**: Cao / TB / Thấp. Quyền truy cập, build môi trường, đọc SRS, setup env = Cao; tài liệu phụ, prototype = TB/Thấp.
- **Trạng thái**: New (mặc định) / Inprogress / Done.
- **BrSE gần giống PM**: cùng "format chung" thiên về tài liệu, giao tiếp, quy trình, không có setup môi trường code. PM = BrSE + quyền quản lý (kênh private/management, SharePoint quản lý, hệ thống KPI/EVM), các việc này đánh Cao.
- **Batch**: nhiều người -> mỗi người một cặp file riêng, tự đủ (đủ A->D). Nhóm A lặp ở từng file một cách có chủ ý để file độc lập; cùng vai trò thì cùng bộ việc, chỉ khác tên và người phụ trách.
- **Thiếu thông tin -> ⏳ TBD**, không bịa URL/DB, không chép mật khẩu/credential.

## Cách làm từng bước (thủ công, đủ chi tiết để làm theo; kèm input/output)
1. Xác định dự án, thành viên, vai trò, định dạng xuất, ngày bắt đầu (mặc định hôm nay, YYYY-MM-DD). Hỏi PM một lượt, không hỏi rời từng trường.
2. Kiểm tra: dự án xác định được; vai trò thuộc catalog hoặc PM đã khai bộ việc; định dạng thuộc {md, excel, both}; nếu dùng Excel thì môi trường có công cụ tạo Excel; link PM cung cấp đúng dạng URL (thiếu -> ⏳ TBD).
3. Dựng danh sách việc theo vai trò (không trộn vai trò khác), theo catalog:

| Role | Nhóm B | Nhóm C |
|---|---|---|
| BE | Setup môi trường: build local (docker/compose), tạo `.env`, cài dependency, migrate DB, kiểm tra API; đọc tài liệu thiết kế BE (kiến trúc/DB/integration); cài Devkit + ignore Devkit khỏi git | Quy trình và review code: CI local, tự review AI, tạo PR -> auto review -> cross/TL review -> khách hàng review |
| FE | Setup môi trường: build local, mở admin/marketplace, cấu hình API URL, đọc tài liệu màn hình/chuyển màn/RBAC, prototype UI | Quy trình và review code (như BE) |
| QA | Setup công cụ QA: tool inspector/quản lý test, clone repo Automation Test, nhận tài khoản test theo role, đọc tài liệu chức năng -> màn hình -> RBAC, nắm quy ước trace test case <-> FR/SCR ID | Môi trường test: quyền + kết nối DEV/STG (URL) và DB (host/port/db/user/tool), prototype |
| BrSE | Nắm bắt và truy cập: SharePoint dự án + spec gốc, kênh giao tiếp khách hàng, quy trình Q&A, cấu trúc tài liệu BD + trace ID, truy cập hệ thống PM chung (dự án + tài liệu) | Quy trình: review spec + sign-off, quản lý CR, lịch họp định kỳ với khách |
| PM | Như BrSE + kênh Teams private/management (nội bộ lead/PMO), SharePoint quản lý, hệ thống PM chung (KPI/EVM), Jira quản lý, registry/PROJECT-MAP, WBS/schedule/weekly, risk/issue | Quy trình: chu kỳ báo cáo tuần/daily/gate review, scope baseline + CR + delivery control |

   - Nhóm A (mọi vai trò): đọc tài liệu nền (overview/onboarding/SRS/dev-workflow), nhận quyền Jira + board + epic, (Dev) clone repo tổng / (QA) repo Automation Test, nắm mốc gần nhất.
   - Nhóm D (mọi vai trò): join Teams, 1-1 với PM, standup đầu tiên, gán task Jira được giao.
   - Mọi vai trò BE/FE/QA: thêm 1 việc nhóm C "Xem thông tin môi trường dự án trên hệ thống PM chung" (link <hệ thống PM nội bộ>). PM và BrSE: thêm việc nhóm B "Truy cập hệ thống PM chung" có link (PM: thêm KPI/EVM, targets; BrSE: dự án + tài liệu).
4. Điền thông tin môi trường (URL DEV/STG, server, DB host/port/db/user, repo) từ hệ thống PM chung của công ty: chi tiết dự án, tài nguyên vật lý (server/môi trường), danh mục dùng chung (environments/servers/repositories/drives). Với DB chỉ ghi cách xin quyền, không chép mật khẩu. Chưa lấy được -> ⏳ TBD.
5. Gán từng việc theo quy tắc: người phụ trách = @thành viên; người hỗ trợ = TL / PM / BA / QA Lead / Infra tùy loại việc; ưu tiên và hạn theo bảng bên dưới; trạng thái = New; ngày xong và ghi chú để trống hoặc ⏳ TBD.
6. Batch: lập bản xem trước (mỗi người: số việc / nhóm / vai trò) để PM xác nhận.
7. Xuất file, kiểm tra theo checklist rồi trạng thái DRAFT; PM điền các ⏳ TBD (link repo test, URL env, DB access) rồi giao trực tiếp cho thành viên (Excel để theo dõi tiến độ, MD để đọc/tick nhanh). Không tự gửi.

## Công thức, ngưỡng & tín hiệu
Không có công thức số. Quy tắc gán ưu tiên và hạn:

| Loại việc | Ưu tiên | Hạn |
|---|---|---|
| Quyền truy cập, build môi trường, đọc SRS, setup env | Cao | D1-D2 |
| Đọc nền (overview/onboarding) | Cao | D1-D2 |
| Quy trình / review code | (ví dụ trong nguồn: Cao) | W1 |
| Tài liệu phụ / prototype | TB hoặc Thấp | (không quy định) |
| Việc chưa chắc (ví dụ gán task Jira) | TB | W1 kèm ⏳ TBD |

## Template / mẫu đầu ra (rút gọn, giữ cấu trúc và các cột/trường)
**Schema mỗi việc: 12 trường**
| # | Trường | Ý nghĩa |
|---|---|---|
| 1 | id | Mã trong nhóm: A1, B2, C3... |
| 2 | group | A. Chung / B. ... / C. ... / D. Ngày đầu và hòa nhập |
| 3 | task | Nội dung việc, rõ ràng, có thể kèm lệnh |
| 4 | role | Chung / BE / FE / QA / PM / BrSE |
| 5 | assignee | Người phụ trách (thường @member) - việc cho ai |
| 6 | support | Người hỗ trợ/duyệt |
| 7 | location | Vị trí/nguồn: link tài liệu, repo, kênh, URL env, lệnh - ở đâu |
| 8 | location_url | (tùy chọn) URL để tạo hyperlink |
| 9 | priority | Cao / TB / Thấp |
| 10 | due | D1, D2, W1... hoặc ngày cụ thể |
| 11 | status | New / Inprogress / Done (mặc định New) |
| 12 | note | Ghi chú; ⏳ TBD nếu chờ bổ sung |
(Nguồn chưa rõ: bảng schema liệt kê 12 trường không có "ngày xong", nhưng dữ liệu mẫu và mô tả nhật ký thay đổi có thêm trường `done_date` (ngày xong); số cột Excel "12" có thể tính khác bảng này.)

**Bản Markdown**: tên file `onboarding-todo-<role>-<tên-kebab>-<YYYY-MM-DD>.{md,xlsx}`. Đầu file: chú giải nguồn; bảng Project | Member | Vai trò | Prepared by | Start date | Status (🟡 DRAFT); chú giải "Vai trò + Phụ trách = việc cho ai; Vị trí/Nguồn = làm ở đâu; 🔴 Cao 🟡 TB 🟢 Thấp; Dn = ngày thứ n, Wn = tuần n". Mỗi nhóm một bảng 8 cột: `✔ | # | Việc cần làm | Vai trò | Phụ trách | Vị trí / Nguồn | Ưu tiên | Hạn` (✔ là checkbox ☐).

**Bản Excel** (đặc tả): 12 cột; cố định 3 cột đầu + hàng tiêu đề; bộ lọc tự động; danh sách thả xuống cho Trạng thái (New, Inprogress, Done), Ưu tiên (Cao, TB, Thấp), Vai trò (Chung, BE, FE, QA, PM, BrSE, Infra); tô màu có điều kiện cho Trạng thái; tô màu nhóm; hyperlink ở cột Vị trí/Nguồn; in ngang vừa khổ giấy; thêm sheet phụ "Hướng dẫn". Mỗi file = 1 sheet vai trò + 1 sheet Hướng dẫn.

**Checklist sau khi sinh**: có chú giải 5 biểu tượng; bảng metadata đủ (Status DRAFT); đủ nhóm A + B/C + D; việc lọc đúng vai trò; mỗi việc có Vai trò + Phụ trách + Vị trí/Nguồn; thiếu link/URL/DB thì ⏳ TBD; ưu tiên hợp lý; tên file đúng quy ước; không commit, không tự gửi; Excel mở được và dropdown, màu, filter hoạt động.

## Lỗi thường gặp & lesson learned (lấy từ nguồn, mỗi ý: sai gì -> hậu quả -> cách tránh)
- Bịa URL/DB khi chưa có -> member vào sai môi trường -> ghi ⏳ TBD, để Infra bổ sung.
- Chép mật khẩu/credential vào checklist -> rò rỉ -> chỉ ghi cách xin quyền.
- Trộn việc của vai trò khác -> nhiễu, làm sai -> lọc theo vai trò đã chọn.
- Gộp nhiều người vào một file -> khó giao và theo dõi tiến độ riêng -> mỗi người một cặp file.
- Bỏ trống Vai trò/Phụ trách/Vị trí -> không biết ai làm, làm ở đâu -> ba cột này luôn phải có.
- Quên việc lấy quyền vào box private/management cho PM -> PM không điều phối được -> thêm và đánh Cao.
- Nhầm checklist với brief -> thiếu hành động hoặc thiếu bối cảnh -> dùng cả hai bổ trợ nhau.

## Ví dụ minh họa (1 ví dụ ngắn có số, lấy hoặc dựng từ nguồn; nếu dựng thì ghi "(ví dụ dựng)")
Mẫu từ nguồn (ẩn danh), vai trò BE, bắt đầu 2026-01-15:
- A1 Đọc project overview + onboarding doc (hỗ trợ PM, Cao, D1); A2 Đọc SRS/spec module được giao (hỗ trợ BA, Cao, D2); A3 Nhận quyền Jira + board + epic (PM, Cao, D1); A4 Clone repo tổng + sub-module (TL, Cao, D1); A5 Nắm mốc gần nhất (PM, TB, D2).
- B1 Build local (docker compose up) Cao D1; B2 Tạo `.env`, cài dependency, migrate DB, kiểm tra API Cao D1; B3 Đọc tài liệu thiết kế BE TB D2; B4 Cài Devkit + ignore khỏi git TB D2.
- C1 Chạy CI local trước PR đầu tiên Cao W1; C2 Tự review AI -> PR -> auto review -> cross/TL review -> merge Cao W1.
- D1 Join Teams + 1-1 PM + standup đầu Cao D1; D2 Gán task Jira cho mình TB, W1 kèm ⏳ TBD.

## Tự kiểm tra (3-5 câu hỏi có đáp án ngắn ngay dưới, dựa trên chính nội dung bài)
1. Hạn D1, D2, W1 nghĩa là gì? -> Ngày đầu, ngày thứ 2, tuần 1.
2. Nhóm nào lặp lại với mọi vai trò? -> A (Chung) và D (Ngày đầu và hòa nhập).
3. PM khác BrSE ở điểm nào? -> PM = BrSE cộng quyền vào box private/management (kênh lãnh đạo/PMO, SharePoint quản lý, KPI/EVM), đánh Cao.
4. Onboard 3 người cùng đợt thì xuất mấy file? -> Mỗi người một cặp file riêng (không gộp).
5. Chưa có URL môi trường thì làm gì? -> Ghi ⏳ TBD, không bịa.

## Liên quan (bài trước/sau trong quy trình, tên thư mục skill khác)
- Trước: Onboarding brief (Ch5·02) (bối cảnh để đọc); kickoff, wbs, Spec thành task (Ch3·02), Xếp người (Ch3·05).
- Sau: Daily sync (Ch4·01) (standup đầu tiên).
- Liên quan: Bàn giao thành viên (Ch5·01), Tiếp quản PM (Ch5·04).
