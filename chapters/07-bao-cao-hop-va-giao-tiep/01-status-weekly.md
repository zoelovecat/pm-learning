---
title: Báo cáo trạng thái hằng tuần (Weekly Status Report)
source: Status tuần (Ch7·01)
stage: Cross-cutting
level: trung bình
prerequisites: [Ch3·03, Ch4·04, Ch6·01, Ch6·03]
---
# Báo cáo trạng thái hằng tuần (Weekly Status Report)

## Mục tiêu học xong bạn làm được gì
- Biến dữ liệu thô của tuần (trạng thái task, ngày thực tế) thành thông tin có ý nghĩa (% hoàn thành, SPI proxy, scope creep %, dự báo ngày kết thúc) rồi trình bày thành một báo cáo tuần cho stakeholder.
- Tính tay SPI proxy, SV proxy, E3, scope creep %, projected end date, EAC/ETC và đánh giá đèn 🟢/🟡/🔴 theo đúng ngưỡng.
- Tách bạch Risk (sự kiện tương lai chưa chắc chắn) với Issue (vấn đề đang xảy ra) trong báo cáo.
- Viết được mục Recommended Actions (Corrective / Preventive / Defect Repair) cho mọi bất thường mức 🔴, và biết leo thang lên ai khi nào.

## Khi nào dùng (thời điểm, ai kích hoạt, điều kiện đầu vào)
- Thời điểm: cuối tuần làm việc (chiều thứ Sáu, "Friday EOD"). Chạy giữa tuần thì phải đánh dấu `PARTIAL` kèm "dữ liệu đến <ngày>".
- Người kích hoạt: PM (dự án đơn, mỗi lần một dự án; không gộp nhiều dự án).
- Tuần theo ISO 8601: thứ Hai đến Chủ nhật, ghi dạng `YYYY-Www` (ví dụ `2026-W25`). Múi giờ mặc định UTC+7.
- Đầu vào BẮT BUỘC (thiếu là dừng, không làm tiếp):
  - Danh sách task có trạng thái xong/chưa xong (`- [x]` / `- [ ]`).
  - Kế hoạch tiến độ (schedule) có ngày baseline bắt đầu/kết thúc.
  - Tên dự án / bối cảnh.
- Đầu vào TÙY CHỌN (thiếu thì ghi `[NO_DATA]`, không chặn, không bịa): sổ rủi ro, sổ vấn đề, báo cáo tuần trước (để tính chênh lệch), WBS/scope baseline (để kiểm scope creep), danh sách stakeholder nhận báo cáo, dữ liệu signal (QS-XX), effort ước lượng từng task.
- Quy tắc nền: báo cáo luôn ở trạng thái DRAFT, PM duyệt rồi mới gửi. Không tự sửa task-list/schedule/risk/issue gốc.

## Khái niệm cốt lõi
Chuỗi PMP Monitor & Control gồm ba tầng dữ liệu:

| Thuật ngữ | Định nghĩa |
|---|---|
| Work Performance Data (WPD) | Dữ liệu thô từ thực thi: trạng thái task, ngày thực tế, git log |
| Work Performance Information (WPI) | WPD đã phân tích: % complete, SPI, scope creep %, forecast |
| Work Performance Report (WPR) | WPI được trình bày cho stakeholder: chính là file báo cáo tuần |

