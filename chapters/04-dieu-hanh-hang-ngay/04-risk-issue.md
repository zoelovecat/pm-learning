---
title: Sổ đăng ký rủi ro và nhật ký vấn đề (Risk Register & Issue Log)
source: Rủi ro & issue (Ch4·04)
stage: Cross-cutting
level: trung bình
prerequisites: [Ch2·01]
---
# Sổ đăng ký rủi ro và nhật ký vấn đề (Risk Register & Issue Log)

## Mục tiêu học xong bạn làm được gì
- Phân biệt rủi ro (risk) và vấn đề (issue) và ghi đúng vào sổ tương ứng.
- Chấm mức độ (Level) rủi ro bằng ma trận Likelihood x Impact, không tự gõ tay.
- Viết chiến lược xử lý 1 dòng và tách thành các action có người thực thi (PIC), hạn (Due), trạng thái, bằng chứng (Evidence).
- Vận hành 4 thao tác: thêm (ADD), cập nhật (UPDATE), nâng cấp rủi ro thành vấn đề (ESCALATE), rà soát hàng tuần (REVIEW).
- Áp dụng quy tắc escalate theo thời gian chưa xử lý, và calibrate Impact theo loại hợp đồng.
- Tránh các anti-pattern làm sổ rủi ro chết.

## Khi nào dùng (thời điểm, ai kích hoạt, điều kiện đầu vào)
- Người kích hoạt: PM. Dùng hàng ngày khi có rủi ro/vấn đề mới, và hàng tuần để rà soát cho báo cáo tuần.
- Điều kiện đầu vào: đã có sổ rủi ro khởi tạo ở kickoff (risk seed) và charter (RACI/leo thang). Thiếu thì dừng, quay lại làm kickoff trước.
- Sổ vấn đề (issue log) chưa có thì tạo mới theo mẫu.
- Bốn thao tác:

| Thao tác | Dùng khi | Cần |
|---|---|---|
| ADD | Rủi ro/vấn đề mới phát sinh | Rủi ro: title, category, likelihood, impact, owner. Vấn đề: title, blocking scope, severity, owner |
| UPDATE | Đổi trạng thái/trường của mục có sẵn, hoặc cập nhật 1 action | ID mục + trường đổi |
| ESCALATE | Rủi ro đã xảy ra thành hậu quả thật | ID rủi ro |
| REVIEW | Rà soát tuần, không thêm mục mới | Không cần thêm |

## Khái niệm cốt lõi
| | Rủi ro (Risk) | Vấn đề (Issue) |
|---|---|---|
| Thời điểm | Có thể xảy ra | Đã xảy ra |
| Chiến lược | Mitigate (giảm), accept (chấp nhận), transfer (chuyển), avoid (tránh) | Khắc phục (resolve) phản ứng |
| Mã ID | `R-<CAT>-NN` | `ISSUE-NNN` |
| Sổ | risk register | issue log |

- **8 nhóm rủi ro**: Scope, Schedule, Resource, Technical, Quality, Dependency, Operations, Compliance.
- **Owner (accountable, cấp risk/issue)**: 1 người chịu trách nhiệm tổng, ghi tên cụ thể + vai trò, không ghi "team".
- **PIC (responsible, cấp action)**: người thực thi 1 action cụ thể; có thể khác Owner và khác nhau giữa các action. Ví dụ: Owner rủi ro Technical là Tech Lead, PIC action "dựng mock server" là Dev, PIC action "đàm phán sandbox" là PM.
- **Strategy (chiến lược)**: 1 dòng ở cấp risk/issue. Việc chi tiết nằm ở bảng action.
- **Action**: Mitigation Action (`MA-NNN`, cho rủi ro) hoặc Resolution Action (`RA-NNN`, cho vấn đề). 1 hàng = 1 việc, không gộp.
- **Evidence**: bằng chứng đã làm thật (link ticket, mail, commit, tài liệu), không chỉ tick DONE. Chưa có ghi `⏳`.
- **Quan hệ khóa ngoại**: cột `Actions` của risk/issue trỏ sang các action; mỗi action có `Risk ID`/`Issue ID` trỏ ngược lại. Hai chiều phải khớp.
- **Vòng đời rủi ro**: NEW -> OPEN -> IN_MITIGATION -> CLOSED; nhánh ESCALATED -> ISSUE (đã xảy ra), ACCEPTED, AVOIDED, TRANSFERRED.
- **Vòng đời vấn đề**: NEW -> OPEN -> IN_RESOLUTION -> RESOLVED -> CLOSED; nhánh ESCALATED.
- **Ý nghĩa trạng thái**: NEW vừa nhận diện chưa đánh giá; OPEN đã đánh giá chưa có xử lý; IN_MITIGATION/IN_RESOLUTION kế hoạch đang chạy; ESCALATED rủi ro đã xảy ra thành vấn đề; ACCEPTED sống chung với rủi ro; AVOIDED/TRANSFERRED đổi hướng hoặc chuyển cho nhà cung cấp; CLOSED đã giải quyết hoặc lỗi thời.
- **Vòng đời action**: TODO -> IN_PROGRESS -> DONE hoặc CANCELLED. DONE và CANCELLED là trạng thái cuối, không quay lại; muốn mở lại việc thì cấp mã action mới.
- **Mã action** tăng đơn điệu suốt đời dự án, không tái dùng số, kể cả action đã hủy.

