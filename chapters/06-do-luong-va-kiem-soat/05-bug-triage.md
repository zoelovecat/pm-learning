---
title: Báo cáo phân loại bug (Bug Triage Report)
source: Bug triage (Ch6·05)
stage: Testing
level: trung bình
prerequisites: []
---
# Báo cáo phân loại bug (Bug Triage Report)

## Mục tiêu học xong bạn làm được gì
- Lấy toàn bộ danh sách bug của dự án, loại bug đã Rejected, gom theo module và đếm Open/Closed.
- Phân biệt được "bug thật" với "spec gap" (khoảng trống đặc tả: spec thiếu hoặc mơ hồ nên dev không có căn cứ), và biết cách chuyển spec gap từ Bug sang Improvement đúng thứ tự, có comment giải thích.
- Phân nhóm bug thật theo 6 category và viết được 1 câu root cause cho mỗi nhóm.
- Đánh giá chất lượng cổng QA qua tỉ lệ bug khách hàng (bug lọt sang nghiệm thu) và kiểm tra tuân thủ quy trình (thiếu trường bắt buộc, gán sai người theo trạng thái).
- Lập báo cáo triage 8 phần cho buổi họp, có mũi tên xu hướng so với lần trước, và đề xuất hành động cho PM.

## Khi nào dùng (thời điểm, ai kích hoạt, điều kiện đầu vào)
- PM muốn rà bug list, phân loại issue, hoặc chuẩn bị họp bug triage (giữa dự án, trước release, hoặc khi thấy bug tồn đọng nhiều).
- Đầu vào: quyền truy cập Jira của dự án (project key), thư mục spec/tài liệu yêu cầu của dự án (nếu có; không có thì chỉ phân tích sơ bộ), và (nếu có) số liệu của lần triage trước để so xu hướng.

## Khái niệm cốt lõi (định nghĩa, thuật ngữ, vì sao quan trọng)
- **Working set**: tập bug sau khi loại `Rejected`. Rejected chỉ đếm số lượng, không đưa vào bất kỳ phân tích nào (module, category, customer, compliance).
- **Open** = `To Do`, `In Progress`, `Confirmming`, `Feedback`. **Closed** = `Done`, `Resolved`, `Deployed`. (Nguồn ghi "Confirmming" đúng như vậy, có vẻ là tên trạng thái trong Jira của dự án.)
- **Spec gap**: hành vi bị báo là "bug" nhưng spec không định nghĩa hoặc dùng ngôn ngữ mơ hồ; dev làm theo cách hiểu hợp lý nên không thể coi là lỗi code. Xử lý: chuyển Bug -> Improvement và yêu cầu BA bổ sung spec.
- **Genuine bug**: spec định nghĩa rõ, hành vi thực tế khác spec.
- **Bug khách hàng** và **bug nội bộ**: dựa trên trường "QC Activity" (trong Jira của nguồn bị gõ sai thành "QC Acitivity"): giá trị `Acceptant Test` = bug khách hàng (lọt sang giai đoạn nghiệm thu); mọi giá trị khác hoặc rỗng = bug nội bộ.
- **Vai trò người được gán** (role) suy từ tên hiển thị: chứa `.QA)` = QA, chứa `.DEV)` = DEV.
- Vì sao quan trọng: nếu báo cáo trên dữ liệu thiếu hoặc lẫn Rejected, số liệu sai; nếu chuyển spec gap mà không kiểm tra spec, bạn đổ oan cho BA hoặc bỏ sót lỗi thật; nếu bỏ qua tuân thủ quy trình, bug đóng mà không có nguyên nhân/phạm vi ảnh hưởng thì không học được gì.

## Cách làm từng bước (thủ công, đủ chi tiết để làm theo; kèm input/output)
1. **Lấy toàn bộ bug.** Lọc theo project, loại issue Bug (và Improvement nếu cần), sắp theo ngày tạo giảm dần. Mỗi trang tối đa 50; nếu tổng > 50 phải lấy hết các trang, đến khi số đã lấy = tổng. Tuyệt đối không báo cáo trên dữ liệu một phần.
   - Trường cần lấy: summary, status, priority, issuetype, components, labels, assignee, updated, issuelinks, QC Activity, Bug Category, Cause Category, Severity, "Nguyên nhân gây ra bug", "Phạm vi ảnh hưởng của bug". Giá trị rỗng giữ nguyên là rỗng, không tự điền.
   - Tách 2 nhóm: Rejected (chỉ đếm) và working set. Ghi: `Total fetched N / Rejected R / Working set N-R`.
