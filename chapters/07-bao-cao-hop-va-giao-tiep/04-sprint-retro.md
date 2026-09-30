---
title: Họp retrospective cuối sprint và kho bài học tích lũy
source: Sprint retro (Ch7·04)
stage: Cross-cutting
level: trung bình
prerequisites: [Ch4·04, Ch7·01]
---
# Họp retrospective cuối sprint và kho bài học tích lũy

## Mục tiêu học xong bạn làm được gì
- Chạy một buổi retro cuối sprint theo định dạng ngắn: Went well / Didn't go well / Blockers / Carry-forward / Action items.
- Viết action item đạt chuẩn (có owner cụ thể, deadline cụ thể, không mơ hồ) và theo dõi carry-forward sang sprint sau.
- Dùng 15 nhóm action item (AI-01 đến AI-15) rút từ kho lesson learned để gợi ý hành động cho từng mục "Didn't go well".
- Phân biệt retro sprint (giữa dự án, lặp lại) với Lessons learned (Ch9·01) cuối phase/dự án.

## Khi nào dùng (thời điểm, ai kích hoạt, điều kiện đầu vào)
- Thời điểm: cuối mỗi sprint, giữa dự án, lặp lại. KHÔNG phải tổng kết đóng dự án (cái đó là Lessons learned (Ch9·01), dạng đầy đủ 4 chiều).
- Người kích hoạt: PM, với ghi chú của PM và ý kiến từ team.
- Đầu vào BẮT BUỘC (thiếu thì dừng, không làm với dữ liệu thiếu): số sprint; ngày bắt đầu và kết thúc sprint (YYYY-MM-DD); ghi chú của PM hoặc ý kiến của team (văn bản tự do).
- Đầu vào TÙY CHỌN (bỏ qua thì ghi `[NO_DATA]`): mục tiêu sprint; sprint goal đạt chưa (Yes / Partial / No); velocity (story point hoặc số task); kế hoạch so với thực tế số task hoàn thành; danh sách người tham gia (PM, Tech Lead, Dev, QA...); retro sprint trước (không có thì carry-forward rỗng, ghi "[No previous retro found]").
- Ngày họp retro nên >= ngày kết thúc sprint; nếu sớm hơn phải xác nhận lại với PM.
- Không thuộc phạm vi: chỉ số code (metric kỹ thuật), quy trách nhiệm cá nhân, dạng Lessons learned (Ch9·01) đầy đủ 4 chiều.

## Khái niệm cốt lõi
- Bốn nhóm nội dung: Went well (tích cực, thành công); Didn't go well (friction, chậm, khó, sai); Blockers (chặn tiến độ trong sprint, chưa giải quyết); Carry-forward (action item của retro trước chưa Done).
- Action item: hành động có owner, deadline và trạng thái (Open / In Progress / Done).
- Carry-forward: mục chưa Done của sprint trước chuyển sang sprint này, đánh dấu 🔁 "(from Sprint N-1)".
- Không blame: tập trung vào quy trình và hệ thống, không gán lỗi cá nhân.
- Kho lesson learned tích lũy (xem mục dưới): dữ liệu do nhiều dự án ghi lại, đã được chắt thành 15 nhóm action item AI-01…AI-15, mỗi nhóm có Owner, "Vấn đề lặp lại" và DoD (tiêu chí hoàn thành).
- Ký hiệu nguồn số liệu: 📄 từ tài liệu | 📋 quy tắc công ty | 💭 PM xác nhận | 🤖 tự suy ra | ⏳ TBD / NO_DATA.

## Cách làm từng bước (thủ công, đủ chi tiết để làm theo; input/output)
**Bước 1. Chuẩn bị.** Input: số sprint, ngày sprint, ghi chú PM/team. Mở file retro của sprint trước (`sprint-(NN-1)`), lấy bảng Action Items, chọn các mục chưa Done làm carry-forward. Output: danh sách carry-forward (hoặc "không có").

