---
title: Phân tích chênh lệch effort thực tế (EVM, E3, dự báo EAC)
source: Effort actuals (Ch6·03)
stage: Cross-cutting
level: trung bình
prerequisites: [Ch3·03, Ch6·01]
---
# Phân tích chênh lệch effort thực tế (EVM, E3, dự báo EAC)

## Mục tiêu học xong bạn làm được gì
- Trả lời câu hỏi "tại sao lệch X%" thay vì chỉ cộng tổng: so sánh effort thực tế với kế hoạch theo task, người/vai trò, phase, module, stage.
- Tính tay Variance, Variance %, EV, AC, PV, CPI, SPI, E3, ETC, EAC, VAC.
- Nhận ra mẫu lặp (vượt chronic, nút thắt vai trò, lệch theo module) mà không đổ lỗi cá nhân.
- Đề xuất hành động, biết khi nào phải re-baseline qua change request.

## Khi nào dùng (thời điểm, ai kích hoạt, điều kiện đầu vào)
- PM kích hoạt khi thấy "đang chạy quá plan", cần đào sâu tín hiệu E3, hoặc theo dõi burn rate/vượt chi phí; thường hằng tuần.
- Đầu vào bắt buộc: effort thực tế từng task (`actual_effort`), effort kế hoạch từng task (baseline trong lịch). Cần thêm trạng thái, owner, vai trò, stage, module, % hoàn thành của task; và BAC (tổng ngân sách effort).
- Nếu task xong mà thiếu thực tế: thử suy từ lịch sử git (chỉ là ước tính, gắn nhãn) hoặc `[NO_DATA]`.
- Thiếu effort kế hoạch hoặc thực tế: dừng, quay lại lập lịch/tách task; không đoán.

## Khái niệm cốt lõi (định nghĩa, thuật ngữ, vì sao quan trọng)
- Đơn vị effort: md (man-day) mặc định; quy đổi 1md = 8mh (man-hour). Chuẩn hóa về một đơn vị trước khi phân tích.
- BAC = Budget at Completion (tổng effort kế hoạch). ETC = Estimate to Complete. EAC = Estimate at Completion. VAC = Variance at Completion (BAC − EAC).
- E3 = tín hiệu chênh lệch effort; ngưỡng mặc định ≤ 10%.
- Task ≤ 1md: kiểm tra chênh lệch hằng ngày, không chỉ hằng tuần.
- Phân tích theo mẫu, không quy lỗi cho cá nhân.
- Ngưỡng CPI/SPI phụ thuộc loại hợp đồng.
- Không sửa ước lượng gốc trong bước phân tích; muốn đổi baseline phải qua change request.

## Cách làm từng bước (thủ công, đủ chi tiết để làm theo; kèm input/output)
1. Chốt ngày snapshot, tên/mã dự án, phạm vi (mặc định toàn dự án). Tùy chọn: đơn vị effort, ngưỡng mẫu (mặc định 10%), chiều phân tích (dự án / phase / người / một tín hiệu).
2. Kiểm tra dữ liệu:
   - Task có trong lịch mà không có trong danh sách task: dừng và hỏi.
   - Task xong thiếu thực tế: đánh dấu, thử git hoặc `[NO_DATA]`.
   - Lệch đơn vị md/mh: chuẩn hóa.
   - Task đang làm thiếu % hoàn thành: CPI/SPI chỉ tính một phần, task đó `[NO_DATA]`.
   - Effort kế hoạch = 0 hoặc thiếu: loại khỏi tính Variance %, ghi chú trong báo cáo.
   - Effort trong task và baseline lịch mâu thuẫn: dừng hỏi, không tự hòa giải.