2. **Gom theo module** (áp thứ tự ưu tiên, dừng ở mức đầu tiên cho ra module rõ ràng):
   1. Labels mô tả module/màn hình (bỏ qua nhãn chung như bug, regression, QA);
   2. Issue links (relates to / is caused by) nếu rõ ràng ngụ ý module;
   3. Đọc toàn bộ tiêu đề, mọi cặp ngoặc vuông, chọn miền chính (ví dụ `[Edit Datasets][List Datasets][List Charts]` -> module Datasets; `[Data Panel][Tables - Add Wizard]` -> Data Panel - Tables; `[Dashboard][Filter][Date Range]` -> Dashboard - Filters);
   4. Tiền tố ngoặc đầu (ví dụ `[APPT-xxx]` -> APPT, `[AUTH]` -> AUTH);
   5. Trường Components (cuối cùng).
   Đếm Total/Open/Closed cho từng module; module có 0 Open là tín hiệu tích cực, nên nêu riêng.
3. **Phân tích spec gap (chỉ bug Open).**
   - Trước hết kiểm tra có đường dẫn spec không. Nếu không có, hỏi PM: cung cấp path (phân tích đầy đủ, `analysis_mode = full`) hay chấp nhận phân tích sơ bộ từ nội dung bug (`preliminary`, độ chính xác thấp hơn; mọi kết quả gắn nhãn "Preliminary (no spec read)").
   - Sàng lọc từ tiêu đề: tín hiệu spec gap = "thiếu"/missing, rate-limit không được nhắc, thiếu option/enum, rule validation chưa định nghĩa, "appropriate behavior" chưa định nghĩa. Tín hiệu bug thật = sai dữ liệu, sai tính toán, tính năng không chạy, crash, lỗi mapping dữ liệu.
   - Ở chế độ full: đọc spec của feature liên quan, tìm BR/AC (business rule / acceptance criteria) bao phủ hành vi bị báo. Spec rõ -> Genuine Bug (giữ Bug). Spec thiếu/mơ hồ -> Spec Gap (ứng viên Improvement). Trích nguyên văn BR/AC bị thiếu hoặc mơ hồ.
   - Đầu ra: danh sách ứng viên (key, summary, BR/AC thiếu, độ tin cậy: `high` nếu đã đọc spec, `low` nếu sơ bộ) + danh sách bug Open kèm nhãn phân loại.
4. **Phân nhóm bug thật** (chỉ genuine bug đang Open) vào 6 category (bảng ở mục dưới). Mỗi category xác định Top Module (module có nhiều bug nhất trong category) và 1 câu root cause (gom theo nguyên nhân, không giải thích từng bug). Sau đó quay lại bảng module điền cột "Top Category" (category nhiều bug nhất của mỗi module).
5. **Xu hướng.** Nếu có số liệu lần chạy trước, hiển thị `giá trị hiện tại + delta có dấu` (ví dụ `45 ↑3`). Không có lịch sử thì bỏ mũi tên.
6. **Phân tích bug khách hàng vs nội bộ** (bỏ hẳn phần này nếu có 0 bug khách hàng): tính số và % bug khách hàng trên working set, bảng Severity (Critical/High/Medium/Low), và 1-2 câu đánh giá chất lượng QA.
7. **Kiểm tra tuân thủ quy trình** trên toàn bộ working set: (a) thiếu 4 trường bắt buộc; (b) vi phạm trạng thái-người được gán (chi tiết ở bảng dưới). Bỏ phần này nếu 0 vi phạm.
8. **Trình bày báo cáo cho PM và DỪNG chờ phản hồi.** Hỏi rõ: "Có muốn chuyển các issue spec gap từ Bug sang Improvement không?". Chỉ sau khi PM phản hồi mới chuyển đổi và mới làm bản HTML.
9. **Chuyển đổi (khi PM đồng ý):** với từng spec gap được duyệt, thêm comment Jira TRƯỚC, rồi mới đổi issue type sang Improvement. Không bao giờ đảo thứ tự.
10. **Lưu số liệu lần chạy** để lần sau so xu hướng (sau khi PM xác nhận đã đọc báo cáo): date, total, open, closed, rejected, spec_gap_count, customer_bugs, compliance_violations, số open/closed theo module.
11. **(Tùy chọn) Xuất báo cáo HTML** sau khi PM đã phản hồi, dù PM chọn chuyển hay không. Điền hết mọi ô, không để sót chỗ trống chưa điền.

