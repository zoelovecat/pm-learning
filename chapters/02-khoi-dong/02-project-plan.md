---
title: Kế hoạch dự án tổng thể (Project Plan)
source: Project plan (Ch2·02)
stage: Initiation
level: trung bình
prerequisites: [Ch2·01]
---
# Kế hoạch dự án tổng thể (Project Plan)

## Mục tiêu học xong bạn làm được gì
- Lập Project Plan theo mẫu TPL-SW-05-01 v1.7 (22 mục + trang bìa + lịch sử thay đổi) bằng cách gom từ charter, WBS, lịch, rủi ro, nhân sự.
- Đặt được bộ chỉ số mục tiêu (Bug rate, CSS, DRE, Leakage, EE, Timeliness, Process Compliance) với LCL/Target/UCL.
- Tính EE (Effort Efficiency) và đổi giờ công sang MM có hệ số rank.
- "Điều chỉnh quy trình" (tailoring): quyết định thực hiện (O) hay không (X, kèm lý do) từng hạng mục của 11 quy trình.
- Nhận biết mục nào là cố định theo quy định, mục nào PM tự quyết, mục nào phải rà lại trước khi ký.

## Khi nào dùng (thời điểm, ai kích hoạt, điều kiện đầu vào)
- Thời điểm: cuối giai đoạn chuẩn bị, sau khi đã có charter, rủi ro seed, lịch và WBS; PM khởi tạo, để PQA và CTO review theo nhóm (Group review).
- Đầu vào bắt buộc: charter (mã và tên dự án, loại hợp đồng, vision, phạm vi phase, vai trò RACI), risk register khởi điểm, lịch (ngày bắt đầu, deadline, ngày các milestone G1-G6, tổng công MM), WBS (công số, cấu trúc phase). Thiếu là dừng, quay lại tài liệu nguồn, không đoán.
- Đầu vào nên có: kết quả ghép nhân sự (mục 15; thiếu thì ⏳ TBD), danh sách task (mục 9).
- Kiểm tra chéo trước khi viết: ngày trong charter lệch lịch quá 1 tuần mà chưa giải thích?; công WBS (MM) so với năng lực trong lịch có vượt (overcommit)?; loại hợp đồng có khớp mặc định tailoring?; tên vai trò nhân sự có khớp RACI của charter? Có mâu thuẫn thì hỏi người quyết định, không tự dung hoà.
- Cập nhật khi: CR đáng kể, chuyển phase, kiểm toán PQA hàng quý.

## Khái niệm cốt lõi
- Project Plan: tài liệu master của dự án; các tài liệu chi tiết (lịch, task, phân công) nằm riêng.
- LCL / Target / UCL: cận dưới / mục tiêu / cận trên của chỉ số. Có hàng "tần xuất đo công ty: Quý".
- Kiểu dự án: Project-based / Labor / Khác; dự án Tài liệu (Document) dùng bộ chỉ số riêng (mục 3).
- Tailoring quy trình: O = có thực hiện; X = không thực hiện và phải ghi lý do; hạng mục bắt buộc không được bỏ im lặng.
- Group review (nhiều người) vs One-person review (một người).
- PQA: bộ phận đảm bảo chất lượng quy trình. CM: quản lý cấu hình.
- Nhãn nguồn: 📄 lấy từ tài liệu có sẵn; 📋 quy định cố định (chỉ bộ phận chất lượng được đổi); 💭 PM xác nhận; 🤖 giả định (PM phải kiểm lại trước khi ký); ⏳ chưa có.