Các khái niệm khác:
- SPI proxy: Schedule Performance Index bản thích ứng theo số task (không tính theo chi phí) = actual_tasks_done / planned_tasks_this_week.
- SV proxy: Schedule Variance thích ứng = actual_tasks_done − planned_tasks_this_week (dương = sớm hơn kế hoạch, âm = trễ).
- EAC (Estimate at Completion): actual_effort_to_date + (remaining × avg_effort_per_task). ETC (Estimate to Complete): EAC − actual_effort_to_date.
- Scope creep %: unplanned_tasks_in_progress / total_in_progress × 100.
- E3 (chênh lệch % hoàn thành): actual% − planned%. (Nguồn chưa rõ: bản template thứ hai định nghĩa E3 = (actual − planned) / planned × 100% là chênh lệch effort với ngưỡng khác; xem mục Công thức.)
- Risk: sự kiện tương lai chưa chắc chắn (có xác suất × tác động), lấy từ Risk Register. Issue: vấn đề đã xảy ra (có tác động thực + hạn giải quyết), lấy từ Issue Log. Không gộp chung một bảng.
- Anomaly: bất thường (overdue quá ngưỡng, signal lệch, risk tăng cấp, E3 vượt ngưỡng).
- Ba loại hành động điều chỉnh: Corrective = sửa sai lệch đã xảy ra; Preventive = ngăn vấn đề xảy ra/tái diễn; Defect Repair = sửa một deliverable cụ thể không đạt yêu cầu.
- Ký hiệu nguồn số liệu trong báo cáo: 📄 từ tài liệu | 📋 quy tắc công ty | 💭 PM xác nhận | 🤖 tự suy ra/giả định | ⏳ TBD / NO_DATA.

## Cách làm từng bước (thủ công, đủ chi tiết để làm theo; input/output)
**Bước 1. Kiểm tra đầu vào.** Input: task-list, schedule, (tùy chọn) risk/issue/báo cáo tuần trước/WBS. Output: danh sách có/không. Thiếu task-list hoặc schedule thì dừng và tạo chúng trước (dựng task từ đặc tả, dựng baseline schedule). Ghi số task active và milestone gần nhất.

**Bước 2. Thu thập metadata.** Tự xác định số tuần ISO, khoảng thứ Hai 00:00 đến Chủ nhật 23:59, tuần trước (ISO week − 1), tên file `YYYY-Www`. Hỏi một lần: tên dự án + PM; chạy Friday EOD hay giữa tuần; audience nội bộ hay bên ngoài (client/sponsor); highlight đặc biệt; ai nhận báo cáo. Bỏ qua thì mặc định: nội bộ, không ghi chú thêm, Friday EOD. Danh sách phân phối phải khớp Communication Management Plan: nội bộ giữ đủ chi tiết; bên ngoài cân nhắc lược bỏ ghi chú nội bộ, blocker nhạy cảm; không có plan thì ghi "default: internal only".

**Bước 3. Kiểm chất lượng dữ liệu.**
- Task-list: phải parse được trạng thái (không thì dừng). Owner, ngày kết thúc kế hoạch, effort là tùy chọn; thiếu owner ghi `[NO_DATA]`; thiếu planned end thì bỏ tính overdue; thiếu effort thì bỏ E3 variance và EAC.
- Schedule: phải có ngày baseline (không thì dừng). Milestone và "planned % mỗi tuần" là tùy chọn.
- Kiểm scope baseline: lấy danh sách deliverable/task đã duyệt trong WBS hoặc scope; task nào có trong task-list mà không có trong đó là "ứng viên scope creep". Không có WBS thì dùng schedule làm proxy (ghi 🤖 fallback). Không có cả hai thì `[NO_DATA]`. Đây chỉ là ứng viên; PM xác nhận là thay đổi đã duyệt hay creep thật.
- Nếu ứng viên > 10% task in-progress thì 🟡; > 20% thì 🔴 và PM phải xác nhận trước khi đi tiếp.