3. Với mỗi task tính Variance = actual − planned và Variance % = (actual − planned) / planned × 100%.
4. Gom theo chiều: người (owner), vai trò (BA/Designer/Dev/QA/Tech Lead), phase (Req/Design/Dev/Test), module, stage (REQ/BD/DEV/UT/TC/TE).
5. Tính EVM: với mỗi task EV = planned × % hoàn thành; AC = actual; PV = planned (đến hiện tại). Cộng lại rồi CPI = EV/AC, SPI = EV/PV. Tính E3 (chênh lệch effort đến hiện tại so với ngưỡng).
6. Dự báo: hệ số chênh lệch (variance factor), ETC, EAC, VAC (công thức ở bảng dưới).
7. Tìm mẫu lặp (bảng mẫu bên dưới). Hỏi nguyên nhân gốc (ví dụ vòng phản hồi khách hàng dài, màn hình phụ thuộc nhau gây làm lại, template thiếu trường hợp biên).
8. Đề xuất hành động: ước lượng lại stage nếu vượt chronic; người dự phòng nếu vai trò là nút thắt; mở change request nếu EAC vượt xa ngân sách. EAC > ngân sách phải cảnh báo rõ và đề xuất re-baseline qua change request.
9. Chốt báo cáo ở trạng thái DRAFT chờ PM duyệt; chụp lại hằng tuần để xem mẫu có kéo dài không.

## Công thức, ngưỡng & tín hiệu
| Tên | Công thức/điều kiện | Ngưỡng | Hành động khi vượt |
|---|---|---|---|
| Variance | actual − planned | — | — |
| Variance % | (actual − planned) / planned × 100% | — | — |
| EV (mỗi task) | planned_effort × percent_complete | — | — |
| AC / PV | AC = actual_effort; PV = planned_effort (đến hiện tại) | — | — |
| CPI | EV_total / AC_total | ≥ 0.95 (Fixed-bid), ≥ 0.90 (T&M) = trong ngân sách | CPI < 0.85 là nghiêm trọng, leo thang |
| SPI | EV_total / PV_total | ≥ 0.95 / ≥ 0.90 = đúng tiến độ | cảnh báo |
| E3 | tín hiệu chênh lệch effort | mặc định ≤ 10% | vàng/đỏ, đào sâu nguyên nhân |
| EAC (EVM) | AC_total + (BAC − EV_total) / CPI | — | nếu > BAC, cảnh báo + change request |
| ETC (EVM) | EAC − AC_total | — | — |
| VAC | BAC − EAC | — | âm = vượt ngân sách |
| ETC (bảng Key metrics) | tổng(effort kế hoạch của task còn lại × hệ số chênh lệch) | — | — |
| EAC (bảng Key metrics) | actual_to_date + ETC | — | — |
| Vượt chronic theo stage | ≥ 5 task cùng stage, chênh lệch trung bình > ngưỡng | ngưỡng mặc định 10% | 🔴 + nguyên nhân gốc |
| Nút thắt vai trò | chênh lệch tổng hợp theo vai trò > 50% | > 50% | 🟡 (vai trò/tải, không cá nhân) |
| Lệch theo module | chênh lệch module >> trung bình dự án | không có số | 🟡 |
| Tần suất kiểm tra | task ≤ 1md: hằng ngày (task đóng vs kế hoạch, burn rate md/ngày, CPI/SPI snapshot); hằng tuần: tổng hợp + xu hướng | phát hiện mẫu sau ≥ 5 task (ngày) / sau ≥ 1 tuần | — |
(nguồn chưa rõ: nguồn mở ra hai công thức EAC/ETC — EVM chuẩn dùng CPI và cách "hệ số chênh lệch" dùng trong ví dụ; câu hỏi mở của nguồn cũng hỏi nên chọn cách nào. Ngoài ra "E3" ở đây là chênh lệch effort so với kế hoạch, ở báo cáo tuần có nghĩa hơi khác — xem Status tuần (Ch7·01).)

## Template / mẫu đầu ra (rút gọn, giữ cấu trúc và các cột/trường)
"Effort Actuals — <ngày>": metadata (Project, Snapshot, Scope, Status = DRAFT).
- Summary: Planned to date | Actual to date | Variance | E3 signal | CPI | SPI | Forecast EAC (so với budget) | VAC.
- Variance Breakdown: By Phase (Phase | Planned | Actual | Variance); By Role (Role | Planned | Actual | Variance | Note); By Stage (Stage | Tasks done | Avg variance | Pattern).
- Pattern Found: mô tả mẫu (ví dụ BD chronic overrun), nguyên nhân gốc, khuyến nghị.
- Forecast: Remaining tasks | Variance factor | ETC | EAC | Budget | VAC.
- Recommended Actions: đánh số, có mức ưu tiên (🔴/🟡/✅) và cách theo dõi.
Kiểm tra sau: thực tế vs kế hoạch lấy từ danh sách task + lịch; CPI/SPI tính nếu đủ dữ liệu; mẫu lặp có nguyên nhân gốc, không quy lỗi cá nhân; EAC > ngân sách -> cảnh báo + đề xuất change request; thiếu dữ liệu `[NO_DATA]`; trạng thái DRAFT.

