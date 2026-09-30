---
title: Theo dõi tín hiệu chất lượng (QS-XX, chỉ số công ty, CPI/SPI) so với ngưỡng
source: Tín hiệu (Ch6·01)
stage: Cross-cutting
level: trung bình
prerequisites: [Ch3·01, Ch3·03]
---
# Theo dõi tín hiệu chất lượng (Signal Monitor)

## Mục tiêu học xong bạn làm được gì
- Phân biệt "tín hiệu" (signal, đo bằng số) với "checklist" (đánh Pass/Fail bằng tay) và biết mỗi thứ dùng để làm gì.
- Đọc ngưỡng đã neo trong lịch/WBS, lấy số thực tế, so sánh và gắn màu 🟢/🟡/🔴.
- Tự tính tay các tín hiệu QS-REQ-01, QS-PRC-07, E3, CPI, SPI và hiểu các chỉ số chất lượng chuẩn của công ty (Bug rate, DRE, leakage, EE, Timeliness, Process Compliance, CSS).
- Viết một "snapshot tín hiệu" có cảnh báo, xu hướng và hành động đề xuất, rồi đưa cho người ra quyết định gate.

## Khi nào dùng (thời điểm, ai kích hoạt, điều kiện đầu vào)
- PM kích hoạt khi muốn "đo chất lượng hôm nay": định kỳ (hàng tuần, theo milestone, cuối dự án) hoặc trước một gate.
- Đầu vào bắt buộc: lịch (schedule) hoặc WBS có neo tín hiệu + ngưỡng; danh sách task có effort thực tế và kế hoạch; nhật ký rủi ro đang sống; effort thực tế (từ task hoặc hệ thống PQA, hoặc PM nhập).
- Đầu vào nên có: loại hợp đồng trong charter (để chọn ngưỡng), snapshot lần trước (để tính xu hướng).
- Thiếu lịch/WBS hoặc danh sách task thì dừng, quay lại lập lịch/tách task trước; không đoán.
- Kết quả cấp cho: báo cáo tuần, gate review (người quyết go/no-go), rủi ro/issue, change request (khi đỏ kéo dài).

## Khái niệm cốt lõi (định nghĩa, thuật ngữ, vì sao quan trọng)
- Signal là "đồng hồ chất lượng": chỉ đo, không quyết. Người quyết go/no-go là gate review. Signal khác checklist (checklist là Pass/Fail thủ công).
- Nguyên tắc số liệu: thiếu dữ liệu thì ghi `[NO_DATA]`, tuyệt đối không bịa số.
- Ba nhóm chỉ số:
  - Chính (PRIMARY): các chỉ số sản xuất của công ty, theo mẫu TPL-SW-05-01 v1.7 (hiệu lực 15/04/2022).
  - Phụ: QS-XX (đề xuất bổ sung có hỗ trợ AI) và CPI/SPI (chuẩn PMI, dành cho bên liên quan quốc tế).
- Ngưỡng: LCL (giới hạn dưới), Target (mục tiêu), UCL (giới hạn trên).
- Ngưỡng phải được đọc từ kế hoạch/charter, không được hard-code ngầm. Nếu ngưỡng ở kế hoạch mâu thuẫn charter thì dừng lại hỏi, không tự ghi đè.
- Ngưỡng thay đổi theo loại hợp đồng; bảng ngưỡng mặc định còn ở trạng thái DRAFT, chờ bộ phận QA công ty xác nhận.

## Cách làm từng bước (thủ công, đủ chi tiết để làm theo; kèm input/output)
1. Chuẩn bị: mở lịch/WBS, lấy danh sách tín hiệu được neo ở milestone (lịch) hoặc gate (WBS) và ngưỡng của từng tín hiệu. Lấy loại hợp đồng trong charter. Mở snapshot lần trước nếu có.
2. Chốt phạm vi: ngày snapshot (mặc định hôm nay), phạm vi (toàn dự án / một milestone / một tín hiệu). Tùy chọn: lọc theo milestone, lọc tín hiệu, ngữ cảnh release, ngưỡng ghi đè, có kéo dữ liệu PQA hay không.
3. Kiểm tra trước khi đo:
   - Tín hiệu trong phạm vi mà không có neo trong lịch/WBS: dừng và hỏi PM.
   - Thiếu loại hợp đồng trong charter: dùng mặc định, ghi chú vào phần metadata.
   - Task nằm trong phạm vi neo mà không có trong danh sách task: đánh dấu bất thường, không tự hòa giải.
   - Thiếu nguồn dữ liệu cho từ 3 tín hiệu trở lên: cảnh báo PM thiết lập nguồn dữ liệu trước.