**Bước 4. Phân tích tuần (WPD thành WPI).**
1. Đếm task theo nhóm: Done (`- [x]` và closed_date trong tuần), Blocked (`- [ ]` có ghi chú blocker), In progress (`- [ ]`, không blocked, chưa overdue), Overdue (planned_end < hôm nay và chưa xong). % complete = done_tasks / total_tasks × 100.
2. Tính SPI proxy, SV proxy (xem bảng). Nếu planned_tasks_this_week = 0 thì SPI = `[NO_DATA]`.
3. Velocity: velocity tuần này = số task done tuần này; so với tuần trước (nếu có báo cáo trước), delta = +X / −X task. So plan vs actual bằng E3.
4. Liệt kê blocker: Task | Owner | Blocked X ngày | Lý do.
5. Scope creep % (dùng ứng viên bước 3). Total in-progress = 0 hoặc thiếu baseline thì `[NO_DATA]`.
6. Risk: so với tuần trước, đếm New (tạo trong tuần), Escalated (xác suất hoặc tác động tăng: Low→Medium, Medium→High), Closed (đã giảm thiểu hoặc hết hạn). Mỗi risk ghi: ID, mô tả, Probability (H/M/L), Impact (H/M/L), Response strategy, Owner.
7. Issue: New, Escalated (mức nghiêm trọng tăng), Resolved. Mỗi issue ghi: ID, mô tả, Actual impact, Owner, Resolution status, Days open.
8. Signal (tùy chọn): lấy snapshot gần nhất trong tuần, so tuần trước bằng ↑ ↓ →.
9. Dự báo (bên dưới). Rồi tổng hợp bảng WPI và đèn tổng thể trước khi viết báo cáo; không viết báo cáo nếu chưa có bảng này.

Dự báo ngày kết thúc: avg_velocity = số task done/tuần, trung bình 4 tuần gần nhất nếu có báo cáo cũ (chỉ có một tuần thì dùng done_this_week, đánh dấu 🤖). Nếu avg_velocity = 0 thì projected_end = `[NO_DATA]` và hỏi PM "tuần này chưa close task nào, có block toàn team không?". Ngược lại: remaining_tasks = total_tasks − done_tasks; weeks_left = remaining_tasks / avg_velocity; projected_end = hôm nay + weeks_left × 7 ngày. Nếu projected_end > schedule end_date thì đánh dấu "Milestone at risk" kèm số ngày trễ.

Dự báo effort: có effort ước lượng thì actual_effort_to_date = tổng actual effort của task done; EAC = actual_effort_to_date + (remaining_tasks × avg effort của remaining tasks); ETC = EAC − actual_effort_to_date. Không có effort thì EAC/ETC = `[NO_DATA]`.

**Bước 5. Viết báo cáo (WPI thành WPR).** Theo khung ở mục Template. Mỗi phần lớn có dòng "Sources:". Số nào thiếu nguồn thì `[NO_DATA]`. Mỗi bất thường 🔴 phải có dòng trong Recommended Actions. Không có 🔴 thì viết "Không có anomaly nghiêm trọng. Không cần Recommended Action." Cuối file có checklist: mọi mục 🤖 và `[NO_DATA]` trong báo cáo phải xuất hiện trong danh sách kiểm. File đã tồn tại thì hỏi: ghi đè hay lưu bản `YYYY-Www-draft2`.

**Bước 6. Dừng và bàn giao.** Tóm tắt: đèn trạng thái, % complete vs plan, SPI, scope creep %, số blocked, forecast; liệt kê Recommended Actions; giữ DRAFT, chờ PM duyệt. Nhắc PM cập nhật: Risk Register (đóng risk đã giảm thiểu, cập nhật risk tăng cấp), Issue Log (đóng issue, ghi ngày giải quyết thực tế), Lessons Learned (nếu có 🔴 thì ghi root cause nếu biết). Chỉ gửi ra ngoài sau khi PM duyệt, qua kênh giao tiếp stakeholder.

## Công thức, ngưỡng & tín hiệu (bảng: tên | công thức/điều kiện | ngưỡng | hành động khi vượt)