## Lỗi thường gặp & lesson learned
- Chỉ cộng tổng mà không trả lời "vì sao lệch" -> PM không có gì để hành động -> luôn tìm mẫu và nguyên nhân gốc.
- Đổ lỗi cá nhân khi vai trò quá tải -> mất niềm tin, sai chẩn đoán -> phân tích theo vai trò/tải.
- Lẫn đơn vị md và mh -> lệch 8 lần -> chuẩn hóa trước (1md = 8mh).
- Task có kế hoạch 0 vẫn tính % -> chia cho 0 -> loại và ghi chú.
- Bịa thực tế khi thiếu -> báo cáo sai -> dùng `[NO_DATA]` hoặc ước tính git có gắn nhãn.
- Tự sửa ước lượng gốc thay vì change request -> baseline mất dấu vết -> re-baseline qua change request.
- Bỏ qua ước lượng heuristic của stage lặp vượt (ví dụ BD luôn +25%) -> tiếp tục vượt -> cập nhật heuristic và buffer review.

## Ví dụ minh họa
Dựa trên mẫu của nguồn (dự án ẩn danh, 2026-08-26): kế hoạch đến nay 87 md, thực tế 96 md -> Variance +9 md (+10.3%); E3 = 10.3% 🟡 (ngưỡng ≤ 10%); CPI 0.91 🟡; SPI 0.94 🟡; ngân sách 145 md.
- Theo stage: REQ 12 task, −5% ✅; BD 11 task, +25% 🔴 chronic; DEV 18 task, +12% 🟡.
- 11/11 task BD đều vượt. Nguyên nhân: vòng phản hồi khách hàng dài, màn hình phụ thuộc nhau gây làm lại, template BD chưa bao phủ trường hợp biên. Khuyến nghị: đổi heuristic BD từ 2md lên 2.5md, thêm buffer review 1 ngày mỗi work package.
- Dự báo: còn 32 task (58 md kế hoạch), hệ số chênh lệch +10.3%, ETC 64 md; EAC = 96 + 64 = 160 md; VAC −15 md (vượt ~10%). Hành động: cập nhật ước lượng BD (+25% cho phần BD còn lại) qua change request; xếp người dự phòng 0.3 FTE cho Designer (trung bình +22%).
(nguồn chưa rõ: nguồn ghi mâu thuẫn giữa phần Summary — EAC 162 md, +12%, VAC −17 md — và phần Forecast — EAC 160 md, −15 md, ~10%; ở đây theo phần Forecast vì cộng đúng 96 + 64 = 160.)

## Tự kiểm tra
1. EV của một task kế hoạch 10md, hoàn thành 60% là bao nhiêu? Đáp: 10 × 0.6 = 6 md.
2. CPI < bao nhiêu thì nghiêm trọng? Đáp: CPI < 0.85.
3. Khi nào gắn cờ "vượt chronic" cho một stage? Đáp: ≥ 5 task cùng stage với chênh lệch trung bình vượt ngưỡng.
4. VAC âm nghĩa là gì? Đáp: EAC lớn hơn BAC, sẽ vượt ngân sách.
5. Nút thắt vai trò xác định thế nào và xử lý ra sao? Đáp: chênh lệch tổng hợp theo vai trò > 50%; xem theo vai trò/tải (không đổ lỗi cá nhân), xếp người dự phòng.

## Liên quan
- Trước: Lập schedule (Ch3·03) (baseline effort), Spec thành task (Ch3·02) (task-list).
- Sau: Change request (Ch4·03) (re-baseline khi VAC nghiêm trọng), Status tuần (Ch7·01) (mục chênh lệch).
- Hai chiều: Tín hiệu (Ch6·01) (E3 chi tiết).