**Bước 2. Thu thập thông tin sprint.** Ghi: số sprint (số nguyên, dùng làm NN trong tên file, đệm 2 chữ số), ngày bắt đầu/kết thúc, ngày họp (mặc định hôm nay), mục tiêu, đạt chưa, velocity, kế hoạch vs thực tế, người tham gia. Không có thì `[NO_DATA]`.

**Bước 3. Kiểm tra hợp lệ.**
- Số sprint là số nguyên dương; ngày bắt đầu < ngày kết thúc.
- Ngày họp >= ngày kết thúc sprint.
- Mỗi carry-forward có owner và deadline gốc; thiếu thì ghi "[missing owner/deadline in source retro]".
- MỌI action item phải có owner (tên hoặc role) và deadline (YYYY-MM-DD hoặc "Sprint N+1"). Thiếu thì hỏi lại; không tự gán, không bỏ qua.

**Bước 4. Phân loại.** Mỗi ý kiến vào đúng 1 nhóm (không đếm đôi):
- Went well: 1–5 mục.
- Didn't go well: 1–5 mục.
- Blockers: liệt kê nếu có.
- Carry-forward: kèm trạng thái Open / In Progress.
Quy tắc: ý mơ hồ như "communication cần cải thiện" thì hỏi lại: đây là Didn't go well hay là action item mới? Blocker đã giải quyết trong sprint: đưa vào Went well nếu giải sớm; vào Didn't go well nếu đã ảnh hưởng velocity. Carry-forward không tự đóng, PM xác nhận từng mục.

**Bước 5. Gợi ý action từ kho bài học.** Với mỗi mục Didn't go well:
1. Khớp nghĩa (không chỉ khớp từ khóa) với 1–2 nhóm AI bằng bảng map bên dưới.
2. Mở nhóm AI đó, chọn 1–3 improvement gốc sát bối cảnh nhất, giữ nguyên ý.
3. Cần thêm lựa chọn thì xem toàn bộ improvement của nhóm.
4. Không khớp nhóm nào thì ghi "[Không có gợi ý sẵn — PM tự định nghĩa]", đừng ép.
5. Một mục có thể map nhiều nhóm; gom gợi ý lại. PM chọn gợi ý thích hợp thành action item nháp; action item nháp vẫn phải có owner + deadline.

**Bước 6. Viết biên bản retro.** Theo khung ở mục Template; trạng thái DRAFT; thiếu dữ liệu ghi `[NO_DATA]`; không dùng ngôn ngữ đổ lỗi. Carry-forward chưa Done tự thành action item sprint này nếu PM xác nhận.

**Bước 7. Bàn giao.** Tóm tắt: số sprint, khoảng thời gian, số mục Went well, số Didn't go well, số action item (kể cả số đến từ gợi ý), số carry-forward. Trạng thái DRAFT chờ team review và ký. Nhắc đưa carry-forward chưa Done vào backlog sprint tiếp theo. Retro có lộ rủi ro hệ thống hay blocker thì mở mục trong sổ rủi ro/vấn đề. Cuối dự án, các retro sprint được tổng hợp vào Lessons learned (Ch9·01).

Bảng map nhanh (tín hiệu trong "Didn't go well" sang nhóm AI):

| Tín hiệu | AI gợi ý |
|---|---|
| Spec/yêu cầu mơ hồ, CR nhiều, hiểu sai yêu cầu | AI-01, AI-02 |
| Không đọc kỹ tài liệu, QA muộn | AI-02 |
| Bug do không khoanh vùng ảnh hưởng / degrade | AI-05 |
| Bug lọt do self-test sơ sài | AI-06 |
| Thiếu review code / review trễ | AI-07 |
| Estimate sai, timeline presale lệch thực tế, thiếu buffer | AI-12, AI-15 |
| Lỗi release/deploy/version/build/môi trường | AI-10 |
| Thao tác production/PRD sai, chưa double-check | AI-11 |
| Không tuân thủ workflow task / logwork, tiến độ/ưu tiên loạn | AI-14, AI-15 |
| Report nhiều/họp tốn effort, miss thông tin giữa các bên | AI-13 |
| Q&A/quyết định không lưu, mất tracking | AI-03 |
| Thiếu môi trường/thiết bị/data test | AI-09 |
| Testcase thiếu bao phủ, viết gộp | AI-08 |
| Tài liệu (DD/BD) thiếu/sai/chưa review | AI-04 |
| Resource/risk/scope/plan không thực tế | AI-15 |