4. Lấy số thực tế theo nguồn:
   - QS-REQ-01, QS-REQ-03: danh sách task + ma trận truy vết.
   - QS-DSG-03: nhật ký review thiết kế cơ bản.
   - QS-DEV-cov: công cụ coverage của CI.
   - QS-PRC-07: dấu vết audit trong danh sách task.
   - QS-TST-*: báo cáo test + bug tracker.
   - E3 / EE: effort thực tế so với kế hoạch trong lịch.
   - Chỉ số chính (Bug rate, DRE, CSS...): hệ thống PQA hoặc PM nhập.
   - CPI / SPI: tính EVM từ danh sách task.
5. So sánh với ngưỡng, tính độ lệch, gắn màu (bảng bên dưới). Tính xu hướng so với snapshot trước: cải thiện (↑), xấu đi (↓), ổn định (→).
6. Viết snapshot: metadata, cảnh báo (đỏ lên đầu file, vàng thành danh sách cảnh báo), bảng trạng thái tín hiệu, bảng xu hướng, hành động đề xuất cho mỗi tín hiệu đỏ/vàng (có người phụ trách + hạn), chi tiết nguồn dữ liệu.
7. Hoàn tất: trạng thái là DRAFT, chờ PM duyệt. Hỏi PM có muốn điều tra trước khi chốt không. Chuyển kết quả cho gate review, báo cáo tuần; đỏ kéo dài thì mở rủi ro mới hoặc re-baseline qua change request.

Cách tự tính bằng tay:
- QS-REQ-01 = số task REQ review đạt / số task REQ đã review × 100% (chưa có task nào review thì `[NO_DATA]`).
- QS-PRC-07: đếm task có đủ dấu vết quy trình: có function_key + stage; có review log (với stage cần review); có PR link (với stage DEV/UT); đóng đúng workflow (không bỏ qua stage). Rồi chia cho tổng task × 100%.
- E3 = (effort thực tế − kế hoạch) / kế hoạch × 100%, với thực tế = tổng effort task hoàn thành trong tuần, kế hoạch = tổng effort task dự kiến trong tuần; kế hoạch = 0 thì `[NO_DATA]`.
- CPI/SPI xem bảng dưới.

## Công thức, ngưỡng & tín hiệu

### Quy tắc gắn màu (độ lệch so với ngưỡng)
| Tên | Điều kiện | Ngưỡng | Hành động |
|---|---|---|---|
| 🟢 | actual = threshold | khớp ngưỡng | ghi nhận |
| 🟡 | lệch 5–10% | 5–10% | đưa vào danh sách cảnh báo + hành động đề xuất |
| 🔴 | lệch > 10% | > 10% | đưa lên đầu file + hành động (người phụ trách, hạn) |

(nguồn chưa rõ: khoảng lệch 0–5% không được gán màu rõ; và "lệch %" dường như là tương đối so với ngưỡng, ví dụ QS-DEV-cov 76% vs 80% ghi "lệch −5%", QS-TST-08 7% vs 5% ghi "+40%"; ví dụ E3 = 11% vs ≤10% lại ghi 🟡.)

### Chỉ số chính của công ty (TPL-SW-05-01 v1.7)
| Chỉ số | Công thức | LCL / Target / UCL | Người phụ trách |
|---|---|---|---|
| Bug rate | Số bug nội bộ / Công số thực tế (theo rank), đơn vị Bug/MM | 3.55 / 4.57 / 8.4 | PM |
| CSS | Theo công thức khảo sát CSS nội bộ, điểm 1-100 | 80 / 90 / 100 | Sales |
| DRE | Số bug nội bộ / (Tổng bug nội bộ + Tổng bug khách hàng phát hiện) | 0.94 / 0.98 / 1.0 | PQA |
| Tỉ lệ leakage | Tổng bug sau release / Tổng công số thực tế (theo rank), Bug/mm | 0 / 0.15 / 0.3 | PQA |
| EE | (Re-estimate của dự án + Công số CR charge được KH) / Số MM sử dụng × hệ số rank, đơn vị % | 95% / 100% / 110% | PM |
| Timeliness | Số SP bàn giao đúng hạn / Tổng số SP cần bàn giao × 100% | 100% / 100% / 100% (mọi bàn giao chậm đều tính) | PM |
| Process Compliance | Tổng số điểm trung bình các item PQA audit, điểm 1-100 | 85 / 92.46 / 100 | PQA |
| Correction Rate | Công số Correction / Công số thực tế (theo rank); Correction = công số fix bug + công số verify bug | không có ngưỡng cố định | PM |
| Tỉ lệ comment code | Số comment khi review code / LOC (LOC = số dòng thay đổi, không phải tổng LOC) | không có ngưỡng cố định | TL |
| Chất lượng testcase | (Số comment nội bộ về TC + Customer feedback về TC) / Tổng số testcase | không có ngưỡng cố định | TestLead |
| Độ chính xác (dự án AI) | tùy miền AI (F1, accuracy, precision/recall), % | theo từng dự án | AI Lead / Data Scientist |

