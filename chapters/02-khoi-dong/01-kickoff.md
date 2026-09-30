---
title: Khởi động dự án - Charter, RACI và Risk seed
source: Kickoff (Ch2·01)
stage: Initiation
level: cơ bản
prerequisites: []
---
# Khởi động dự án - Charter, RACI và Risk seed

## Mục tiêu học xong bạn làm được gì
- Lập được Project Charter theo mẫu TPL-SM-02-01 v1.3 (11 mục + Approval + phụ lục Sales/AM) từ bộ tài liệu SRS đã có.
- Thu thập đủ các thông tin bắt buộc (MUST) trước khi viết charter và biết trường nào được phép bỏ qua.
- Ánh xạ từng yêu cầu phi chức năng (NFR) thành tiêu chí thành công đo được.
- Lập bảng RACI mức vai trò, đúng quy tắc "mỗi việc chỉ 1 A".
- Dựng Risk register khởi điểm (5-10 rủi ro seed) theo loại hợp đồng.
- Biết dừng ở trạng thái DRAFT v1 để người có thẩm quyền duyệt, không tự lập lịch chi tiết hay task chi tiết.

## Khi nào dùng (thời điểm, ai kích hoạt, điều kiện đầu vào)
- Thời điểm: trước khi bắt đầu dự án hoặc ngay sau khi dự án start (Sales/AM làm charter và tài liệu kickoff "trước khi start dự án"; họp kickoff "trước/ngay sau khi start").
- Người kích hoạt: PM khi nhận dự án mới (Sales/AM chuẩn bị charter và bàn giao cho SBU).
- Đầu vào bắt buộc từ SRS: `1-introduction` (vision/mục tiêu), `2-overall-description` (scope tổng quan), `4-system-features-list` (danh sách feature dạng `F-<PROJ>-NN`).
- Đầu vào nên có: `7-quality-attributes` (NFR; thiếu thì tiêu chí thành công chỉ định tính), `6-external-interfaces` (đầu vào cho rủi ro).
- Thiếu tài liệu bắt buộc: dừng lại, yêu cầu viết SRS trước, không đoán.

## Khái niệm cốt lõi
- Project Charter: tài liệu khai sinh dự án (vision, scope, lịch sơ bộ, ước lượng, đội, điều kiện thoả thuận). Tạo ở mức sơ bộ, chi tiết hoá ở bước sau.
- RACI: R = Responsible (người thực hiện); A = Accountable (người chịu trách nhiệm cuối cùng, chỉ 1 người); C = Consulted (được tham vấn, hai chiều); I = Informed (được thông báo, một chiều).
- Risk seed: bộ rủi ro mẫu theo loại hợp đồng để khỏi bắt đầu từ trang trắng; sau kickoff sẽ được quản lý "sống" (thêm, đóng rủi ro).
- Loại hợp đồng: Fixed-bid / T&M / Offshore / R&D / Internal - quyết định bộ rủi ro seed.
- Đơn vị công số: 1 MM (Man-Month) = 20 MD (Man-Day).
- Nhãn nguồn dữ liệu nên gắn vào từng trường: 📄 lấy từ tài liệu có sẵn; 📋 theo quy định/mẫu cố định; 💭 PM xác nhận; 🤖 giả định (PM phải rà lại); ⏳ chưa có (TBD).
- Trạng thái đầu ra: DRAFT v1, chờ duyệt.

## Cách làm từng bước (thủ công, đủ chi tiết để làm theo; input/output)
1. Kiểm tra SRS. Input: bộ SRS. Xác nhận có 3 file bắt buộc. Trích: vision (§1), scope (§2), feature list (§4), NFR threshold (§7, nếu có), phụ thuộc bên ngoài (§6, nếu có). Tóm tắt (số feature, NFR có/không) và xác nhận với người phụ trách trước khi đi tiếp.
2. Thu thập thông tin bắt buộc (MUST) - thiếu là dừng:
   - Tên dự án + mã dự án (định dạng `<PROJ>-YYYY-NNN`); Sponsor (vai trò + tên); PM owner (thường là chính bạn); SBU; loại hợp đồng (Fixed-bid / T&M / Offshore / R&D / Internal); target go-live (sơ bộ).
   - Tuỳ chọn (được bỏ qua): `budget_cap` (mặc định ⏳ TBD); `customer_pic` (N/A nếu Internal); `scope_out` (nếu bỏ qua thì PM tự ghi rõ ranh giới ngoài phạm vi).
