---
title: Duy trì baseline phạm vi tích lũy (hợp đồng gốc + CR đã duyệt)
source: Scope baseline (Ch6·04)
stage: Cross-cutting
level: cơ bản
prerequisites: [Ch2·01, Ch4·03]
---
# Duy trì baseline phạm vi tích lũy (hợp đồng gốc + CR đã duyệt)

## Mục tiêu học xong bạn làm được gì
- Trả lời câu hỏi "phạm vi hôm nay là gì so với lúc ký hợp đồng?".
- Lập baseline hiện tại = danh sách tính năng gốc + mọi CR đã duyệt (thêm, bỏ, sửa).
- Tính % tăng trưởng phạm vi và chênh lệch effort; đặt số phiên bản baseline đúng quy tắc.
- Xử lý xung đột giữa các CR và các trường hợp thiếu dữ liệu.

## Khi nào dùng (thời điểm, ai kích hoạt, điều kiện đầu vào)
- PM chạy lại mỗi khi có một CR mới được duyệt, hoặc khi cần so sánh phạm vi hiện tại với hợp đồng gốc ("scope growth", "CR đã duyệt ảnh hưởng gì").
- Đầu vào bắt buộc: danh sách tính năng gốc (trong phần Scope/Features của charter; hoặc trong SRS/WBS nếu charter dẫn tới), tên + mã dự án.
- Đầu vào tùy chọn: thư mục CR (không có thư mục = không có CR, baseline = hợp đồng gốc); ước lượng effort từng tính năng.
- Thiếu charter: dừng, quay lại bước khởi động (kickoff); không đoán phạm vi.
- Mỗi lần chỉ xử lý một dự án. Người chạy không được duyệt CR, không sửa charter/SRS gốc, không gửi thông báo cho bên liên quan.

## Khái niệm cốt lõi (định nghĩa, thuật ngữ, vì sao quan trọng)
| Thuật ngữ | Định nghĩa |
|---|---|
| Contract baseline | Danh sách tính năng trong charter lúc ký hợp đồng; không thay đổi |
| Current baseline | Contract baseline + mọi CR đã duyệt tính đến ngày as-of |
| Delta | Thay đổi phạm vi của từng CR: Added (+), Removed (−), Modified (~) |
| Scope growth % | (features_added − features_removed) / total_original × 100 |
| Effort delta | Tổng thay đổi effort của mọi CR đã duyệt (md) |
- Vì sao quan trọng: nếu không giữ baseline tích lũy thì không chứng minh được phạm vi đã tăng bao nhiêu và vì sao, nên tranh cãi với khách hàng, sai ước lượng và báo cáo.
- Chỉ CR ở trạng thái duyệt (approved) mới tính; bỏ qua draft, pending, rejected, deferred.
- Thiếu số thì ghi `[NO_DATA]`, không bịa.

## Cách làm từng bước (thủ công, đủ chi tiết để làm theo; kèm input/output)
1. Quét thư mục CR. Chỉ lấy CR có trạng thái approved (trong frontmatter hoặc phần đầu). Ghi lại số CR tìm thấy / đã duyệt / bỏ qua và lý do bỏ qua.
2. Chốt: ngày as-of (mặc định hôm nay, UTC+7), tên/mã dự án, nguồn danh sách tính năng gốc (xác nhận nếu có nhiều nguồn), đơn vị effort (md; nếu charter dùng giờ thì h), số phiên bản baseline.
3. Số phiên bản: `v<major>.<số CR đã duyệt>`, bắt đầu từ v1; ví dụ 3 CR đã duyệt -> `v1.3`. PM có thể đặt nhãn khác.
4. Lập danh sách gốc từ charter. Mỗi tính năng cần: feature_id (bắt buộc; thiếu thì gán tự động F-XXX tuần tự và ghi `[auto-id]`), module (bắt buộc), tên tính năng (bắt buộc), ước lượng effort (md, hoặc `[NO_DATA]` nếu tài liệu không có; không bịa), trạng thái mặc định là Original.
5. Với mỗi CR đã duyệt, đọc: cr_id, tiêu đề, ngày duyệt, người duyệt, các tính năng thay đổi (phần Scope Impact / Features / Changes), effort_delta (phần Cost Impact / Effort, đơn vị md hoặc h). Phân loại từng mục:
   - `Added` / `New feature` / `+` -> loại +.
   - `Removed` / `Out of scope` / `-` -> loại −.
   - `Modified` / `Changed` / `Updated` / `~` -> loại ~.
   - Thiếu phần nào thì `[NO_DATA]` cho trường đó.
6. Xử lý xung đột: CR sau sửa tính năng mà CR trước đã bỏ -> dừng và hỏi PM. Cùng một tính năng được thêm ở 2 CR -> gộp, ghi các CR ID.
7. Tính tổng hợp (mục công thức) rồi lập ba bảng: phạm vi gốc, bảng delta của CR, phạm vi hiện tại (tính năng bị bỏ gạch ngang; cột Origin ghi Original / CR-xxx / Original + CR-xxx).
8. Đánh dấu DRAFT, chờ PM duyệt mới dùng làm tài liệu chính thức. Chạy lại mỗi khi có CR mới duyệt, tăng phiên bản.