## Cách làm từng bước (thủ công, đủ chi tiết để làm theo; input/output)

### Trước mỗi lần cập nhật
1. Mở sổ rủi ro, sổ vấn đề, charter. Đếm: rủi ro/vấn đề đang mở, High/Critical đang mở, vấn đề quá hạn theo quy tắc leo thang, số action (tổng, DONE, CANCELLED, quá hạn, DONE thiếu Evidence), mã `MA`/`RA` lớn nhất đã cấp.
2. Xác định người nhận leo thang từ RACI trong charter.

### ADD rủi ro
1. Chọn nhóm (1 trong 8), Likelihood (L/M/H), Impact (L/M/H/Critical), Owner.
2. Tra Level trong ma trận (không tự đoán). Nếu là rủi ro Scope/Estimate thì calibrate Impact theo loại hợp đồng (xem bảng bên dưới); chưa biết loại hợp đồng thì hỏi PM, không tự suy.
3. Viết chiến lược 1 dòng. Nếu chọn chấp nhận (ACCEPT) thì ghi rõ lý do; "monitor thêm" trơn là chấp nhận trá hình và cần hỏi lại lý do.
4. Khai các action: mỗi action 1 việc, PIC riêng (tên cụ thể, không "team"), Due riêng (ngày hoặc `⏳ TBD`). Trạng thái ban đầu `TODO`, Evidence `⏳`.
5. Điền cột `Actions` của rủi ro = danh sách mã vừa cấp. Bỏ bước này sẽ sinh action mồ côi.
6. Điền Trigger (điều kiện chuyển thành vấn đề) và Realize By; khuyến nghị cho rủi ro High/Critical. Chưa có ngưỡng định lượng thì dùng chỉ số thay thế có sẵn (ví dụ chênh lệch effort E3 từ tín hiệu giám sát).
7. Cập nhật dòng tổng kết (số action, % hoàn thành, số quá hạn) và ngày cập nhật.
- Rủi ro High/Critical mà `Actions = —` thì cảnh báo (mitigation rỗng).
- Due sớm hơn ngày Identified của rủi ro cha thì hỏi lại.

### ADD vấn đề
Vấn đề chỉ tạo khi hậu quả đã xảy ra (task trễ, bug thật, deliverable bị chặn). Trường bắt buộc: title (sự kiện đã xảy ra), blocking scope (phần/module bị chặn), severity (High/Medium/Low), owner, ngày. Tùy chọn: From Risk, Resolution (strategy), các RA action, Due tổng của vấn đề (khác Due từng action).

### UPDATE
- Mục cấp risk/issue: sửa trường, ghi thêm vào History cùng dòng (không xóa dòng cũ), tính lại Level nếu L/I đổi.
- Action (`MA-*`/`RA-*`): đổi Status và điền Evidence ngay trên dòng action; không ghi vào History của risk.
- Thêm action cho rủi ro đã có là 2 việc: thêm dòng action (mã kế tiếp) và ghi mã đó vào cột `Actions` của cha.
- Chuyển DONE mà không có Evidence: hỏi lại 1 lần; PM vẫn bỏ qua thì ghi DONE + Evidence `⏳`, để REVIEW đánh dấu 🟡; không tự bịa Evidence.
- Mục không tồn tại trong sổ thì hỏi lại, không tự tạo.
- Không chuyển ngược CLOSED -> OPEN.

