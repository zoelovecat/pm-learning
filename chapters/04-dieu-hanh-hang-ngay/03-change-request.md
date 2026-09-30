---
title: Xử lý Change Request (CR) - từ diff spec đến quyết định
source: Change request (Ch4·03)
stage: Development
level: trung bình
prerequisites: [Ch4·04]
---
# Xử lý Change Request (CR) - từ diff spec đến quyết định

## Mục tiêu học xong bạn làm được gì
- Phân loại một yêu cầu thay đổi thành 1 trong 6 loại CR và biết trọng tâm phân tích của từng loại.
- So sánh spec trước/sau để ra danh sách task NEW / REMOVED / MODIFIED kèm effort.
- Phân tích tác động theo 5 chiều (lịch, effort/chi phí, rủi ro, chất lượng, nguồn lực), xếp mức nghiêm trọng theo ma trận và đề xuất APPROVE / DEFER / REJECT có điều kiện.
- Lập tài liệu CR để sponsor ký, và biết việc phải làm SAU khi được duyệt (re-baseline) - và việc TUYỆT ĐỐI không làm trước khi được duyệt.

## Khi nào dùng (thời điểm, ai kích hoạt, điều kiện đầu vào)
- Khi khách hàng (hoặc nội bộ) đề nghị thay đổi spec/phạm vi/kỹ thuật/lịch/chất lượng/nguồn lực/chính sách sau khi đã có baseline.
- PM kích hoạt. Kết quả là bản nháp để sponsor duyệt; PM **không tự duyệt**.
- Đầu vào bắt buộc (thiếu thì dừng, không đoán; gợi ý làm bước thượng nguồn):
  - Phiên bản spec **trước** (mã commit hoặc bản chụp) - nếu thiếu thì PM cung cấp.
  - Phiên bản spec **sau** (spec hiện tại).
  - Danh sách tính năng (SRS phần 4 + kết quả diff) - thượng nguồn: Spec thành task (Ch3·02).
  - Baseline lịch (`schedule.md`) - thượng nguồn: Lập schedule (Ch3·03).
  - Loại hợp đồng (trong charter) - thượng nguồn: Kickoff (Ch2·01).
- Đầu vào tùy chọn: bảng giá theo người-ngày (rate card; chưa có nguồn tự động, PM nhập tay), lý do/mô tả CR, giá trị nghiệp vụ (ảnh hưởng quyết định DEFER hay APPROVE), cờ re-baseline.

## Khái niệm cốt lõi (định nghĩa, thuật ngữ, vì sao quan trọng)
- **Change Request (CR)**: yêu cầu thay đổi chính thức đối với baseline. Nếu không đo tác động và không có chữ ký thì thay đổi trôi vào dự án âm thầm (scope creep) và ăn vào lịch/lợi nhuận.
- **Baseline**: bản kế hoạch đã chốt (lịch, phạm vi) dùng làm mốc so sánh.
- **Re-baseline**: chốt lại kế hoạch sau khi CR được duyệt. Quyết định theo từng CR: làm ngay (`--rebaseline-now`) hoặc xếp hàng (`--queue`; mặc định nếu PM bỏ qua là xếp hàng).
- **Feature ID**: quy ước `F-<PROJ>-<MOD>-NN` để đánh số tính năng khi phân tích tác động.
- **md**: người-ngày (man-day) - đơn vị effort trong ma trận.
- **6 loại CR**:

  | Loại | Kích hoạt | Trọng tâm |
  |---|---|---|
  | Scope | khách thêm/bớt tính năng | diff danh sách tính năng - tác động lớn nhất |
  | Tech | đổi stack/kiến trúc | làm lại thiết kế + phát triển |
  | Schedule | khách dời deadline | re-baseline lịch |
  | Quality | ngưỡng chất lượng thay đổi | tiêu chí cổng + theo dõi tín hiệu |
  | Resource | nghỉ việc / mở rộng | ghép người (Xếp người, Ch3·05) + năng lực |
  | Customer | thay đổi chính sách | mẫu tuân thủ (compliance) |
- **Loại hợp đồng quyết định cách tính tiền**: Fixed-bid - ghi rõ khách chịu chi phí hay công ty chịu (ảnh hưởng biên lợi nhuận); T&M - nhân effort với đơn giá.

