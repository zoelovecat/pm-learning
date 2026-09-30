---
title: PM tiếp quản giữa chừng - dựng lại bộ hồ sơ PM từ hệ thống dự án
source: Tiếp quản PM (Ch5·04)
stage: Closure
level: nâng cao
prerequisites: [Ch5·01, Ch5·02]
---
# PM tiếp quản giữa chừng - dựng lại bộ hồ sơ PM từ hệ thống dự án

## Mục tiêu học xong bạn làm được gì
- Khi nhận dự án đang chạy mà không có hồ sơ PM (lịch, báo cáo tuần, gate, risk, CR), biết dựng lại bộ hồ sơ tối thiểu từ hệ thống PM chung (và Jira dự phòng) để làm retro (Lessons learned, Ch9·01) và đóng dự án (closeout) mà không phải lập kế hoạch lại từ đầu.
- Biết phân biệt dữ liệu đồng bộ (proxy, chưa phải quyết định chính thức) với hồ sơ chính thức.
- Biết chính sách ghi đè, cách ghi khoảng trống (gap) và nhờ kỹ năng/quy trình nào bổ sung.

## Khi nào dùng (thời điểm, ai kích hoạt, điều kiện đầu vào)
- PM mới tiếp quản giữa chừng, thiếu hồ sơ để chạy quy trình đóng dự án. PM kích hoạt.
- Bắt buộc có: mã dự án trong hệ thống PM chung (project id số) và chế độ làm việc. Nếu không xác định được project id hoặc không truy cập được hệ thống -> dừng, không bịa dữ liệu.
- Nên có ít nhất 1 trong: milestone, deadline, báo cáo tuần, CR. Nếu thiếu cả chi tiết lẫn milestone/deadline thì lịch không đủ cho retro; PM bổ sung tay hoặc lập lại lịch.
- Khác với: onboarding brief (bản đọc một lần, không tạo hồ sơ bắt buộc cho việc đóng dự án) và Bàn giao thành viên (Ch5·01) (bàn giao con người/HR).

