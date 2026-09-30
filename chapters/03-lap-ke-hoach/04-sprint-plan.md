---
title: Lập sprint backlog - chọn task theo ưu tiên và capacity
source: Sprint plan (Ch3·04)
stage: Planning
level: cơ bản
prerequisites: [Ch3·02, Ch3·03]
---
# Lập sprint backlog - chọn task theo ưu tiên và capacity

## Mục tiêu học xong bạn làm được gì
- Chọn được tập task cho một sprint từ task list: lọc, sắp theo ưu tiên, xếp vừa capacity từng vai trò.
- Tính utilization theo vai trò và phân loại OVER / WARN / OK.
- Dùng velocity của sprint trước để kiểm tra độ hợp lý của lượng task chọn.
- Gán vai trò (không gán người) cho từng task và ghi danh sách task bị loại kèm lý do.

## Khi nào dùng (thời điểm, ai kích hoạt, điều kiện đầu vào)
- Thời điểm: đầu mỗi sprint (planning), sau khi đã có task list, WBS và (nếu có) lịch tổng.
- Người kích hoạt: PM.
- Đầu vào bắt buộc: task list (có priority + effort, còn task chưa Done); WBS (phase/WP/milestone để nhóm task); số thứ tự sprint; capacity từng vai trò (md/sprint) do PM cung cấp.
- Tùy chọn: ngày bắt đầu sprint (mặc định ngày làm việc kế tiếp sau sprint trước); độ dài sprint (mặc định 2 tuần = 10 ngày làm việc); velocity của sprint trước (không có thì bỏ qua kiểm velocity); mục tiêu sprint (PM tự viết; chưa có thì ghi TBD); lịch tổng (nếu có thì đọc sprint window đã lập).
- Thiếu task list hoặc WBS thì dừng, làm bước tách task và lập lịch trước.

## Khái niệm cốt lõi (định nghĩa, thuật ngữ, vì sao quan trọng)
- **Sprint backlog**: tập task đã cam kết cho một sprint.
- **Capacity theo vai trò**: số md mỗi vai trò (Dev, BA, QA, PM) làm được trong sprint - do PM cung cấp, không do công cụ tự đoán.
- **Committed effort**: tổng effort các task được gán cho vai trò đó trong sprint.
- **Utilization**: tỉ lệ committed / capacity.
- **Velocity**: khối lượng thực tế làm xong ở sprint trước; dùng làm "thước" để nhận biết chọn quá nhiều/quá ít.
- **Sprint goal**: 1-2 câu ngắn, do PM định nghĩa, chép nguyên văn, không diễn đạt lại.
- Chỉ gán *vai trò*, không gán tên người; gán người là bước sau (xem Xếp người, Ch3·05).

## Cách làm từng bước (thủ công, đủ chi tiết để làm theo; kèm input/output)
1. **Kiểm tra đầu vào.** Tổng số task chưa Done, phân bổ theo priority (High/Medium/Low), số task thiếu estimate; các phase/WP hoạt động trong khoảng sprint; sprint window trong lịch nếu có. Xác nhận với PM.
2. **Thu thập lựa chọn:** số sprint (NN), ngày bắt đầu, độ dài (mặc định 2 tuần = 10 ngày làm việc); capacity theo vai trò (Dev, BA, QA, PM, đơn vị md); velocity sprint trước; sprint goal.
3. **Chọn task:**
   1. Lọc task có trạng thái khác Done.
   2. Sắp theo priority: High -> Medium -> Low; cùng priority thì sắp theo Task ID.
   3. Cộng dồn effort theo vai trò; dừng khi vai trò chạm giới hạn capacity.
   4. Task vượt capacity đánh dấu OVER - không tự bỏ qua, phải hỏi PM: cắt task / tăng capacity / dời sang sprint sau.
   5. Nếu có velocity: so tổng effort đã chọn với velocity, lệch > 20% thì cảnh báo và hỏi PM xác nhận trước khi tiếp.
4. **Gán vai trò.** Nếu task list đã có field Role hoặc Stage thì dùng trực tiếp; thiếu thì suy theo stage:

| Stage | Vai trò mặc định |
|---|---|
| REQ, BD | BA |
| DEV, UT | Dev |
| TC, TE, BV | QA |
| PM-*, COMM | PM |

   Task đa stage (ví dụ DEV+UT cùng task): chia effort theo tỉ lệ và ghi cả hai vai trò. Đánh dấu rõ role đọc từ task list hay do bạn suy luận.
5. **Lập tài liệu sprint** (`sprint-NN`, NN 2 chữ số, ví dụ `sprint-01`): bảng Capacity Summary, Sprint Backlog, Excluded Tasks; sprint goal chép nguyên văn từ PM; không ghi đè sprint đã tồn tại khi chưa hỏi PM.
6. **Bàn giao DRAFT.** Nêu tóm tắt capacity, task bị cắt, vai trò gần giới hạn; chạy checklist; gợi ý bước gán người.

## Công thức, ngưỡng & tín hiệu
Velocity:
```
velocity_actual   = tổng effort task hoàn thành trong sprint trước (md)
velocity_planned  = tổng effort task committed đầu sprint trước (md)
velocity_ratio    = velocity_actual / velocity_planned
Cảnh báo nếu |effort_selected - velocity_actual| / velocity_actual > 20%
```
Capacity:
```
capacity_available(role) = capacity_per_role(role)   [md, PM cung cấp]
effort_committed(role)   = Σ effort các task gán cho role đó trong sprint
utilization(role)        = effort_committed(role) / capacity_available(role) × 100%
```