### ESCALATE (rủi ro thành vấn đề)
1. Đặt rủi ro ESCALATED, History ghi `-> ISSUE-NNN`. Chỉ áp dụng cho rủi ro đang OPEN hoặc IN_MITIGATION; action không được escalate.
2. Tạo vấn đề liên kết 1-1 (mặc định), hoặc 1-N nếu PM ghi rõ.
3. Action phòng ngừa của rủi ro giữ nguyên. REVIEW sẽ soi trường hợp "rủi ro đã xảy ra mà action phòng ngừa còn TODO".
4. Thông báo cho các bên do PM tự gửi.

### Đóng rủi ro / giải quyết vấn đề
Mọi action của nó phải ở DONE hoặc CANCELLED. Còn TODO/IN_PROGRESS thì hỏi: hủy luôn (CANCELLED + lý do) hay giữ mở. Dòng action ở nguyên trong bảng action làm nhật ký kiểm toán. Chuyển mục sang bảng Closed Risks / Resolved Issues.

### REVIEW hàng tuần
1. So từng rủi ro/vấn đề với quy tắc leo thang; liệt kê mới, đã escalate, đã đóng, quá hạn trong tuần.
2. Quét bảng action: action quá hạn, DONE thiếu Evidence, % hoàn thành.
3. Rủi ro High/Critical mà mọi action đều `Due = ⏳ TBD` thì đánh dấu 🟡 riêng.
4. Tính chỉ số xu hướng (bảng bên dưới). Viết khối để dán vào báo cáo tuần.

### Kiểm tra tính toàn vẹn trước khi lưu (làm 2 lần: trên sổ hiện tại và trên bản nháp sau khi sửa)
1. Mọi mã trong cột `Actions` phải tồn tại ở bảng action.
2. Mọi dòng action có `Risk ID`/`Issue ID` trỏ tới mục tồn tại trong file (đang mở hoặc đã đóng).
3. Với mục đang mở, cột `Actions` và backlink phải khớp 2 chiều.
4. `MA-*` không nằm ở bảng Resolution Actions và ngược lại.
- Sai điều nào thì dừng, sửa rồi mới lưu.
- Quy tắc 3 chỉ áp cho mục đang mở, vì bảng đã đóng chỉ có 4 cột và không có cột Actions.
- Ngoại lệ duy nhất cố ý không cưỡng chế: DONE thiếu Evidence chỉ cảnh báo, để tránh người dùng bịa link cho xong.

## Công thức, ngưỡng & tín hiệu (bảng: tên | công thức/điều kiện | ngưỡng | hành động khi vượt; không có thì ghi "Không có")

**Ngưỡng Likelihood**: L < 30%; M 30-70%; H > 70%.

**Ma trận Level (3x4)**

| Likelihood / Impact | Low | Medium | High | Critical |
|---|---|---|---|---|
| Low | Low | Low | Medium | High |
| Medium | Low | Medium | High | Critical |
| High | Medium | High | Critical | Critical |

**Quy tắc leo thang**

| Level | Chưa xử lý sau | Hành động |
|---|---|---|
| Critical | 1 ngày | Leo thang ngay lên Sponsor |
| High | 3 ngày | Leo thang PM Lead / Sponsor hàng tuần |
| Medium | 7 ngày | Xem trong báo cáo tuần |
| Low | 14 ngày | Xem hàng tháng |

Cho phép ghi đè số ngày theo dự án (Critical 1, High 3, Medium 7, Low 14 là mặc định). Vấn đề có thể đặt Due gấp hoặc chậm hơn quy tắc mặc định miễn có lý do rõ ghi trong Resolution (strategy).

**Calibrate Impact theo loại hợp đồng (rủi ro Scope/Estimate) - bản nháp, chưa qua QA duyệt**