## Cách làm từng bước (thủ công, đủ chi tiết để làm theo; kèm input/output)
1. **Xác nhận baseline.** Input: spec trước/sau, lịch, charter. Trích: loại hợp đồng, ngày mốc (milestone) trong baseline, danh sách tính năng hiện có. Output: tóm tắt (spec trước/sau, loại hợp đồng, số milestone) -> xác nhận với chính mình/PM trước khi tiếp.
2. **Thu thập thông tin CR.** Bắt buộc: mã CR (đề xuất `CR-<NN>`), loại CR (scope/tech/schedule/quality/resource/customer), người yêu cầu (khách/nội bộ + đầu mối nếu có), mô tả 1-2 dòng gồm lý do, spec trước/sau. Tùy chọn: rate card, giá trị nghiệp vụ, cờ re-baseline (mặc định xếp hàng).
3. **Diff spec.**
   - CR loại Scope hoặc Tech: so sánh spec, liệt kê task NEW / REMOVED / MODIFIED kèm effort (dùng công cụ diff của bài tách task).
   - CR Schedule/Quality/Resource/Customer: diff ngữ cảnh nếu có, tập trung vào chiều tương ứng.
   - Xác nhận bảng task delta với PM trước khi phân tích; không âm thầm "tự cho khớp".
4. **Phân tích tác động 5 chiều** (checklist ở mục Công thức):
   - *Lịch*: chạy thử lịch với task list mới (chỉ so sánh, **chưa ghi** vào lịch chính), so ngày từng milestone baseline vs mới, gắn cờ nếu go-live trượt.
   - *Effort/Chi phí*: cộng effort delta từ diff; T&M nhân đơn giá; Fixed-bid ghi khách hấp thụ hay ảnh hưởng biên lợi nhuận.
   - *Rủi ro*: rủi ro mới do thay đổi; rủi ro hiện có đổi mức không; sau khi duyệt đưa vào sổ risk.
   - *Chất lượng*: tín hiệu bị ảnh hưởng (ví dụ scope tăng -> QS-REQ-03 truy vết yêu cầu, QS-DEV-cov độ phủ), nguồn tham khảo từ theo dõi tín hiệu nếu có dữ liệu.
   - *Nguồn lực*: vai trò/kỹ năng mới cần -> gợi ý ghép người theo mã task.
   - Xác nhận các giả định (đơn giá, chính sách khách) với PM.
5. **Xếp mức nghiêm trọng** bằng ma trận (bên dưới) và **đề xuất quyết định** theo bảng heuristic; ghi rõ điều kiện.
6. **Lập tài liệu CR** theo mẫu, trạng thái "DRAFT - pending sponsor approval"; ghi trường Re-baseline (`queue`/`now`).
7. **Dừng và bàn giao.** In tóm tắt diff + tác động + đề xuất, chạy checklist. **Không sửa lịch** trước khi sponsor ký, không tự commit.
8. **Sau khi duyệt (chỉ khi có chữ ký thật)**: re-baseline (xem mục dưới).

### Re-baseline sau khi duyệt
1. Lưu bản lịch cũ thành `schedule.v<N>.md`.
2. Chạy lại bước lập lịch với task list mới.
3. Cập nhật ngày go-live mục tiêu trong charter nếu trượt.
4. Đưa rủi ro phát sinh vào sổ risk (xem bài Rủi ro & issue, Ch4·04).
5. Kiểm lại phạm vi kế hoạch phát hành nếu CR ảnh hưởng.
Quy ước đánh version lịch: `schedule.v1`, `schedule.v2` do PM duy trì. Báo cáo tuần nêu CR đang chờ/đã duyệt. Có thể giữ sổ CR chung `INDEX.md` gồm: CR ID | Type | Severity | Status | Date | Sponsor decision.

## Công thức, ngưỡng & tín hiệu (bảng: tên | công thức/điều kiện | ngưỡng | hành động khi vượt)
**Ma trận mức nghiêm trọng**

| Mức | Chênh lệch lịch | Chênh lệch effort | Chênh lệch chi phí |
|---|---|---|---|
| Trivial | 0 ngày | < 1 md | < $500 |
| Low | 1-3 ngày | 1-5 md | $500-$2k |
| Medium | 4-10 ngày | 5-15 md | $2k-$10k |
| High | 11-30 ngày | 15-40 md | $10k-$50k |
| Critical | > 30 ngày | > 40 md | > $50k |

**Heuristic quyết định**