| Tên | Công thức / điều kiện | Ngưỡng | Hành động khi vượt |
|---|---|---|---|
| % complete | done_tasks / total_tasks × 100 | Xem status matrix | Đối chiếu plan % |
| SPI proxy | actual_tasks_done / planned_tasks_this_week | > 1.0 🟢 sớm hơn; 0.9–1.0 🟡 hơi trễ; < 0.9 🔴 trễ | Corrective: tăng velocity, gán lại task hoặc giảm scope |
| SV proxy | actual_tasks_done − planned_tasks_this_week | ≥ 0 🟢; −1 đến −2 🟡; ≤ −3 🔴 | Như SPI |
| E3 (bản chính) | actual% − planned% | > −5% 🟢; −5% đến −10% 🟡; < −10% 🔴 (hoặc milestone slip 🔴) | Xem mục hành động |
| E3 (bản template thứ hai) | (actual − planned) / planned × 100%, mặc định ngưỡng 10% | 🟡 10–15%; 🔴 > 15% (effort variance) | (nguồn chưa rõ: hai định nghĩa E3 khác nhau, xem Ví dụ và cuối bài) |
| Overdue | planned_end < hôm nay, chưa xong | 0 🟢; 1–2 task ≤ 3 ngày 🟡; ≥ 3 task hoặc > 3 ngày 🔴 | Corrective |
| Blockers | Số task blocked | 0 🟢; 1–2 🟡; ≥ 3 hoặc blocking milestone 🔴 | Leo thang, gỡ blocker |
| Scope creep % | unplanned_in_progress / total_in_progress × 100 | ≤ 10% 🟢; > 10% 🟡; > 20% 🔴 | PM xác nhận unauthorized work, mở change request nếu cần |
| Forecast variance | projected_end − schedule end | ≤ 0 ngày trễ 🟢; 1–7 ngày 🟡; > 7 ngày 🔴 | Preventive: fast-track critical path, thương lượng buffer |
| Forecast (cách khác) | projected_end vs schedule end | ≤ end 🟢; trễ < 1 tuần 🟡; trễ ≥ 1 tuần 🔴 | Như trên |
| Issue days open (tác động cao) | Số ngày mở | ≤ 2 🟢; 3–5 🟡; > 5 🔴 | Defect Repair: escalate Tech Lead, cấp tài nguyên xử lý riêng |
| Signal QS-XX vs threshold | Lệch so với ngưỡng của signal | Lệch 5–10% 🟡; > 10% 🔴 (nguồn chưa rõ: "lệch" tính theo điểm % hay tỷ lệ) | Xem bài tín hiệu chất lượng |
| Milestone date | Trạng thái mốc | Cảnh báo có thể trượt 🟡; đã trượt 🔴 | Thông báo Sponsor |

Ma trận đèn tổng thể (status code):

| Điều kiện | Trạng thái |
|---|---|
| 0 task overdue, % complete ≥ plan, 0 blocker mới, SPI ≥ 1.0, scope creep ≤ 10% | 🟢 On track |
| 1–2 task overdue ≤ 3 ngày, hoặc % complete −5% vs plan, hoặc SPI 0.9–1.0, hoặc scope creep 10–20% | 🟡 At risk |
| ≥ 3 task overdue, hoặc % complete −10% vs plan, hoặc milestone slip, hoặc SPI < 0.9, hoặc scope creep > 20% | 🔴 Off track |

(Nguồn chưa rõ: biên SPI = 1.0 được ghi "> 1.0 🟢" ở bảng ngưỡng nhưng "SPI ≥ 1.0" 🟢 ở ma trận; và bản template thứ hai còn thêm điều kiện "≥ 1 signal 🔴" vào 🔴, "1 signal 🟡" vào 🟡, "mọi signal đạt threshold" vào 🟢; bản này cũng ghi overdue 🟡 = 1–3 ngày, 🔴 = > 3 ngày.)

Leo thang:

| Điều kiện | Lên ai | Hành động |
|---|---|---|
| 1–2 anomaly 🔴, team tự xử được | PM | PM xem Recommended Actions, gán owner, theo dõi |
| Milestone trượt ≥ 1 tuần | PM + Sponsor | Báo Sponsor; tạo change request nếu cần đổi baseline |
| Scope creep > 20% chưa xác nhận | PM + Sponsor | Xác nhận unauthorized work; theo quy trình change control chính thức |
| Issue chưa xử lý > 5 ngày, tác động cao | PM + Tech Lead / Delivery Manager | Leo thang trong daily standup hoặc email riêng |
| SPI < 0.7 (hiệu suất tiến độ rất kém) | PM + Sponsor | Họp khẩn; cân nhắc giảm scope hoặc bơm thêm nguồn lực |

