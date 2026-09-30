---
title: Chạy checklist Pass/Fail cho gate, phase, release
source: Checklist (Ch6·02)
stage: Cross-cutting
level: cơ bản
prerequisites: [Ch6·01]
---
# Chạy checklist Pass/Fail cho gate, phase, release

## Mục tiêu học xong bạn làm được gì
- Chạy một checklist thủ công cho một gate (G1–G6), một phase, một release hoặc một module, đánh Pass/Fail/N-A từng mục kèm bằng chứng.
- Phân loại mục (Standard / Critical / Auto / Optional) và biết mục nào bắt buộc phải có bằng chứng.
- Gộp nhiều template, loại trùng, và tính đề xuất BLOCK / REVIEW / READY.
- Lập biên bản chạy checklist để người review ký và chuyển cho người quyết gate.

## Khi nào dùng (thời điểm, ai kích hoạt, điều kiện đầu vào)
- PM kích hoạt trước một gate (G1 Charter, G2 SRS, G3 BD, G4 Code, G5 UAT, G6 Go-live), khi review một phase (review yêu cầu, review thiết kế), trước khi triển khai/rollback, hoặc theo yêu cầu riêng của khách hàng (ví dụ compliance).
- Đầu vào bắt buộc: loại phạm vi (gate/phase/release/module); mã phạm vi (ví dụ G4, R-KM-01, Phase-Design); template checklist (một hoặc nhiều); người review (vai trò + tên).
- Đầu vào tùy chọn: mã dự án, mã release, đường dẫn bằng chứng (PR, báo cáo test...), chế độ duyệt hàng loạt.
- Thiếu một trong các mục bắt buộc: dừng lại, nhờ PM cung cấp hoặc chọn template, không đoán.

## Khái niệm cốt lõi (định nghĩa, thuật ngữ, vì sao quan trọng)
- Checklist KHÔNG phải signal: checklist không đưa vào tính QS-XX; hai việc độc lập (xem Tín hiệu, Ch6·01). Quy trình gate cần cả hai để quyết định.
- Template là nguồn gốc nội dung; người chạy không tự soạn hay hard-code nội dung checklist.
- Người chạy checklist không tự chấm hộ người review và không tự ký. Đề xuất (BLOCK/REVIEW/READY) không phải quyết định gate cuối cùng — gate review quyết.
- Mỗi lần chạy giữ lại thành một file riêng (ví dụ `G4-2026-08-26`, `G4-2026-09-02`); không ghi đè ngầm, lịch sử chỉ thêm vào.
- Loại mục:
| Loại | Ý nghĩa | Tiêu chí đạt |
|---|---|---|
| Standard | Mục thông thường | Review thủ công + bằng chứng |
| Critical | Chặn: fail thì gate ABORT | Phải đạt tuyệt đối |
| Auto | Kiểm tra tự động từ dữ liệu | Truy vấn git/CI/PQA |
| Optional | Khuyến nghị | Pass/Fail/N-A đều được |

## Cách làm từng bước (thủ công, đủ chi tiết để làm theo; kèm input/output)
1. Xác định phạm vi và mã phạm vi. Mã hợp lệ: G1–G6, R-`<PROJ>-NN`, Phase-*, hoặc mã module.
2. Chọn template. Cấu trúc thư mục mẫu: `gate/` (G1-charter, G2-srs, G3-bd, G4-code, G5-uat, G6-golive), `phase/` (req-review, design-review), `release/` (pre-deploy, rollback-ready), `customer/` (ví dụ customer-A-compliance). Nguồn chuẩn là kho template của công ty; nếu chưa có thì dùng thư mục dự phòng cùng cấu trúc.
3. Kiểm tra: template đọc được và có danh sách mục; mã phạm vi khớp loại template (ví dụ G4 -> template gate G4-code); nếu template và phạm vi mâu thuẫn thì dừng hỏi, không tự sửa; tên file kết quả chưa tồn tại (chạy lại thì tạo file mới); có người review được chỉ định.
4. Xác nhận với PM danh sách template và số mục sau khi gộp.
5. Gộp template (nếu nhiều): lấy hợp của các mục; loại trùng theo mã mục (giữ mục đầu tiên hoặc mục có mức nghiêm trọng cao nhất); mục Critical từ bất kỳ template nào đều chặn cả lần chạy.
6. Chấm từng mục:
   - Mục Auto: điền sẵn từ dữ liệu (git, CI, PQA), ghi câu truy vấn nguồn trong bằng chứng, thiếu dữ liệu thì `[NO_DATA]`. Ví dụ: "PR có ≥ 1 reviewer approve" kiểm tra bằng truy vấn git/PR.
   - Mục còn lại: hỏi người review Pass / Fail / N-A kèm bằng chứng và ghi chú (có thể duyệt hàng loạt nếu tự tin).
   - Mục Critical: bắt buộc bằng chứng, không được bỏ qua.
7. Tổng hợp: Total, Pass, Fail, N/A, số Critical fail, Pass rate % (không tính N/A), đề xuất (bảng dưới).
8. Lập biên bản (mẫu bên dưới), đánh dấu "DRAFT — pending sign". Người review ký thủ công (Approve / Reject / Conditional).
9. Gợi ý bước tiếp: chạy gate review để kết hợp checklist + signal -> go / hold / abort. Không tự gọi thay người quyết, không commit.