## Khái niệm cốt lõi (định nghĩa, thuật ngữ, vì sao quan trọng)
- **Bộ hồ sơ seed**: các file dựng nhanh từ dữ liệu hệ thống: lịch (schedule), báo cáo tuần (status), gate, risk register, CR (+ INDEX), tùy chế độ thêm charter tối thiểu và effort.
- **3 chế độ**:
  - seed-lessons (mặc định): chuẩn bị retro; tạo schedule, status/*, gates/*, risk, cr/* (+ cr/INDEX).
  - seed-closeout: seed-lessons + charter tối thiểu + effort stub nếu có chỉ số.
  - refresh: chỉ cập nhật file đã đồng bộ trước (có banner `synced-from: ksystem`), bỏ qua file PM đã sửa tay.
- **Banner đồng bộ**: khối bắt buộc ở đầu mọi file seed, ghi synced-from, thời điểm, project id, chế độ, độ phủ (full/partial/stub) và cảnh báo "dữ liệu kéo từ hệ thống, không thay thế output chính thức".
- **Proxy gate**: cột mốc (milestone) của hệ thống được dùng thay gate. KHÔNG phải quyết định G1-G6 chính thức; quyết định Go/Hold/Abort chỉ có khi chạy Gate review (Ch8·02). Tiêu đề ghi "(synced proxy - chưa chạy Gate review, Ch8·02)", Decision = NOT_REVIEWED (proxy).
- **Độ phủ (coverage)**: full / partial / stub / none cho từng file.
- **Nguyên tắc không bịa**: số liệu chỉ từ dữ liệu kéo về; thiếu -> [NO_DATA] hoặc ⏳ TBD.
- **Chú giải nguồn**: 🌐 hệ thống PM · 🤖 tự giả định · ⏳ TBD (thêm 📄 tài liệu, 📋 quy tắc, 💭 PM xác nhận ở một số mẫu).
- Vì sao quan trọng: giúp PM mới có dữ liệu lịch sử để rút bài học mà vẫn minh bạch phần nào là suy diễn.

## Cách làm từng bước (thủ công, đủ chi tiết để làm theo; kèm input/output)
1. **Xác định dự án và quét hồ sơ hiện có**: lấy project id; liệt kê thư mục hồ sơ PM: schedule (thiếu/rỗng/có/có đã đồng bộ), số file status, gates, risk, số file CR, charter (chế độ closeout). File có sẵn và không có banner `synced-from: ksystem` được coi là PM tự viết -> không ghi đè trừ khi PM chọn ghi đè bắt buộc.
2. **Chọn tham số**:
   - Chế độ: seed-lessons (mặc định) / seed-closeout / refresh.
   - Chính sách ghi đè: skip-existing (mặc định) / refresh-synced-only / force-all (PM phải gõ xác nhận rõ).
   - Khoảng dữ liệu: báo cáo tuần 12 tuần ISO gần nhất (hoặc toàn bộ nếu ít hơn 12); có tạo seed rỗng cho CR/risk (mặc định Yes, skeleton + [NO_DATA]); dùng Jira dự phòng cho risk/CR (mặc định Yes nếu có khóa Jira). Tuần ISO tính Thứ Hai - Chủ Nhật.
3. **Kéo dữ liệu (chỉ đọc)** theo thứ tự: chi tiết dự án (tên, mã, mô tả, giải pháp, ngày bắt đầu/kết thúc, trạng thái, khách hàng, PM); sub-data: milestones, deadlines, change-requests, project-indicator-reports, members, evaluations, project-monitor-reports, communications (tùy chọn), project-documents (tùy chọn); báo cáo tuần project-weekly-reports (phân trang 50/trang; nếu rỗng thử báo cáo tuần mới rồi chi tiết mới nhất). Cấm mọi thao tác ghi/đồng bộ/phê duyệt/tạo/xóa/cập nhật trên hệ thống.
4. **Jira dự phòng** (chỉ khi có khóa Jira): risk/issue proxy `project = KEY AND type in (Risk, Bug) AND status != Done` (điều chỉnh theo board); CR proxy `labels = change-request` hoặc type Change, chỉ khi CR của hệ thống rỗng; epic có due date bổ sung lịch khi milestone mỏng. Jira không thay hệ thống PM cho timeline chính khi milestone đủ.
5. **Lập bảng độ phủ và gap trước khi ghi**:

| Target | Nguồn | Độ phủ | Hành động |
|---|---|---|---|
| schedule | milestones + deadlines + detail | full/partial/none | seed/stub; dừng mềm nếu none và không có detail |
| status/YYYY-WW | báo cáo tuần | N tuần | seed từng tuần; 0 tuần -> 1 stub [NO_DATA] + gợi ý Status tuần (Ch7·01) |
| gates | milestones (+ indicators) | proxy | seed proxy gate (🤖); thiếu gate chính thức -> gap Gate review (Ch8·02) |
| risk | evaluations / Jira / rỗng | ... | seed register; rỗng -> skeleton + [NO_DATA] |
| cr/<id> | change-requests | N CR | 1 file/CR + INDEX; 0 -> INDEX rỗng + note |
| charter | detail + members | chỉ closeout | charter tối thiểu |
| effort/<date> | indicators | chỉ closeout | stub variance nếu có số, không thì bỏ qua + gap |

   Quy tắc xung đột: file PM tự viết khác hệ thống -> không ghi đè âm thầm, liệt kê xung đột và hỏi lại. Ngày milestone hệ thống khác ngày Jira -> ưu tiên hệ thống, ghi chú xung đột.
6. **Xác nhận gap report với PM rồi mới ghi** theo thứ tự: schedule, status theo tuần, gates, risk, cr/INDEX + cr/<id>, (closeout) charter và effort; mọi file mở đầu bằng banner.
7. **Quy tắc đặt tên/định danh**: risk `R-SYNC-NN` khi hệ thống không có id; CR `CR-KS-<id>` hoặc khóa Jira; gate dùng mã milestone M1, M2... theo thứ tự (không map cứng G1-G6 trừ khi tên milestone khớp).
8. **Ghi bản kê SYNC-MANIFEST**: Synced at | Mode | project id | phiên bản kỹ năng; bảng "Files written" (Path | Action: created/skipped/refreshed | Coverage); bảng "Gaps -> upstream" (Gap | kỹ năng đề xuất).
9. **Bàn giao cho PM**: trạng thái DRAFT. Báo: chế độ, số file ghi, số file bỏ qua, số gap. PM: (1) rà soát manifest và từng seed, nhất là proxy gate và risk; (2) bổ sung gap bằng quy trình gốc; (3) chạy Lessons learned (Ch9·01); (4) đủ retro + hypercare/effort thì closeout. Không coi proxy gate là Gate review (Ch8·02) chính thức; không coi risk seed là đã mitigate.

## Công thức, ngưỡng & tín hiệu
| Tên | Công thức/điều kiện | Ngưỡng | Hành động khi vượt |
|---|---|---|---|
| Cửa sổ status | Số tuần ISO gần nhất | 12 tuần (hoặc toàn bộ nếu <12) | Chỉ seed trong cửa sổ |
| Phân trang báo cáo tuần | per_page | 50 | Duyệt hết trong cửa sổ |
| Độ phủ lịch none | Không detail dates, không milestones, không deadlines | none | Dừng mềm: vẫn seed risk/CR/status nếu có, báo không đủ cho retro, PM bổ sung tay hoặc lập lịch |
| Cảnh báo tuần lịch mẫu | "Weekly: E3 <= 10%" (mặc định của quy tắc công ty, chưa neo từ WBS) | 10% | Ghi trong mẫu lịch; (nguồn chưa rõ: E3 không được định nghĩa trong các file này) |
| Ưu tiên nguồn xung đột ngày | Ngày milestone hệ thống vs Jira | - | Ưu tiên hệ thống |
| Đơn vị effort mẫu | md | - | Ghi trong mẫu |

Chính sách ghi đè:
| Trạng thái file | skip-existing | refresh-synced-only | force-all |
|---|---|---|---|
| thiếu | ghi | ghi | ghi |
| có `synced-from: ksystem` | bỏ qua | ghi | ghi |
| PM tự viết (không banner) | bỏ qua | bỏ qua | ghi (sau xác nhận) |

## Template / mẫu đầu ra (rút gọn, giữ cấu trúc và các cột/trường)
- **Banner**: front-matter gồm synced-from: ksystem; synced-at (ISO-8601); ksystem_project_id; skill; mode; coverage + dòng cảnh báo handover sync seed.
- **schedule.md**: Field/Value/Src (Project Code, Start Date, Target Go-live/End, Status, Effort Unit = md, Buffer = ⏳ TBD, Total Effort = [NO_DATA], Sync coverage); §1 Milestone và Signal Anchor `# | Milestone | Plan Date | Actual/Status | Phase | Signal | Threshold | Owner`; §2 Task Schedule = [NO_DATA] (không dựng lại task list); §3 Critical Path = ⏳ TBD (không suy ra khi thiếu phụ thuộc); §4 Capacity Check = [NO_DATA]; §5 Roles Summary `Role | Members | Src`.
- **status/YYYY-WW.md**: ISO week, Status code (🟢/🟡/🔴/⏳; chỉ suy ra từ nội dung báo cáo nếu rõ, không đoán), Report source id; §1 Progress summary; §2 Milestones this week `Milestone | Plan | Actual | Note`; §3 Blockers/Risks `Item | Severity | Note`; §4 Plan next week; §5 Metrics `Metric | Value | Src`. Status code 🤖 cần PM xác nhận trước khi dùng cho retro.
- **gates**: Proxy id, Milestone name, Date, Ksystem status, Mapped formal gate (G1-G6 hoặc unmapped), Decision = NOT_REVIEWED (proxy); bảng tín hiệu `Signal/Indicator | Value | Threshold | Src`; Checklist/evidence = [NO_DATA]. Nếu tên milestone khớp gate công ty (Charter/SRS/BD/Code/UAT/Go-live) thì gợi ý map G1-G6 để PM xác nhận. Dùng cho retro như sự kiện lịch sử, không như gate pass chính thức.
- **risk.md**: Last updated, Total active, Level breakdown (Critical/High/Medium/Low); Active Risks `ID | Title | Cat | L | I | Level | Status | Owner | Identified | Mitigation | Actions | Trigger | Realize By | History` (R-SYNC-01, L/I/Level = ⏳ để PM calibrate, Status OPEN); Mitigation Actions `Action ID | Risk ID | Action | PIC | Due | Status | Evidence`; Closed Risks `ID | Title | Closed Date | Close Reason`. Nếu không có risk nào: một hàng [NO_DATA].
- **cr**: INDEX `CR ID | Title | Status | Date | File`; mỗi CR: CR ID, Title, Status, Requested date, Requester, Decision (approved/rejected/pending/⏳); §1 Description; §2 Impact (Scope/Schedule/Cost/Risk đều ⏳; muốn đầy đủ thì chạy lại quy trình Change request, Ch4·03); §3 Decision và evidence.
- **charter.md** (chỉ closeout): Project Code/Name, Customer, PM, Start, End/Go-live, Contract type ⏳, SBU ⏳; §1 Vision/Summary; §2 Scope (high level); §3 Out of scope = ⏳ TBD; §4 RACI (members snapshot); §5 Success criteria = ⏳ TBD (lấy từ mục tiêu chỉ số nếu có, không bịa ngưỡng). Không thay charter chuẩn của kickoff.
- **Bảng "Gap -> kỹ năng bổ sung"**: không có ksystem id -> Thiết lập PM (Ch1·03); không có quyết định G1-G6 chính thức -> Gate review (Ch8·02); risk mỏng -> Rủi ro & issue (Ch4·04); không có lịch sử báo cáo tuần -> Status tuần (Ch7·01); không có variance effort -> Effort actuals (Ch6·03); không có hypercare/release -> hypercare / Release plan (Ch8·01); chỉ cần brief cho thành viên -> Onboarding brief (Ch5·02); sẵn sàng retro -> Lessons learned (Ch9·01); sẵn sàng đóng chính thức -> closeout.

## Lỗi thường gặp & lesson learned (lấy từ nguồn, mỗi ý: sai gì -> hậu quả -> cách tránh)
- Coi proxy gate là gate chính thức -> báo cáo sai quyết định Go/Hold/Abort -> luôn dán nhãn proxy, chạy Gate review (Ch8·02) nếu cần chính thức.
- Bịa ngày milestone, CR hoặc risk -> retro dựa trên dữ liệu sai -> chỉ dùng dữ liệu kéo về; thiếu -> [NO_DATA].
- Ghi đè hồ sơ PM đã tự viết -> mất công sức -> chính sách mặc định skip-existing; force-all cần xác nhận rõ.
- Dựng task list/critical path giả từ milestone -> lịch sai -> để [NO_DATA]/⏳ TBD, dùng Spec thành task (Ch3·02) + Lập schedule (Ch3·03).
- Đoán status code (🟢🟡🔴) -> kết luận sai -> chỉ suy ra khi báo cáo nói rõ; PM xác nhận.
- Coi risk seed là đã xử lý -> rủi ro thật bị bỏ sót -> PM calibrate L/I/Level, điền owner và mitigation.
- Thiếu banner/nhãn nguồn -> không phân biệt được seed và hồ sơ thật -> banner + chú giải bắt buộc ở mọi file.
- Chạy retro/closeout ngay lập tức mà chưa rà soát -> dùng dữ liệu chưa kiểm -> PM rà soát manifest trước.

## Ví dụ minh họa (1 ví dụ ngắn có số, lấy hoặc dựng từ nguồn; nếu dựng thì ghi "(ví dụ dựng)")
(Ví dụ dựng, theo quy tắc trong nguồn) PM mới nhận dự án <mã-dự-án>, chế độ seed-lessons, chính sách skip-existing. Quét: schedule chưa có, 0 status, 0 gate, risk chưa có, 0 CR. Hệ thống có 4 milestone, 8 báo cáo tuần, 2 CR, 0 risk/evaluation. Kết quả: schedule (partial); 8 file status (đủ trong cửa sổ 12 tuần); 4 proxy gate M1-M4 (Decision NOT_REVIEWED); risk.md có 1 hàng [NO_DATA]; cr/INDEX + 2 file CR-KS-<id>. Manifest ghi gap: Gate review (Ch8·02) (chưa có G1-G6 chính thức), Rủi ro & issue (Ch4·04) (risk mỏng). PM rà soát rồi chạy Lessons learned (Ch9·01).

## Tự kiểm tra (3-5 câu hỏi có đáp án ngắn ngay dưới, dựa trên chính nội dung bài)
1. Khác nhau giữa seed-lessons và seed-closeout? -> seed-closeout thêm charter tối thiểu và effort stub (nếu có chỉ số).
2. File PM tự viết bị xử lý ra sao ở chế độ mặc định? -> skip-existing: bỏ qua; chỉ force-all (sau xác nhận) mới ghi đè.
3. Proxy gate có phải quyết định G1-G6 không? -> Không; Decision = NOT_REVIEWED, phải chạy Gate review (Ch8·02) để có quyết định chính thức.
4. Cửa sổ báo cáo tuần mặc định? -> 12 tuần ISO gần nhất (hoặc toàn bộ nếu ít hơn 12).
5. Ngày milestone hệ thống khác Jira thì theo bên nào? -> Hệ thống PM chung, kèm ghi chú xung đột.

## Liên quan (bài trước/sau trong quy trình, tên thư mục skill khác)
- Trước: Thiết lập PM (Ch1·03) (registry, ksystem id).
- Song hành: Onboarding brief (Ch5·02), Bàn giao thành viên (Ch5·01).
- Sau: Lessons learned (Ch9·01) -> closeout; gap: Rủi ro & issue (Ch4·04), Gate review (Ch8·02), Effort actuals (Ch6·03), hypercare, Release plan (Ch8·01), Status tuần (Ch7·01).