## Cách làm từng bước (thủ công, đủ chi tiết để làm theo; input/output)
1. Gom đầu vào và thông tin PM: loại dự án (Project-based/Labor/Khác), PM owner, có phải dự án Document không (có: mục 3; không: mục 2).
2. Quyết định các lựa chọn (được bỏ qua, có mặc định): vòng đời phát triển (mặc định Hybrid); tailoring O/X (mặc định theo loại hợp đồng); buffer % (mặc định theo ma trận nháp); ngưỡng chỉ số (mặc định giữ nguyên); sản phẩm bàn giao, review, loại test (mặc định chuẩn); các khoản chi mục 10 (mặc định 4 nhóm, tổng 55.000.000 VND); tần suất liên lạc; kỹ năng từng thành viên (⏳ sau ghép nhân sự); chủ đề đào tạo thêm (theo khoảng trống kỹ năng); CM inline hay file riêng (inline nếu < 10MM, file riêng nếu ≥ 10MM); tinh chỉnh L/I rủi ro (tự đánh giá).
3. Ánh xạ nguồn cho từng mục: mục 1 từ charter + PM; mục 2-3 từ danh mục chỉ số + ghi đè; mục 4 từ scope charter + vòng đời PM chọn; mục 5 PM duyệt từng dòng O/X; mục 6-8 chuẩn + tuỳ chỉnh; mục 9 từ WBS + danh sách task; mục 10 4 nhóm chuẩn; mục 11 từ lịch; mục 12 chuẩn + SLA bên ngoài; mục 13 từ risk register; mục 14 chuẩn; mục 15 từ kết quả ghép nhân sự hoặc ⏳; mục 16 từ phase WBS + lịch; mục 17 CM; mục 18-19 chuẩn + khoảng trống kỹ năng; mục 20 từ hướng dẫn hoạt động của lịch. Không bịa.
4. Viết theo thứ tự: bìa + lịch sử -> mục 1 -> mục 2-3 -> mục 4-5 -> mục 6-10 -> mục 11-14 -> mục 15-20. Đầu tài liệu có chú giải nhãn nguồn; mỗi mục lớn có dòng "Sources".
5. Cuối tài liệu lập 3 bảng rà soát: 🤖 giả định (Section | Item | Action), ⏳ TBD, 💭 đã xác nhận.
6. Đặt trạng thái DRAFT v1, chờ PQA + CTO Group review. Sau khi ký, theo dõi chỉ số theo mục 2 và kiểm tra tuân thủ tailoring ở các cổng.
7. Quyết định tự động theo ngữ cảnh (🤖, PM phải kiểm): Internal R&D -> kiểu "Khác", giảm ngân sách, CR chuyển CTO điều chỉnh scope (mục 1, 10); Internal và > 100MD -> thêm đào tạo "Internal product domain" (mục 19); risk có R-TEC-* mức High -> architecture spike ở Phase 1 (mục 4); lịch từng có G3 HOLD -> siết checklist G3 (mục 5); không có KH bên ngoài -> Sales/AM là N/A, KH = PQA/nội bộ (mục 1, 12).

## Công thức, ngưỡng & tín hiệu (bảng: tên | công thức/điều kiện | ngưỡng | hành động khi vượt; không có thì ghi "Không có")
Mục 2 - Dev-MT-Test (bộ chỉ số chính):

| # | Chỉ số | Công thức | LCL | Target | UCL | Owner | Tần suất đo |
|---|---|---|---|---|---|---|---|
| 1 | Tỉ lệ comment code | Số comment / LOC (LOC = dòng thay đổi) | - | - | - | TL | Weekly + Milestone + End |
| 2 | Chất lượng testcase | (comment nội bộ + feedback KH) / total TC | - | - | - | TestLead | Sau review testcase |
| 3 | Bug rate | Bug nội bộ / công số thực tế theo rank | 3.55 | 4.57 | 8.4 Bug/MM | PM | Weekly + Milestone + End |
| 4 | Correction Rate | Công số Correction / công số thực tế theo rank (Correction = fix bug + verify bug) | - | - | - | PM | Weekly + Milestone |
| 5 | CSS (Customer Satisfaction Score) | Theo công thức CSS hiện hành | 80 | 90 | 100 điểm | Sales | Milestone + End |
| 6 | DRE (Defect Removal Efficiency) | bug nội bộ / (bug nội bộ + bug KH) | 0.94 | 0.98 | 1.0 | PQA | Milestone + End |
| 7 | Tỉ lệ leakage | Tổng bug sau release / công số thực tế theo rank | 0 | 0.15 | 0.3 Bug/MM | PQA | Theo sự kiện (sau release) |
| 8 | EE (Effort Efficiency) | (Re-estimate + CR charge) / MM x hệ số rank | 95% | 100% | 110% | PM | Weekly + Milestone + End |
| 9 | Timeliness | SP đúng hạn / Tổng SP x 100% | 100% | 100% | 100% | PM | (nguồn không ghi) |
| 10 | Process Compliance | Tổng điểm trung bình các item PQA đánh giá | 85 | 92.46 | 100 điểm | PQA | Milestone + End |
Dự án AI có thêm "Độ chính xác" (công thức theo lĩnh vực AI, owner và tần suất tự xác định). Hành động khi vượt LCL/UCL: nguồn không nêu; các chỉ số này được theo dõi bằng tín hiệu giám sát (nguồn chưa rõ: hành động cụ thể).