Cách đọc:
- Bug rate: < 3.55 có thể test chưa đủ kỹ; 4.57 là bình thường; > 8.4 là nghiêm trọng, cần phân tích nguyên nhân gốc.
- DRE: 1.0 = phát hiện 100% bug nội bộ; < 0.94 = khách hàng phát hiện quá nhiều bug.
- Leakage: 0 = không có bug sau release (có thể test quá chặt); 0.15 chấp nhận được (khoảng 1 bug mỗi 7 MM); > 0.3 nghiêm trọng.
- EE: < 95% effort vượt ước lượng; 100% bằng ước lượng; > 110% ước lượng dư hoặc hiệu suất đặc biệt tốt.
- Lưu ý EE: Re-estimate phải do Trưởng bộ phận phê duyệt; mẫu số tính cả BrSE JP, không tính intern; CR charge chỉ tính khi hệ số đã chốt với khách hàng và sales đã thu tiền.
- Đổi giờ công sang MM (dự án Base): MM_used = tổng [(logwork Jira − OT chưa hệ số + OT đã hệ số) × hệ số rank] / 8 / 20 (nguồn chưa rõ: dấu trừ/cộng giữa hai loại OT đúng như nguồn ghi; dự án Labor có 3 trường hợp theo (công chuẩn − lễ − nghỉ mát) so với ngày đi làm thực tế, nguồn không nêu chi tiết).
- Tần suất đo cấp dự án: Bug rate, Correction Rate, EE, comment code: hàng tuần + milestone + cuối dự án (Correction Rate: hàng tuần + milestone); CSS, DRE, Process Compliance: milestone + cuối dự án; leakage: theo từng release; Timeliness: mỗi deliverable; chất lượng testcase: milestone + sau review TC. Cấp công ty đo theo quý.
- Dự án tài liệu (dịch, tư vấn, không có phát triển): thêm Feedback rate KH = Số comment KH / page (sheet Excel + page Word/Doc), do PM phụ trách; CSS, EE, Timeliness, Process Compliance giữ công thức như trên.

### Tín hiệu QS-XX và E3
| Tín hiệu | Tên | Công thức | Ngưỡng | Hành động khi vượt |
|---|---|---|---|---|
| QS-REQ-01 | Tỉ lệ review yêu cầu đạt | reviewed_pass / total_reviewed × 100% | xem ma trận | gắn màu, cảnh báo |
| QS-REQ-03 | Độ đầy đủ truy vết | mapped_features / total_features × 100% | xem ma trận (nguồn không có hàng) | như trên |
| QS-DSG-03 | Tỉ lệ lỗi thiết kế | design_defects / total_design_items × 100% | xem ma trận | như trên |
| QS-DEV-cov | Unit test coverage | covered_lines / total_lines × 100% | xem ma trận | như trên |
| QS-PRC-07 | Tuân thủ quy trình | tasks_followed_process / total_tasks × 100% | xem ma trận | như trên |
| QS-TST-02 | Mật độ lỗi | defects / KLOC | không nêu | như trên |
| QS-TST-04 | Tỉ lệ lọt lỗi | post_release_defects / total_defects × 100% | xem ma trận | như trên |
| QS-TST-08 | Tỉ lệ reopen | reopened_bugs / total_bugs × 100% | không nêu (ví dụ dùng ≤ 5%) | như trên |
| QS-TST-09 | Độ phủ test (luồng/lỗi) | covered_flows / total_flows × 100% | không nêu | như trên |
| E3 | Chênh lệch effort | (actual − planned) / planned × 100% | mặc định ≤ 10% | vàng/đỏ theo bảng màu |