## Công thức, ngưỡng & tín hiệu
| Tên | Công thức | Ngưỡng | Hành động khi vượt |
|---|---|---|---|
| current_scope_features | total_original_features + features_added − features_removed | — | — |
| scope_growth_% | (features_added − features_removed) / total_original_features × 100 | không có ngưỡng trong nguồn | — |
| effort_original | SUM(effort_estimate của phạm vi gốc), bỏ qua `[NO_DATA]` | — | ghi số bị bỏ qua |
| effort_delta | SUM(effort_delta của mọi CR đã duyệt), bỏ qua `[NO_DATA]` | — | ghi số bị bỏ qua |
| effort_current | effort_original + effort_delta | — | — |
| effort_delta_% | effort_delta / effort_original × 100 | — | — |
| Baseline version | v<major>.<cr-count> | — | — |
Nếu bất kỳ đầu vào nào là `[NO_DATA]` thì metric đó ghi `[NO_DATA]`. Feature Modified được đếm riêng (features_modified) nhưng không vào công thức scope growth.
(nguồn chưa rõ: nguồn không nêu ngưỡng cảnh báo cho scope growth; ngưỡng scope creep 10%/20% ở báo cáo tuần là khái niệm khác — xem Status tuần (Ch7·01).)

## Template / mẫu đầu ra (rút gọn, giữ cấu trúc và các cột/trường)
"Scope Baseline — <tên dự án> (<mã>)": chú giải nguồn (📄 từ charter/spec, 📋 giả định/mặc định, 💭 PM nhập, 🤖 tự tính).
- Metadata: Project | As-of | Baseline version | PM | Status = DRAFT | Original feature count | CRs applied.
- Summary Stats: Original features | Features added | Features removed | Features modified | Current scope features | Scope growth | Effort original | Effort delta | Effort current.
- Original Contract Scope: ID | Module | Feature | Effort | Status.
- CR Delta Table: CR ID | Type (+/−/~) | Feature ID | Module | Feature | Effort Delta | Approved Date.
- Current Scope: ID | Module | Feature | Effort | Origin (tính năng bị bỏ gạch ngang, ghi "Removed CR-xxx").
Kiểm tra sau: mọi trường bắt buộc có nguồn; thiếu = `[NO_DATA]`; CR bị bỏ qua có liệt kê + lý do; scope growth đúng công thức; tính năng bị bỏ gạch ngang; nhãn phiên bản khớp số CR áp dụng; trạng thái DRAFT.

## Lỗi thường gặp & lesson learned
- Đưa CR chưa duyệt vào baseline -> phạm vi phình lên sai -> chỉ tính status approved.
- Tự sửa charter khi có CR -> mất mốc hợp đồng gốc -> giữ charter, baseline là lớp cộng dồn bên ngoài.
- Bịa ước lượng effort khi tài liệu không có -> tổng sai -> `[NO_DATA]` và ghi số bị bỏ qua.
- Bỏ qua xung đột giữa CR (CR sau sửa cái CR trước đã bỏ) -> baseline vô nghĩa -> dừng hỏi PM.
- Đếm hai lần một tính năng được thêm ở nhiều CR -> gộp và ghi các CR ID.
- Quên chạy lại sau khi có CR mới duyệt -> baseline lỗi thời -> chạy lại mỗi khi có CR mới.

## Ví dụ minh họa
Ví dụ trong nguồn: 20 tính năng gốc, 3 Added, 1 Removed -> scope growth = (3 − 1) / 20 × 100 = 10%; tính năng hiện tại = 20 + 3 − 1 = 22.
Bảng delta mẫu:
| CR | Loại | Tính năng | Effort |
|---|---|---|---|
| CR-001 | + | F-021 Refund flow (Payment) | +4 md |
| CR-002 | ~ | F-003 Add MFA (Authentication) | +2 md |
| CR-003 | − | F-007 Remove PDF export (Reporting) | −3 md |
Effort gốc 85 md, delta +9 md -> hiện tại 94 md (delta ≈ 10.6%: 9 / 85, giải thích thêm; nguồn không ghi số này). Phiên bản v1.3.
(nguồn chưa rõ: tổng delta của 3 dòng mẫu cộng lại là +3 md, còn Summary mẫu ghi +9 md và "Features modified = 2"; có thể còn CR/tính năng bị lược trong bảng rút gọn.)

## Tự kiểm tra
1. CR ở trạng thái pending có vào baseline không? Đáp: không, chỉ approved.
2. Tính scope growth: 40 tính năng gốc, 6 Added, 2 Removed. Đáp: (6 − 2) / 40 × 100 = 10%.
3. Sau 5 CR đã duyệt, nhãn phiên bản mặc định? Đáp: v1.5.
4. Hai CR cùng thêm một tính năng thì làm gì? Đáp: gộp, ghi chú các CR ID.
5. CR không ghi effort thì xử lý ra sao? Đáp: ghi `[NO_DATA]`, bỏ qua khi cộng tổng và ghi chú số bị bỏ qua.

## Liên quan
- Trước: kickoff (charter với danh sách tính năng gốc), Change request (Ch4·03) (CR đã duyệt).
- Sau: Status tuần (Ch7·01) (mục phạm vi), Giao tiếp stakeholder (Ch7·03) (thông báo delta phạm vi cho nhà tài trợ), Ước tính chào giá (Ch1·01) (dùng làm đầu vào ước lượng dự án tương tự).
- Liên quan: Status tuần (Ch7·01) (kiểm tra scope creep hằng tuần).
