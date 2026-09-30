# Từ điển thuật ngữ PM (cho người mới học)

Nguồn: 35 bài trong `chapters/` (giáo trình PM Kaopiz). Nghĩa được lấy đúng như các bài dùng; chỗ bài không định nghĩa rõ thì ghi "(bài chưa định nghĩa rõ)".
Cách đọc mã bài: `Ch4·04` = chương 4, bài 04 (Rủi ro và issue). Riêng bài tổng quan là `Ch0·00`.
Các bài gọi chung là bài; thuật ngữ tiếng Anh giữ nguyên như trong bài.

## Bảng chữ cái

| Thuật ngữ | Nghĩa | Bài |
|---|---|---|
| **0-9** | | |
| 3 dot vote | Bình chọn 3 phiếu, chọn top 3 mục làm action trong buổi retro. | Ch9·01 |
| 3P | Progress / Plans / Problems: cập nhật việc đã làm, sẽ làm, vướng mắc. P1 viết thì quá khứ, P2 tương lai, P3 hiện tại; mỗi phần tối đa 5 gạch đầu dòng. | Ch7·03 |
| 4Ls | Định dạng retro cho phase: Liked / Learned / Lacked / Longed for. | Ch9·01 |
| 5 Whys | Hỏi "Why" tới 5 lần để ra Root Cause rồi ghi Systemic Fix; dùng cho sự cố/hold/abort nghiêm trọng (retro trong 48 giờ). | Ch9·01 |
| **A** | | |
| A (trong RACI) | Accountable: người chịu trách nhiệm cuối cùng, mỗi việc chỉ 1 người. | Ch2·01 |
| AC (acceptance criteria) | Tiêu chí chấp nhận gắn với yêu cầu; task REQ là "chốt AC + UC flow", unit test viết theo AC. Trong "BR/AC" là business rule / acceptance criteria. | Ch3·02, Ch6·05 |
| AC (trong EVM) | Tổng actual_effort của các task (effort thực tế cộng dồn). Bài không mở rộng chữ viết tắt. | Ch6·01, Ch6·03 |
| Acceptant Test | Giá trị trường "QC Activity" trên Jira; bug mang giá trị này là bug khách hàng (lọt sang giai đoạn nghiệm thu). | Ch6·05 |
| Acceptance (chấp nhận) | Khách xác nhận bằng lời/email (điều kiện để bắt đầu closeout), sau đó ký chính thức. | Ch9·02 |
| ACCEPT / ACCEPTED | Chiến lược rủi ro: sống chung với rủi ro, phải ghi lý do; "monitor" trơn là chấp nhận trá hình. | Ch4·04 |
| Action (MA/RA) | Việc chi tiết xử lý một rủi ro (Mitigation Action, MA-NNN) hoặc vấn đề (Resolution Action, RA-NNN); 1 hàng = 1 việc, có PIC, Due, Status, Evidence. | Ch4·04 |
| Action item (retro) | Hành động cải thiện có owner cụ thể + deadline cụ thể + trạng thái (Open / In Progress / Done); không được là "Team" hay "ASAP". | Ch7·04, Ch9·01 |
| activity_date / standup_date | activity_date là ngày dữ liệu; standup_date = activity_date + 1 ngày, dùng ở tiêu đề báo cáo daily. | Ch4·02 |
| ADD / UPDATE / ESCALATE / REVIEW | Bốn thao tác trên sổ rủi ro/vấn đề: thêm mới; đổi trạng thái/trường; nâng rủi ro đã xảy ra thành vấn đề; rà soát hằng tuần. | Ch4·04 |
| AI-01 đến AI-15 | 15 nhóm action item rút từ kho lesson learned (vd AI-01 confirm spec với khách, AI-05 khoanh vùng ảnh hưởng, AI-10 quản lý release, AI-11 thận trọng production, AI-13 nhịp communication, AI-15 resource/risk/scope). Mỗi nhóm có Owner, ưu tiên và DoD. | Ch7·04 |
| AM | "Sales/AM": bài dùng AM phụ trách họp định kỳ với khách, xử lý invoice, CR, đổi nhân sự, trouble. Chữ đầy đủ bài chưa định nghĩa rõ. | Ch2·01 |
| Anchors | Phần của Sailboat: điều kéo chậm dự án lại (ma sát quy trình, phụ thuộc, nợ). | Ch9·01 |
| Anomaly | Bất thường trong báo cáo tuần (overdue quá ngưỡng, signal lệch, rủi ro tăng cấp, E3 vượt ngưỡng); mỗi anomaly 🔴 phải có Recommended Action. | Ch7·01 |
| Append-only | Chỉ ghi thêm, không sửa/xóa dòng cũ (nhật ký hypercare, nhật ký kiểm toán gate, History của rủi ro, Lịch sử bàn giao). | Ch8·04, Ch8·02 |
| APPROVE / DEFER / REJECT | Ba đề xuất quyết định cho một CR (kèm điều kiện); PM chỉ đề xuất, Sponsor duyệt. | Ch4·03 |
| Approved-as-is (A) | Nhóm item review: reviewer xác nhận đúng, không cần đổi; không chặn sign-off. | Ch2·03 |
| Archive checklist | Mục 9 của closeout: danh sách lưu trữ (tag source `vX.Y.Z-final`, tài liệu, báo cáo cuối...), PM tự tick khi đã làm thật. | Ch9·02 |
| Ask % / ask/tell ratio | Tỉ lệ câu hỏi so với phát biểu của người được coaching; mục tiêu theo loại họp (Standup 30-40%, Review 50%+, Decision 20-30%, Customer sync 40-50%). | Ch7·02 |
| Assignee | Người đang được gán ticket (trạng thái hiện tại), không chứng minh ai đã làm; công việc ghi công theo performer. | Ch4·01, Ch4·02 |
| Auto (loại mục checklist) | Mục kiểm tra tự động từ dữ liệu (git/CI/PQA), thiếu dữ liệu thì `[NO_DATA]`. | Ch6·02 |
| Availability (mức rảnh) | % thời gian còn nhận việc của một người, suy từ số ticket đang mở, không vượt participation rate. | Ch3·05 |
| **B** | | |
| BA | Vai trò chốt yêu cầu/đặc tả (REQ, BD); BA Lead là A của SRS và duyệt G2; bổ sung AC khi có spec gap. Chữ đầy đủ bài chưa nêu. | Ch2·01, Ch3·04, Ch6·05 |
| BAC | Budget at Completion: tổng effort kế hoạch. | Ch6·03 |
| Baseline | Bản kế hoạch đã duyệt và "đóng băng" (lịch, phạm vi) làm mốc so sánh; thay đổi sau đó đo so với nó. Trong hypercare, baseline là giá trị tín hiệu chụp trước deploy. | Ch3·03, Ch4·03, Ch8·04 |
| Baseline schedule locked | Mốc kết thúc giai đoạn 2 Planning trong vòng đời. | Ch0·00 |
| Batch (chế độ) | Ghép người cho cả list task (Team Match); hoặc mỗi thành viên onboard là một cặp file riêng. | Ch3·05, Ch5·03 |
| BD (Basic Design) | Thiết kế cơ bản; M3 BD Approved, gate G3, và mã công đoạn BD trong track Dev. | Ch0·00, Ch3·02 |
| Bench | Người/năng lực dư chưa có việc (gap dương, tô vàng); hành động đề xuất như cross-train. | Ch1·02 |
| Bid / Bid ID | Việc chào giá trước khi có dự án; Bid ID dạng `BID-YYYY-NNN`. | Ch1·01 |
| Blocker | Việc bị chặn tiến độ. Jira công ty không có status Blocked nên blocker (J2) là task không phải Bug ở status Confirmming hoặc Bug chưa Done (loại Rejected/Pending). | Ch4·01, Ch4·02 |
| BLOCK 🔴 | Đề xuất của checklist khi có Critical fail > 0; chỉ là đề xuất, gate review mới quyết. | Ch6·02 |
| BR | Business rule; xuất hiện trong "BR/AC" khi đọc spec để phân tích spec gap. | Ch6·05 |
| BrSE | Vai trò cầu nối khách hàng (Q&A, review spec, CR, truy cập hệ thống PM); "BrSE JP" là BrSE bên Nhật (tính trong mẫu số EE, không tính vào quy mô MM đội VN). Giống PM nhưng không có quyền management. | Ch5·03, Ch2·02 |
| Buffer | Phần đệm cộng thêm theo loại hợp đồng (Fixed-bid 15%, T&M 10%, Offshore 20%, R&D 25%, Internal 10%, Compliance 20%); áp lên đường găng khi lập lịch. Bản nháp chờ QA xác nhận. | Ch1·01, Ch3·03 |
| Bug category (6 loại) | Sáu nhóm bug thật: UI/UX, Data/Logic, Validation, State/Navigation, Session/Auth, Integration/Sync. | Ch6·05 |
| Bug khách hàng / bug nội bộ | Dựa trên QC Activity: `Acceptant Test` là bug khách hàng, mọi giá trị khác hoặc rỗng là bug nội bộ. | Ch6·05 |
| Bug rate | Bug nội bộ / công số thực tế (theo rank), đơn vị Bug/MM; LCL/Target/UCL = 3.55 / 4.57 / 8.4; chủ: PM. | Ch2·02, Ch6·01 |
| Burn-up | Slide 3 trong dàn ý steering ("Burn-up mốc"). Bài chưa định nghĩa rõ; burndown không xuất hiện trong bài nào. | Ch7·03 |
| Bus factor (BUS_FACTOR, R02) | Cờ 🔴 khi một người chiếm >= 70% PR merged + cập nhật Jira (cuộn 7 ngày). | Ch4·02 |
| BV | Mã công đoạn test: verify bug của module; nuôi QS-TST-08. | Ch3·02 |
| **C** | | |
| Candidate pool | Nhóm ứng viên xếp người: chỉ gồm thành viên đã thuộc dự án. | Ch3·05 |
| Capacity | Công số sẵn có (md) của SBU/vai trò/nhóm trong một kỳ (tháng, tuần, sprint); so với effort kế hoạch ra utilization. | Ch1·02, Ch3·03, Ch3·04 |
| Capture (chế độ) | Chế độ daily sync ngay sau standup: ghi quyết định miệng, action item, blocker mới; nối thêm vào file prep cùng ngày. | Ch4·01 |
| Carry-forward | Action item của retro trước chưa Done, chuyển sang sprint này (đánh dấu 🔁, mã CF-01...). PM xác nhận từng mục. | Ch7·04 |
| Carry-over | Task chuyển sang ngày sau; Iron Law cấm ("no carry-over"): task > 1 md phải tách. | Ch3·02, Ch0·00 |
| Catalog bài học | Sổ bài học tích lũy qua các dự án, mỗi dòng mã `L-YYYY-NNN`, kèm Mitigation; nuôi báo giá và kickoff dự án sau. | Ch9·01 |
| Charter (Project Charter) | Tài liệu khai sinh dự án theo mẫu TPL-SM-02-01 (11 mục + Approval + phụ lục Sales/AM); DRAFT v1 chờ duyệt. | Ch2·01 |
| Checklist | Danh sách Pass/Fail/N-A thủ công cho gate/phase/release/module; khác signal và không đưa vào tính QS-XX. | Ch6·02 |
| CM | Configuration Management (quản lý cấu hình); PROC-SW-02; CM Plan riêng (TPL-SW-02-01) khi dự án >= 10MM hoặc >= 3 member. | Ch2·02 |
| Code freeze | Bước chốt nhánh trước release (Tech Lead); là prereq nếu đã freeze. | Ch8·03 |
| COMM | Mã task Common (communication), 1 task mỗi dự án, effort 0.5/tuần. | Ch3·02, Ch3·03 |
| Committed | Công số còn lại đã cam kết cho dự án đang chạy (dự báo năng lực); hoặc tổng effort task gán cho một vai trò trong sprint. | Ch1·02, Ch3·04 |
| Competency | Năng lực chuẩn hóa 0-1 từ level L1-L5 (tuyến tính hoặc senior-weighted). | Ch3·05 |
| Compliance | (a) Loại hợp đồng, buffer 20%; (b) nhóm rủi ro; (c) mẫu tuân thủ khi CR loại Customer; (d) Process Compliance. | Ch3·03, Ch4·04, Ch4·03 |
| Confirmming | Status Jira của công ty (viết đúng hai chữ m): chờ khách/xác nhận; task ở đây bị coi là blocker. | Ch4·02 |
| Contract baseline / Current baseline | Contract baseline = tính năng trong charter lúc ký hợp đồng (không đổi); Current baseline = contract baseline + mọi CR đã duyệt tính đến ngày as-of. | Ch6·04 |
| Contract type | Fixed-bid / T&M / Offshore / R&D / Internal (thêm Compliance ở buffer/ngưỡng); quyết định buffer, risk seed, ngưỡng tín hiệu, cách tính tiền CR. | Ch2·01, Ch3·03 |
| Corrective / Preventive / Defect Repair | Ba loại hành động điều chỉnh: sửa sai lệch đã xảy ra / ngăn xảy ra hoặc tái diễn / sửa một deliverable cụ thể không đạt. | Ch7·01 |
| Correction Rate | Công số Correction (fix bug + verify bug) / công số thực tế theo rank; không có ngưỡng cố định. | Ch2·02, Ch6·01 |
| CPI | Cost Performance Index = EV / AC; >= 1 đúng/dưới ngân sách; ngưỡng mặc định >= 0.95 Fixed-bid, >= 0.90 T&M; < 0.85 là nghiêm trọng. | Ch6·01, Ch6·03 |
| CR (Change Request) | Yêu cầu thay đổi chính thức đối với baseline, cần đo tác động 5 chiều và chữ ký Sponsor. Sáu loại: Scope, Tech, Schedule, Quality, Resource, Customer. | Ch4·03 |
| CR charge | Công số CR khách đã chốt hệ số và Sales đã thu tiền; cộng vào tử số của EE. | Ch2·02, Ch6·01 |
| Critical (loại mục checklist) | Mục chặn: fail thì gate ABORT/đề xuất BLOCK, luôn phải có bằng chứng. | Ch6·02 |
| Critical (Level rủi ro) | Mức cao nhất; chưa xử lý sau 1 ngày phải leo thang ngay lên Sponsor. | Ch4·04 |
| Critical path (đường găng) | Chuỗi task dài nhất quyết định ngày kết thúc; buffer áp lên chuỗi này. | Ch3·03 |
| CSS | Customer Satisfaction Score, điểm 1-100; LCL/Target/UCL = 80 / 90 / 100; chủ: Sales. | Ch2·02, Ch6·01 |
| CTO | Người duyệt Project Plan cùng PQA (Group review); ký Người duyệt. | Ch2·02 |
| Customer PIC | Đầu mối phía khách hàng, đồng duyệt các gate G2, G3, G5, ký closeout. Bài chưa định nghĩa riêng chữ này. | Ch2·01, Ch8·02 |
| **D** | | |
| D1, D2 / W1 | Hạn tương đối trong checklist onboarding: Dn = ngày thứ n, Wn = tuần n. | Ch5·03 |
| DACI Timeline | Định dạng retro theo dõi từng quyết định lớn: Decision, Driver, Approver, Contributors, Informed, Outcome, Lesson. | Ch9·01 |
| Daily sync (standup snapshot) | Bản chụp nhanh 1 trang đầu ngày (blocker, xong hôm qua, đang làm, quá hạn, mới, git); 2 chế độ prep và capture. | Ch4·01 |
| Deferred (D) | Nhóm item review ngoài scope hiện tại, chuyển CR hoặc phase sau; không chặn sign-off nhưng cần CR nếu có tác động. | Ch2·03 |
| Deliverable | Tài liệu/sản phẩm đo được ở cuối phase (vd SRS Approved, UAT Report). | Ch3·01 |
| Delta (scope) | Thay đổi phạm vi của từng CR: Added (+), Removed (-), Modified (~). | Ch6·04 |
| Depends on | Cột phụ thuộc giữa task: BD sau REQ, DEV sau BD, UT sau DEV, TE sau TC và mọi DEV của module. | Ch3·02 |
| deprecated (tag) | Gắn cho task của section bị xóa; không xóa cứng để giữ audit. | Ch3·02 |
| design-change-after-coding (tag) | Section §6/§7 đổi sau khi DEV in-progress/done; nuôi QS-DSG-03 và E3. | Ch3·02 |
| DEV | Mã công đoạn phát triển trong track Dev (theo function); DEV/UT giao cho Dev. | Ch3·02, Ch3·04 |
| Diff (chế độ) | Chế độ so sánh phiên bản spec cũ/mới để sinh task delta và tag; cần `spec_version`. | Ch3·02 |
| DoD | Tiêu chí hoàn thành của mỗi nhóm action item AI-xx. | Ch7·04 |
| Dominance | Cờ khi một người chiếm > 60% tổng số từ trong cuộc họp. | Ch7·02 |
| DRAFT / DRAFT v1 | Trạng thái mặc định của mọi tài liệu đầu ra: bản nháp chờ người có thẩm quyền duyệt/ký; PM không tự gửi hay tự ký. | hầu hết các bài (vd Ch2·01, Ch8·01) |
| DRE | Defect Removal Efficiency = bug nội bộ / (bug nội bộ + bug khách hàng); LCL/Target/UCL = 0.94 / 0.98 / 1.0; chủ: PQA. | Ch2·02, Ch6·01 |
| **E** | | |
| E3 | Tín hiệu chênh lệch effort thực tế so với kế hoạch = (actual - planned) / planned x 100%; ngưỡng mặc định <= 10% (theo dõi hằng tuần từ Planning). Ở Ch7·01 bản chính định nghĩa E3 = actual% - planned% (chênh lệch % hoàn thành). | Ch0·00, Ch6·01, Ch6·03, Ch7·01 |
| EAC | Estimate at Completion: dự báo tổng effort khi hoàn thành. EVM: AC + (BAC - EV) / CPI; báo cáo tuần: actual_to_date + phần còn lại; > BAC thì cảnh báo và đề xuất CR. | Ch6·03, Ch7·01 |
| EE | Effort Efficiency = (Re-estimate + CR charge) / MM_used (x hệ số rank); LCL/Target/UCL = 95% / 100% / 110%; chủ: PM. | Ch2·02, Ch6·01 |
| Effort unit | Đơn vị effort: md mặc định (1 md = 8 mh); có thể chọn mh. | Ch3·03, Ch6·03 |
| EMV | Expected Monetary Value: `EMV_per_risk = probability x financial_impact` trong phân tích rủi ro nâng cao. | Ch4·04 |
| Epic / module | Nếu spec chỉ tới mức epic/module, task ghi mức Module-level, không ép xuống function. | Ch3·02 |
| Escalation (4 mức) | Level 1 mâu thuẫn đội (PM, trong tuần); Level 2 nguồn lực/scope/rủi ro (PM Lead + SBU Manager, 3 ngày); Level 3 chiến lược/khách hàng (Sponsor + Director, 1 ngày); Level 4 khủng hoảng (CEO + Legal). | Ch2·01 |
| ESCALATE / ESCALATED | Rủi ro đã xảy ra thành hậu quả thật -> tạo ISSUE liên kết; trạng thái rủi ro ESCALATED. Chỉ áp cho rủi ro OPEN hoặc IN_MITIGATION. | Ch4·04 |
| ETC | Estimate to Complete: dự báo effort còn lại; EVM: EAC - AC. | Ch6·03 |
| EV | Earned Value = tổng(planned_effort x % hoàn thành) theo task. | Ch6·01, Ch6·03 |
| EVM | Earned Value Management: bộ chỉ số CPI, SPI, EV, AC, PV, EAC, ETC, VAC theo chuẩn PMI. | Ch0·00, Ch6·03 |
| Evidence | Bằng chứng đã làm thật của một action (link ticket, mail, commit, tài liệu); chưa có ghi `⏳`; DONE thiếu Evidence chỉ cảnh báo 🟡. | Ch4·04 |
| Exit criteria | Tiêu chí thoát hypercare: 0 sự cố P1, mọi tín hiệu trong ngưỡng, không escalation từ khách, snapshot đủ N/N ngày. | Ch8·04 |
| Exposure | Tổng mức phơi nhiễm rủi ro; cờ khi > 2 lần baseline. Bài không định nghĩa exposure và baseline. | Ch4·04 |
| **F** | | |
| F-<PROJ>-<MOD>-NN | Feature ID / function: đơn vị đo chất lượng (vd F-KM-REL-04). | Ch3·01, Ch3·02 |
| Fixed-bid | Loại hợp đồng giá cố định: buffer 15%, 8 risk seed mặc định, Impact scope/estimate ở mức Critical, ngưỡng tín hiệu chặt (QS-REQ-01 >= 95%). | Ch1·01, Ch2·01, Ch4·04 |
| Filler | Từ đệm (ờ, à, kiểu, kiểu như, uh, um, like...); cờ khi > 5/phút. | Ch7·02 |
| FTE | Dùng trong "Min FTE (avg)" và "5 FTE blended"; bài chưa định nghĩa rõ, không nêu công thức. | Ch1·01, Ch3·03 |
| Function | Đơn vị đo chất lượng; module là nhóm function dùng để lập lịch, gate, release. | Ch3·02 |
| **G** | | |
| G1-G6 | Sáu gate: G1 Charter (Initiation), G2 SRS, G3 BD, G4 code, G5 UAT (Ch0·00 tách G5a/G5b), G6 Go/No-go release. Điểm ra quyết định cuối mỗi giai đoạn dựa trên tín hiệu + checklist + rủi ro. | Ch0·00, Ch8·02 |
| G5a / G5b | Chỉ Ch0·00 chia: M5a System Test Done (G5a) và M5b UAT Sign-off (G5b: QA Lead + Customer PIC). Các bài khác chỉ có G5 = UAT Sign-off. | Ch0·00 |
| Gap (năng lực) | capacity - committed - (pipeline_demand x win_probability); dương = bench, âm = overcommit. | Ch1·02 |
| Gate | Điểm ra quyết định đi tiếp hay không ở cuối giai đoạn/milestone. | Ch0·00, Ch8·02 |
| Gate review | Bước chấm gate bằng tín hiệu + checklist + số rủi ro High/Critical mở, đề xuất GO / HOLD / ABORT; stakeholder mới ký. | Ch8·02 |
| Genuine bug | Bug thật: spec định nghĩa rõ, hành vi thực tế khác spec. | Ch6·05 |
| GHOST (R01) | Cờ 🔴: thành viên roster phân bổ >= 10% nhưng không có hoạt động Jira/Bitbucket trong cửa sổ. | Ch4·02 |
| GO / GO with risks | Quyết định gate: mọi tiêu chí đạt (kèm kế hoạch giảm thiểu nếu còn 1-2 rủi ro High/Critical). | Ch8·02 |
| GO / HOLD / NO-GO (bid) | Khuyến nghị cuối của bản ước tính chào giá. Bài chưa định nghĩa riêng HOLD ở đây. | Ch1·01 |
| Go-live (M6) | Mốc đưa lên production; G6 là gate Go/No-go trước đó. | Ch0·00 |
| Greedy | Chính sách gán việc mặc định: một người nhận nhiều task nếu remain_avail còn đủ. | Ch3·05 |
| Group review / One-person review | Review nhiều người (Project plan, SRS, design, test plan) vs một người (CM Plan). | Ch2·02 |
| **H** | | |
| Handover | Bàn giao: cho team support khi đóng dự án, hoặc bàn giao công việc khi thành viên rời/chuyển. | Ch5·01, Ch9·02 |
| Healthy | Trạng thái năng lực: net gap từ -10 đến +50 md/quý. | Ch1·02 |
| Hedging | Từ rào đón làm yếu câu quyết định (có lẽ, tôi nghĩ là, I think, maybe); cờ khi > 3/phút. | Ch7·02 |
| HiPPO | Quyết định theo ý kiến người có chức vụ cao nhất; gate và chấm điểm bằng dữ liệu để tránh. | Ch0·00, Ch1·01 |
| HOLD (gate) | Duyệt có điều kiện: nêu tiêu chí trượt, điều kiện, ngày review lại mặc định +5 ngày làm việc; quá hạn thì leo thang Sponsor. | Ch8·02 |
| Hotfix | Loại release vá khẩn (hypercare 24h, review mỗi 4h). | Ch8·01, Ch8·04 |
| Hybrid | (a) Vòng đời Waterfall-Agile (mặc định trong Project Plan); (b) định dạng retro mặc định: START/STOP/CONTINUE x 4 chiều. | Ch2·02, Ch9·01 |
| Hypercare | Giai đoạn giám sát chặt sau go-live: Major 7 ngày, Minor 3, Patch 1, Hotfix 24 giờ; so tín hiệu với baseline trước deploy; kết thúc khi hết cửa sổ và mọi chỉ số xanh. | Ch0·00, Ch8·04 |
| **I** | | |
| I (trong RACI) | Informed: được thông báo (một chiều). | Ch2·01 |
| ICE | (Impact x Confidence x Ease) / 3, mỗi thành phần thang 1-10; phân loại nhanh backlog. Bài ghi ví dụ mâu thuẫn công thức. | Ch1·01 |
| Idempotent | Chạy lại sinh task vẫn theo Task ID, chỉ thêm task mới, giữ Est/Status PM đã điền. | Ch3·02 |
| IDENTITY_GAP (R10) | Cờ 🟡: user Bitbucket/Jira không ghép được với roster. | Ch4·02 |
| Impact | Mức tác động của rủi ro: Low / Medium / High / Critical; rủi ro Scope/Estimate được calibrate theo loại hợp đồng. | Ch4·04 |
| Initiation | Giai đoạn 1: kickoff, charter, risk seed, RACI; M1 Charter Approved, G1. | Ch0·00 |
| Internal | Loại hợp đồng nội bộ: buffer 10%; risk seed thêm R-PRI-01, R-RES-02. | Ch2·01, Ch3·03 |
| Iron Law | Mỗi task hoàn thành trong <= 1 md; ước lượng > 1 md bắt buộc tách. | Ch3·02 |
| Issue | Vấn đề đã xảy ra (có tác động thực, hạn giải quyết); ID `ISSUE-NNN`; sổ riêng (issue log). Severity chỉ High/Medium/Low. | Ch4·04 |
| **J** | | |
| J2 | Định nghĩa blocker của công ty trên Jira (task Confirmming hoặc Bug chưa Done, loại Rejected/Pending). | Ch4·02 |
| **K** | | |
| Kano | Mô hình phân loại (Must-be / Performance / Excitement / Indifferent / Reverse) cho chiến lược đầu tư từng nhóm. | Ch1·01 |
| Kickoff | Khởi động dự án: lập charter, RACI, risk seed (Ch2·01). | Ch2·01 |
| KLOC | Nghìn dòng code, mẫu số của mật độ lỗi QS-TST-02 (defects / KLOC). | Ch6·01 |
| ksystem | Hệ thống quản lý dự án chung của công ty; nguồn `ksystem_project_code` và dữ liệu seed khi tiếp quản PM. Bài dùng như tên hệ thống. | Ch1·03, Ch5·04 |
| **L** | | |
| L-YYYY-NNN | Mã một bài học trong catalog (vd L-2026-001); ghi kèm Mitigation. | Ch9·01 |
| Labor / Project-based / Base / Khác | Kiểu dự án trong Project Plan, ảnh hưởng cách tính MM_used và bộ chỉ số (dự án Document có bộ riêng). | Ch2·02 |
| LCL / Target / UCL | Cận dưới / mục tiêu / cận trên của một chỉ số chất lượng. | Ch2·02, Ch6·01 |
| Leakage | Tỉ lệ bug sau release / công số thực tế theo rank (Bug/MM); LCL/Target/UCL = 0 / 0.15 / 0.3; đo theo từng release; chủ: PQA. | Ch2·02, Ch6·01 |
| Lecture mode | Người được coaching có > 2 lần độc thoại > 200 từ. | Ch7·02 |
| Level (rủi ro) | Mức tra ma trận Likelihood x Impact: Low / Medium / High / Critical; không tự gõ tay. Quy tắc leo thang: Critical 1 ngày, High 3, Medium 7, Low 14. | Ch4·04 |
| Level L1-L5 | Thang năng lực khi xếp người; không có kỹ năng thật thì suy từ chức danh (job title proxy) và gắn `[PROXY]`. | Ch3·05 |
| Lessons learned | Rút kinh nghiệm cuối phase/release/dự án theo 4 chiều (Process, Team, Customer, Technical), ra action item + catalog. | Ch9·01 |
| Likelihood | Khả năng xảy ra: L < 30%, M 30-70%, H > 70%. | Ch4·04 |
| LOC | Số dòng thay đổi (không phải tổng dòng code) khi tính tỉ lệ comment code. | Ch2·02, Ch6·01 |
| LTV | Vai trò dev (Dev/Frontend/Backend) trong roster và xếp người; bài không mở rộng chữ. | Ch3·05, Ch4·02 |
| **M** | | |
| M0-M7 | Milestone: M1 Charter Approved, M2 SRS Approved, M3 BD Approved, M4 Code Complete, M5a System Test Done, M5b UAT Sign-off, M6 Go-live, M7 Project Closed; M0 là mốc pre-project. | Ch0·00 |
| MA-NNN | Mã Mitigation Action của rủi ro; tăng đơn điệu, không tái dùng số. | Ch4·04 |
| Major / Minor / Patch / Hotfix | Bốn loại release, quyết định cửa sổ hypercare 7 ngày / 3 ngày / 1 ngày / 24 giờ. | Ch8·01, Ch8·04 |
| Margin | Biên lợi nhuận cộng lên chi phí; mặc định 20%; Sales quyết, ghi `margin_override` nếu đổi. | Ch1·01 |
| MD / md | Man-day (người-ngày). 1 MM = 20 MD; 1 md = 8 mh; task <= 1 md. | Ch0·00, Ch3·02 |
| MH / mh | Man-hour (người-giờ). 1 MM = 160 MH; 1 md = 8 mh. | Ch0·00, Ch6·03 |
| Milestone | Mốc cần đạt, tối thiểu 1 mỗi phase, gắn tín hiệu neo; ngày milestone = late finish của task cuối phase. | Ch0·00, Ch3·01, Ch3·03 |
| Mitigate | Chiến lược giảm rủi ro (cùng accept, transfer, avoid). | Ch4·04 |
| Mitigation velocity | closed / raised của rủi ro; < 0.5 là chậm tiến độ. | Ch4·04 |
| MM | Man-Month (người-tháng). 1 MM = 20 MD = 160 MH. | Ch0·00, Ch2·01 |
| Module | Nhóm function/cluster; đơn vị lập lịch, gate, release; track Test theo module. | Ch3·02 |
| MoSCoW | Must 60% / Should 20% / Could 10% / Won't 10% tổng phạm vi; chia phase (M = Phase 1, S = Phase 2, C = Phase 3). Nếu mọi thứ đều Must thì vô nghĩa. | Ch1·01 |
| Monte Carlo | Với dự án > $100k hoặc > 6 tháng: mô phỏng 10k lần lấy mẫu P/I để ra vùng đệm ở mức tin cậy 50/80/95%. | Ch4·04 |
| Must-fix (M) | Nhóm item review chặn sign-off (sai/thiếu/vi phạm business rule); Must-fix Open > 0 thì NOT READY. | Ch2·03 |
| **N** | | |
| N/A | Not applicable: mục checklist/bàn giao không áp dụng (kèm ghi chú); không tính vào Pass rate. | Ch5·01, Ch6·02 |
| `[NEEDS_CONFIRM]` | Nhãn cho loại NFR chưa có tiêu chí thành công, cần PM xác nhận. | Ch2·01 |
| NFR | Yêu cầu phi chức năng (hiệu năng, bảo mật, tuân thủ); ánh xạ thành tiêu chí thành công đo được trong charter. | Ch2·01 |
| Nice-to-have (N) | Nhóm item review cải thiện, PM tự quyết, không chặn sign-off. | Ch2·03 |
| `[NO_DATA]` | Nhãn khi thiếu dữ liệu; không bịa, không bỏ mục. | nhiều bài (vd Ch6·01, Ch7·01) |
| NO-GO | Khuyến nghị bỏ bid (cạnh GO/HOLD); G6 còn gọi Go/No-go release. | Ch1·01, Ch0·00 |
| Non-delivery | Việc không phải giao hàng (họp, đồng bộ khách, quản lý dự án, deploy ops); loại khỏi báo cáo PM nhưng giờ worklog vẫn cộng. | Ch4·02 |
| NOT READY / READY | Kết luận sign-off spec: Must-fix Open > 0 -> NOT READY; = 0 -> READY. | Ch2·03 |
| NOT_REVIEWED (proxy) | Giá trị Decision của proxy gate (chưa chạy Gate review). | Ch5·04 |
| NPS | Chỉ số hài lòng khách (đối chiếu với CSS ở PMI: NPS/CSAT); do PM cung cấp, thiếu thì `[NO_DATA]`. Bài chưa định nghĩa công thức. | Ch6·01, Ch9·02 |
| **O** | | |
| O / X (tailoring) | O = thực hiện hạng mục quy trình; X = không thực hiện và phải ghi lý do. | Ch2·02 |
| Offshore | Loại hợp đồng: buffer 20%; risk seed thêm múi giờ, ngôn ngữ, onboarding. | Ch1·01, Ch2·01 |
| one_per_member | Chính sách gán tối đa 1 task mới mỗi người; task thừa vào danh sách chưa gán. | Ch3·05 |
| Onboarding brief / todo | Brief là tài liệu "đọc trước" cho người mới; todo là checklist việc để làm (12 trường, 4 nhóm A/B/C/D). | Ch5·02, Ch5·03 |
| Open / Closed (bug) | Open = To Do, In Progress, Confirmming, Feedback; Closed = Done, Resolved, Deployed. | Ch6·05 |
| Open item (RC-...) | Một ý kiến/câu hỏi cần xử lý trong review spec; ID `RC-<feature-code>-<NNN>`, đủ ID, Description, Section ref, Raised by. | Ch2·03 |
| Original Estimate (origin estimate) | Estimate ban đầu trên ticket; thiếu (với ticket đã có worklog) vào danh sách "Quy trình" cần nhắc. | Ch4·02 |
| OVER / WARN / OK | Utilization sprint theo vai trò: > 100% OVER, >= 90% WARN, < 90% OK. Lập lịch tuần: > 100% OVER, < 50% UNDER. | Ch3·03, Ch3·04 |
| Overcommit | Năng lực thiếu: net gap -10 đến -50 md/quý (Critical khi < -50). | Ch1·02 |
| Overdue / quá hạn | planned_end (duedate) < hôm nay và chưa xong; trong standup không tính Resolved/Deployed. | Ch4·01, Ch7·01 |
| Owner | Người chịu trách nhiệm tổng của một risk/issue (1 tên cụ thể, không ghi "team"). | Ch4·04 |
| **P** | | |
| P1-P4 (sự cố) | Mức nghiêm trọng sự cố sau release; P1 critical dừng sinh hoạt hằng ngày, chuyển ứng phó khẩn cấp (hotfix/rollback). Bài chưa định nghĩa chi tiết P2-P4. | Ch8·04, Ch9·02 |
| Participation rate | % thời gian được phân bổ cho dự án (vd 50 hoặc 100); mức rảnh ban đầu không vượt trần này. | Ch3·05 |
| PARTIAL | Đánh dấu báo cáo tuần chạy giữa tuần, hoặc kết quả log release khi window chưa xong. | Ch7·01, Ch8·03 |
| Pending from Customer | Mục trong báo cáo khách: việc đang chờ phía khách kèm hạn cần có. | Ch7·03 |
| Phase / Phase distribution | Giai đoạn vòng đời; phân bổ công số chuẩn Requirements 8% / Design 18% / Development 50% / Testing 18% / Project Mgmt 6%. | Ch1·01, Ch3·01 |
| PIC | Người thực thi một action cụ thể (responsible, cấp action), có thể khác Owner. "Customer PIC" là đầu mối bên khách. | Ch4·04 |
| Pipeline demand | Nhu cầu từ bid chưa thắng, tính có trọng số theo xác suất thắng. | Ch1·02 |
| Plus / Delta | Định dạng retro hai cột: điều hiệu quả / điều sẽ thay đổi; hợp phiên phản hồi khách. | Ch9·01 |
| PM-* | Mã task PM: PM-KICKOFF, PM-PLAN, PM-TRACK, PM-GATE, PM-CLIENT, PM-RETRO, PM-OTHER (effort mặc định: KICKOFF 2, PLAN 3, TRACK 0.5/tuần, GATE 1/gate). | Ch3·02, Ch3·03 |
| PMI | Chuẩn quốc tế: CPI/SPI, DDE/DRE, NPS/CSAT... đối chiếu với chỉ số công ty. | Ch6·01 |
| PMO | Họp PMO hàng tuần, kênh lãnh đạo/PMO; bài chưa định nghĩa rõ. | Ch2·02, Ch5·03 |
| PQA | Bộ phận đảm bảo chất lượng quy trình; đo DRE, leakage, Process Compliance; review Project Plan cùng CTO. | Ch2·02 |
| PR / PR_JIRA_DRIFT (R06) | PR (pull request); cờ 🟡 khi PR đã merge mà Jira liên kết không thuộc Done/Resolved/Deployed. | Ch4·02 |
| PRD / STG | Môi trường production / môi trường trước đó (bài dùng "STG với PRD"); không tạo/sửa/xóa trên PRD khi chưa báo và được khách đồng ý. Bài không mở rộng chữ viết tắt. | Ch7·04, Ch5·03 |
| PROC-* | Mã quy trình công ty trong tailoring Project Plan: PROC-SW-01 gia công tổng thể, SW-02 quản lý cấu hình, SW-03 phát triển + yêu cầu, SW-04 Design, SW-05 quản trị dự án, SW-06 Code, SW-08 Release app, SW-09 (Fix bug và Quản lý CR, bài ghi trùng), SW-10 Bamboo CI/CD, QA-01 Kiểm thử. | Ch2·02 |
| Process Compliance | Điểm trung bình các item PQA audit, 1-100; LCL/Target/UCL = 85 / 92.46 / 100; đối chiếu QS-PRC-07. | Ch2·02, Ch6·01 |
| Project Plan | Tài liệu master theo mẫu TPL-SW-05-01 v1.7 (22 mục), PQA + CTO Group review. | Ch2·02 |
| `[PROXY]` / proxy | Nhãn cho dữ liệu suy đoán thay thế (level từ chức danh; proxy gate; SPI/SV proxy tính theo số task). | Ch3·05, Ch5·04, Ch7·01 |
| Proxy gate | Milestone hệ thống dùng thay gate; không phải quyết định G1-G6 chính thức (Decision = NOT_REVIEWED). | Ch5·04 |
| PV | Planned Value = tổng planned_effort đến hiện tại. | Ch6·01, Ch6·03 |
| **Q** | | |
| QS-XX | Tín hiệu chất lượng định lượng gắn với milestone/gate (mã dạng QS-REQ-01...). Chỉ đo, không quyết; người quyết là gate review. | Ch0·00, Ch6·01 |
| QS-REQ-01 | Tỉ lệ review yêu cầu đạt = reviewed_pass / total_reviewed x 100%; G2: >= 95%. | Ch3·01, Ch6·01 |
| QS-REQ-03 | Độ đầy đủ truy vết UC - feature - test = mapped / total features; G2: = 100%. | Ch3·01, Ch6·01 |
| QS-DSG-03 | Tỉ lệ lỗi thiết kế = design_defects / total_design_items; G3: <= 5%. | Ch3·01, Ch6·01 |
| QS-DEV-cov | Unit test coverage = covered_lines / total_lines; G4: >= 80% (ký hiệu đặc biệt không theo dạng QS-XXX-NN). | Ch3·01, Ch6·01 |
| QS-PRC-07 | Tuân thủ quy trình = tasks_followed_process / total_tasks; G4 và G6: >= 90%. | Ch3·01, Ch6·01 |
| QS-TST-02 | Mật độ lỗi (defects / KLOC); G5a: <= baseline của dự án. | Ch3·01, Ch6·01 |
| QS-TST-04 | Tỉ lệ lọt lỗi = post_release_defects / total_defects; UAT: <= 2%. | Ch3·01, Ch6·01 |
| QS-TST-08 | Tỉ lệ reopen = reopened_bugs / total_bugs; UAT: <= 5%. | Ch3·01, Ch6·01 |
| QS-TST-09 | Độ phủ test (luồng/lỗi) = covered_flows / total_flows; do TVP + TC nuôi. | Ch3·02, Ch6·01 |
| QS-PRC-02, -06, -08 / QS-PRF-* / QS-OPS-* | Chỉ được nhắc tên (PM track nuôi QS-PRC-02/06/08; Performance QS-PRF-*; Availability QS-OPS-*); bài chưa định nghĩa rõ ý nghĩa. | Ch3·02, Ch2·01 |
| Quote range | Khoảng giá chào Low (cạnh tranh) / Mid (tiêu chuẩn, khuyến nghị) / High (buffer thoải mái). | Ch1·01 |
| **R** | | |
| R-<CAT>-NN | Mã rủi ro (vd R-SCOPE-01, R-EFF-01); risk seed theo loại hợp đồng. | Ch2·01, Ch4·04 |
| R01-R11 | 11 cờ rủi ro tự động của báo cáo daily: GHOST, BUS_FACTOR, WORKLOG_GAP, WORKLOG_TEAM, ALLOCATION_EXPIRED, PR_JIRA_DRIFT, STALE_PR, BLOCKER_AGING, UNASSIGNED_WIP, IDENTITY_GAP, OVERALLOCATED. | Ch4·02 |
| R1, R2... (review round) | Vòng review spec; vòng mới tăng số vòng, giữ nguyên ID item cũ. | Ch2·03 |
| RA-NNN | Mã Resolution Action của vấn đề. | Ch4·04 |
| RACI | Bảng vai trò: R Responsible, A Accountable (chỉ 1), C Consulted (hai chiều), I Informed (một chiều); chỉ ghi vai trò, không ghi tên. | Ch2·01 |
| Rank (hệ số rank) | Hệ số theo cấp bậc dùng khi quy đổi giờ công sang MM; bài chưa nêu bảng hệ số. | Ch2·02, Ch6·01 |
| Rate card | Bảng đơn giá theo người-ngày; không tự bịa. | Ch1·01, Ch4·03 |
| Re-baseline | Chốt lại lịch/baseline sau khi CR được duyệt (lưu bản cũ `schedule-v{N}-YYYYMMDD` hoặc `schedule.v<N>`); mặc định xếp hàng (`--queue`) hoặc làm ngay (`--rebaseline-now`). | Ch3·03, Ch4·03 |
| Re-estimate | Tổng công PM đánh giá lại đã được Trưởng bộ phận phê duyệt; tử số của EE. | Ch2·02 |
| READY 🟢 | Đề xuất checklist: tất cả Pass. | Ch6·02 |
| Realize By / Realized as issue | Hạn dự kiến rủi ro có thể xảy ra / rủi ro đã xảy ra thành issue thật. | Ch4·04, Ch9·02 |
| Registry | File `projects.yaml` lưu định danh dự án: `jira_key`, `bitbucket_project_key`, `ksystem_project_code` (bắt buộc), không commit vào git. | Ch1·03 |
| REQ | Mã công đoạn chốt yêu cầu (AC + UC flow), 0.5 md; giao BA. | Ch3·02, Ch3·04 |
| Release | Đợt bàn giao lên production, ID `R-<PROJ>-NN`; release plan có 7 mục, áp nhiều template (N-N). | Ch8·01 |
| Reopen rate | QS-TST-08. | Ch6·01 |
| Resource (CR/nhóm rủi ro) | CR loại Resource: nghỉ việc/mở rộng; nhóm rủi ro Resource. | Ch4·03, Ch4·04 |
| Retro / Retrospective | Họp nhìn lại; retro sprint (giữa dự án, format ngắn) khác Lessons learned (cuối phase/dự án, 4 chiều). | Ch7·04, Ch9·01 |
| REVIEW (checklist) 🟡 | Đề xuất khi Standard fail > 20%. | Ch6·02 |
| RICE | (Reach x Impact x Confidence) / Effort (person-month). | Ch1·01 |
| Risk | Sự kiện tương lai chưa chắc chắn (xác suất x tác động); ghi vào risk register. | Ch4·04, Ch7·01 |
| Risk markup | Phần cộng thêm vào công số theo bài học/rủi ro miền (vd banking +10% tổng, lặp BD +25% Design). | Ch1·01 |
| Risk seed | Bộ rủi ro khởi điểm theo loại hợp đồng (Fixed-bid 8, T&M 6, thêm Offshore/R&D/Internal). | Ch2·01 |
| Rollback | Quay lui sau deploy; trigger: Critical bug > 30% người dùng trong 4h, hiệu năng suy giảm > 50%, customer escalation P1, dữ liệu hỏng; PM quyết định (tham vấn Tech Lead + Sponsor). | Ch8·01, Ch8·03 |
| Root cause | Nguyên nhân gốc; nhóm bug theo root cause (Requirement/Coding/Test/Communication). | Ch7·04, Ch9·01 |
| Roster | Danh sách thành viên dự án (vai trò, % phân bổ, ngày vào/ra); ngày phân bổ hết hạn không tự loại người khỏi dự án. | Ch4·02 |
| RTM | Requirements Traceability Matrix: xác định luồng nghiệp vụ liên quan và khoanh vùng ảnh hưởng. | Ch7·04 |
| RTO | Recovery Time Objective: thời gian phục hồi mục tiêu, mặc định 30 phút (ghi cả trong ghi sự cố hypercare). | Ch8·01, Ch8·04 |
| **S** | | |
| Sailboat | Định dạng retro dự án: Sun, Wind, Anchors, Rocks, Island. | Ch9·01 |
| SBU | Đơn vị kinh doanh (đơn vị có capacity riêng); SBU Manager phân bổ nguồn lực; gồm trong charter. Bài chưa mở rộng chữ. | Ch1·02, Ch2·01 |
| Schedule | Lịch: ngày từng task, dependency, đường găng, milestone, capacity; DRAFT v1. | Ch3·03 |
| Scope creep | Phạm vi lan âm thầm khi thay đổi không đo tác động/không có chữ ký; trong báo cáo tuần = unplanned_in_progress / total_in_progress x 100% (<= 10% xanh, > 10% vàng, > 20% đỏ). | Ch4·03, Ch7·01 |
| Scope growth % | (features_added - features_removed) / total_original x 100. | Ch6·04 |
| Seed (bộ hồ sơ seed) | Hồ sơ dựng nhanh từ hệ thống khi tiếp quản PM (lịch, status, gates, risk, CR); 3 chế độ seed-lessons, seed-closeout, refresh. | Ch5·04 |
| Severity | Mức nghiêm trọng của issue: High / Medium / Low; CR: Trivial / Low / Medium / High / Critical theo ma trận. | Ch4·04, Ch4·03 |
| Signal (tín hiệu) | Chỉ số định lượng "đồng hồ chất lượng" so với ngưỡng; gắn 🟢🟡🔴. | Ch6·01 |
| Signal anchor | Tín hiệu định lượng neo vào milestone để biết "đạt chưa". | Ch3·01 |
| Sign-off | Xác nhận chính thức rằng spec/gate/closeout đủ tốt; với spec là ngưỡng đếm được (Must-fix Open = 0). | Ch2·03 |
| SPI | Schedule Performance Index = EV / PV; >= 1 kịp tiến độ; ngưỡng mặc định >= 0.95 Fixed-bid, >= 0.90 T&M. | Ch6·01, Ch6·03 |
| SPI proxy / SV proxy | Bản thích ứng theo số task: SPI proxy = tasks done / tasks planned tuần này; SV proxy = done - planned. | Ch7·01 |
| Spec change | Thay đổi spec do khách (giờ công lớn, nhiều mục, thiếu UI design) xử lý bằng CR; tag `spec-change`/`rework` nuôi QS-REQ-01, QS-PRC-07. | Ch2·01, Ch3·02 |
| Spec gap | Hành vi bị báo là bug nhưng spec thiếu/mơ hồ; chuyển Bug -> Improvement (comment Jira trước, đổi type sau, khi PM duyệt). | Ch6·05 |
| Sponsor | Người duyệt charter, CR, các gate và ký closeout; người nhận leo thang. Bài chưa định nghĩa riêng. | Ch2·01, Ch4·03 |
| Sprint / sprint backlog / sprint goal | Mặc định 2 tuần = 10 ngày làm việc; backlog là tập task cam kết; goal 1-2 câu do PM viết, chép nguyên văn. | Ch3·04 |
| SRS | Bộ tài liệu đặc tả yêu cầu; nguồn cho vision, scope, feature list (§4), NFR (§7); M2 SRS Approved/G2. Chữ viết tắt bài không mở rộng. | Ch2·01, Ch0·00 |
| SSOT | Nguồn template chuẩn (DB của công cụ quản lý); thiếu thì dùng danh mục dự phòng. | Ch8·01 |
| Stage | Công đoạn (REQ, BD, DEV, UT, TP, TVP, TC, TE, BV, TR...); quyết định tín hiệu nào được nuôi. | Ch3·02 |
| Stale | Ticket không cập nhật N ngày = max(0, ngày báo cáo - ngày updated). | Ch4·02 |
| Standard (loại mục checklist) | Mục thông thường, cần review thủ công + bằng chứng. | Ch6·02 |
| START / STOP / CONTINUE | Bắt đầu / ngừng / tiếp tục làm gì; mỗi nhóm 1-3 mục; retro nhanh < 30 phút. | Ch9·01 |
| Status code | 🟢 On track / 🟡 At risk / 🔴 Off track của báo cáo tuần (theo overdue, % complete, SPI, scope creep). | Ch7·01 |
| Status weekly | Báo cáo trạng thái tuần (chiều thứ Sáu, tuần ISO YYYY-Www). | Ch7·01 |
| Steering | Đối tượng truyền thông: dàn ý 5-10 slide (8 slide), chiến lược, quyết định cần ra. | Ch7·03 |
| Success criteria | Tiêu chí thành công đo được ánh xạ từ NFR; hoặc cột tiêu chí thành công của action item retro. | Ch2·01, Ch9·01 |
| SV | Schedule Variance; SV proxy = tasks done - planned tuần này (dương = sớm). | Ch7·01 |
| **T** | | |
| T&M | Time and Material: buffer 10%; risk seed 6; Impact scope theo giờ thực tế Medium (mm_committed: High). | Ch1·01, Ch4·04 |
| Tailoring | Điều chỉnh quy trình: quyết định O/X cho từng hạng mục của 11 quy trình PROC. | Ch2·02 |
| TBD (⏳) | Chưa có, chờ bổ sung; không bịa URL/số. | nhiều bài |
| TC | Mã công đoạn: tạo và review testcase của module (0.5-1 md); giao QA. | Ch3·02, Ch3·04 |
| TE | Mã công đoạn: thực thi test e2e/manual của module; phụ thuộc TC và mọi DEV của module. | Ch3·02 |
| Tech Lead (TL) | Vai trò A cho kiến trúc, BD, DEV, UT; duyệt G3, G4. | Ch2·01, Ch8·02 |
| Template (TPL-*) | Mẫu tài liệu công ty. Trong bài: TPL-SM-02-01 (charter, v1.3), TPL-SW-05-01 (Project Plan, v1.7), TPL-SW-02-01 (CM Plan), TPL-HR-14-01 (kế hoạch bàn giao), TPL-SW-01-* / TPL-QA-01-* (tài liệu trong tailoring); TPL-STD-WEB, TPL-STD-API, TPL-MIG-DB, TPL-HOTFIX, TPL-CUSTOMER-A, TPL-INT-3RD là template release dự phòng. | Ch2·01, Ch2·02, Ch5·01, Ch8·01 |
| Timeliness | Số SP bàn giao đúng hạn / tổng SP x 100%; mục tiêu 100% (mọi bàn giao chậm đều tính). | Ch2·02, Ch6·01 |
| TP / TVP / TR | Track Test: Test Plan / Test Viewpoint / Test Report của module (mỗi loại 1 md). | Ch3·02, Ch3·03 |
| Track | Bốn track task: Dev (theo function), Test/QA (theo module), PM, Common. | Ch3·02 |
| Trigger (rủi ro) | Điều kiện chuyển rủi ro thành vấn đề. | Ch4·04 |
| **U** | | |
| UAT | User Acceptance Test; M5b UAT Sign-off/G5 với QS-TST-08 <= 5%, QS-TST-04 <= 2%. | Ch0·00, Ch8·02 |
| UC | Use case; ví dụ "UC flow", truy vết UC - feature - test. Bài không mở rộng chữ. | Ch3·02, Ch6·01 |
| Underutilized | Trạng thái năng lực: net gap > +50 md/quý. | Ch1·02 |
| Utilization | Committed / capacity x 100%; tuần lập lịch > 100% OVER hoặc < 50% UNDER. | Ch3·03, Ch3·04 |
| UT | Mã công đoạn unit test theo AC (0.5 md); giao Dev. | Ch3·02 |
| **V** | | |
| VAC | Variance at Completion = BAC - EAC; âm = vượt ngân sách. | Ch6·03 |
| Variance / Variance % | actual - planned; (actual - planned) / planned x 100%. | Ch6·03 |
| Vault | Kho bí mật; tài liệu chỉ ghi "credential: see vault: <đường dẫn>", không ghi mật khẩu/token. | Ch5·01, Ch9·02 |
| Velocity | Khối lượng thực tế làm xong ở sprint trước (md hoặc số task) làm thước cho lần chọn sau (cảnh báo khi lệch > 20%); ở báo cáo tuần = số task done/tuần. | Ch3·04, Ch7·01 |
| **W** | | |
| Walk / prereq | Bước còn lại trong đêm deploy (DB migration, application deploy, smoke test...) / bước phải xong trước (G5, checklist pre-deploy, G6 GO). | Ch8·03 |
| WBS | Work Breakdown Structure: cây Project - Phase - Deliverable - Work Package; chỉ tạo slot WP, không sinh task chi tiết, không đặt lịch. | Ch3·01 |
| Weighted demand | Công số bid x xác suất thắng; bid dưới 40% loại khỏi nhu cầu có trọng số. | Ch1·02 |
| Window (deploy) | Khung ngày + giờ deploy đã chốt trong release plan (mặc định UTC+7). | Ch8·01 |
| Working set | Tập bug sau khi loại Rejected; mọi phân tích module/category dùng tập này. | Ch6·05 |
| WP (Work Package) | Nhóm công việc cùng một deliverable; ID `WP-<STAGE>-NN`, owner là một vai trò. | Ch3·01 |
| WPD / WPI / WPR | Work Performance Data (dữ liệu thô) / Information (đã phân tích) / Report (trình bày cho stakeholder = báo cáo tuần). | Ch7·01 |
| WSJF | Cost of Delay / Job Size; CoD = User-Business Value + Time Criticality + Risk Reduction/Opportunity; thang 1, 2, 3, 5, 8, 13, 20. | Ch1·01 |
| **Ký hiệu, nhãn** | | |
| 🟢 / 🟡 / 🔴 | Trạng thái màu. Tín hiệu: 🟢 khớp ngưỡng, 🟡 lệch 5-10%, 🔴 lệch > 10%. Báo cáo tuần: On track / At risk / Off track. Hypercare: Stable / Watch / Alert. Cờ rủi ro/action: 🔴 nặng, 🟡 cần chú ý. | Ch6·01, Ch7·01, Ch8·04 |
| ✅ / ⬜ / ☐ | ✅ đạt; ⬜ ô chờ ký, để trống; ☐ checkbox việc cần làm. | Ch8·02, Ch5·03 |
| ⏳ | TBD / chưa có (dùng cả trong Evidence chưa có). | Ch4·04 |
| 📄 📋 💭 🤖 🌐 | Nhãn nguồn số liệu: 📄 từ tài liệu; 📋 quy tắc công ty/mẫu cố định; 💭 PM xác nhận; 🤖 giả định/tự suy ra (PM phải rà lại); 🌐 dữ liệu hệ thống trực tiếp. | Ch2·01, Ch3·05 |
| 🔁 | Đánh dấu carry-forward "(from Sprint N-1)". | Ch7·04 |
| ↑ ↓ → | Xu hướng so với snapshot trước: cải thiện / xấu đi / ổn định (với Open bug thì ↑ là xấu). | Ch6·01, Ch6·05 |
| ● / ▲ | Phụ lục Sales/AM: ● vai trò chính, ▲ hỗ trợ. | Ch2·01 |
| `§UNKNOWN`, `Unnamed`, `⚠ cần PM` | Nhãn khi item review không rõ section/reviewer, hoặc task thiếu AC/Est/dependency cần PM điền. | Ch2·03, Ch3·02 |