### CPI/SPI (EVM, chuẩn PMI, chỉ số phụ)
| Tên | Công thức | Ngưỡng | Hành động |
|---|---|---|---|
| EV | tổng(planned_effort × % hoàn thành) theo task | — | — |
| AC | tổng(actual_effort) theo task | — | — |
| PV | tổng(planned_effort) đến hiện tại | — | — |
| CPI | EV / AC (≥ 1 đúng/dưới ngân sách; < 1 vượt ngân sách) | mặc định ≥ 0.90 (T&M) / ≥ 0.95 (Fixed-bid) | gắn màu, cảnh báo |
| SPI | EV / PV (≥ 1 kịp/vượt tiến độ; < 1 chậm) | mặc định ≥ 0.90 (T&M) / ≥ 0.95 (Fixed-bid) | gắn màu, cảnh báo |

### Ma trận ngưỡng theo loại hợp đồng (DRAFT, chờ QA công ty xác nhận)
| Tín hiệu | Fixed-bid | T&M | Offshore | R&D | Internal | Compliance |
|---|---|---|---|---|---|---|
| QS-REQ-01 | ≥ 95% | ≥ 90% | ≥ 92% | ≥ 85% | ≥ 90% | ≥ 100% |
| QS-DSG-03 | ≤ 5% | ≤ 7% | ≤ 6% | ≤ 10% | ≤ 7% | ≤ 3% |
| QS-DEV-cov | ≥ 85% | ≥ 75% | ≥ 80% | ≥ 70% | ≥ 75% | ≥ 90% |
| QS-PRC-07 | ≥ 95% | ≥ 88% | ≥ 90% | ≥ 80% | ≥ 88% | ≥ 95% |
| QS-TST-04 | ≤ 2% | ≤ 3% | ≤ 2.5% | ≤ 5% | ≤ 3% | ≤ 1% |
| E3 | ≤ 10% | ≤ 15% | ≤ 12% | ≤ 25% | ≤ 15% | ≤ 8% |
| CPI | ≥ 0.95 | ≥ 0.90 | ≥ 0.92 | ≥ 0.85 | ≥ 0.90 | ≥ 0.95 |
| SPI | ≥ 0.95 | ≥ 0.90 | ≥ 0.92 | ≥ 0.85 | ≥ 0.90 | ≥ 0.95 |

### Đối chiếu ba hệ chỉ số
| Khái niệm | Chỉ số công ty | QS-XX | PMI |
|---|---|---|---|
| Phát hiện lỗi | DRE (0.94–1.0) | QS-TST-* | DDE / DRE |
| Lỗi sau release | leakage (≤ 0.3) | QS-TST-04 (≤ 2%) | defect leakage rate |
| Năng suất test | Bug rate (3.55–8.4) | — | Defects per KLOC |
| Hài lòng KH | CSS (80–100) | — | NPS / CSAT |
| Hiệu quả effort | EE (95–110%) | E3 (≤ 10%) | CPI (≥ 0.95) |
| Hiệu quả tiến độ | Timeliness (100%) | — | SPI (≥ 0.95) |
| Chất lượng quy trình | Process Compliance (85–100) | QS-PRC-07 (≥ 90%) | Process audit score |

(nguồn chưa rõ: ngưỡng QS-PRC-07 ≥ 90% ở bảng đối chiếu và ví dụ khác với ma trận theo loại hợp đồng, nơi Fixed-bid là ≥ 95%; ma trận dùng làm nguồn chính, còn ví dụ có thể dùng loại hợp đồng khác.)

## Template / mẫu đầu ra (rút gọn, giữ cấu trúc và các cột/trường)
Snapshot tín hiệu — tiêu đề "Signal Snapshot — <ngày giờ>":
- Bảng metadata: Project | Snapshot date (múi giờ Asia/Ho_Chi_Minh) | Scope | Previous snapshot | Status = DRAFT.
- ⚠ Alerts: 🔴 liệt kê từng tín hiệu đỏ (giá trị, ngưỡng, độ lệch); 🟡 liệt kê tín hiệu vàng.
- Signal Status: Signal | Actual | Target | Status | Trend | Source.
- Trend (so với snapshot trước): Signal | Last | Current | Delta.
- Suggested Actions: mỗi tín hiệu đỏ/vàng một mục, có Owner và Target (mốc thời gian, ví dụ "trước G4").
- Data Sources Detail: nguồn nào, đọc lúc nào, bao nhiêu task; nguồn thiếu ghi `[NO_DATA]`.

