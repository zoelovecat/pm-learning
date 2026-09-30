---
title: Ghép người với việc (Team Match) - chọn ứng viên và phân công task theo tải thực tế
source: Xếp người (Ch3·05)
stage: Planning
level: trung bình
prerequisites: [Ch2·01, Ch3·03]
---
# Ghép người với việc (Team Match)

## Mục tiêu học xong bạn làm được gì
- Chấm điểm và xếp hạng ứng viên cho 1 task/role theo 3 tiêu chí: kỹ năng, mức rảnh, năng lực.
- Tính được "mức rảnh" (availability) của từng thành viên từ số ticket đang làm.
- Phân công cả 1 backlog cho nhiều người mà không làm ai quá tải (greedy, one_per_member, balanced).
- Biết khi nào dữ liệu là suy đoán (proxy) và phải ghi rõ để người duyệt kiểm lại.
- Nhận ra các cảnh báo: xung đột dự án khác, trần tham gia (participation) thấp hơn effort, task không ai nhận được.

## Khi nào dùng (thời điểm, ai kích hoạt, điều kiện đầu vào)
- Thời điểm: giai đoạn lập kế hoạch (sau khi có lịch/timeline và danh sách task), lúc kickoff cần điền tên vào vai trò, khi sprint planning, và khi một change request cần thêm nguồn lực.
- Người kích hoạt: PM.
- Ba tình huống:

| Tình huống | Cách làm | Ghi chú |
|---|---|---|
| Có cả list task cần phân công | Chế độ batch (phân công hàng loạt) | Sprint planning: `one_per_member` hoặc `balanced`; backlog 5-20 task ưu tiên người rảnh: `greedy` |
| Chỉ 1 task/role khó, cần so sánh nhiều người | Chế độ single (top N ứng viên) | Mặc định top N = 10 |
| Chưa có task, chỉ cần dựng team theo vai trò | `team_compose` (khai báo danh sách role) | Có thêm ma trận xung đột giữa các role |

- Đầu vào bắt buộc (single): hồ sơ kỹ năng (tên kỹ năng + level tối thiểu), timeline (start..end), effort % cần, dự án nguồn nhân sự.
- Đầu vào bắt buộc (batch): danh sách task (>= 1, mỗi task có id + title), dự án, khóa dự án bên công cụ ticket, timeline chung.
- Thiếu đầu vào bắt buộc thì dừng lại, không đoán.

## Khái niệm cốt lõi
- **Candidate pool (nhóm ứng viên)**: chỉ gồm thành viên đã thuộc dự án, không tìm rộng ra cả đơn vị.
- **Availability (mức rảnh)**: % thời gian còn có thể nhận việc, suy từ số ticket đang mở của người đó.
- **Participation rate (trần tham gia)**: % thời gian người đó được phân bổ cho dự án (ví dụ 50 hoặc 100). Mức rảnh ban đầu không được vượt trần này.
- **Level L1-L5**: thang năng lực. Khi không có dữ liệu kỹ năng thật, suy từ chức danh (job title proxy) và luôn gắn nhãn `[PROXY]`.
- **Competency (năng lực chuẩn hóa)**: level quy về 0-1 (tuyến tính hoặc senior-weighted).
- **Role fit**: vai trò của người có khớp loại việc không (dev, QA, PM, BrSE).
- **Greedy / one_per_member / balanced**: ba chính sách gán việc hàng loạt (xem dưới).
- **Cảnh báo, không tự loại**: nhiều xung đột chỉ được đánh dấu để PM quyết; kết quả luôn là DRAFT, PM chọn.
- Nhãn nguồn dữ liệu dùng trong bản kết quả: 📄 từ tài liệu, 📋 quy tắc công ty, 💭 PM xác nhận, 🤖 giả định, 🌐 dữ liệu hệ thống trực tiếp, ⏳ chưa có.

## Cách làm từng bước (thủ công, đủ chi tiết để làm theo; input/output)

