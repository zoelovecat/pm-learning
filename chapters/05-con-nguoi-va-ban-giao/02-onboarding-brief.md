---
title: Brief onboarding "đọc trước" cho thành viên join giữa dự án
source: Onboarding brief (Ch5·02)
stage: Cross-cutting
level: cơ bản
prerequisites: []
---
# Brief onboarding "đọc trước" cho thành viên join giữa dự án

## Mục tiêu học xong bạn làm được gì
- Soạn một tài liệu "read this first" giúp thành viên mới hiểu dự án, giai đoạn, việc được giao, rủi ro chính và liên hệ quan trọng ngay ngày đầu.
- Biết lấy thông tin từ nguồn thật (hệ thống PM, Jira, tài liệu scope/lịch, repo) khi dự án chạy giữa chừng và không có file charter/WBS.
- Chọn được chế độ đơn (1 người) hay gộp (nhiều người cùng nhóm vai trò) và cá nhân hóa theo vai trò (BE/FE/QA...).
- Tự kiểm tra brief bằng checklist trước khi chia sẻ.

## Khi nào dùng (thời điểm, ai kích hoạt, điều kiện đầu vào)
- Khi có thành viên mới join khi dự án đã chạy. PM kích hoạt và PM duyệt bản nháp trước khi chia sẻ.
- Đầu vào bắt buộc (là thông tin, không bắt buộc là file): (1) tóm tắt dự án + timeline; (2) phase hiện tại + milestone; (3) tên + vai trò thành viên mới.
- Nguồn ưu tiên 1 là file (charter, WBS); nguồn ưu tiên 2 là nguồn thật (hệ thống quản lý dự án, tài liệu scope/lịch, SRS, epic Jira). Thiếu hoàn toàn nguồn cho một thông tin bắt buộc -> dừng, nói rõ thiếu gì, không đoán.
- Không làm: tự giao task, gửi thông báo, tạo task mới. Brief là để ĐỌC (còn checklist việc để LÀM: xem bài Onboarding todo, Ch5·03).

## Khái niệm cốt lõi (định nghĩa, thuật ngữ, vì sao quan trọng)
- **Brief "read this first"**: tài liệu ngắn gọn cá nhân hóa, giúp người mới hiểu bối cảnh mà không phải hỏi từng người.
- **Chế độ đơn (single)**: 1 thành viên = 1 brief.
- **Chế độ gộp (combined)**: từ 2 người cùng "role-class" (ví dụ đều là dev, gồm BE/FE) trở lên onboard cùng đợt -> 1 brief: bối cảnh chung viết 1 lần + 1 mục riêng cho mỗi người + Day-1 theo vai trò. Nhóm khác hẳn nhau -> brief riêng cho từng người.
- **Nguồn thật**: dự án giữa chừng thường không có file PM; các mốc ngày lấy từ tài liệu scope/lịch làm chuẩn (chính xác hơn Jira nếu Jira chưa cập nhật).
- **Chú giải nguồn**: 📄 file dự án · 📋 quy ước/quy tắc · 💭 PM cung cấp · 🤖 tự sinh · ⏳ chờ bổ sung/TBD. Bắt buộc ở đầu file để người đọc biết thông tin đến từ đâu.
- **[NO_DATA]**: dấu cho phần không có dữ liệu; không bịa, không bỏ mục.
- Vì sao quan trọng: người mới đọc đúng bối cảnh giảm thời gian hỏi lại và sai sót ở tuần đầu.

