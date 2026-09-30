---
title: Lập schedule - timeline, buffer, capacity và neo tín hiệu
source: Lập schedule (Ch3·03)
stage: Planning
level: trung bình
prerequisites: [Ch3·01, Ch3·02]
---
# Lập schedule - timeline, buffer, capacity và neo tín hiệu

## Mục tiêu học xong bạn làm được gì
- Từ task list và WBS dựng được lịch: ngày bắt đầu/kết thúc từng task, dependency, đường găng (critical path), milestone.
- Chọn được buffer % theo loại hợp đồng và áp lên đường găng.
- Ước lượng effort cho task thiếu estimate bằng bảng heuristic, và biết phải xin PM xác nhận.
- Kiểm tra capacity theo tuần, nhận ra tuần quá tải hoặc thừa tải, và biết các phương án xử lý.
- Re-baseline lịch đúng cách khi có change request được duyệt.

## Khi nào dùng (thời điểm, ai kích hoạt, điều kiện đầu vào)
- Thời điểm: sau khi có task list (đã có Est) và WBS; trước khi phân công người và lập sprint.
- Người kích hoạt: PM.
- Đầu vào bắt buộc: task list (có effort hoặc ước lượng được); WBS (phase, milestone, tín hiệu neo); charter (contract type, target go-live); ngày bắt đầu (PM cung cấp).
- Tùy chọn: kiểm tra ngưỡng NFR trong thuộc tính chất lượng của SRS.
- Thiếu task list hoặc WBS thì dừng, làm bước tách task và WBS trước.

## Khái niệm cốt lõi (định nghĩa, thuật ngữ, vì sao quan trọng)
- **Effort unit**: mặc định `md` (man-day); PM có thể chọn `mh` với 1md = 8mh.
- **Critical path (đường găng)**: chuỗi task dài nhất quyết định ngày kết thúc; buffer áp lên chuỗi này.
- **Buffer %**: dự phòng cộng thêm trên đường găng, phụ thuộc loại hợp đồng.
- **Baseline**: bản lịch được duyệt và "đóng băng"; các thay đổi sau đó so với bản này.
- **Capacity**: khả năng của nhóm theo tuần (md), so với effort kế hoạch để ra utilization.
- Tín hiệu neo của milestone lấy từ WBS, không tự định nghĩa ở bước lập lịch.
- Mặc định: 5 ngày làm việc/tuần, lịch nghỉ lễ VN, múi giờ UTC+7. (Nguồn ghi lịch nghỉ theo từng công ty là kế hoạch tương lai.)
- Lịch này không gán người cụ thể (bài Xếp người, Ch3·05) và không tính chi phí.

## Cách làm từng bước (thủ công, đủ chi tiết để làm theo; kèm input/output)
1. **Kiểm tra đủ dữ liệu.** Đếm số task, tổng effort hiện có, task thiếu estimate; liệt kê milestone và tín hiệu từ WBS. Xác nhận với PM.
2. **Hỏi PM các lựa chọn** theo 4 cụm: Timeline (`start_date`, số ngày làm việc/tuần, lịch nghỉ lễ); Effort (đơn vị md/mh, có đồng ý dùng heuristic cho task thiếu estimate không); Buffer (mặc định theo contract type, có ghi đè không); Tín hiệu (xác nhận ngưỡng từ WBS).
3. **Điền effort thiếu.** Task đã có effort trong task list thì dùng trực tiếp. Thiếu thì dùng bảng heuristic (dưới) **sau khi PM xác nhận**, và đánh dấu là giả định. Heuristic cũ (REQ:1, BD:2, DEV:3) đã bị bỏ (deprecated).
4. **Dựng lịch.**
   - Nhóm task theo phase/WP của WBS.
   - Đặt dependency: ưu tiên cột `Depends on` của task list; không có thì suy theo chuỗi stage (dưới).
   - Tính forward pass: early start / early finish theo lịch làm việc.
   - Cộng buffer % lên đường găng theo contract type.
   - Ngày milestone = late finish của task cuối phase; tín hiệu đọc từ WBS.
   - Nếu dependency trong task list mâu thuẫn với chuỗi stage: dừng và hỏi PM.