### A. Single: chọn người cho 1 task
1. Khai hồ sơ kỹ năng, ví dụ React L4, TypeScript L3, cùng timeline và effort %. Kiểm tên kỹ năng có nằm trong danh mục kỹ năng chuẩn của tổ chức; không khớp thì chọn tên gần nhất.
2. Lập danh sách ứng viên = toàn bộ thành viên dự án. Loại người nằm trong danh sách loại trừ; nếu có lọc phòng ban thì giữ đúng phòng ban.
3. Với từng người, thu hồ sơ: tên, tên Jira, phòng ban, vai trò (LTV, PM, PQA, BrSE...), chức danh, participation rate, ngày bắt đầu/kết thúc phân bổ.
4. Xác định level: dùng kỹ năng thật nếu có; không có thì suy từ chức danh (bảng "Job title -> level" bên dưới), ghi `[PROXY]`.
5. Tính mức rảnh: đếm ticket đang mở của người đó (trạng thái không phải Done/Resolved/Closed, cập nhật trong 90 ngày gần nhất), trừ theo bảng bên dưới.
6. Tính điểm: `score = w_skill x skill_match + w_avail x avail_norm + w_comp x competency_norm`.
7. Lọc: loại người có `avail_pct < effort_pct` hoặc `score < 0.5`; ghi cảnh báo xung đột.
8. Xuất bảng xếp hạng + phân tích điểm từng người + cảnh báo, trạng thái DRAFT. PM chọn người rồi tự cập nhật cột Assignee trong lịch.

### B. Batch: phân công cả backlog
1. Xác nhận đủ đầu vào; bỏ task đã Done/Cancelled.
2. Lập "trạng thái nguồn lực" mỗi thành viên: vai trò, chức danh, participation rate, ...
3. Mức rảnh ban đầu:
   - `jira_avail_pct = max(0, 100 - jira_load)`
   - `initial_avail_pct = min(jira_avail_pct, participation_rate)`; `remain_avail_pct = initial_avail_pct` (trừ dần khi gán việc).
   - Truy vấn ticket: người được gán, trạng thái không phải Done/Resolved/Closed, cập nhật trong 90 ngày, thuộc dự án. Bỏ dự án lọc để tìm xung đột chéo dự án (chỉ cảnh báo, không trừ mức rảnh).
4. Làm giàu task: suy `role_hint` (xem bảng), quy đổi effort sang % (`effort_pct_equiv = effort_md x 10`; 1 md xấp xỉ 10% trong sprint 2 tuần, sprint 1 tuần PM có thể dùng 8). Thiếu effort thì mặc định 1 md hoặc hỏi PM.
5. Sắp xếp task: priority (high -> low), rồi effort_md giảm dần, rồi id tăng dần.
6. Với mỗi task: lọc người đủ điều kiện (role_fit >= 0.2, `remain_avail_pct >= effort_pct_equiv`, không bị loại trừ; với `one_per_member` thêm điều kiện chưa có task nào). Chấm `assign_score`, chọn người cao nhất (hòa: remain_avail cao hơn, ít task hơn). Gán, trừ `remain_avail`. Không ai đủ điều kiện thì đưa vào danh sách chưa gán kèm lý do (thiếu rảnh / đã có 1 task / lệch vai trò).
7. Xuất: bảng gán theo task, kế hoạch theo từng thành viên, danh sách chưa gán, cảnh báo, hành động cho PM. Trạng thái DRAFT.

### Suy role từ task (batch)
Ưu tiên 1: cột Stage. Ưu tiên 2: từ khóa trong title/description (không phân biệt hoa thường). Mâu thuẫn thì ghi chú và ưu tiên Stage.

| Stage | role_hint |
|---|---|
| REQ, BD | BA |
| DEV, UT | LTV |
| TC, TE, BV | PQA |
| PM-*, COMM | PM |

| Từ khóa | role_hint |
|---|---|
| react, frontend, ui, màn hình, screen, vite, mui; api, nestjs, backend, endpoint, database | LTV |
| test, testcase, qa, bug verify | PQA |
| pm, kickoff, stakeholder, schedule | PM |
| brse, bridge, khách hàng, spec review | BrSE |

## Công thức, ngưỡng & tín hiệu (bảng: tên | công thức/điều kiện | ngưỡng | hành động khi vượt; không có thì ghi "Không có")