3. Kiểm tra chéo: mã dự án chưa trùng charter cũ; SBU có tồn tại; nếu SRS và thông tin PM cung cấp mâu thuẫn thì dừng lại hỏi, không tự dung hoà im lặng.
4. Viết charter đúng mẫu (xem phần Template). Nguồn điền:
   - (1) Nội dung công việc, (3) Bối cảnh, (4) Scope: từ SRS §1, §2, §4.
   - (2) Thông tin khách hàng: hỏi PM/Sales.
   - (5) Nền tảng phát triển: từ SRS, hoặc giả định rồi PM rà lại.
   - (6) Schedule, (7) Ước lượng: chỉ để placeholder, sẽ chi tiết hoá bằng lập lịch và ước lượng sau.
   - (8) Team: chỉ ghi vai trò; tên người điền sau khi ghép nhân sự.
   - Tiêu chí thành công (nhúng vào (11) hoặc phụ lục): ánh xạ NFR §7 (bảng bên dưới). Loại NFR thiếu ghi `[NEEDS_CONFIRM]`.
   - RACI: dùng mẫu, chỉ vai trò, không ghi tên.
   - Đầu tài liệu: chú giải nguồn dữ liệu; mỗi mục lớn có dòng "Sources"; Status = DRAFT v1.
5. Lập RACI (mức dự án, mức feature, mức tài liệu, truyền thông; xem Template). Quy tắc: 1 việc chỉ 1 A; có thể nhiều R/C/I; tránh ô trống.
6. Chọn bộ rủi ro seed theo loại hợp đồng: Fixed-bid mặc định 8; T&M mặc định 6; cộng thêm phần bổ sung Offshore/R&D/Internal. Mỗi rủi ro có ID, tiêu đề, nhóm, Likelihood, Impact, Level, biện pháp, owner.
7. Dừng và bàn giao: tóm tắt thay đổi, giữ DRAFT v1, chạy checklist cuối (charter đúng mẫu 11 mục, mọi trường MUST có nguồn, tiêu chí thành công phủ NFR §7 hoặc `[NEEDS_CONFIRM]`, RACI chỉ vai trò, số rủi ro khớp loại hợp đồng, Status = DRAFT v1), gợi ý bước kế tiếp là WBS. Không lập lịch chi tiết, không sinh task chi tiết.

## Công thức, ngưỡng & tín hiệu (bảng: tên | công thức/điều kiện | ngưỡng | hành động khi vượt; không có thì ghi "Không có")
Charter không có công thức tính toán riêng, nhưng có các quy đổi/ngưỡng sau:

| Tên | Công thức/điều kiện | Ngưỡng | Hành động |
|---|---|---|---|
| Quy đổi công số | Tổng MM = Tổng MD / 20 | 1 MM = 20 MD | Dùng nhất quán khi ước lượng |
| Công số Test | Ước lượng theo công Dev | ≈ 30% công Dev | Kiểm tra lại nếu lệch nhiều |
| Buffer (Fixed-bid) | Biện pháp của R-EFF-01 | 15% | Kiểm tra E3 hàng tuần |
| Tiêu chí Performance | Response time ≤ X ms | tín hiệu QS-PRF-* | Điền X từ NFR |
| Tiêu chí Availability | Uptime ≥ X% | tín hiệu QS-OPS-* | Điền X từ NFR |
| Tiêu chí Quality | Defect leak ≤ X% | QS-TST-04 ≤ 2% | Theo dõi tín hiệu |
| Tiêu chí Process | Process compliance | QS-PRC-07 ≥ 90% | Theo dõi tín hiệu |
| Tiêu chí Schedule | Effort variance | E3 ≤ 10% | Theo dõi tín hiệu |
| Tiêu chí Requirements | Traceability đầy đủ | QS-REQ-03 = 100% | Theo dõi tín hiệu |
| Thay đổi sau khi phát triển | Giờ công tương ứng nhỏ, ít mục | thay đổi quy mô nhỏ: điều chỉnh trong lịch ban đầu | Giờ công lớn hoặc nhiều mục đa dạng = spec change, điều chỉnh giờ công |
| Thiếu UI design của KH / yêu cầu đổi | Phát sinh việc thêm | - | Coi là spec change, xử lý bằng quy trình Change Request |
| Họp Sales-AM cùng 1 KH | Chủ động họp | ít nhất 1 tháng/1 lần | Chia sẻ tình hình dự án, KH, kế hoạch khai thác |