| Loại (mã) | Impact khi scope nở / estimate lệch | Lý do |
|---|---|---|
| Fixed-bid (`fixed_bid`) | Critical | Vượt effort là lỗ trực tiếp, khó thương lượng lại |
| T&M theo giờ thực tế (`tm_hourly`) | Medium | Tự bù bằng billing; rủi ro chủ yếu về quan hệ/lịch |
| T&M theo MM cam kết đầu tháng (`mm_committed`) | High (gần Fixed-bid) | Không có billing bù trong tháng; chỉ gỡ bằng CR xin thêm MM cần khách duyệt |
| Offshore (`offshore`) | Medium | Chi phí nội bộ, ảnh hưởng lịch/nguồn lực nội bộ |
| Internal R&D (`internal_rnd`) | Medium | Không bill khách, tác động nội bộ |

**Các chỉ số xu hướng (REVIEW)**

| Chỉ số | Công thức / điều kiện | Ngưỡng | Hành động |
|---|---|---|---|
| Số rủi ro đang mở | Đếm | Xu hướng tăng | Cảnh báo |
| Tổng mức phơi nhiễm (exposure) | - | > 2 lần baseline | Đánh dấu |
| Mitigation velocity | closed / raised | < 0.5 | Chậm tiến độ |
| Action completion % | `count(DONE) / count(tổng, trừ CANCELLED)` | < 50% với rủi ro High/Critical | Chậm tiến độ |
| Action quá hạn | `Due` đã qua và `Status` không thuộc {DONE, CANCELLED} | > 0 | Đánh dấu 🔴 từng action, nêu PIC + Due |
| DONE thiếu Evidence | `Status = DONE` và `Evidence = ⏳` | > 0 | Đánh dấu 🟡 |
| Due = ⏳ TBD | Không tính quá hạn | - | Riêng High/Critical treo TBD thì 🟡 |
| Mẫu số completion = 0 | Chưa có action hoặc tất cả CANCELLED | - | In `— (0 action)`, không in 0%, không chia |

**Phân tích nâng cao (tùy chọn, cho presales/gate/dự án lớn; không thay ma trận L/M/H hàng ngày)**

| Mức | Xác suất P | Tác động I (theo lịch) |
|---|---|---|
| 1 | < 10% | < 1 ngày |
| 2 | 10-30% | 1-3 ngày |
| 3 | 30-50% | 3-10 ngày |
| 4 | 50-70% | 10-30 ngày |
| 5 | > 70% | > 30 ngày / sự cố production |

Công thức: `score = probability x impact x category_weight`; `EMV_per_risk = probability x financial_impact`. Trọng số nhóm: Technical 1.2, Resource 1.1, Schedule 1.0, Financial 1.4, Scope 1.1, Dependency 1.0, Operations 1.0, Compliance 1.2, Safety 1.3.

| Score | Chiến lược |
|---|---|
| >= 18 | AVOID |
| 12-18 | MITIGATE |
| 8-12 | TRANSFER |
| < 8 | ACCEPT |

Hệ số dung sai ngân sách theo rủi ro: Fixed-bid 0.15, T&M 0.10, Internal R&D 0.25, Compliance-critical 0.30. Với dự án > $100k hoặc > 6 tháng: mô phỏng Monte Carlo 10k lần lấy mẫu P/I để ra vùng đệm ở mức tin cậy 50% / 80% / 95%, đưa vào lịch.

## Template / mẫu đầu ra (rút gọn, giữ cấu trúc, cột, trường)

**Sổ rủi ro** - đầu file: chú giải nguồn (📄 từ tài liệu, 📋 quy tắc công ty, 💭 PM xác nhận, 🤖 giả định, ⏳ chưa có), bảng tóm tắt: `Last updated | Total active | Level breakdown (Critical/High/Medium/Low) | Mitigation actions {done}/{total} DONE (pct%) · overdue: N | Closed (lifetime)`.

`Active Risks` (14 cột): `ID | Title | Cat | L | I | Level | Status | Owner | Identified | Mitigation (strategy) | Actions | Trigger | Realize By | History`.

`Mitigation Actions` (7 cột): `Action ID (MA-NNN) | Risk ID | Action | PIC | Due | Status (TODO/IN_PROGRESS/DONE/CANCELLED) | Evidence`.

`Closed Risks` (4 cột): `ID | Title | Closed Date | Close Reason (RESOLVED/OBSOLETE/AVOIDED/ACCEPTED)`.

**Nhật ký vấn đề** - tóm tắt: `Last updated | Total active | Resolution actions {done}/{total} DONE (pct%) · overdue | Resolved lifetime`.