Mục 3 - dự án Document:

| # | Chỉ số | Công thức | LCL | Target | UCL | Owner | Tần suất |
|---|---|---|---|---|---|---|---|
| 1 | Tỉ lệ feedback tài liệu KH | Comment KH / số page (số sheet Excel + số page doc) | - | - | - | PM | Milestone + End |
| 2 | CSS | Theo công thức CSS hiện hành | 80 | 90 | 100 | Sales | Milestone + End |
| 3 | EE | Như công thức Dev-MT-Test | 95% | 100% | 110% | PM | Weekly + Milestone + End |
| 4 | Timeliness | SP đúng hạn / Tổng SP | 100% | 100% | 100% | PM | - |
| 5 | Process Compliance | Tổng điểm trung bình items PQA | 85 | 92.46 | 100 | PQA | Milestone + End |

Công thức EE chi tiết (đổi giờ công MH sang MM có hệ số rank):
- EE = EE_numerator / MM_used, với EE_numerator = Re-estimate + CR charge.
- Dự án Base: MM_used = tổng [(logwork_jira - OT_chưa_hệ_số + OT_đã_hệ_số) x hệ_số_rank] / 8 / 20.
- Dự án Labor: TH1 (Công chuẩn - lễ - mát > 20d VÀ ngày đi làm thực tế > 20d): MM = tổng [...] / 8 / số ngày đi làm thực tế. TH2 (công chuẩn - lễ - mát > 20d VÀ ngày đi làm < 20d): MM = tổng [...] / 8 / 20. TH3 (công chuẩn - lễ - mát < 20d): MM = tổng [...] / 8 / số ngày đi làm thực tế.
- Re-estimate: tổng công PM đánh giá lại đã được Trưởng bộ phận phê duyệt. Mẫu số gồm BrSE JP, KHÔNG gồm intern. CR charge: theo hệ số đã chốt với KH (Sales đã thu được tiền).
- (nguồn chưa rõ: ngày đi làm thực tế đúng bằng 20 không thuộc trường hợp nào; công thức EE_numerator trong tham chiếu không có "x hệ số rank" ở tử số, còn ở bảng chỉ số có.)

Các ngưỡng khác:

| Tên | Điều kiện | Ngưỡng | Hành động |
|---|---|---|---|
| CM Plan riêng | Dự án lớn | ≥ 10MM hoặc ≥ 3 member | Lập CM Plan (TPL-SW-02-01); dưới ngưỡng thì ghi trong mục 17 |
| Tài liệu kiểm soát thay đổi | Dự án nhỏ | < 10MM | Bắt buộc, làm cuối dự án |
| Chi phí phát sinh dự trù | Mục 10 | Đi lại 5.000.000; công tác phí 30.000.000; mua sắm thiết bị 15.000.000 (không gồm máy làm việc của member); teambuilding 5.000.000; tổng 55.000.000 VND | Sponsor xác nhận mặc định |
| Tần suất kiểm toán PQA | Mục 14 | Hàng quý (và theo milestone) | Báo cáo PQA quý + PQA cuối dự án; escalation PQA -> PM -> CTO |