Thứ tự báo cáo gửi PM: 1) KPI Summary (total, open, closed, rejected, kèm xu hướng); 2) Thống kê theo module (có cột Top Category); 3) Category breakdown; 4) Customer vs Internal (bỏ nếu 0 bug khách hàng); 5) Danh sách hành động cho bug Open thật; 6) Vấn đề tuân thủ (chỉ khi có); 7) Spec gap chờ PM quyết; 8) Khuyến nghị cho PM theo mức ưu tiên.

## Công thức, ngưỡng & tín hiệu (bảng: tên | công thức/điều kiện | ngưỡng | hành động khi vượt)
| Tên | Công thức/điều kiện | Ngưỡng | Hành động |
|---|---|---|---|
| Phân trang | Tổng > 50 | > 50 | Lấy tiếp các trang (0, 50, 100...) đến khi đã lấy = tổng |
| Working set | Tổng - Rejected | - | Chỉ dùng tập này cho bước 2-7 |
| Bug khách hàng | QC Activity = `Acceptant Test` | bất kỳ | Có bug khách hàng thì thêm phần Customer vs Internal |
| Tỉ lệ bug khách hàng cao | % bug khách hàng / working set | > 30% kèm Critical/High | Kết luận cổng QA trước release chưa đủ |
| Tỉ lệ bug khách hàng thấp | như trên | < 10% và chỉ Medium/Low | Ghi nhận cổng QA hiệu quả |
| Done + QA | status = Done và người được gán là QA | vi phạm | Cờ: "Closed Done với QA assignee - expect DEV" |
| Deployed + DEV | status = Deployed và người được gán là DEV | vi phạm | Cờ: "DEV assigned at Deployed - needs QA verification" |
| Resolved + DEV quá giờ | status = Resolved, role DEV, (bây giờ - updated) | > 4h | Cờ: DEV giữ Resolved quá lâu, cần chuyển cho QA; ghi số giờ (ví dụ 7.2h) |
| Resolved + QA không qua DEV | status = Resolved, role QA, changelog không có người DEV nào trước đó | có | Cờ: "Resolved không qua DEV - cần kiểm tra quy trình" (nếu không xem được changelog thì bỏ qua) |
| Thiếu trường bắt buộc | 1 trong 4 trường (Bug Category, Cause Category, Nguyên nhân gây ra bug, Phạm vi ảnh hưởng của bug) bị rỗng | bất kỳ | Bug đã đóng: ưu tiên cao; bug đang mở: ưu tiên trung bình |
| Mũi tên xu hướng | Open ↑ = xấu; Closed ↑ = tốt; Customer bugs ↑ = xấu; Compliance violations ↑ = xấu | so với lần trước | Hiển thị `giá trị ↑/↓delta` |
| Tỉ lệ đóng / mở (HTML) | `round(CLOSED / TOTAL * 100)`; tương tự OPEN | - | Hiển thị KPI |
| Genuine bug (HTML) | OPEN_COUNT - SPEC_GAP_COUNT | - | - |
| Thanh phân bố module (HTML) | MOD_TOTAL / TOTAL * 100; MOD_OPEN / TOTAL * 100 | - | - |