## Cách làm từng bước (thủ công, đủ chi tiết để làm theo; kèm input/output)
1. **Xác định dự án và nguồn**: xác định mã dự án; ghi nguồn sẽ dùng (charter/WBS hoặc nguồn thật). Nếu chưa có trong danh mục dự án thì tra trực tiếp hệ thống PM/Jira.
2. **Thu thập thông tin cho từng thành viên**: tên đầy đủ (dùng làm tên file); vai trò + role-class (`dev` (BE/FE), `qa`, `ba`, `pm`, `devops`...); tài khoản Jira/email (email dạng `<handle>@<domain-công-ty>`); ngày bắt đầu (mặc định hôm nay, định dạng YYYY-MM-DD); module/task được giao (chưa giao -> ⏳ TBD).
3. **Chọn chế độ**: 1 người -> đơn; >=2 cùng role-class -> gộp; >=2 khác hẳn nhóm -> nhiều brief đơn (hoặc hỏi PM).
4. **Danh bạ liên hệ chính (bắt buộc)**: PM, Tech Lead, BA Lead, QA Lead, đầu mối khách hàng (nếu có): mỗi người cần tên đầy đủ + kênh liên lạc (Teams/email). Thiếu thì hỏi, không để TBD cho liên hệ quan trọng.
5. **Kiểm tra hợp lệ**: task ID phải tồn tại trong danh sách task (không thấy -> dừng và hỏi); task đã closed/done -> báo PM xem có cần giao việc khác; module phải khớp tên module trong WBS (không khớp -> hỏi PM, không tự sửa).
6. **Trích xuất bối cảnh** (thiếu -> [NO_DATA], không bịa):
   - Tóm tắt dự án: tên, mã, khách hàng, mục tiêu (tối đa 3 gạch đầu dòng), timeline (bắt đầu -> go-live/hạn), tech stack.
   - Phase hiện tại (kèm % nếu có), tối đa 3 milestone sắp tới kèm ngày cụ thể, module thành viên phụ trách + trạng thái.
   - Task giao: chỉ lọc task thuộc module/task ID của người đó; mỗi task gồm ID, tiêu đề, trạng thái, ưu tiên, hạn, phụ thuộc.
   - Top 3 rủi ro: xếp theo mức độ, Critical trước rồi High; mỗi rủi ro gồm ID, mô tả ngắn, severity, biện pháp đang thực hiện. Không có risk register -> [NO_DATA], vẫn giữ mục.
   - Liên hệ chính: sắp xếp PM -> Tech Lead -> BA -> QA -> Client.
   - Link quan trọng: Spec/BA docs, Jira board, repo code, kênh Teams, thiết kế (Figma...).
7. **Cá nhân hóa theo vai trò** (khung ví dụ dev web, điều chỉnh theo dự án thật):

| Role | Tài liệu nên đọc | Setup Day-1 |
|---|---|---|
| BE | architecture doc, ADR (vì sao chọn stack), DB schema, API integration spec | repo code BE, env/DB, migrate, chạy API |
| FE | UI/screen spec, screen-transition, security/RBAC, prototype (nếu có) | repo code FE, chạy dev server, kết nối API |

8. **Viết brief** theo khung bên dưới. Đặt file ở thư mục docs/PM của dự án (không nhất thiết là repo code; nếu repo tách rời thì nêu rõ repo nào ở đầu file và link repo code ở mục Links).
9. **Kiểm tra theo checklist sau khi sinh**, đặt trạng thái DRAFT, PM duyệt rồi chia sẻ trực tiếp (Zalo/Teams/email). Không tự commit git.

## Công thức, ngưỡng & tín hiệu
Không có công thức. Quy tắc lọc đáng nhớ:

| Tên | Điều kiện | Ngưỡng | Hành động |
|---|---|---|---|
| Số rủi ro hiển thị | Xếp theo severity | Top 3 (Critical trước, High sau) | Bỏ phần còn lại khỏi brief |
| Số milestone sắp tới | Kèm ngày cụ thể | Tối đa 3 | Lấy ngày từ tài liệu scope/lịch làm chuẩn |
| Mục tiêu dự án | Ngắn gọn | Tối đa 3 gạch đầu dòng (khung ví dụ: <=2 câu) | Rút gọn |
| Ngày standup đầu tiên | Không chỉ định | Ngày bắt đầu + 1 ngày làm việc | Dùng mặc định |
| Mọi mục | Thiếu dữ liệu | - | Ghi [NO_DATA], không bỏ mục |

## Template / mẫu đầu ra (rút gọn, giữ cấu trúc và các cột/trường)
Tên file: đơn `<role>-<tên-kebab>-<YYYY-MM-DD>.md`; gộp `onboarding-<mã-dự-án>-<roleclass>-<YYYY-MM-DD>.md`.

Đầu file: chú giải nguồn; bảng Field/Value: Project | Member | Role | Start date | Prepared by | Status (🟡 DRAFT).

Các mục:
1. Project Overview: Client | Objective | Timeline | Tech stack.
2. Current Phase & Milestones: phase hiện tại; bảng `Milestone | Date | Status`; module phụ trách.
3. Your Assigned Tasks: `ID | Title | Status | Priority | Due | Depends on`.
4. Top 3 Risks: `ID | Risk | Severity | Mitigation`.
5. Key Contacts: `Role | Tên | Liên lạc`.
6. Important Links: `Loại | Link` (Jira board, repo, BA specs, kênh Teams, thiết kế).
7. Day 1 Checklist (cụ thể, không chung chung): đọc brief; setup môi trường theo tài liệu (hoặc hỏi Tech Lead); join kênh Teams; tạo tài khoản Jira và nhận task; clone repo và chạy thử local; 1-on-1 ngắn với PM (15 phút); tham gia standup đầu tiên (lắng nghe nếu chưa sẵn sàng cập nhật); đọc BA spec module được giao.