`Active Issues` (11 cột): `ID | Title | Blocking scope | From Risk | Severity | Status | Owner | Date | Resolution (strategy) | Actions | Due`.

`Resolution Actions` (7 cột): giống bảng Mitigation nhưng `Action ID (RA-NNN)` và `Issue ID`. `Resolved Issues`: `ID | Title | Resolved Date | Resolution`.

Quy tắc điền: Level tính từ ma trận; Severity chỉ 3 mức High/Medium/Low (nếu nghiêm trọng hơn thường lệ thì mô tả trong Blocking scope, không tự chế mức mới); ACCEPT thì `Actions = —`; mặc định 1 rủi ro -> 1 vấn đề; History ghi thêm mỗi lần UPDATE/ESCALATE.

**Khối rà soát tuần (dán vào báo cáo tuần)**: các mục `New this week`, `Escalated this week`, `Closed this week`, `Overdue per escalation rule`, `Mitigation actions status` (quá hạn, DONE thiếu Evidence, Completion), `Summary` (số rủi ro/vấn đề đang mở kèm xu hướng, số High/Critical đang mở).

**Cấu hình tùy chọn theo dự án**: `contract_type` (5 giá trị trên), `escalation_override` (critical_days/high_days/medium_days/low_days), `category_extra` (thêm nhóm ngoài 8 nhóm, nếu dự án cần).

## Lỗi thường gặp & lesson learned (sai gì -> hậu quả -> cách tránh)

| Sai | Hậu quả | Cách tránh |
|---|---|---|
| Sổ để cũ (stale) | Rủi ro thật bị bỏ sót | Rà soát tuần và đưa vào báo cáo tuần |
| Ghi việc cần làm (action item) vào sổ rủi ro | Lẫn rủi ro với task | Tách sổ rủi ro và danh sách task |
| Mọi rủi ro đều Medium | Không thấy ưu tiên | Buộc chọn L/M/H rõ ràng |
| Mitigation là "monitor" | Chấp nhận trá hình, không ai hành động | Ghi ACCEPT kèm lý do hoặc kế hoạch cụ thể |
| Owner là "team" | Không ai chịu trách nhiệm | Một tên cụ thể; PIC ghi ở từng action |
| Không bao giờ đóng | Sổ phình to | Đóng mục lỗi thời hàng quý |
| Hậu quả đã xảy ra nhưng để OPEN | Thiếu leo thang kịp thời | ESCALATE ngay, không chờ họp tuần |
| Hai rủi ro cùng nguyên nhân gốc báo rời rạc | Che mất tương quan | Ghi "liên quan R-xxx" trong History/Mitigation |
| Nhồi nhiều action + nhiều PIC vào 1 ô | Không theo dõi được | 1 hàng = 1 việc, PIC riêng |
| Tick DONE không có link | Không biết đã làm thật chưa | Luôn kèm Evidence; REVIEW đánh dấu 🟡 nêu PIC |
| Gộp 2 việc (dùng "và", ";", "+") trong 1 ô | Khó theo dõi trạng thái | Tách thành 2 action |
| Thêm action nhưng quên cập nhật cột `Actions` của cha | Action mồ côi | Làm đủ 2 việc |
| Đóng rủi ro khi còn action TODO | Mất dấu việc chưa làm | Hủy có lý do hoặc giữ mở |
| Áp cứng một mức Impact cho mọi hợp đồng | Level sai lệch | Calibrate theo loại hợp đồng |

Lesson learned: đổi Status action không ghi vào History (History chỉ cho biến động cấp risk); Evidence hiện do PM nhập tay, không tự kiểm chứng.

## Ví dụ minh họa (ngắn, có số; dựng thì ghi "(ví dụ dựng)")
(ví dụ dựng, theo mẫu nguồn) Thêm rủi ro `R-RESOURCE-02`: "Thành viên mới ramp-up chậm sau khi tăng size team", nhóm Resource, L = H, I = M -> Level tra ma trận = High. Owner: <Tech Lead>. Chiến lược: "Buddy pairing + checkpoint velocity". Action: `MA-008` (ghép cặp với senior, PIC <Member A>, Due 2026-07-09, TODO, Evidence ⏳) và `MA-009` (checkpoint velocity/quality mỗi 2 sprint, PIC <Tech Lead>, Due 2026-07-16). Owner khác PIC.