## Công thức, ngưỡng & tín hiệu (bảng: tên | công thức/điều kiện | ngưỡng | hành động khi vượt)
Không có công thức số. Có các quy tắc định lượng và chuẩn kiểm sau.

| Tên | Điều kiện | Ngưỡng | Hành động khi vượt |
|---|---|---|---|
| Số mục mỗi nhóm | Went well; Didn't go well | 1–5 mục mỗi nhóm | Gộp hoặc chọn mục quan trọng nhất |
| Action item hợp lệ | Có owner + deadline | Bắt buộc 100% | Thiếu thì hỏi lại, không tự gán |
| Owner | Người cụ thể | Không được là "Team" | Chỉ định tên/role cụ thể |
| Deadline | YYYY-MM-DD hoặc "Sprint N+1" | Không được "ASAP" | Đặt ngày cụ thể |
| Mô tả action | Hành động cụ thể | Không được kiểu "Cải thiện communication" | Chia nhỏ thành hành động làm được |
| Carry-forward | Status khác Done ở retro trước | Mọi mục | Đưa vào backlog hoặc action item mới |
| Ngày họp | Ngày họp >= ngày kết thúc sprint | — | Xác nhận lại với PM |
| Độ ưu tiên nhóm AI | Xem bảng lesson learned bên dưới | 🔴 Cao / 🟡 TB | Ưu tiên xử lý nhóm 🔴 |

## Template / mẫu đầu ra (rút gọn, giữ cấu trúc, cột, trường)
```markdown
# Sprint NN Retro (DRAFT)
> Sources: 💭 PM notes + team input | 📄 sprint-(NN-1) retro (carry-forward)
(Bảng ký hiệu nguồn 📄 📋 💭 🤖 ⏳)

## Sprint Info
Sprint | Period (YYYY-MM-DD → YYYY-MM-DD) | Retro held | Sprint goal | Goal achieved? (Yes/Partial/No/[NO_DATA])
Velocity | Participants | Status = DRAFT

## Went Well            - [item]
## Didn't Go Well       - [item]
## Action item gợi ý theo Didn't go well
| Didn't go well | AI khớp | Action item gợi ý | Chọn? |   (chưa có gợi ý thì ghi "PM tự định nghĩa")
## Blockers             - [blocker hoặc "None this sprint"]
## Carry-forward from Sprint NN-1
| # | Action (from Sprint NN-1) | Owner | Original Deadline | Status |  (CF-01... ; Open / In Progress)
## Action Items
| # | Action | Owner | Deadline | Status |   (AI-01... ; Open)
```
Checklist sau khi viết: đã xác nhận số sprint và ngày; mỗi Didn't go well có gợi ý hoặc ghi PM tự định nghĩa; mỗi action item có owner + deadline không mơ hồ; carry-forward có trạng thái rõ; không có ngôn ngữ đổ lỗi; có bảng ký hiệu nguồn ở đầu; trạng thái DRAFT.

## Lỗi thường gặp & lesson learned (sai gì -> hậu quả -> cách tránh)
**A. Lỗi khi chạy retro**
- Action item mơ hồ ("Cải thiện communication") -> không ai làm, retro sau lặp lại y nguyên -> viết hành động cụ thể, kiểm được.
- Owner là "Team" hoặc deadline "ASAP" -> không có trách nhiệm giải trình -> một người cụ thể và ngày cụ thể.
- Quên carry-forward -> vấn đề cũ lặp lại -> luôn mở retro trước, xét từng mục chưa Done.
- Ngôn ngữ đổ lỗi -> team ngại nói thật -> nói về quy trình, không về người.
- Ép gán gợi ý không khớp -> action vô nghĩa -> không khớp thì ghi "PM tự định nghĩa".