## Template / mẫu đầu ra (rút gọn, giữ cấu trúc, cột, trường)
```markdown
# Weekly Status Report — Week YYYY-Www
> DRAFT — chờ PM review và approve trước khi distribute.
(Bảng ký hiệu nguồn: 📄 📋 💭 🤖 ⏳)

| Field | Value |
| Project | <tên-dự-án> | PM | <PM> |
| Week | YYYY-Www (Mon DD/MM → Sun DD/MM) | Reported | YYYY-MM-DD |
| Status | 🟢 / 🟡 / 🔴 | Prev week | link tuần trước hoặc — |

## 1. Summary  (Sources: task-list + schedule + ghi chú PM)
| Metric | This Week | Prev Week | Delta | Status |
Tasks done | Tasks blocked | Tasks overdue | % complete | Plan % (từ schedule)
SPI proxy | SV proxy | Scope creep % | Velocity (tasks/week)

## Forecast
| Metric | Value | Basis | Status |
Avg velocity (X tasks/week, Y tuần rolling) | Remaining tasks | Projected end date
Schedule end date (baseline) | Variance (+X/−X days) | EAC effort | ETC effort
> Milestone at risk: <milestone> — projected end trễ X ngày

## 2. Progress detail
Done this week: [task] — owner — closed date
Blocked: Task | Owner | Blocked (ngày) | Lý do
In progress → next week: [task] — owner — ETA

## 3. Signal snapshot (optional): Signal | This Week | Prev Week | Threshold | Status
## 4. Milestone status: Milestone | Baseline date | Projected date | Variance | Status
## 5a. Risks (Risk Register): ID | Risk description | Probability | Impact | Response (Mitigate/Accept/Transfer/Avoid) | Owner | Status
   + Changes this week: New / Escalated (old → new level) / Closed (reason)
## 5b. Issues (Issue Log): ID | Issue description | Actual impact (High/Med/Low) | Owner | Resolution status | Days open
   + Changes this week: New / Resolved
## 6. Next week plan: Next week focus (task, owner, ETA); Key dependencies / risks to watch
## 10. Recommended Actions: # | Anomaly | Type | Recommended Action | Owner | Target date
## Post-generation review checklist: 🤖 assumed | ⏳ TBD | 💭 PM confirmed
```
Bản mẫu thứ hai (dạng rút gọn, dành cho dự án có PQA/git) có các mục: Highlights (anomaly đặt ngay sau metadata) → 1 Progress (Tasks done/in progress/blocked/overdue, % complete, Effort actual (md) kèm E3, Commits) → 2 Milestone & Signals → 3 Tasks Done → 4 Tasks Blocked/Behind (Task | Owner | Blocker | Days late | Action) → 5 Risk & Issue (New/Escalated, Closed) → 6 Plan Next Week → 7 Asks (quyết định cần stakeholder) → 8 Git Activity → 9 PQA (nếu có). Cột bảng Progress: Metric | This Week | Last Week | Plan | Variance | Status.

## Lỗi thường gặp & lesson learned (sai gì -> hậu quả -> cách tránh)
- Bịa số khi thiếu dữ liệu -> báo cáo mất tin cậy, quyết định sai -> ghi `[NO_DATA]` kèm lý do, liệt kê trong checklist.
- Gộp Risk và Issue chung một bảng -> lẫn "có thể xảy ra" với "đã xảy ra", không rõ ai xử lý gì -> luôn tách 5a / 5b.
- Có bất thường 🔴 mà không có Recommended Action -> báo cáo chỉ "kể", không dẫn tới hành động -> mỗi 🔴 một dòng có Type, Owner, Target date.
- Chia cho 0 khi tuần không có kế hoạch task hoặc velocity = 0 -> SPI/ngày kết thúc vô nghĩa -> dùng guard: `[NO_DATA]` và hỏi PM (có block toàn team không).
- Coi ứng viên scope creep là creep thật -> đổ lỗi nhầm cho team -> chỉ là ứng viên, PM xác nhận (có thể là thay đổi đã duyệt).
- Chạy giữa tuần mà không đánh dấu PARTIAL -> so sánh SPI với tuần đủ bị méo -> gắn PARTIAL và ngày dữ liệu.
- Gửi báo cáo nội bộ nguyên bản cho khách -> lộ blocker nhạy cảm -> chọn audience từ đầu, khớp Communication Plan.
- Chỉ dựa một tuần để dự báo -> forecast dao động -> dùng trung bình tối đa 4 tuần; một tuần thì đánh dấu 🤖.
- Không cập nhật Risk Register/Issue Log sau báo cáo -> sổ lệch báo cáo tuần sau -> làm theo danh sách nhắc cập nhật ở bước 6.