| Mức | Giá trị nghiệp vụ | Đề xuất |
|---|---|---|
| Trivial / Low | rõ (bất kỳ mức rõ ràng) | APPROVE |
| Medium | rõ | APPROVE (kèm điều kiện) |
| High | Critical | APPROVE (kèm re-plan) |
| High | không rõ | DEFER |
| Critical | vượt ngân sách | REJECT (thương lượng lại phạm vi) |

**Checklist 5 chiều tác động**
- Lịch: milestone baseline vs mới - go-live có trượt không?
- Effort/Chi phí: tổng delta x đơn giá (Fixed-bid vs T&M).
- Rủi ro: rủi ro mới + rủi ro cũ đổi mức.
- Chất lượng: QS-REQ-03 (truy vết), QS-DEV-cov (độ phủ, ví dụ cần thêm UT để giữ >= 80%), các tín hiệu cổng.
- Nguồn lực: vai trò/kỹ năng mới.

Công thức chi phí (T&M): chi phí delta = effort delta (md) x đơn giá (ví dụ mẫu $400/md).

## Template / mẫu đầu ra (rút gọn, giữ cấu trúc và các cột/trường)
```
# Change Request - CR-<NN> - DRAFT
(Chú giải nguồn dữ liệu)
| Field | Value |  CR ID | Project | Date Raised | Type | Requester | Description | Re-baseline (queue/now) | Status (DRAFT - pending sponsor approval)
## 1. Spec Diff
### Before  - danh sách tính năng, tổng effort kế hoạch
### After (proposed) - tính năng cũ + tính năng mới (NEW), tổng effort mới (+delta)
### Task Delta | Task | Status (NEW/REMOVED/MODIFIED) | Effort | Phase |  ... Total
## 2. Impact Analysis
### Schedule Impact | Milestone | Baseline | New | Delta |
### Effort/Cost Impact - effort delta, Severity, cost delta @ đơn giá (nếu T&M)
### Risk Impact | Risk | Level | Change |
### Quality Impact - tín hiệu bị ảnh hưởng
### Resource Impact - vai trò mới, task cần ghép người
## 3. Severity  (mức + lý do ngắn)
## 4. Recommended Decision (APPROVE/DEFER/REJECT + điều kiện + việc re-plan sau duyệt dạng checkbox)
## 5. Sponsor Approval | Role | Name | Decision | Sign Date | Note |   (Customer PIC / Sponsor / PM - để trống, chờ ký)
## 6. If Rejected - Alternative  (ví dụ dời tính năng sang phase 2 để giữ go-live baseline)
```
Checklist sau khi lập: mọi trường bắt buộc có nguồn; task delta đã xác nhận với PM; mức nghiêm trọng khớp ma trận; quyết định có điều kiện rõ; lịch chưa bị sửa trước khi sponsor ký; trạng thái DRAFT; không commit.

## Lỗi thường gặp & lesson learned (lấy từ nguồn, mỗi ý: sai gì -> hậu quả -> cách tránh)
- Sửa lịch chính ngay khi nhận CR -> lịch không còn khớp với hợp đồng/ chữ ký -> chỉ chạy thử để so sánh; ghi lịch chỉ sau khi sponsor ký.
- Tự đoán spec trước hoặc loại hợp đồng khi thiếu -> phân tích sai gốc -> dừng, xin mã commit/bản chụp và đọc charter.
- Không xác nhận task delta với PM -> effort lệch được đẩy sang bước sau -> xác nhận bảng delta trước khi phân tích.
- Bỏ qua chiều chất lượng (truy vết, độ phủ test) -> tính năng mới không có test/trace -> luôn kiểm QS-REQ-03 và QS-DEV-cov.
- Quên đưa rủi ro phát sinh vào sổ risk sau khi duyệt -> rủi ro không có người theo dõi -> sau duyệt cập nhật sổ risk (bài Rủi ro & issue, Ch4·04).
- Không ghi phương án thay thế khi bị từ chối -> khách không thấy lựa chọn -> luôn có mục "If Rejected - Alternative" (ví dụ dời sang phase 2).
- Nhầm loại hợp đồng khi tính chi phí -> áp đơn giá cho hợp đồng Fixed-bid (không tính thêm tiền) -> đọc loại hợp đồng trước khi tính; Fixed-bid ghi rõ ai chịu.