Sáu category bug thật:
| Category | Bao gồm |
|---|---|
| UI/UX | Lệch giao diện/layout so với thiết kế |
| Data/Logic | Sai dữ liệu, mapping, tính toán |
| Validation | Rule validation code sai |
| State/Navigation | Trạng thái mobile, bàn phím, stack điều hướng |
| Session/Auth | Đăng nhập, token, vòng đời session |
| Integration/Sync | Lỗi đồng bộ dữ liệu bên thứ ba |

## Template / mẫu đầu ra (rút gọn, giữ cấu trúc và các cột/trường)
Bảng thống kê module:
```
| Module | Total | Open | Closed | Top Category |
| [MODULE] - [Mô tả] | N | N | N | [category] |
| **Total** | **N** | **N** | **N** | |
```
Bảng category: `Category | Count | Top Module | Root Cause (1 câu)`.
Danh sách hành động bug Open: `ID | Summary | Category | Status | Priority`.
Bảng thiếu trường: `Issue | Summary | Status | Missing fields`. Bảng vi phạm trạng thái: `Issue | Status | Assignee (role) | Violation`.

Comment Jira khi chuyển Bug -> Improvement (giữ cấu trúc):
```
**[Chuyển Bug -> Improvement]**
**Lý do:** [spec gap ngắn gọn]
Cụ thể, spec [FEATURE-CODE] [mô tả vấn đề, ví dụ: chỉ định nghĩa "sensible length limits" mà không define min/max; không có AC cho case numbers-only hay special-chars-only].
DEV implement theo [cách hiểu hợp lý / happy path], không có basis để handle [behavior được report].
**Action cần thiết:** BA bổ sung AC cho [FEATURE-CODE] về [những gì cần define: field rules, flow AC, enum values...].
```
Câu mở đầu "Lý do" theo loại gap:
| Loại spec gap | Câu mở |
|---|---|
| Business rule thiếu | Business rule "[rule]" chưa được đặc tả trong spec và AC. |
| Yêu cầu bảo mật | Yêu cầu [rate limit/security feature] không xuất hiện trong spec/AC; đây là security requirement cần được đặc tả rõ. |
| Thiếu enum/option | Option "[value]" chưa có trong danh sách enum được định nghĩa trong spec. |
| Rule validation mơ hồ | Spec chỉ định nghĩa "[vague term]" - không có AC cụ thể về min/max, allowed characters, hay pattern. |
| Edge case UX | Edge case "[scenario]" chưa được cover trong AC. Spec chỉ define happy path. |
| Hành vi khi tràn input | Spec chỉ có max limit, không define behavior khi vượt quá (trim / reject / show error). |
| Rule lọc | Rule "[filter rule]" chưa được định nghĩa trong spec. DEV hiển thị theo dữ liệu API trả về. |
| Debounce/throttle | Behavior [throttle/debounce] khi [action] chưa được đặc tả. DEV không có basis implement. |

Bản HTML (tùy chọn) gồm: thẻ KPI, bảng module có thanh phân bố, thẻ category, bảng bug Open, thẻ spec gap, bảng khuyến nghị PM (4 nhóm: immediate / spec-gap / process / prevent, mỗi dòng có người phụ trách và thời điểm), và timeline 4 khối: This Week / Next Sprint / Before Sprint / Ongoing.

## Lỗi thường gặp & lesson learned (lấy từ nguồn, mỗi ý: sai gì -> hậu quả -> cách tránh)
- Báo cáo khi mới lấy trang đầu -> số liệu thiếu, kết luận sai -> lấy hết các trang đến khi đủ tổng.
- Để Rejected lẫn vào phân tích -> đếm module/category phồng lên -> lọc Rejected ngay sau khi lấy.
- Chuyển Bug -> Improvement khi chưa đọc spec -> có thể là bug thật bị đổ cho spec -> đọc spec, trích BR/AC thiếu; nếu không có spec thì gắn nhãn Preliminary và độ tin cậy `low`.
- Đổi issue type trước rồi mới comment -> mất lý do trên lịch sử -> luôn comment trước.
- Trộn bug Open và Closed trong cùng bảng, hoặc đưa bug đã đóng vào danh sách hành động -> đội xử lý nhầm việc -> tách Open/Closed ở mọi bảng.
- Tạo bản HTML hoặc chuyển đổi khi PM chưa xem báo cáo -> mất cổng duyệt -> chờ PM phản hồi.
- Hiển thị mục Customer vs Internal khi 0 bug khách hàng, hoặc mục Compliance khi 0 vi phạm -> báo cáo nhiễu -> bỏ hẳn các mục trống.
- Nhầm tên trường QC Activity do tên bị gõ sai trong Jira ("Acitivity") -> tìm trường không ra -> dùng mã trường tùy chỉnh (nguồn: `customfield_10803`; các trường khác: Bug Category `10301`, Cause Category `10302`, Severity `10300`, Nguyên nhân `11203`, Phạm vi ảnh hưởng `11200`).
- Ngôn ngữ mơ hồ trong spec là nguồn spec gap phổ biến: xem "Ví dụ" bên dưới.