| Tên | Công thức / điều kiện | Ngưỡng | Hành động |
|---|---|---|---|
| skill_match | `avg(min(level_actual / level_required, 1.0))` trên từng kỹ năng trong hồ sơ | - | Đầu vào của score |
| avail_norm | `avail_pct / 100` | - | Đầu vào của score |
| competency_norm | `avg(skill_level / 5)` trên các kỹ năng khớp | - | Đầu vào của score |
| Score single | `w_skill x skill_match + w_avail x avail_norm + w_comp x competency_norm` | Trọng số mặc định 0.5 / 0.3 / 0.2 | `score < 0.5` loại (cảnh báo nếu còn < 5 người) |
| Loại vì thiếu rảnh | `avail_pct < effort_pct` | - | Loại |
| Cảnh báo quá ít | Số người đạt sau lọc | < 5 | Cảnh báo PM |
| avail_pct | `max(0, 100 - sum(load_deductions))` | - | Xem bảng trừ tải |
| Timeestimate | nếu có `timeestimate` (giây): `load_pct += min(50, total_estimate_hours x 5)` | Trần cộng 50 | Cộng tải, "cap trước khi trừ" |
| Xung đột chéo dự án | Ticket đang mở, cùng người, `duedate` chồng lên `[start, end]`, không lọc dự án | - | Đánh dấu Conflicts, không tự loại |
| Trần tham gia thấp | `participation_rate < effort_pct` | - | Đánh dấu Conflicts, không tự loại |
| Thiếu tên Jira | Không có `jira_name` | - | Cảnh báo; PM ước lượng mức rảnh hoặc loại (dự phòng: phần trước `@` của email) |
| Role fit lệch | Ví dụ PQA cho task DEV | role_fit 0.2 | Vẫn xếp hạng, ghi cảnh báo; chỉ loại khi score < 0.5 (single) |
| Score batch | `assign_score = w_role x role_fit + w_avail x avail_fit + w_level x level_fit` | Trọng số mặc định 0.35 / 0.45 / 0.20 | Gán người cao nhất |
| avail_fit | `remain_avail_pct / 100` | `remain_avail_pct < effort_pct_equiv` | Không đủ điều kiện |
| level_fit | `min(proxy_level / expect_level, 1.0)` | - | Đầu vào |
| Balanced | `adjusted_score = assign_score - 0.05 x count(assigned_tasks)` | - | Trải nhẹ, vẫn cho >1 task nếu điểm cao |
| Quy đổi effort | `effort_pct_equiv = effort_md x 10` | 1 md xấp xỉ 10% (sprint 2 tuần) | Sprint 1 tuần: PM đặt 8 |

**Bảng trừ tải theo trạng thái ticket (mỗi ticket)**

| Trạng thái | Trừ |
|---|---|
| In Progress / In Review / Testing | -25% |
| To Do / Open có duedate nằm trong timeline | -15% |
| Confirmming / chờ khách hàng | -10% |

**Trọng số gợi ý cho single**

| Bối cảnh | skill | avail | comp |
|---|---|---|---|
| Kỹ thuật khó | 0.6 | 0.2 | 0.2 |
| Gấp, cần người rảnh | 0.3 | 0.5 | 0.2 |
| Cần senior dẫn dắt | 0.4 | 0.2 | 0.4 |
| Chuẩn | 0.5 | 0.3 | 0.2 |

**Competency**: tuyến tính L1=0.2, L2=0.4, L3=0.6, L4=0.8, L5=1.0. Senior-weighted: L1=0.1, L2=0.25, L3=0.45, L4=0.7, L5=1.0.

**role_fit (batch)**: role_hint thuộc vai trò của người = 1.0; task dev + chức danh có Software Engineer = 0.85; task QA + PQA = 1.0; task PM + PM = 1.0; task BrSE + BrSE = 1.0; lệch = 0.2.

**level_fit (batch)**: task có từ "senior", "lead", "architecture" kỳ vọng L4+; task dev mặc định L3; "junior", "support", "fix nhỏ" kỳ vọng L2.

**Job title -> level (proxy)**: khớp theo mã chức danh, dự phòng theo tên (chứa chuỗi, không phân biệt hoa thường).

| Mã / tên | Level | competency (tuyến tính) |
|---|---|---|
| DEV1, Fresher | L1 | 0.2 |
| DEV2, Junior | L2 | 0.4 |
| DEV3, Middle | L3 | 0.6 |
| DEV4, Senior | L4 | 0.8 |
| DEV5, Expert/Principal | L5 | 1.0 |
| BSE1-BSE2 (Fresher/Junior Bridge) | L2 | 0.4 |
| BSE3 (Middle Bridge) | L3 | 0.6 |
| BSE4+ (Senior Bridge) | L4 | 0.8 |
| PM1-PM2, Project Manager, Junior PM | L3 | 0.6 |
| PM3+, Senior Project Manager | L4 | 0.8 |
| PQA1, Fresher PQA | L2 | 0.4 |
| PQA2+, Middle/Senior PQA | L3-L4 | 0.6-0.8 |
| Không khớp | L2 (mặc định dev) | 0.4 |