Khung chế độ gộp: A. Project context (chung: overview, phase và milestone kèm ngày, liên hệ chính, link, top risks) -> B, C... mỗi người một mục (task/⏳TBD, module, tài liệu theo vai trò) -> D. Day-1 checklist theo vai trò (chung: đọc brief, join Teams, tài khoản Jira, 1-1 PM, standup; riêng từng vai trò: setup và tài liệu riêng).

## Lỗi thường gặp & lesson learned (lấy từ nguồn, mỗi ý: sai gì -> hậu quả -> cách tránh)
- Bắt buộc phải có file charter/WBS mới làm được -> dự án giữa chừng thường không có file -> bị kẹt (bài học từ thử nghiệm thật đầu tiên) -> lấy thông tin từ nguồn thật.
- Lấy mốc ngày từ Jira chưa cập nhật -> người mới hiểu sai deadline -> ưu tiên ngày từ tài liệu scope/lịch.
- Hiển thị toàn bộ danh sách task -> người mới bị ngợp -> chỉ task của người đó.
- Để trống tên hoặc kênh liên hệ -> người mới không biết hỏi ai -> hỏi lại PM cho đủ.
- Checklist Day-1 chung chung -> không làm theo được -> ghi lệnh/tài liệu cụ thể theo vai trò.
- Tự đoán nội dung thiếu -> thông tin sai -> ghi [NO_DATA] hoặc ⏳ TBD.
- Lặp bối cảnh chung cho từng người trong chế độ gộp -> dài dòng, dễ lệch -> viết 1 lần.
- Chưa có cơ chế hết hạn/phiên bản (nguồn chưa rõ): gắn ngày + phase ở metadata và tạo bản mới khi sang phase mới.

## Ví dụ minh họa (1 ví dụ ngắn có số, lấy hoặc dựng từ nguồn; nếu dựng thì ghi "(ví dụ dựng)")
(Từ mẫu trong nguồn, ẩn danh) Brief cho <Member A> (Developer) dự án <mã-dự-án>, timeline 2026-05-01 -> 2026-09-30, phase 2 Backend Development. Milestone: API hoàn thành 2026-07-01 (đang làm), UAT 2026-08-15, Go-live 2026-09-30. Task T-045 (tích hợp cổng thanh toán, High, hạn 2026-06-20, phụ thuộc T-040). Top rủi ro: R-003 (Critical) Payment API đổi spec -> khóa version, xác nhận với khách 2026-06-15; R-007 (High) thiếu test data; R-012 (High) hạn UAT sát. Day-1: đọc brief, setup dev, join kênh, clone repo, 1-1 15 phút với PM, standup 9:30.

## Tự kiểm tra (3-5 câu hỏi có đáp án ngắn ngay dưới, dựa trên chính nội dung bài)
1. Khi nào dùng chế độ gộp? -> Từ 2 người cùng role-class onboard cùng đợt; bối cảnh chung viết 1 lần.
2. Không có charter/WBS thì sao? -> Lấy từ nguồn thật (hệ thống PM, tài liệu scope/lịch, Jira); chỉ dừng khi không nguồn nào cấp được.
3. Số rủi ro hiển thị và cách xếp? -> Top 3, Critical trước rồi High.
4. Thiếu dữ liệu ở một mục thì làm gì? -> Ghi [NO_DATA]/⏳ TBD, giữ mục, không bịa.
5. Trạng thái của brief khi vừa soạn? -> DRAFT, PM duyệt rồi chia sẻ trực tiếp.

## Liên quan (bài trước/sau trong quy trình, tên thư mục skill khác)
- Trước: kickoff, wbs, Spec thành task (Ch3·02), Xếp người (Ch3·05) (cung cấp charter, phase/module, task, phân vai).
- Song hành: Onboarding todo (Ch5·03) (việc để làm); Bàn giao thành viên (Ch5·01) (thành viên rời); Tiếp quản PM (Ch5·04) (PM tiếp quản).
- Sau: Daily sync (Ch4·01) (thành viên mới dự standup đầu tiên).