Kiểm tra sau khi lập: ngưỡng lấy từ kế hoạch/charter; chỉ số chính tham chiếu đúng bảng; thiếu số thì `[NO_DATA]`; mọi 🔴 nằm ở phần Alerts; có xu hướng nếu có snapshot trước; trạng thái DRAFT.

## Lỗi thường gặp & lesson learned
- Hard-code ngưỡng hoặc ghi đè ngầm ngưỡng khi kế hoạch và charter lệch nhau -> kết quả không bảo vệ được trước gate -> luôn đọc ngưỡng từ kế hoạch/charter, có mâu thuẫn thì dừng hỏi.
- Bịa số khi thiếu nguồn -> quyết định gate dựa trên dữ liệu giả -> ghi `[NO_DATA]`.
- Nhầm signal với checklist -> trộn hai loại đánh giá -> signal chỉ đo, checklist Pass/Fail riêng, cả hai đưa vào gate review.
- Coi signal là quyết định go/no-go -> vượt quyền -> chỉ đo, để gate review quyết.
- Tính "comment code" theo tổng LOC -> sai mẫu số -> dùng số dòng thay đổi.
- Tính EE mà không kiểm tra re-estimate đã được duyệt, hay không loại intern/đưa BrSE JP vào đúng -> EE lệch -> theo các "ghi chú quan trọng" ở trên.
- Đỏ kéo dài mà không hành động -> lệch chất lượng tích lũy -> mở rủi ro mới hoặc re-baseline qua change request.
- Bug rate thấp hơn LCL được hiểu là tốt -> bỏ qua khả năng test chưa kỹ -> xem nó là dấu hiệu cần kiểm tra.

## Ví dụ minh họa
Dựa trên ví dụ trong nguồn (dự án ẩn danh <tên-dự-án>, snapshot 2026-08-26):
- QS-REQ-01 = 96% so với ≥ 95% -> 🟢.
- QS-DEV-cov = 76% so với ≥ 80% -> 🔴 (nguồn ghi lệch −5%; tuần trước 72% -> ↑ +4%). Hành động: đội dev bổ sung unit test module Release, người phụ trách Dev Lead, hạn trước G4.
- QS-TST-08 = 7% so với ≤ 5% (lệch +40%) -> 🔴.
- E3 = 11% so với ≤ 10% -> 🟡; tuần trước 9% nên xấu đi +2%.
- Bug rate: `[NO_DATA]` vì chờ PQA, mục tiêu 4.57 Bug/MM.

(nguồn chưa rõ: ví dụ của nguồn ghi 2 tín hiệu đỏ và 1 vàng, phù hợp quy tắc màu; độ lệch −5% của 76 vs 80 nằm sát ranh giới vàng/đỏ mà vẫn gắn 🔴.)

## Tự kiểm tra
1. Signal khác checklist ở điểm nào? Đáp: signal là số đo tự động/định lượng, chỉ đo không quyết; checklist là Pass/Fail thủ công; gate review quyết.
2. Bug rate 9.1 Bug/MM, ngưỡng 3.55/4.57/8.4 nói gì? Đáp: vượt UCL 8.4, mức nghiêm trọng, phải phân tích nguyên nhân gốc.
3. Tính DRE nếu 49 bug nội bộ và 1 bug do khách hàng tìm ra. Đáp: 49 / (49 + 1) = 0.98 (bằng Target).
4. Độ lệch bao nhiêu thì 🟡 và bao nhiêu thì 🔴? Đáp: 5–10% là 🟡, > 10% là 🔴, đúng ngưỡng là 🟢.
5. Thiếu số liệu coverage từ CI thì ghi gì? Đáp: `[NO_DATA]`, không được ước lượng.

## Liên quan
- Nguồn ngưỡng (trước): Lập schedule (Ch3·03), wbs, Release plan (Ch8·01), Project plan (Ch2·02).
- Sau: Gate review (Ch8·02) (quyết gate), Status tuần (Ch7·01) (mục tín hiệu), Rủi ro & issue (Ch4·04) (đỏ kéo dài -> rủi ro), Change request (Ch4·03) (re-baseline).
- Song song / bổ sung: Checklist (Ch6·02) (checklist, không phải signal), Effort actuals (Ch6·03) (đào sâu E3/EE), hypercare (leakage), Giao tiếp stakeholder (Ch7·03) (CSS), Lessons learned (Ch9·01).