Khi dùng proxy, mọi kỹ năng trong hồ sơ dùng chung 1 level: `level_actual = job_title_proxy_level`. Gợi ý vai trò theo loại task: Dev/Frontend/Backend -> LTV; PM/điều phối -> PM; QA -> PQA hoặc LTV có kỹ năng test; BrSE/bridge -> BrSE. Lệch vai trò chỉ ghi chú.

**Ba chính sách gán (batch)**

| Chính sách | Hành vi | Khi dùng |
|---|---|---|
| `greedy` (mặc định) | 1 người nhận nhiều task nếu `remain_avail` còn đủ | Backlog nhỏ, ưu tiên người rảnh nhất |
| `one_per_member` | Tối đa 1 task/người trong đợt gán | Muốn trải đều; task thừa vào danh sách chưa gán, gợi ý tăng nhân sự, giảm effort hoặc chuyển greedy |
| `balanced` | Greedy có phạt -0.05 mỗi task đã gán | Trải nhẹ |

Ràng buộc: 1 task = 1 assignee chính; task phụ thuộc (Depends on) chỉ ghi chú, chưa xử lý thứ tự; tổng effort gán vượt participation cap thì cảnh báo.

## Template / mẫu đầu ra (rút gọn, giữ cấu trúc, cột, trường)

**Single: "Team Match - <Task ID> (<Role>) - DRAFT"**
- Bảng thông tin: Generated | Task ID/Role | Dự án | Khóa Jira | Timeline | Effort | Skill required | Department filter | Exclude | Weights | Candidate pool (vd 12 -> 7 đạt) | Status: DRAFT - PM chọn.
- Top Candidates: `Rank | User ID | Name | Score | Skill % | Avail % | Comp | Dept | Note`.
- Score breakdown: mỗi người 1 dòng công thức thay số.
- Conflicts & Warnings; Data sources (mỗi ứng viên: skills / avail / profile lấy từ đâu, gắn `[PROXY]` nếu suy từ chức danh); Action - PM chọn.

**Batch: "Task Assign Suggest - <tên-dự-án> - DRAFT"**
- Bảng thông tin: Project | Jira | Timeline | Tasks in | Assigned | Unassigned | Policy | Weights.
- Assign by task: `Task | Title | Role | Suggest | Score | Avail trước/sau | Note`.
- Plan by member: mỗi người 1 khối (Jira avail initial, Ksystem cap tức participation, Assigned effort, Remain) + bảng `Task | Effort | Score`.
- Unassigned/Backlog: `Task | Lý do`.
- Conflicts & Warnings; Action - PM (duyệt, cập nhật lịch/assignee, chạy lại sau khi cân bằng tải).

**Team_compose (danh sách role)**: mỗi dòng `role | skills | level | effort | timeline`, ví dụ BA L4 50%, Tech Lead L5 30%, Dev x3 L3-L4 80%. Kết quả: top N mỗi role + ma trận xung đột giữa các role (1 người không được chồng 2 role).

**Checklist sau khi lập**
- [ ] Tên kỹ năng đã kiểm với danh mục; dự án đã xác định
- [ ] Ứng viên = thành viên dự án, duyệt hết các trang dữ liệu
- [ ] Level ghi `[PROXY]` nếu suy từ chức danh
- [ ] Mức rảnh tính cho từng người; participation_rate so với tổng effort đã gán
- [ ] Trọng số ghi trong kết quả; có phân tích điểm từng người
- [ ] Có mục Conflicts nếu chồng lịch; cảnh báo nếu < 5 người đạt
- [ ] Task chưa gán đều có lý do; trạng thái DRAFT; không tự sửa lịch chính thức