Escalate: ngày 2026-07-02 có bug thật chặn Tester -> `R-RESOURCE-02` thành ESCALATED, tạo `ISSUE-014` (Severity High, Blocking scope: cụm Module-X, Due 2026-07-03 do PM đặt chứ không áp mặc định 3 ngày). `MA-008/009` vẫn TODO nên REVIEW sẽ soi.

Rủi ro Scope: L = H, hợp đồng `mm_committed` -> Impact High -> Level Critical. Cùng tình huống: `fixed_bid` Impact Critical -> Level Critical; `tm_hourly` Impact Medium -> Level High.

Vòng đời 1 action: `MA-003` TODO (2026-06-20) -> IN_PROGRESS (2026-07-08, Evidence: ticket + nhánh code) -> DONE (2026-07-16, Evidence: ticket + PR merged). Trong khi đó `MA-001` có Due 2026-07-06, còn IN_PROGRESS ngày 2026-07-08 nên REVIEW báo 🔴 quá 2 ngày, nêu PIC. `MA-006` bị gõ "done" không link nên REVIEW báo 🟡 DONE thiếu Evidence. Completion mẫu: 1/8 DONE (12%) - hiển thị 12% theo nguồn.

## Tự kiểm tra (3-5 câu hỏi, đáp án ngắn ngay dưới)
1. Risk hay issue: "Khách chưa trả spec, có thể trễ 1 tuần" và "Task X đã trễ 2 ngày vì thiếu spec"?
   Đáp án: câu đầu là risk (`R-<CAT>-NN`); câu sau là issue (`ISSUE-NNN`) vì đã xảy ra.
2. Likelihood = M, Impact = High thì Level? Chưa xử lý bao lâu phải leo thang?
   Đáp án: High; 3 ngày.
3. Owner khác PIC ở điểm nào?
   Đáp án: Owner chịu trách nhiệm tổng cấp risk (1 người); PIC thực thi 1 action cụ thể, có thể khác Owner.
4. Khi nào một action bị coi là quá hạn, và mẫu số % hoàn thành tính thế nào?
   Đáp án: `Due` đã qua và Status không thuộc {DONE, CANCELLED}; `DONE / (tổng trừ CANCELLED)`, mẫu số 0 thì in `— (0 action)`.
5. Vì sao DONE thiếu Evidence chỉ cảnh báo chứ không chặn?
   Đáp án: chặn cứng sẽ khiến người dùng bịa link; mục tiêu là bằng chứng thật, nên REVIEW nêu tên PIC.

## Liên quan (bài trước/sau)
- Trước: Kickoff và charter (sinh risk seed và RACI), Giám sát tín hiệu (tín hiệu đỏ -> rủi ro mới).
- Sau/song song: Change request (CR và rủi ro thực tế, đặc biệt rủi ro Scope), Báo cáo tuần (dán khối rà soát), Gate review (rủi ro High/Critical để quyết go/hold), Đóng dự án và Lessons learned (rủi ro đã đóng thành bài học), Truyền thông với stakeholder (PM tự gửi thông báo leo thang).

**Ghi chú nguồn chưa rõ**
- (nguồn chưa rõ: bảng calibrate Impact theo loại hợp đồng là bản nháp, chưa qua QA duyệt; 5 giá trị và mức Impact chưa xác nhận.)
- (nguồn chưa rõ: "Total exposure > 2x baseline" không định nghĩa exposure và baseline.)
- (nguồn chưa rõ: ma trận Level có 4 mức Impact nhưng Severity của vấn đề chỉ có 3 mức, không có Critical.)
- (nguồn chưa rõ: các dải score 12-18 và 8-12 chồng biên với ">= 18" và "< 8"; không nói biên thuộc dải nào.)
- (nguồn chưa rõ: Likelihood dùng L/M/H theo % ở sổ hằng ngày, còn phân tích nâng cao dùng thang 1-5; hai thang không quy đổi.)
- (nguồn chưa rõ: Status action 4 mức, Evidence dạng tự do hay bắt buộc link, số nhóm rủi ro và thang ma trận có chuẩn công ty chưa, đều nằm trong câu hỏi mở của nguồn.)
- (nguồn chưa rõ: 1/8 DONE ghi 12%; phép tính đúng là 12.5%, có thể đã làm tròn xuống.)