## Ví dụ minh họa (1 ví dụ ngắn có số, lấy hoặc dựng từ nguồn; nếu dựng thì ghi "(ví dụ dựng)")
Từ nguồn (dự án nhiều module, ẩn danh): 62 bug -> 2 trang (50 + 12). Sau khi gom module: 20 Open, 42 Closed.

| Module | Total | Open | Closed |
|---|--:|--:|--:|
| AUTH | 8 | 3 | 5 |
| APPT | 15 | 6 | 9 |
| PROFILE | 12 | 4 | 8 |
| NOTIFY | 7 | 2 | 5 |
| PAYMENT | 20 | 5 | 15 |
| **Total** | **62** | **20** | **42** |

Sàng lọc 20 bug Open: 6 ứng viên từ tiêu đề (từ khóa "thiếu", "missing", validation mơ hồ); đọc spec: 4 spec gap, 2 bug thật. Còn 16 bug thật: UI/UX 4, Data/Logic 5, Validation 3, Integration/Sync 4. Ví dụ gap: spec ghi "sensible length limits" nhưng không có min/max; rate-limit không có trong AC nào; giá trị lọc không có trong enum; hành vi tràn input (trim, reject hay báo lỗi) không xác định. PM duyệt cả 4 -> comment Jira -> chuyển Improvement.

Bảng ngôn ngữ mơ hồ -> cái còn thiếu:
| Ngôn ngữ mơ hồ trong spec | Thiếu gì |
|---|---|
| "sensible length limits" | Không có min/max |
| "appropriate error handling" | Không có AC cho các case lỗi cụ thể |
| "standard security measures" | Không liệt kê yêu cầu cụ thể |
| "user-friendly validation" | Không có pattern/regex/ký tự cho phép |

## Tự kiểm tra (3-5 câu hỏi có đáp án ngắn ngay dưới, dựa trên chính nội dung bài)
1. Vì sao phải lọc Rejected trước khi phân tích, và Rejected được xử lý ra sao?
   - Rejected chỉ đếm, không đưa vào bước module/category/customer/compliance; phân tích chạy trên working set.
2. Một issue ở trạng thái Resolved, người được gán là DEV, cập nhật cách đây 7.2 giờ. Có vi phạm không?
   - Có: quá 4h ở Resolved với DEV, cần chuyển cho QA.
3. Có 40 bug, 14 bug khách hàng, phần lớn Critical/High. Kết luận về QA?
   - 35% > 30% kèm Critical/High: cổng QA trước release chưa đủ. (ví dụ dựng)
4. Thứ tự đúng khi chuyển spec gap là gì?
   - Comment Jira trước, đổi issue type sang Improvement sau; và chỉ khi PM đã duyệt.
5. Khi không có spec, kết quả spec gap được xử lý thế nào?
   - Chế độ preliminary: gắn nhãn Preliminary, độ tin cậy low, PM phải kiểm tra thủ công.

## Liên quan (bài trước/sau trong quy trình, tên thư mục skill khác)
- Trước: bài về viết/đọc spec và acceptance criteria (nguồn spec để đối chiếu).
- Sau: Sprint retro (Ch7·04) (đưa vấn đề lặp lại của bug thành action), Giao tiếp stakeholder (Ch7·03) (báo cáo kết quả cho các bên).