## Ví dụ minh họa (ngắn, có số; dựng thì ghi "(ví dụ dựng)")
Ví dụ dựng theo bản mẫu bàn giao: Done 8/19 task (42%, plan 45%); SPI 0.93 🟡; 2 task blocked; scope creep 8% 🟢; projected end 2026-07-15 so với baseline 2026-07-12 nghĩa là At risk trễ 3 ngày. Tổng thể 🟡 At risk. Recommended Actions: 2 Corrective, 1 Preventive.

Ví dụ dựng bước tính dự báo: 19 task, 8 done nên remaining = 11; avg_velocity = 4 task/tuần nên weeks_left = 11 / 4 = 2,75 tuần, projected_end = hôm nay + 2,75 × 7 ngày (khoảng 19 ngày). Nếu baseline end sớm hơn 7 ngày thì variance 🔴.

Ví dụ dựng bản mẫu thứ hai (dự án <tên-dự-án>): Highlights gồm "Task T-018 overdue 4 ngày (blocker: khách chưa xác nhận API)" 🔴, "E3 = 14% (threshold 10%)" 🟡, "QS-REQ-01 = 96% (target ≥ 95%)" 🟢; Tasks done 8 (tuần trước 6, plan 7); % complete 42% (tuần trước 36%, plan 45%, variance −3% 🟡).

## Tự kiểm tra (3-5 câu hỏi, đáp án ngắn ngay dưới)
1. Tuần này 6 task done, kế hoạch 8. SPI proxy, SV proxy và đèn là gì?
   Đáp án: SPI = 6/8 = 0.75 (< 0.9 nên 🔴); SV = 6 − 8 = −2 (🟡 theo bảng SV; đèn tổng thể vẫn 🔴 do SPI < 0.9).
2. Có 10 task in-progress, 3 nằm ngoài scope baseline. Scope creep % và hành động?
   Đáp án: 3/10 × 100 = 30% > 20% nên 🔴; PM phải xác nhận unauthorized work trước khi đi tiếp, leo thang PM + Sponsor nếu chưa xác nhận.
3. Vì sao Risk và Issue phải ở hai bảng khác nhau?
   Đáp án: Risk là sự kiện tương lai có xác suất × tác động; Issue đã xảy ra với tác động thực và hạn giải quyết; gộp sẽ lẫn cách xử lý.
4. Velocity 0 tuần này thì dự báo ngày kết thúc xử lý ra sao?
   Đáp án: projected_end = `[NO_DATA]` (🤖), hỏi PM xem có block toàn team không.
5. Một issue mức tác động cao đã mở 6 ngày, phải làm gì?
   Đáp án: > 5 ngày là 🔴; Defect Repair, escalate PM + Tech Lead/Delivery Manager và cấp người xử lý riêng.

## Liên quan (bài trước/sau)
- Trước: lập task-list từ đặc tả; lập baseline schedule; sổ rủi ro/vấn đề; bài tín hiệu chất lượng (QS-XX) nếu dùng §3 Signal.
- Sau: giao tiếp stakeholder (gửi báo cáo sau khi PM duyệt); họp gate review (dùng milestone, % complete, forecast, Recommended Actions làm đầu vào); Sprint retro (bài 04) dùng báo cáo tuần làm nguyên liệu.
- Chưa rõ trong nguồn (cần PM công ty xác nhận): ma trận đèn có tùy biến theo dự án không; ngưỡng overdue/E3 có đúng chuẩn công ty không; so tuần trước hay xu hướng 4 tuần; thứ tự ưu tiên nguồn effort (trường task, git, PQA).