Escalation (trong mẫu RACI): Level 1 (mâu thuẫn đội): PM giải quyết trong tuần; Level 2 (nguồn lực/scope/rủi ro): PM Lead + SBU Manager trong 3 ngày; Level 3 (chiến lược/khách hàng): Sponsor + Director trong 1 ngày; Level 4 (khủng hoảng): CEO + Legal (nếu cần).

## Template / mẫu đầu ra (rút gọn, giữ cấu trúc, cột, trường)
Charter TPL-SM-02-01 v1.3 (hiệu lực 14/02/2025):
- Metadata: Project Code; Mã template; Template version; Tên dự án; Người tạo (Sales/AM); Ngày tạo; Người xác nhận (Sales Lead/AM Boss); Sale phụ trách; AM phụ trách; Status = DRAFT v1.
- (1) Nội dung công việc.
- (2) Thông tin khách hàng: Tên công ty; Địa điểm; Người đại diện; Hình thức liên lạc; Khách hàng mới Có/Không; Mức độ tiềm năng (Rất cao/Cao/Trung bình/Thấp).
- (3) Bối cảnh (2-4 câu: vì sao KH cần làm, pain point, cơ hội, bối cảnh thị trường).
- (4) Scope: bảng Phase | Nội dung công việc | Ghi chú (Định nghĩa yêu cầu; Phát triển/Unit test; Test tích hợp; thêm bớt tuỳ dự án).
- (5) Nền tảng: Backend, Frontend, Database, Server.
- (6) Schedule: ngày bắt đầu; ngày bàn giao cuối cùng; ngày nghiệm thu; service in; Gantt sơ bộ T1-T6 (Định nghĩa yêu cầu, Design UI, Development, Test và fix bug, Release, Acceptance test, Public).
- (7) Ước lượng công số: Tổng = Quản lý + Dev + Test + Khác; bảng chi tiết Category | Bậc 1 | Bậc 2 | Bậc 3 | Công số MD | Ghi chú; dòng Tổng MD và Tổng MM = TOTAL/20.
- (8) Team: PM, TL, BrSE (optional), PG, QA, kèm tóm tắt kinh nghiệm; nếu chưa có tên thì ghi ý tưởng cơ cấu (ví dụ 1 PM, 1 BrSE, 1 TL, 3 DEV, 1 Tester; ưu tiên PM, TL, DEV trước, Tester vào sau theo Schedule).
- (9) Tư liệu KH cung cấp (tài liệu yêu cầu/architecture; UI Design; tài khoản store/cloud; thiết bị test nếu không có).
- (10) Sản phẩm bàn giao (source code qua Git/Bitbucket hoặc theo KH chỉ định; tài liệu kỹ thuật; khác).
- (11) Điều kiện thoả thuận: bảo mật ANTT; chất lượng sản phẩm; liên lạc và báo cáo (daily/weekly/monthly); nhân sự (kinh nghiệm, ngôn ngữ, chứng chỉ, NDA cá nhân); môi trường phát triển và thiết bị kiểm thử; yêu cầu khác (quy tắc thay đổi yêu cầu, xem bảng ngưỡng).
- Approval: Sales phụ trách, AM phụ trách, Customer PIC, PM (sau khi Sales bàn giao); mỗi người có Signed và Date.
- Phụ lục Sales/AM (● chính, ▲ hỗ trợ), 14 dòng, trích: thông báo CMO phân công AM (Sales ●); ký hợp đồng NDA/HDCB/PO (Sales ●); bàn giao cho AM theo template handover (Sales ●, AM ▲); làm charter và tài liệu kickoff trước khi start (Sales ●, AM ▲); bàn giao dự án cho SBU trước khi start (Sales ●, AM ▲); thực hiện kickoff (Sales ●, AM ▲); họp định kỳ với KH hàng tuần/tháng (AM ●, Sales ▲); xử lý invoice, CR, đổi nhân sự (AM ●, Sales ▲); xử lý trouble (AM ●, Sales ▲); khai thác dự án mới, thăm hỏi, quà, giới thiệu thông tin mới (Sales ● là chính). Áp dụng cho KH mới, từ PO đầu tiên đến PO + 1 năm, hiệu lực từ 01/2025.