5. **Kiểm capacity.** Lấy dự báo headcount/capacity của đơn vị theo tuần, so với effort kế hoạch: tô nổi tuần utilization > 100% hoặc < 50%. Tuần quá tải: chọn hướng xử lý trước khi chốt (kéo dài timeline / thêm người / thuê ngoài). Không có dữ liệu capacity tự động thì PM nhập thủ công và đánh dấu TBD.
6. **Bàn giao DRAFT v1.** Nêu tóm tắt đường găng, các tuần quá tải; chạy checklist; gợi ý bước phân công người theo vai trò.
7. **Re-baseline khi có CR duyệt:** lưu bản cũ vào kho lưu trữ với tên `schedule-v{N}-YYYYMMDD` (N tăng dần, ví dụ `schedule-v1-2026-09-15`), ghi baseline mới vào file lịch chính, ghi chênh lệch phiên bản trong hồ sơ CR. PM duyệt v1 thì đóng băng baseline; v2 so sánh với bản đã lưu.

## Công thức, ngưỡng & tín hiệu
Heuristic effort (Q4.2, iron law: task <= 1md):

| Stage | Mặc định (md) | Tách nếu > 1md |
|---|---|---|
| REQ | 0.5 | Theo AC |
| BD | S=0.5 / M=1 / L=1.5 | Theo screen state / theo dependency |
| DEV | S=0.5 / M=1 / L=1.5 | Theo API / theo component |
| UT | 0.5 | Theo function |
| TC | 0.5-1 | Theo nhóm scenario |
| TE | 0.5-1 | Theo mỗi vòng trên mỗi module |
| BV | 0.5 | Theo cycle |
| TP/TVP/TR | 1 mỗi loại | Theo module |
| PM-* | tùy loại: PM-KICKOFF 2, PM-PLAN 3, PM-TRACK 0.5/tuần, PM-GATE 1/gate | |
| COMM | 0.5/tuần | Chi phí giao tiếp |

Buffer % theo loại hợp đồng (nguồn ghi DRAFT, chờ QA nội bộ xác nhận):

| Contract Type | Buffer % |
|---|---|
| Fixed-bid | 15% |
| T&M | 10% |
| Offshore | 20% |
| R&D | 25% |
| Internal | 10% |
| Compliance | 20% |

Lý do (nguồn): Fixed-bid rủi ro scope creep cao; T&M tính tiền theo thực tế; Offshore tốn chi phí giao tiếp; R&D bất định.

Dependency: (1) mỗi function: REQ -> BD -> DEV -> UT -> chuỗi test module; (2) mỗi module test: TP -> TVP -> TC -> TE (sau mọi DEV của module) -> BV -> TR; (3) PM-GATE phụ thuộc DEV + test của module, PM-TRACK xuyên suốt.

Capacity: `Utilization = Planned (md) / SBU Capacity`; cảnh báo khi > 100% (OVER) hoặc < 50% (UNDER). (Công thức Utilization là suy ra từ cột Planned/Capacity/Utilization trong mẫu nguồn, giải thích thêm.)

Tín hiệu neo dự phòng khi WBS thiếu: SRS Approved: QS-REQ-01 >= 95% / QS-REQ-03 = 100%; Basic Design Approved: QS-DSG-03 <= 5%; Code Complete: QS-DEV-cov >= 80% / QS-PRC-07 >= 90%; System Test Done: QS-TST-02 <= baseline; UAT Sign-off: QS-TST-08 <= 5% / QS-TST-04 <= 2%; Go-live: QS-PRC-07 >= 90%; hằng tuần: E3 <= 10%.

## Template / mẫu đầu ra (rút gọn, giữ cấu trúc và các cột/trường)
```
# Schedule — <Project> (<CODE>) (DRAFT v1)
Trường: Project Code | Start Date | Target Go-live | Effort Unit | Buffer (vd 15% Fixed-bid) | Total Effort | Status
## 1. Milestone & Signal Anchor: # | Milestone | Date | Phase | Signal | Threshold | Owner role   (+ Weekly: E3 <= 10%)
## 2. Task Schedule: Task ID | Title | Phase | Stage | WP | Effort | Start | End | Depends | Role | Status
## 3. Critical Path: tổng ngày làm việc (không slack) + buffer = tổng sau buffer
## 4. Capacity Check: Week | Planned (md) | Capacity | Utilization | Status (OVER / UNDER)
## 5. Roles Summary: Role | Total effort (md) | Min FTE (avg)
```
Checklist: đã đọc task list + WBS + charter; mọi task có effort hoặc heuristic đã PM xác nhận; ngày milestone và tín hiệu khớp WBS; đường găng và buffer được ghi lại; tuần lệch capacity được đánh dấu; DRAFT v1; nếu có CR thì có đường dẫn archive.