## Template / mẫu đầu ra (rút gọn, giữ cấu trúc, cột, trường)
- Bìa: Tên kế hoạch, Mã dự án, Mã template TPL-SW-05-01, Template version 1.7, Document version, Ngày hiệu lực. Lịch sử thay đổi: Ngày | Trạng thái (A/M/D) | Nội dung | Phiên bản | Người thực hiện. Ký: Người duyệt (CTO), Người kiểm tra (PQA), Người tạo (PM).
- 1 Thông tin chung: Mã, tên, phase, kiểu dự án, ngày bắt đầu/kết thúc dự định, mục tiêu (2-3 câu), quy mô MM (cho team VN, KHÔNG tính BrSE bên Nhật), deadline; bảng giai đoạn release.
- 2-3 Mục tiêu (bảng ở trên). 4 Phương án phát triển: Waterfall / V-model / Agile (Scrum, Kanban) / Hybrid Waterfall-Agile / DevOps continuous / Khác.
- 5 Điều chỉnh quy trình (bảng # | Hạng mục | Tài liệu | Hướng dẫn | Thực hiện O/X | Lý do không). Danh sách 11 PROC: PROC-SW-01 gia công tổng thể (bắt buộc); PROC-SW-02 quản lý cấu hình (bắt buộc); PROC-SW-05 quản trị dự án (bắt buộc); PROC-SW-03 phát triển + quản lý yêu cầu (bắt buộc); PROC-SW-04 Design (tuỳ scope, bỏ khi KH chuyển design); PROC-SW-06 Code (bắt buộc nếu có code); PROC-SW-09 Fix bug (bắt buộc); PROC-SW-10 Bamboo CI/CD (tuỳ, bỏ khi KH có CI riêng); PROC-QA-01 Kiểm thử (bắt buộc); PROC-SW-08 Release app (tuỳ, chỉ mobile app); PROC-SW-09 Quản lý CR (tuỳ, khi có CR). (Nguồn dùng PROC-SW-09 cho cả Fix bug và Quản lý CR - nguồn chưa rõ.) Một số hạng mục tiêu biểu: ước lượng (TPL-SW-01-03-01, bắt buộc); đo CPI và SPI (TPL-SW-05-06, bắt buộc với Project-based); checklist Security (TPL-SW-01-08, bắt buộc); final inspection (TPL-SW-01-04); biên bản nghiệm thu (TPL-SW-01-02); Test plan (TPL-QA-01-01), Test Viewpoint (TPL-QA-01-10), Test Summary Report, checklist for release (TPL-SW-01-05) đều bắt buộc; Q&A (TPL-SW-03-05) bắt buộc (Excel hoặc Jira); code review checklist (TPL-SW-06-01) bắt buộc; đóng dự án: báo cáo kết thúc (TPL-SW-05-08) và meeting minutes bắt buộc.
- 6 Sản phẩm bàn giao: Phase | Sản phẩm (Design, Source code, Testing document, Release note) | Ngày (= ngày hợp đồng) | Ghi chú.
- 7 Kế hoạch review: Sản phẩm | Loại (Group/One-person) | Người review | Khi nào. Ví dụ: Project plan - Group, PQA + CTO, cuối giai đoạn chuẩn bị; URD/SRS/RM sheet/Use Case - Group, khi đạt 90% tìm hiểu yêu cầu; Design - Group, khi đạt 90% giai đoạn design; Test plan - Group, khi đạt 90% công việc; Testcase, test data - Group, sau mỗi function/module; CM Plan - One-person.
- 8 Kế hoạch kiểm thử: loại test (Unit, Integration, System, UAT, Performance, Security, Regression, Load/Stress, Compatibility), môi trường (Dev, Staging, UAT, Pre-production, Production), bảng thiết bị (Loại | Thông số | Số lượng | Ghi chú).
- 9 Ước tính: Phase (Requirements, Design, Development, Testing, Release) | Effort plan MD | Note; dòng Total.
- 11 Milestones: hai bảng, thoả thuận với KH và nội bộ (Khái quát công việc | Thời gian | Sản phẩm). Cột mốc chuẩn G1-G6.
- 12 Truyền thông: nội bộ (báo cáo tiến độ daily meeting hàng ngày; Q&A hàng ngày; họp PMO hàng tuần) và bên ngoài (báo cáo KH email + weekly call).
- 13 Rủi ro: Nguồn | Risk | Ảnh hưởng | Khả năng | Biện pháp. 14 PQA: chủ PQA, tần suất, phạm vi (Bug rate, DRE, Leakage, EE, Timeliness, Process Compliance), phương pháp (Group review milestone + spot check hàng tuần).
- 15 Nhân sự: (I) Vị trí | Họ tên | Skill hiện tại | Skill cần có | Đánh giá phù hợp; (II) Vị trí | Tên | % tham gia | Lịch. 16 Khung phase: Khởi động (KHDA, KHCT); Dịch tài liệu (nếu KH JP; TLYC); Phân tích thiết kế (TKTT, TKCT, TKCSDL); Lập trình; Kiểm thử (KHKT, KBKT, BCKT, HDSD); Chuyển giao.
- 17 CM (danh mục tài liệu cho dự án < 10MM: loại | tên | owner | phân quyền). 18 Tài nguyên (phần mềm, phần cứng, cloud, tài liệu). 19 Đào tạo: Technical, Business domain, Process (Quality system 3 hrs; Configuration management 2 hrs; Group review 4 hrs; bắt buộc Quality và CM). 20 Hướng dẫn thứ tự hoạt động (hoạt động 1 đầu tiên; 2 và 3 sau 1; 4 sau 2; 5 sau cả 2 và 3; 6 sau 4 và 5).
- Sign-off: Project Manager, Giám đốc SBU/CTO, PQA reviewer.

## Lỗi thường gặp & lesson learned (sai gì -> hậu quả -> cách tránh)
| Sai | Hậu quả | Cách tránh |
|---|---|---|
| Đoán khi thiếu charter/lịch/WBS | Kế hoạch sai gốc | Dừng, hoàn tất tài liệu nguồn trước |
| Tự dung hoà mâu thuẫn charter - lịch - WBS | Sai lệch ngầm | Hỏi người quyết định |
| Bỏ hạng mục quy trình bắt buộc không có lý do | Không tuân thủ, bị PQA trừ điểm | Chỉ chọn X kèm lý do được xác nhận |
| Đổi cận LCL/Target/UCL cố định (📋) tuỳ ý | Chỉ số mất ý nghĩa | Chỉ ghi đè khi có lý do, do bộ phận chất lượng quyết |
| Không rà các mục 🤖 | Giả định sai được ký | Rà bảng 🤖 trước khi ký |
| Tính MM đội VN kèm BrSE bên Nhật | Sai quy mô | Mục 1: quy mô cho team VN, không tính BrSE JP (còn mẫu số EE thì gồm BrSE JP, không gồm intern) |
| Lẫn phiên bản kế hoạch và phiên bản template | Nhầm hồ sơ | Nâng version kế hoạch thủ công, tách riêng version template |
| Không cập nhật khi có CR lớn/chuyển phase | Kế hoạch lệch | Cập nhật khi CR đáng kể, chuyển phase, kiểm toán quý |
| Milestone/Risk trong plan không khớp lịch/risk register | Mâu thuẫn tài liệu | Đối chiếu trước khi trình duyệt |

## Ví dụ minh họa (ngắn, có số; dựng thì ghi "(ví dụ dựng)")
(ví dụ dựng) <tên-dự-án> Project-based, Dev-MT-Test. Bug nội bộ 50, công thực tế 12 MM theo rank -> Bug rate = 50/12 = 4,17 Bug/MM: nằm trong [3.55; 8.4], gần Target 4.57. Bug nội bộ 49, bug KH 1 -> DRE = 49/(49+1) = 0.98, đạt Target. EE: Re-estimate + CR charge = 11,4 MM, MM_used = 12 -> EE = 95%, chạm LCL. Dự án 8 MM, 2 member (< 10MM và < 3 member) nên CM ghi inline, không cần CM Plan riêng; ngân sách phát sinh mặc định 55.000.000 VND do Sponsor xác nhận.

## Tự kiểm tra (3-5 câu hỏi, đáp án ngắn ngay dưới)
1. Bộ ba LCL/Target/UCL của Bug rate và DRE? -> Bug rate 3.55 / 4.57 / 8.4 Bug/MM; DRE 0.94 / 0.98 / 1.0.
2. Khi nào phải có CM Plan riêng? -> Dự án ≥ 10MM hoặc ≥ 3 member; nhỏ hơn thì ghi inline.
3. Công thức MM_used cho dự án Base? -> Tổng [(logwork - OT_chưa_hệ_số + OT_đã_hệ_số) x hệ_số_rank] / 8 / 20.
4. Hạng mục quy trình bắt buộc muốn không làm thì sao? -> Đánh X kèm lý do được xác nhận, không bỏ im lặng.
5. Ngân sách phát sinh mặc định gồm những gì và tổng bao nhiêu? -> Đi lại 5M, công tác phí 30M, thiết bị 15M, teambuilding 5M; tổng 55.000.000 VND.

## Liên quan (bài trước/sau)
- Trước: 01-kickoff (charter, risk seed); WBS, lập lịch, ghép nhân sự (chương 03 và 05).
- Sau: theo dõi tín hiệu/chỉ số (chương 06), kiểm tra cổng G1-G6, checklist review theo mục 7, quản lý rủi ro sống (chương 04), Change Request khi cần tái baseline kế hoạch.