**B. Kho lesson learned: cấu trúc dữ liệu (mô tả định tính)**
- Bảng gần 3.000 dòng (2.984), khoảng 266 mã dự án, mỗi dòng gồm 8 cột: STT | Project code | Project name | Title | Description | Improvement | Type | Label.
- Cột Type/Label do người ghi tự nhập nên không thống nhất. Nhiều nhãn gần nghĩa nhau, ví dụ: Coding (~484 dòng), Technical (~173), Communication (~153), Testing (~152) và Test (~142), Quản lý dự án (~85) và Project management (~46), Quản lý (~66), Quy trình (~64), Spec (~63), Requirement (~46), Tài liệu (~44). Vì vậy khi phân tích nên gom theo chủ đề nghĩa, không theo nhãn thô.
- Các nhóm mẹo kỹ thuật một lần (coding cụ thể, performance, tool/thư viện, kỹ năng cá nhân, khác) đã được loại khỏi 15 nhóm action item và coi là kho kiến thức kỹ thuật.

**C. 15 nhóm action item chắt lọc (số lượng improvement gốc, ưu tiên, owner, vấn đề lặp lại, DoD)**

| ID | Action item | Owner | Ưu tiên | Số improvement gốc |
|---|---|---|---|---:|
| AI-01 | Confirm & làm rõ spec/yêu cầu với KH trước khi code | BrSE / Dev / PM | 🔴 Cao | 225 |
| AI-02 | Đọc & phân tích kỹ tài liệu, QA sớm | Dev / Tester | 🔴 Cao | 159 |
| AI-03 | Note lại mọi Q&A / spec / quyết định | Cả team | 🔴 Cao | 107 |
| AI-04 | Review tài liệu nội bộ & mô tả đầy đủ trước khi gửi KH | Dev / BrSE / PM | 🔴 Cao | 123 |
| AI-05 | Xác định & test vùng ảnh hưởng trước khi sửa code/bug | Dev | 🔴 Cao | 154 |
| AI-06 | Self-test / self-review trước khi chuyển tester | Dev | 🟡 TB | 66 |
| AI-07 | Review chéo code & dùng checklist | Dev / Leader | 🟡 TB | 80 |
| AI-08 | Viết testcase clear, bao phủ đủ (RTM) & review TC | Tester | 🔴 Cao | 158 |
| AI-09 | Chuẩn bị & confirm môi trường / thiết bị / data test sớm | Tester / BrSE | 🟡 TB | 59 |
| AI-10 | Quản lý version/build & quy trình release/deploy | Dev / Leader | 🔴 Cao | 142 |
| AI-11 | Thận trọng thao tác production/PRD | Cả team | 🔴 Cao | 67 |
| AI-12 | Estimate có buffer, sát thực tế | Dev / PM | 🟡 TB | 86 |
| AI-13 | Thiết lập nhịp communication | PM / BrSE | 🔴 Cao | 178 |
| AI-14 | Quản lý task / độ ưu tiên / tiến độ | Leader / PM | 🟡 TB | 108 |
| AI-15 | Quản lý resource / risk / scope từ đầu dự án | PM | 🔴 Cao | 184 |

DoD theo nhóm (giữ ý gốc):
- AI-01: mọi task có spec/scope được confirm trước khi coding; không code khi spec chưa rõ.
- AI-02: mỗi task có vòng đọc-hiểu + Q&A trước khi code; điểm mơ hồ được raise trong ngày phát hiện.
- AI-03: task có log Q&A đầy đủ; thay đổi spec từ KH được phản ánh vào tài liệu.
- AI-04: tài liệu review nội bộ và đủ param/message trước khi gửi KH.
- AI-05: mỗi thay đổi có ghi chú phạm vi ảnh hưởng và được test bao phủ phần đó.
- AI-06: chỉ chuyển tester sau khi self-test pass theo checklist.
- AI-07: mọi PR/testcase có review chéo + checklist trước khi merge/approve.
- AI-08: testcase được review + map đủ yêu cầu trước round test.
- AI-09: môi trường và data test sẵn sàng, được verify trước khi test.
- AI-10: mỗi release có version ghi nhận, quy trình deploy chuẩn hóa.
- AI-11: mọi thao tác PRD có xác nhận KH + double-check được ghi nhận.
- AI-12: estimate kèm buffer và cơ sở; re-estimate khi scope đổi.
- AI-13: có nhịp họp/định kỳ; issue được escalate nội bộ trong ngày phát hiện.
- AI-14: board task phản ánh đúng ưu tiên/tiến độ; report đầy đủ hằng ngày.
- AI-15: có kế hoạch resource/risk/scope rõ; có cơ chế phân tích root cause bug.