## Cặp dễ nhầm

| Cặp | Phân biệt (theo các bài) | Bài |
|---|---|---|
| Risk vs Issue | Risk là sự kiện tương lai (ID `R-<CAT>-NN`, chiến lược mitigate/accept/transfer/avoid); Issue đã xảy ra (ID `ISSUE-NNN`, phản ứng resolve). Hai sổ riêng, không gộp một bảng; rủi ro thành hậu quả thật thì ESCALATE thành issue. | Ch4·04, Ch7·01 |
| CR vs scope creep | CR là yêu cầu thay đổi chính thức có đo tác động và chữ ký Sponsor; scope creep là thay đổi trôi vào dự án âm thầm không qua CR. Scope creep % trong báo cáo tuần chỉ là "ứng viên", PM xác nhận có phải thay đổi đã duyệt không. | Ch4·03, Ch7·01 |
| Scope creep % vs Scope growth % | Scope creep % (Ch7·01) = task ngoài baseline đang làm / tổng in-progress; Scope growth % (Ch6·04) = (added - removed) / tổng tính năng gốc của các CR đã duyệt. Bài nói rõ đây là hai khái niệm khác nhau. | Ch7·01, Ch6·04 |
| Baseline vs plan | Baseline là bản lịch/phạm vi đã duyệt, đóng băng, làm mốc so sánh (đổi chỉ qua CR + re-baseline); Project Plan là tài liệu master 22 mục; "planned" là số kế hoạch đo lệch với thực tế. Contract baseline không đổi, Current baseline cộng dồn CR. | Ch3·03, Ch2·02, Ch6·04 |
| G5a vs G5b | Chỉ Ch0·00 tách: G5a/M5a System Test Done và G5b/M5b UAT Sign-off (QA Lead + Customer PIC). Các bài khác chỉ có một G5 = UAT Sign-off; QS-TST-02 gắn System Test Done, QS-TST-08/04 gắn UAT. | Ch0·00, Ch3·01, Ch8·02 |
| Signal vs checklist | Signal đo bằng số, chỉ đo; checklist là Pass/Fail thủ công; hai luồng độc lập, gate review kết hợp cả hai để quyết. | Ch6·01, Ch6·02 |
| Proxy gate vs gate chính thức | Proxy gate là milestone hệ thống dùng thay, Decision = NOT_REVIEWED; quyết định G1-G6 chỉ có sau khi chạy Gate review. | Ch5·04, Ch8·02 |
| HOLD của gate vs HOLD của bid | Gate: duyệt có điều kiện, phải review lại (+5 ngày làm việc), khác GO và ABORT. Bid: HOLD là một khuyến nghị cạnh GO/NO-GO, bài không định nghĩa rõ. G6 còn gọi Go/No-go release. | Ch8·02, Ch1·01 |
| Owner vs PIC | Owner chịu trách nhiệm tổng cấp risk/issue (1 người); PIC thực thi một action cụ thể, có thể khác Owner và khác giữa các action. | Ch4·04 |
| MA vs RA | MA-NNN là action xử lý rủi ro (bảng Mitigation Actions); RA-NNN là action xử lý vấn đề (bảng Resolution Actions); không lẫn bảng. | Ch4·04 |
| Assignee vs performer | Assignee là trạng thái hiện tại; công (Resolved, merge...) ghi cho người thực hiện theo changelog/dòng thời gian PR. | Ch4·01, Ch4·02 |
| E3 vs EE vs CPI | Cùng đo hiệu quả effort: E3 (chênh lệch effort so kế hoạch, <= 10%), EE (95-110%, có Re-estimate + CR charge), CPI (EV/AC). Riêng E3 ở Ch7·01 còn có bản định nghĩa chênh lệch % hoàn thành (nguồn ghi hai định nghĩa). | Ch6·01, Ch6·03, Ch7·01 |
| SPI vs SPI proxy | SPI (EVM) = EV / PV; SPI proxy (báo cáo tuần) = task done / task planned tuần này, không tính theo chi phí. | Ch6·01, Ch7·01 |
| DRE vs leakage vs QS-TST-04 | DRE = bug nội bộ / (nội bộ + khách), muốn cao; leakage = bug sau release / công số (Bug/MM), muốn thấp; QS-TST-04 = post-release defects / total defects (%), <= 2%. | Ch6·01 |
| Spec gap vs genuine bug vs spec change | Spec gap: spec thiếu/mơ hồ nên dev làm theo cách hiểu hợp lý (chuyển Improvement, BA bổ sung AC). Genuine bug: spec rõ nhưng hành vi khác. Spec change: khách đổi yêu cầu, xử lý bằng CR. | Ch6·05, Ch2·01 |
| Deferred (D) vs DEFER | Deferred (D) là nhóm item review ngoài scope hiện tại, không chặn sign-off; DEFER là một đề xuất quyết định cho CR (khi High mà giá trị nghiệp vụ không rõ). | Ch2·03, Ch4·03 |
| Capacity vs availability vs participation rate | Capacity là công số sẵn có của SBU/vai trò/nhóm (md); availability là % rảnh của một người (từ ticket đang mở); participation rate là trần % phân bổ cho dự án, mức rảnh ban đầu = min(Jira avail, participation). | Ch1·02, Ch3·03, Ch3·05 |
| Velocity vs mitigation velocity | Velocity là khối lượng done mỗi sprint/tuần; mitigation velocity = rủi ro closed / raised (< 0.5 chậm). | Ch3·04, Ch7·01, Ch4·04 |
| P1 trong 3P vs P1 sự cố | Trong 3P, P1 = Progress (phần đầu). Trong sự cố, P1 là mức nghiêm trọng cao nhất (critical, cần ứng phó khẩn cấp); P1 cũng là mức customer escalation kích hoạt rollback. | Ch7·03, Ch8·04, Ch8·01 |
| Retro sprint vs Lessons learned | Retro sprint: giữa dự án, lặp lại, format ngắn (Went well / Didn't go well...). Lessons learned: cuối phase/release/dự án, 4 chiều, ra action item + catalog. | Ch7·04, Ch9·01 |
| Onboarding brief vs todo | Brief là tài liệu để ĐỌC bối cảnh; todo (checklist) là danh sách việc để LÀM với owner, ưu tiên, hạn. | Ch5·02, Ch5·03 |
| Bàn giao thành viên vs tiếp quản PM vs closeout | Bàn giao thành viên: một người rời/chuyển (TPL-HR-14-01). Tiếp quản PM: PM mới dựng lại hồ sơ seed từ hệ thống. Closeout: đóng cả dự án. Không thay thế nhau. | Ch5·01, Ch5·04, Ch9·02 |
| Level (rủi ro) vs Level L1-L5 | Level rủi ro là mức Low/Medium/High/Critical từ ma trận; Level L1-L5 là thang năng lực nhân sự khi xếp người. | Ch4·04, Ch3·05 |