| Trạng thái | Điều kiện | Hành động |
|---|---|---|
| OVER | utilization > 100% | Dừng, hỏi PM: cắt task / tăng capacity / kéo sang sprint sau |
| WARN | utilization >= 90% | Đánh dấu cảnh báo, tiếp tục |
| OK | utilization < 90% | Bình thường |
| Velocity check | lệch > 20% so với velocity_actual | Cảnh báo, PM xác nhận |

Mặc định: sort ưu tiên High -> Medium -> Low -> Task ID; ngưỡng quá tải 100% capacity; cảnh báo gần giới hạn >= 90%.

## Template / mẫu đầu ra (rút gọn, giữ cấu trúc và các cột/trường)
```
# Sprint NN — <Project> (<CODE>) (DRAFT)
Trường: Sprint | Start Date | End Date | Duration (10 ngày làm việc) | Status DRAFT
## Sprint Goal   (chép nguyên văn từ PM; chưa có thì TBD)
## 1. Capacity Summary: Role | Capacity (md) | Committed (md) | Utilization | Status
## 2. Sprint Backlog: Task ID | Title | Phase | Stage | WP | Effort (md) | Role | Priority | Status
## 3. Excluded Tasks (over capacity / deferred): Task ID | Title | Effort (md) | Reason
```
Checklist: đã đọc task list + WBS; số sprint/độ dài/capacity đã PM xác nhận; không còn OVER; role đã có nguồn (task list) hoặc suy luận và PM xác nhận; sprint goal rõ (hoặc TBD); mọi task bị loại có lý do; DRAFT; đã gợi ý bước gán người.

## Lỗi thường gặp & lesson learned (lấy từ nguồn, mỗi ý: sai gì -> hậu quả -> cách tránh)
- Tự bỏ task khi vượt capacity mà không hỏi PM -> mất quyết định ưu tiên của PM -> đánh dấu OVER, hỏi PM.
- Chọn sprint vượt capacity vai trò (kể cả khi tổng đội "đủ") -> một vai trò quá tải -> tính utilization theo từng vai trò.
- Bỏ qua velocity khi có số liệu -> cam kết quá tay hoặc quá nhẹ -> đối chiếu, lệch > 20% thì xác nhận.
- Tự viết/paraphrase sprint goal -> lệch ý PM -> chép nguyên văn, hoặc để TBD.
- Gán tên người thay vì vai trò trong bước này -> lẫn vai trò -> chỉ gán vai trò.
- Task đa stage gán một vai trò duy nhất -> tải các vai trò sai -> chia effort theo tỉ lệ, ghi cả hai vai trò.
- Không liệt kê task bị loại -> mất dấu công việc bị dồn -> luôn có bảng Excluded kèm lý do.
- (nguồn chưa rõ: `velocity_ratio` được định nghĩa nhưng không dùng trong ngưỡng nào; phép kiểm 20% dùng `velocity_actual`.)
- (nguồn chưa rõ: utilization đúng 100% được xếp WARN vì >= 90%; OVER chỉ khi > 100%.)
- (nguồn chưa rõ: cách chia tỉ lệ effort cho task đa stage không được nêu.)

## Ví dụ minh họa (1 ví dụ ngắn có số, lấy hoặc dựng từ nguồn; nếu dựng thì ghi "(ví dụ dựng)")
Từ mẫu nguồn: capacity Dev 20 md, committed 18 -> 90% (WARN); BA 10 / 8 -> 80% (OK); QA 10 / 9 -> 90% (WARN); PM 5 / 4 -> 80% (OK). Task `T-010 F-KM-05 DEV` (3.0 md) không vừa capacity Dev -> loại, lý do "Dev over capacity, dời sprint sau". (ví dụ dựng) Velocity sprint trước = 40 md; sprint này chọn 50 md -> lệch |50-40|/40 = 25% > 20% -> cảnh báo, PM phải xác nhận.

## Tự kiểm tra (3-5 câu hỏi có đáp án ngắn ngay dưới, dựa trên chính nội dung bài)
1. Vai trò Dev có capacity 20 md, committed 19 md - trạng thái gì?
   - 95% >= 90% -> WARN (chưa OVER).
2. Sprint mặc định dài bao nhiêu?
   - 2 tuần = 10 ngày làm việc.
3. Thứ tự chọn task?
   - High -> Medium -> Low; cùng priority theo Task ID.
4. Khi nào cảnh báo velocity?
   - Khi |effort_selected - velocity_actual| / velocity_actual > 20%.
5. Task stage TC, TE, BV mặc định gán cho vai trò nào?
   - QA.

## Liên quan (bài trước/sau trong quy trình, tên thư mục skill khác)
- Trước: Spec thành task (Ch3·02), WBS (Ch3·01), Lập schedule (Ch3·03).
- Sau: Xếp người (Ch3·05) (gán người cụ thể); theo dõi hằng ngày (Daily sync, Ch4·01); báo cáo tuần (Status tuần, Ch7·01); sprint retro.