**D. Chủ đề và lesson tiêu biểu (giữ ý, ẩn danh)**
1. Yêu cầu/CR (AI-01): chủ động đẩy khách xác nhận và mời các bên liên quan tham gia sớm để tránh phát sinh CR ở cuối phase; khách xác nhận muộn và bên liên quan chỉ tham gia khi gần kết thúc là nguyên nhân CR muộn.
2. Yêu cầu (AI-01): cần xác định hướng giải quyết với Leader và chuẩn bị solution cụ thể, bao quát mọi trường hợp trước khi viết code.
3. Yêu cầu (AI-01): xác nhận từng điểm một; làm rõ điểm 1 xong mới hỏi điểm 2, 3, 4, tránh hỏi dài dòng gây khó hiểu.
4. Đọc tài liệu (AI-02): đọc và phân tích kỹ đặc tả trước khi code để phát hiện điểm mơ hồ; mơ hồ phát hiện khi code gần xong thì rất tốn kém.
5. Đọc tài liệu (AI-02/AI-04): tài liệu do khách đưa (nhất là phần phát triển mới) có thể không đúng hoàn toàn; khi phát hiện cần cập nhật thì báo khách sớm.
6. Ghi chép (AI-03): cần ai đó (PM/BrSE) chủ động kiểm tra tài liệu của khách có thay đổi không; nhờ khách thông báo mỗi khi thay đổi spec; thống nhất tài liệu nào là nguồn yêu cầu chính xác nhất.
7. Ghi chép (AI-03): biến các comment của khách thành quy tắc/checklist chung để thành viên mới chỉ cần đọc là nắm.
8. Tài liệu (AI-04): thống nhất format tài liệu với các bên từ sớm để khớp nhận thức và bớt refactor; viết "một tài liệu, nhiều đối tượng đọc hiểu" kèm mockup, flow, ví dụ dữ liệu test.
9. Self-test (AI-06): khi self-test phải so sánh toàn diện giữa các màn hình, kiểm tra mọi case, kể cả lỗi nhỏ UI (màu, vị trí, text, title tab, font).
10. Review chéo (AI-07): nếu có ít nhất 2 dev cùng code thì mặc định mỗi người phải nắm code người kia; bố trí ít nhất 2 backend ngay từ đầu để có review chéo và quy trình code review bắt buộc.
11. Testcase (AI-08): từ lúc tìm hiểu spec đến khi viết testcase, lập Requirements Traceability Matrix (RTM) để xác định luồng nghiệp vụ liên quan và khoanh vùng ảnh hưởng.
12. Release (AI-10): version migration đặt theo timestamp đến giây để tránh trùng; nhánh development luôn chứa source mới nhất, nhánh version độc lập, và khi làm task xác định version rồi base từ đúng nhánh đó.
13. Release (AI-10): khi release trên công cụ admin, tách cửa sổ theo môi trường (hoặc dùng extension hiển thị nhãn môi trường) để không lẫn STG với PRD.
14. Production (AI-11): tuyệt đối không tạo/sửa/xóa trên môi trường PRD khi chưa báo và nhận đồng ý của khách, đồng thời team có phương án double-check; không release nội dung ngoài scope hoặc chưa báo khách.
15. Estimate (AI-12): luôn để tối thiểu buffer 1~2 ngày ở giữa để phát sinh vẫn không đổi lịch release; tìm hiểu kỹ logic code liên quan trước khi estimate.
16. Estimate (AI-12): với khách nhạy cảm về chi phí, estimate thận trọng, nắm mức trần khách chấp nhận, chia nhỏ phạm vi để dễ được duyệt.
17. Giao tiếp (AI-13): phát hiện issue thì chia sẻ nội bộ ngay để PM/BrSE nắm và phán đoán; lập checklist phạm vi release do TL và PM điền đủ trước khi release; kick-off kế hoạch thông tin: ai báo, báo gì, báo khi nào.
18. Quản lý task (AI-14): khi nhân sự bị điều phối, đánh giá ảnh hưởng lên task cũ, xác định tỷ lệ có thể cover (ví dụ 30%) và minh bạch với người liên quan; khi task không cân bằng thì chia sẻ cho người đang rảnh kèm bàn giao đầy đủ.
19. Quản lý dự án (AI-15): phân loại bug theo root cause (Requirement / Coding / Test / Communication...), gán owner cho từng nhóm nguyên nhân, phân tích theo từng dev, theo dõi đến khi xong.
20. Quản lý dự án (AI-15): đặt timeline cứng cho review QA, buffer ít nhất 2 ngày giữa Test Plan và execution, có escalation khi scope đổi, công bố plan sớm cho stakeholder.
Pattern chung: hầu hết bài học quay về ba gốc: (1) yêu cầu không rõ hoặc không được ghi lại; (2) thiếu kiểm tra/đối chiếu trước khi chuyển bước (self-test, review chéo, double-check); (3) thiếu nhịp giao tiếp và buffer trong kế hoạch.