## Công thức, ngưỡng & tín hiệu
| Tên | Công thức/điều kiện | Ngưỡng | Hành động khi vượt |
|---|---|---|---|
| Pass rate | Pass / (Total − N/A) × 100% | không có ngưỡng riêng | báo cáo |
| Đề xuất BLOCK 🔴 | Critical fail > 0 | > 0 | chặn; gate review quyết |
| Đề xuất REVIEW 🟡 | Standard fail > 20% | > 20% | gate review xem xét |
| Đề xuất READY 🟢 | Tất cả Pass | — | gate review quyết |
(nguồn chưa rõ: "Standard fail > 20%" tính trên số mục Standard hay tổng số mục, không nêu; các trạng thái trung gian như Standard fail ≤ 20% nhưng > 0 không được nêu — nguồn chỉ nêu "else READY" ở một chỗ và "All pass" ở chỗ khác.)

## Template / mẫu đầu ra (rút gọn, giữ cấu trúc và các cột/trường)
Tiêu đề: "Checklist Run — <mã phạm vi> <tên> — DRAFT"; dòng nguồn: template + câu trả lời của PM/người review.
- Metadata: Scope | Project | Release | Run Date | Reviewer (vai trò/tên) | Templates Applied | Status = DRAFT — pending sign.
- Summary: Total items | Pass | Fail | N/A | Critical fails | Pass rate (excluding N/A); dòng Skill recommendation.
- Items by Section (mỗi section một bảng): ID | Item | Type | Result | Evidence | Note.
- Critical Fails: mỗi mục một khối gồm Action, Owner, Re-check.
- Reviewer Sign: Role | Name | Decision (⬜ Approve / Reject / Conditional) | Sign Date.
Danh sách kiểm tra sau khi lập: danh sách template đã xác nhận trước khi chạy; mục Critical có bằng chứng; mục Auto ghi nguồn truy vấn; đề xuất ≠ quyết định gate; tên file duy nhất theo ngày chạy; không commit.

## Lỗi thường gặp & lesson learned
- Bỏ qua bằng chứng cho mục Critical -> gate được thông qua trên niềm tin -> Critical luôn phải có bằng chứng.
- Tự chấm, tự ký thay người review -> mất tính độc lập -> chỉ người review ký.
- Trộn checklist vào tính signal -> số QS-XX bị bóp méo -> giữ hai luồng độc lập.
- Ghi đè kết quả lần chạy cũ -> mất lịch sử -> mỗi lần chạy một file theo ngày.
- Hiểu đề xuất là quyết định -> PM tự dừng/thông qua gate -> chỉ gate review quyết.
- Gộp template nhưng không loại trùng theo mã mục -> đếm đôi -> dedupe theo ID; Critical ở template nào cũng chặn.
- Câu hỏi còn mở trong nguồn: mã mục `<SECTION>-<NN>` có duy nhất giữa các template không; quy tắc đồng thuận khi nhiều người review chưa được nêu.

## Ví dụ minh họa
Dựa trên mẫu trong nguồn (dự án ẩn danh): chạy G4 Code Complete ngày 2026-08-26 với hai template (gate G4-code và customer compliance).
- Tổng 26 mục: Pass 22, Fail 3, N/A 1, Critical fail 0. Pass rate 88% (không tính N/A; 22 / 25).
- Đề xuất: 🟡 REVIEW vì có 3 mục Standard fail.
- Ví dụ mục: CR-01 "Mỗi PR có ≥ 1 reviewer approve" (Auto) đạt nhờ truy vấn git; CR-04 "Code duplication < 5%" (Standard) fail vì SonarQube ghi 7%.
- Ví dụ mục Critical fail (khác lần chạy): UT-CHK-04 "UT cho module Release đạt 80%" thực tế 72% -> Critical, Action: bổ sung coverage; Owner: Dev Lead; chạy lại checklist sau khi sửa.
(nguồn chưa rõ: 3 fail/26 mục ≈ 11.5% nên dưới 20%, nhưng ví dụ vẫn ghi REVIEW; có thể tính trên nhóm Standard hay có lý do khác.)

## Tự kiểm tra
1. Khi nào đề xuất là BLOCK? Đáp: Critical fail > 0.
2. Pass rate tính thế nào? Đáp: Pass trên tổng đã trừ mục N/A.
3. Chạy lại checklist G4 ngày khác thì làm gì với file cũ? Đáp: giữ nguyên, tạo file mới theo ngày (giữ mọi lần chạy).
4. Ai ký biên bản? Đáp: người review, thủ công; người chạy không tự ký.
5. Mục Auto thiếu dữ liệu ghi gì? Đáp: `[NO_DATA]`.

## Liên quan
- Trước: Release plan (Ch8·01) (chỉ định template áp dụng), wbs / Lập schedule (Ch3·03) (ngữ cảnh gate).
- Sau: Gate review (Ch8·02) (kết hợp checklist + signal -> quyết định); Status tuần (Ch7·01) tham chiếu trạng thái checklist.
- Song song: Tín hiệu (Ch6·01) (signal khác checklist).