## Ví dụ minh họa (1 ví dụ ngắn có số, lấy hoặc dựng từ nguồn; nếu dựng thì ghi "(ví dụ dựng)")
Ví dụ trong nguồn (CR-003, loại Scope, khách yêu cầu thêm xuất báo cáo Excel và dashboard PDF):
- Trước: F-KM-01..F-KM-06 (6 tính năng), tổng effort kế hoạch 145md. Sau: thêm F-KM-07 (xuất Excel), F-KM-08 (xuất PDF), tổng 165md (+20md). Task delta: 10 task mới, 20md.
- Lịch: milestone M6 Go-live từ 2026-09-30 sang 2026-10-10 (+7 ngày).
- Chi phí: +20md; ở đơn giá $400/md (nếu T&M) = $8,000. Rủi ro mới R-010 (Medium). Chất lượng: 2 tính năng mới cần truy vết QS-REQ-03; cần thêm UT để giữ QS-DEV-cov >= 80%. Nguồn lực: 1 BE Dev.
- Nguồn kết luận mức **MEDIUM** (trượt 7 ngày, +20md) và đề xuất **APPROVE with conditions**: (1) khách chấp nhận chi phí + go-live trượt; (2) xác nhận có BE Dev. Nếu bị từ chối: dời F-KM-07/08 sang phase 2, giữ go-live baseline.
- Quan sát cho người học: theo ma trận, +7 ngày và $8,000 nằm ở Medium, nhưng +20md nằm ở khung High (15-40 md). Nguồn kết luận Medium mà không nói cách tổng hợp nhiều chiều (xem mục nguồn chưa rõ).

## Tự kiểm tra (3-5 câu hỏi có đáp án ngắn ngay dưới, dựa trên chính nội dung bài)
1. Bạn nhận CR loại Schedule. Có sửa file lịch ngay không?
   - Không. Chỉ chạy thử để so sánh; chỉ re-baseline sau khi sponsor ký.
2. Theo ma trận, CR trượt 12 ngày là mức nào và nếu giá trị nghiệp vụ không rõ thì đề xuất gì?
   - High (11-30 ngày); giá trị không rõ -> DEFER.
3. Kể 5 chiều phân tích tác động.
   - Lịch, effort/chi phí, rủi ro, chất lượng, nguồn lực.
4. Việc phải làm sau khi CR được duyệt (re-baseline)?
   - Lưu lịch cũ thành schedule.v<N>, lập lịch lại, cập nhật go-live trong charter nếu trượt, đưa rủi ro vào sổ, kiểm lại phạm vi phát hành.
5. Feature ID dùng quy ước nào?
   - `F-<PROJ>-<MOD>-NN`.

## Liên quan (bài trước/sau trong quy trình, tên thư mục skill khác)
- Trước: Kickoff (Ch2·01) (charter, loại hợp đồng), Lập schedule (Ch3·03) (baseline lịch), Spec thành task (Ch3·02) (diff task).
- Sau: Lập schedule (Ch3·03) (re-baseline), Xếp người (Ch3·05) (nguồn lực mới), Rủi ro & issue (Ch4·04) (rủi ro phát sinh; quan hệ hai chiều với rủi ro Scope/Estimate hiện thực hóa), Release plan (Ch8·01) (phạm vi phát hành), Status tuần (Ch7·01) (CR trong báo cáo tuần), `monitor-signal` (nguồn tác động chất lượng).
- Nguồn chưa rõ / mâu thuẫn:
  - Ma trận không nêu cách chọn mức khi các cột lệch nhau (ví dụ mẫu: lịch/chi phí Medium nhưng effort +20md nằm khung High mà kết luận Medium). Cách tổng hợp (lấy mức cao nhất hay ưu tiên cột nào) chưa được nói.
  - Bảng heuristic quyết định không phủ hết mọi tổ hợp (ví dụ Medium mà giá trị không rõ; Critical mà ngân sách chưa vượt; Trivial/Low mà giá trị không rõ); dòng "Trivial/Low - Any clear" chưa giải thích rõ.
  - Ngưỡng dùng đơn vị tiền "$" mà nguồn không nói có áp cho mọi hợp đồng/tiền tệ.
  - Nguồn tự ghi 5 câu hỏi mở chưa chốt: mẫu CR chuẩn của công ty (trường bắt buộc), ngưỡng severity có hợp lý cho đa số dự án, đơn giá lấy từ charter/hợp đồng/hệ thống, gộp re-baseline theo lô hay theo từng CR, quy trình từ chối có cần lý do để kiểm toán với khách. Do đó ma trận và heuristic nên hiểu là quy ước hiện hành, chưa phải chuẩn cuối.