## Lỗi thường gặp & lesson learned (sai gì -> hậu quả -> cách tránh)
- Dùng level suy từ chức danh như thể là năng lực thật -> chọn nhầm người -> luôn ghi `[PROXY]` và để PM xác nhận level.
- Bỏ qua trần participation (ví dụ cap 50% mà effort 80%) -> gán quá tải trên giấy -> lấy `min(jira_avail, participation_rate)`, cảnh báo khi effort > cap, điều chỉnh phân bổ nguồn lực.
- Truy vấn ticket dùng trạng thái không tồn tại (ví dụ `Cancelled`, `Deployed`) -> truy vấn lỗi -> chỉ dùng `NOT IN (Done, Resolved, Closed)` hoặc bỏ trạng thái không có.
- Thành viên chưa gắn tên Jira -> không tính được mức rảnh -> PM map tay hoặc loại.
- Dùng `one_per_member` khi thiếu người cùng vai trò -> nhiều task chưa gán -> thêm thành viên vào dự án hoặc đổi sang `greedy`.
- Tin điểm số tuyệt đối -> bỏ qua ngữ cảnh -> điểm chỉ là gợi ý DRAFT; PM quyết và tự cập nhật lịch/ticket.
- 0 người đạt -> do quá tải ticket -> cân lại ticket, giảm effort, hoặc chờ người rảnh.
- Chỉ chạy 1 lần rồi để đó -> tải thay đổi -> chạy lại khi tải Jira đổi nhiều; so `remain_avail` với thực tế ở standup.

## Ví dụ minh họa (ngắn, có số; dựng thì ghi "(ví dụ dựng)")
(ví dụ dựng, theo mẫu nguồn) Task T-005 "React Frontend Dev", effort 80%, yêu cầu React L4, TypeScript L3.
- Người A: 1 ticket In Progress -> trừ 25% -> `avail_pct = 75`. Vì 75 < 80 nên bị loại (`avail_pct < effort_pct`). Điều này minh họa quy tắc loại.
- Người B: không có ticket đang mở -> `avail_pct = 100`; giả sử skill_match = 0.90, competency = 0.75: `score = 0.5 x 0.90 + 0.3 x 1.00 + 0.2 x 0.75 = 0.45 + 0.30 + 0.15 = 0.90`. Đạt ngưỡng 0.5.

(ví dụ dựng, batch) Người C cap 50%, Jira avail 100 -> `initial = min(100, 50) = 50`. T-005 3 md -> 30%; còn 20%. T-006 2 md -> 20%: đủ, còn 0. Với `greedy` C nhận cả hai; với `one_per_member` T-006 chuyển cho người khác hoặc vào danh sách chưa gán.

## Tự kiểm tra (3-5 câu hỏi, đáp án ngắn ngay dưới)
1. Công thức score single và trọng số mặc định?
   Đáp án: `w_skill x skill_match + w_avail x avail_norm + w_comp x competency_norm`; 0.5 / 0.3 / 0.2.
2. Người có 1 ticket In Progress và 2 ticket To Do (duedate trong timeline) còn rảnh bao nhiêu?
   Đáp án: 100 - 25 - 15 - 15 = 45%.
3. Cap participation 50%, Jira avail 100%; task 4 md thì còn rảnh bao nhiêu sau khi gán?
   Đáp án: initial 50; 4 md = 40% -> còn 10%.
4. Khi nào dùng `one_per_member` và rủi ro của nó?
   Đáp án: muốn mỗi người tối đa 1 task mới; rủi ro là task thừa không ai nhận.
5. Vì sao phải ghi `[PROXY]`?
   Đáp án: level suy từ chức danh, không phải kỹ năng đã đo; cần PM xác nhận.

## Liên quan (bài trước/sau)
- Trước: Lập lịch (timeline), Sinh danh sách task từ spec, Kickoff và RACI.
- Sau: Sprint planning (gắn task đã có người vào sprint), Cập nhật lịch với assignee, Change request khi cần thêm người, Dự báo năng lực (capacity).

**Ghi chú nguồn chưa rõ**
- (nguồn chưa rõ: trọng số single 0.5/0.3/0.2 và batch 0.35/0.45/0.20 khác nhau có chủ đích; nguồn ghi batch "ưu tiên availability như PM yêu cầu".)
- (nguồn chưa rõ: "cap trước khi trừ" của `timeestimate` không nói `load_pct` cộng vào đâu trong công thức `avail_pct`; hiểu là cộng vào tổng tải.)
- (nguồn chưa rõ: mẫu nguồn ghi `0.5x1.00 + 0.3x0.90 + 0.2x0.80 = 0.92` nhưng phép tính đúng ra 0.93; có thể do làm tròn hoặc số liệu khác.)
- (nguồn chưa rõ: role_fit >= 0.2 làm điều kiện đủ điều kiện, trong khi role lệch cũng đã bằng 0.2 nên thực tế không loại ai vì vai trò.)
- (nguồn chưa rõ: PQA2+ nêu L3-L4 mà không nói tiêu chí phân Middle hay Senior.)