## Lỗi thường gặp & lesson learned (lấy từ nguồn, mỗi ý: sai gì -> hậu quả -> cách tránh)
- Dùng heuristic cũ REQ:1, BD:2, DEV:3 -> task vượt 1md, trễ dồn -> dùng bảng Q4.2, task <= 1md.
- Áp heuristic effort mà không hỏi PM -> con số không có chủ -> luôn xin xác nhận và đánh dấu giả định.
- Tự định nghĩa tín hiệu ở bước lập lịch -> lệch WBS -> chỉ đọc từ WBS; chỉ dùng bảng dự phòng khi WBS thiếu.
- Bỏ qua mâu thuẫn dependency task list vs chuỗi stage -> lịch sai -> dừng, hỏi PM.
- Không kiểm capacity hoặc bỏ qua tuần OVER -> đội quá tải, trễ -> chọn hướng xử lý (kéo timeline, thêm người, thuê ngoài) trước khi chốt.
- Sửa đè lịch cũ khi có CR -> mất baseline để so sánh -> archive bản cũ theo quy ước tên, ghi chênh lệch trong CR.
- Gán người cụ thể vào lịch -> lẫn vai trò -> chỉ ghi vai trò, phân công người là bước sau.
- (nguồn chưa rõ: các tỉ lệ buffer ghi DRAFT chờ QA xác nhận; chưa rõ bằng công thức nào cộng buffer lên đường găng - ví dụ nguồn: 65 ngày + 10 ngày = 75 với buffer 15%, tức làm tròn 9.75 -> 10 (suy luận).)
- (nguồn chưa rõ: cột "Min FTE (avg)" không nêu công thức; ví dụ 65 md -> 3.0 FTE.)

## Ví dụ minh họa (1 ví dụ ngắn có số, lấy hoặc dựng từ nguồn; nếu dựng thì ghi "(ví dụ dựng)")
Từ mẫu nguồn: dự án Fixed-bid, buffer 15%, tổng effort 145 md. Đường găng 65 ngày làm việc (không slack) + buffer 10 ngày = 75 ngày. Capacity tuần 2026-W25: kế hoạch 35 md, capacity 30 md -> utilization 117% (OVER) -> PM phải chọn: kéo dài timeline / thêm người / thuê ngoài. Role Dev: 65 md tổng, Min FTE 3.0. Milestone M2 SRS Approved (2026-06-17) neo QS-REQ-01 >= 95%.

## Tự kiểm tra (3-5 câu hỏi có đáp án ngắn ngay dưới, dựa trên chính nội dung bài)
1. Buffer mặc định cho hợp đồng Fixed-bid, R&D và Internal?
   - 15%, 25%, 10%.
2. Tuần nào bị gắn cờ về capacity?
   - Utilization > 100% hoặc < 50%.
3. Effort mặc định của PM-KICKOFF, PM-PLAN, PM-TRACK, PM-GATE?
   - 2; 3; 0.5/tuần; 1/gate.
4. Ngày milestone được tính thế nào?
   - Late finish của task cuối phase; tín hiệu đọc từ WBS.
5. Khi có CR được duyệt cần làm gì với lịch cũ?
   - Lưu bản cũ theo quy ước `schedule-v{N}-YYYYMMDD`, ghi baseline mới, ghi chênh lệch trong hồ sơ CR.

## Liên quan (bài trước/sau trong quy trình, tên thư mục skill khác)
- Trước: WBS (Ch3·01), Spec thành task (Ch3·02).
- Sau: Xếp người (Ch3·05) (gán người theo vai trò + timeline), Sprint plan (Ch3·04); theo dõi tiến độ vs kế hoạch (Status tuần, Ch7·01); change request (re-baseline); theo dõi tín hiệu (Tín hiệu, Ch6·01).