RACI mức dự án (cột: Sponsor | PM | Tech Lead | BA Lead | QA Lead | Customer PIC | SBU Mgr), trích:
- Charter approval: Sponsor A, PM R, còn lại C/I.
- Scope change (CR): Sponsor A, PM R.
- Requirements (SRS): BA Lead A/R.
- Architecture decision: Tech Lead A/R.
- Test plan: QA Lead A/R.
- Resource allocation: SBU Mgr A/R.
- Risk mitigation và Status reporting: PM A/R.
- UAT sign-off: QA Lead A và Customer PIC A; Gate review G1-G6: Sponsor A và Customer PIC A; Release decision: Sponsor A và Customer PIC A. (nguồn chưa rõ: các dòng này có hai chữ A, mâu thuẫn với quy tắc "1 việc chỉ 1 A"; có thể hiểu là hai bên cùng phê duyệt.)

RACI mức feature (`F-XXX-NN`): REQ chốt AC (R BA, A BA Lead); BD Basic Design (R Designer + Tech Lead, A Tech Lead); DEV (R Dev, A Tech Lead); UT (R Dev, A Tech Lead); TC Testcase design (R QA, A QA Lead); TE Test execution (R QA, A QA Lead). Có thêm RACI mức tài liệu (Charter: R PM, A Sponsor) và truyền thông (báo cáo tuần cho sponsor: PM R/A).

Risk register (DRAFT v1): tiêu đề gồm Generated | Contract Type | Risk count; bảng Active Risks: ID | Title | Category | Likelihood | Impact | Level | Mitigation | Owner; mục Closed Risks (trống lúc đầu).

Rủi ro seed:

| Loại | ID | Tiêu đề | Biện pháp |
|---|---|---|---|
| Fixed-bid (8) | R-SCOPE-01 | Scope creep từ KH | CR process strict |
| | R-EFF-01 | Underestimate effort | Buffer 15%, kiểm tra E3 hàng tuần |
| | R-RES-01 | Resource turnover | Backup plan cho mỗi vai trò |
| | R-CST-01 | KH chậm xác nhận | Escalation matrix |
| | R-TEC-01 | Framework mới | POC sớm |
| | R-TST-01 | Môi trường test trễ | Yêu cầu sớm tuần 1 |
| | R-INT-01 | Tích hợp hệ thống KH | Spike + contract test |
| | R-REL-01 | Trùng cửa sổ release | Xác nhận với ops từ kick-off |
| T&M (6) | R-SCOPE-01 | Scope drift không kiểm soát | Kiểm tra scope hàng tuần |
| | R-RES-01 | Nhân sự bị kéo sang dự án khác | Khoá trong MSA |
| | R-EFF-01 | KH phản biện hour log | Timesheet hàng ngày |
| | R-COM-01 | Communication overhead | Daily standup + báo cáo tuần |
| | R-CST-01 | Chậm phê duyệt | SLA trong MSA |
| | R-TST-01 | Chất lượng thấp vì không có AC cố định | Checklist theo phase |

Bổ sung: Offshore: R-COM-02 múi giờ, R-LANG-01 ngôn ngữ, R-ONB-01 onboarding/handover. R&D: R-TEC-02 tính khả thi chưa rõ, R-SCOPE-02 pivot thường xuyên. Internal: R-PRI-01 ưu tiên thấp hơn dự án KH, R-RES-02 phân bổ part-time.