## Ví dụ minh họa (ngắn, có số; dựng thì ghi "(ví dụ dựng)")
(ví dụ dựng) Sprint 4 của <tên-dự-án>, retro sau khi kết thúc sprint. Didn't go well: "Nhiều bug lọt sang tester vì self-test sơ sài". Map: AI-06 (self-test) và AI-07 (review chéo). Gợi ý chọn: chỉ chuyển tester sau khi self-test pass theo checklist; mỗi PR có review chéo. Action item: "AI-01: Tạo checklist self-test màn hình; Owner: <Member A>; Deadline: Sprint 5; Status: Open". Carry-forward: "CF-01: Lập nhịp cập nhật Q&A với khách (from Sprint 3); Owner: <PM>; Original Deadline: 2026-07-03; Status: In Progress" (ngày dựng). Mục "Cải thiện communication" bị từ chối vì mơ hồ và được chia thành hành động cụ thể.

## Tự kiểm tra (3-5 câu hỏi, đáp án ngắn ngay dưới)
1. Vì sao "Owner: Team, Deadline: ASAP" bị coi là sai?
   Đáp án: không có người chịu trách nhiệm cụ thể và không có mốc kiểm; phải chỉ định một người và ngày YYYY-MM-DD hoặc "Sprint N+1".
2. Bug lọt do dev không khoanh vùng ảnh hưởng khi sửa. Map sang nhóm nào?
   Đáp án: AI-05 (xác định và test vùng ảnh hưởng trước khi sửa code/bug).
3. Retro sprint khác Lessons learned (Ch9·01) ở đâu?
   Đáp án: retro sprint là giữa dự án, lặp lại, định dạng ngắn; Lessons learned (Ch9·01) đầy đủ 4 chiều dùng cho phase/dự án.
4. Blocker đã được giải quyết trong sprint nhưng làm chậm velocity thì xếp vào đâu?
   Đáp án: Didn't go well (nếu giải sớm thì Went well).
5. Mục Didn't go well không khớp nhóm AI nào thì làm gì?
   Đáp án: ghi "[Không có gợi ý sẵn — PM tự định nghĩa]", không ép gán.

## Liên quan (bài trước/sau)
- Trước: báo cáo tuần (bài 01) và họp hằng ngày (nguồn blocker trong sprint).
- Sau: lập kế hoạch sprint tiếp theo (action item và carry-forward đi vào đó); sổ rủi ro/vấn đề (nếu retro lộ rủi ro hệ thống); Lessons learned (Ch9·01) cuối dự án (tổng hợp các retro sprint).