Mẫu điền của nguồn (Fixed-bid), Category / Likelihood / Impact / Level / Owner: R-SCOPE-01 Scope M/H/High/PM; R-EFF-01 Schedule M/H/High/PM; R-RES-01 Resource L/H/Medium/PM + SBU Mgr; R-CST-01 Dependency M/M/Medium/PM; R-TEC-01 Technical M/M/Medium/Tech Lead; R-TST-01 Dependency M/M/Medium/QA Lead; R-INT-01 Technical L/H/Medium/Tech Lead; R-REL-01 Operations L/M/Low/PM. (Nguồn chưa nêu ma trận L x I -> Level; chỉ có các ví dụ trên.)

## Lỗi thường gặp & lesson learned (sai gì -> hậu quả -> cách tránh)
| Sai | Hậu quả | Cách tránh |
|---|---|---|
| Nhiều A trên 1 việc | Trách nhiệm loãng | Mỗi việc 1 A (soát lại các dòng UAT sign-off, Gate review) |
| Mọi người đều là C | Họp bất tận, quyết định chậm | Chỉ để C người thật sự cần |
| Không có I cho stakeholder | Bất ngờ, mất niềm tin | Luôn liệt kê người cần được thông báo |
| RACI làm một lần, không cập nhật | Lệch thực tế | Rà lại khi đội/scope đổi |
| RACI không có đường escalation | Xung đột bị kẹt | Kèm 4 mức escalation |
| Ghi tên người vào RACI/team lúc kickoff | Sai khi đổi nhân sự | Chỉ ghi vai trò, điền tên sau |
| Đoán khi thiếu SRS/thông tin bắt buộc | Charter sai từ gốc | Dừng, yêu cầu bổ sung |
| Tự dung hoà mâu thuẫn SRS vs thông tin PM | Sai lệch ngầm | Hỏi lại người quyết định |
| NFR không có tiêu chí thành công | Không đo được | Mỗi NFR ít nhất 1 tiêu chí, thiếu thì `[NEEDS_CONFIRM]` |
| Dùng lại format charter 7 mục cũ | Thiếu mục bắt buộc | Luôn dùng mẫu 11 mục |
| Chốt lịch/ước lượng chi tiết ngay ở kickoff | Vượt phạm vi charter | Để placeholder, chi tiết ở bước lập kế hoạch |

## Ví dụ minh họa (ngắn, có số; dựng thì ghi "(ví dụ dựng)")
(ví dụ dựng) <tên-dự-án>, Fixed-bid, SRS có 12 feature, NFR §7 có Performance và Availability. Ước lượng sơ bộ: Dev 100 MD, Test ≈ 30% = 30 MD, Quản lý 15 MD, Khác 5 MD; Tổng 150 MD = 7,5 MM (150/20). Tiêu chí thành công: response time ≤ X ms (QS-PRF-*), uptime ≥ X% (QS-OPS-*), X lấy từ SRS §7; loại Quality thiếu -> `[NEEDS_CONFIRM]`. Risk seed 8 dòng Fixed-bid; RACI có Sponsor là A duy nhất của Charter approval. Trạng thái DRAFT v1, chờ Sponsor và Customer PIC duyệt.

## Tự kiểm tra (3-5 câu hỏi, đáp án ngắn ngay dưới)
1. Kể các trường MUST trước khi viết charter? -> Tên + mã dự án, Sponsor, PM owner, SBU, loại hợp đồng, target go-live (và từ SRS: feature list, vision, NFR nếu có).
2. 1 MM bằng bao nhiêu MD, công Test ước ≈ bao nhiêu phần công Dev? -> 20 MD; ≈ 30%.
3. Fixed-bid mặc định bao nhiêu rủi ro seed, T&M bao nhiêu? -> 8 và 6.
4. Trong RACI, quy tắc về A là gì? -> Mỗi việc chỉ 1 A, có thể nhiều R/C/I, không để ô trống.
5. Khi nào thay đổi yêu cầu sau khi phát triển được coi là spec change? -> Khi giờ công lớn, hoặc nhiều mục đa dạng, hoặc phát sinh do thiếu UI design từ KH / yêu cầu thay đổi.

## Liên quan (bài trước/sau)
- Trước: SRS / giai đoạn trước dự án và thiết lập (chương 01).
- Sau: 02-project-plan (Kế hoạch dự án tổng thể); WBS và lập lịch (chương 03); ghép nhân sự (chương 05); quản lý rủi ro sống (chương 04).
