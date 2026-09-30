---
title: Rút kinh nghiệm (Lessons Learned / Retrospective) cho PM
source: Lessons learned (Ch9·01)
stage: Closure
level: trung bình
prerequisites: [Ch7·04, Ch8·04]
---
# Rút kinh nghiệm (Lessons Learned / Retrospective) cho PM

## Mục tiêu học xong bạn làm được gì
- Chọn đúng phạm vi retro (sprint / phase / release / project) và khoảng thời gian cần nhìn lại.
- Gom số liệu nền (lệch tiến độ, lệch effort, gate, CR, rủi ro, sự cố hypercare, NPS) trước khi họp, để cuộc họp dựa trên dữ liệu chứ không dựa trên cảm tính.
- Chọn 1 trong 8 định dạng retro phù hợp ngữ cảnh và điều phối buổi retro theo 4 chiều: Process, Team, Customer, Technical.
- Viết action item có owner, hạn, tiêu chí thành công; chắt lọc thành bài học đưa vào catalog để dự án sau dùng lại.
- Nhận ra và tránh các anti-pattern (retro thành buổi đổ lỗi, action mơ hồ, không có catalog...).

## Khi nào dùng (thời điểm, ai kích hoạt, điều kiện đầu vào)
- Do PM kích hoạt, ở các mốc: cuối sprint (nếu áp dụng), cuối phase, sau khi hypercare của một release đã đóng, hoặc khi đóng dự án. Sự cố nghiêm trọng: retro trong vòng 48 giờ.
- Cửa sổ dữ liệu theo phạm vi:

| Phạm vi | Khi nào | Cửa sổ nhìn lại |
|---|---|---|
| Sprint | Cuối sprint | 2 tuần gần nhất |
| Phase | Cuối phase | Suốt thời gian phase |
| Release | Sau khi hypercare đóng | Vòng đời release |
| Project | Đóng dự án | Toàn dự án |

- Đầu vào BẮT BUỘC (thiếu thì dừng, bổ sung trước, không tự bịa số): bảng tiến độ (kế hoạch vs thực tế theo milestone), kết quả các gate (pass/hold/abort), lịch sử báo cáo trạng thái hằng tuần, sổ rủi ro (vòng đời rủi ro đã đóng), lịch sử CR.
- Đầu vào TÙY CHỌN: nhật ký hypercare (khi retro release), báo cáo effort chi tiết, sự tham gia của khách hàng, phản hồi ẩn danh của team, NPS khách hàng.
- Nếu PM nhận bàn giao giữa chừng và không có hồ sơ từ giai đoạn lập kế hoạch: phải dựng lại tối thiểu 5 nhóm dữ liệu trên (từ hệ thống quản lý dự án cũ) trước, chấp nhận là dữ liệu "proxy" có hạn chế.

## Khái niệm cốt lõi
- **Retro của PM khác retro kỹ thuật**: retro kỹ thuật nhìn chỉ số code, đóng góp từng người, chu kỳ tuần. Retro PM nhìn quy trình, đội nhóm, khách hàng; dữ liệu là tiến độ, gate, CR, rủi ro; đầu ra là action item + catalog; đối tượng đọc là mọi stakeholder.
- **4 chiều (4-dimension)**: Process (workflow, gate, checklist, độ chính xác của tín hiệu), Team (cộng tác, giao tiếp, năng lực/capacity), Customer (quan hệ, phản hồi, mức hài lòng), Technical (công cụ, nợ kỹ thuật, quyết định kiến trúc).
- **START / STOP / CONTINUE**: bắt đầu làm gì, ngừng làm gì, tiếp tục làm gì. Áp cho từng chiều.
- **Action item (AI)**: việc cải thiện cụ thể, bắt buộc có owner + hạn (due) + tiêu chí thành công.
- **Catalog bài học**: sổ tích lũy bài học qua các dự án, mỗi dòng có mã `L-YYYY-NNN`, để dự án/báo giá sau tham chiếu.
- **[NO_DATA]**: nhãn ghi vào ô số liệu khi thiếu dữ liệu. Không suy đoán.
- **Không đổ lỗi**: tập trung vào hệ thống/quy trình, không vào cá nhân. Retro nháp (DRAFT) đến khi team review và ký.

## Cách làm từng bước (thủ công, đủ chi tiết để làm theo; input/output)
1. **Kiểm tra dữ liệu đầu vào.** Lập danh sách hồ sơ đang có/thiếu (tiến độ, gate, trạng thái, rủi ro, CR; hypercare nếu release). Trích nhanh: milestone kế hoạch vs thực tế; tổng gate passed/hold/abort; rủi ro đã đóng vs còn mở trong kỳ; số CR đã xử lý; các báo cáo trạng thái trong kỳ. Thiếu mục bắt buộc thì bổ sung trước.
2. **Chốt thông tin họp.** Bắt buộc: phạm vi, ngày bắt đầu kỳ, ngày kết thúc kỳ, ngày họp retro (mặc định hôm nay), người tham gia (theo vai trò: PM, Tech Lead...). Tùy chọn (nếu bỏ qua): khách hàng tham gia (mặc định retro chỉ PM), phản hồi ẩn danh (PM bật theo từng chiều), Release ID (N/A nếu không phải release), định dạng retro (mặc định Hybrid, xem mục Template), NPS/hài lòng khách (`[NO_DATA]`).
3. **Kiểm tra tính hợp lệ.** Phạm vi thuộc 4 loại; kỳ nằm trong dữ liệu sẵn có; nếu retro release mà chưa có hypercare thì quyết định bỏ qua hay làm hypercare trước; định dạng khớp phạm vi; tên tài liệu đầu ra theo dạng `<scope>-<date>`. Phạm vi không khớp dữ liệu thì hỏi lại, không tự dung hòa.
4. **Tổng hợp số liệu (Numbers Summary).**
   - Tiến độ: chênh lệch số ngày theo từng milestone, tổng độ trễ ròng; đếm milestone đạt/lỡ.
   - Effort: % thực tế so với kế hoạch; mẫu vượt mãn tính theo giai đoạn/module (nếu có). Chưa có báo cáo effort thì dùng ước tính từ trạng thái nếu PM đồng ý.
   - Gate: passed/hold/abort, các hold đáng chú ý.
   - Rủi ro và CR: rủi ro đóng vs leo thang vs còn mở; CR duyệt/từ chối/hoãn.
   - Hypercare (nếu release): sự cố P1/P2/P3, phản hồi khách.
   - Lịch sử trạng thái: chủ đề blocker, vấn đề lặp lại.
   PM rà lại số liệu trước khi họp.
5. **Điều phối 4 chiều** (không bỏ chiều nào): hỏi START/STOP/CONTINUE lần lượt cho Process, Team, Customer, Technical theo định dạng đã chọn. Áp dụng mẹo điều phối ở mục Công thức/ngưỡng.
6. **Viết action item**: bảng `# | Item | Owner | Due | Success Criteria`. Item mơ hồ ("cải thiện giao tiếp") thì ép cụ thể hóa lại. Mỗi item phải có owner + hạn.
7. **Chắt bài học vào catalog**: mỗi bài học một dòng `L-YYYY-NNN: <tên bài học>. Mitigation: <hành động>.` và ghi tham chiếu đến tài liệu retro.
8. **Hoàn thiện**: đầu trang ghi nguồn dữ liệu; trạng thái DRAFT; số liệu thiếu ghi `[NO_DATA]`; không dùng ngôn ngữ đổ lỗi; phần chữ ký để trống (⬜) chờ team review. Nếu là retro dự án thì bước kế tiếp là đóng dự án (xem bài Closeout). Bài học còn được dùng làm đầu vào cho báo giá sau và cho việc gieo rủi ro ở kickoff dự án mới.
- Input: hồ sơ dự án trong kỳ + ý kiến team. Output: tài liệu retro (DRAFT) + các dòng catalog.

## Công thức, ngưỡng & tín hiệu (bảng: tên | công thức/điều kiện | ngưỡng | hành động khi vượt; không có thì ghi "Không có")
Repo không đặt ngưỡng cảnh báo cho chỉ số retro. Có các quy tắc/số cần giữ nguyên:

| Tên | Công thức / điều kiện | Ngưỡng | Hành động |
|---|---|---|---|
| Schedule variance | Δ số ngày mỗi milestone; độ trễ ròng | Không đặt ngưỡng | Ghi vào Numbers Summary |
| Effort variance | % thực tế so với kế hoạch | Không đặt ngưỡng | Ghi; nêu mẫu vượt mãn tính nếu có |
| Số mục START/STOP/CONTINUE | Mỗi nhóm nêu 1-3 mục (định dạng SST) | 1-3 mục/nhóm | Vượt thì chọn lọc lại |
| Thời lượng retro nhanh | Định dạng START/STOP/CONTINUE | dưới 30 phút | Dùng khi cần nhanh |
| Bình chọn ưu tiên | 3 dot vote, tập trung top 3 | 3 phiếu | Chọn top 3 làm action |
| Brainstorm im lặng | Cá nhân ghi trước khi thảo luận | 5 phút | Sau đó mới thảo luận nhóm |
| Retro sự cố nghiêm trọng | Kể từ khi xảy ra sự cố | trong vòng 48 giờ | Dùng Root Cause Analysis (5 Whys) |
| Điểm sức khỏe team | Psychological safety, Collaboration, Conflict handling | thang 1-10 | Dùng trong Team Dynamics |
| Action item hợp lệ | Có owner và hạn | bắt buộc cả hai | Thiếu thì bổ sung, không chốt |

Nhịp retro theo quy mô dự án:

| Quy mô | Nhịp retro | Định dạng |
|---|---|---|
| Nhỏ (dưới 3 tháng) | Cuối phase + cuối dự án | START/STOP/CONTINUE + Sailboat |
| Vừa (3-6 tháng) | Cuối mỗi phase | Hybrid |
| Lớn (6+ tháng) | Mini 2 tuần/lần + cuối phase + cuối dự án | Plus/Delta (mini), 4Ls (phase), Sailboat (dự án) |
| Sự cố nghiêm trọng | Trong 48 giờ | Root Cause Analysis (5 Whys) |

Chọn định dạng theo ngữ cảnh:

| Ngữ cảnh | Định dạng khuyến nghị | Lý do |
|---|---|---|
| Cuối sprint (nếu áp dụng) | START/STOP/CONTINUE | Nhanh, hướng hành động |
| Hoàn thành phase | 4Ls + Anchor | Đào sâu, cân bằng tích cực/tiêu cực |
| Gate G2/G3/G4 hold/abort | Root Cause Analysis | Tập trung vào vấn đề |
| Post-mortem release | DACI Timeline | Lần theo dòng quyết định |
| Đóng dự án | Sailboat + Lessons Catalog | Toàn diện, áp dụng được cho tương lai |
| Phiên phản hồi khách hàng | Plus/Delta | Gọn gàng, hướng khách |
| Xung đột/căng thẳng team | Team Dynamics | Tập trung hành vi |

(nguồn chưa rõ: "4Ls + Anchor" chỉ nêu trong bảng chọn, danh mục định dạng không mô tả riêng "Anchor"; hiểu là dùng 4Ls kèm phần "Anchors" như trong Sailboat.)

### Catalog 8 định dạng retro
1. **START / STOP / CONTINUE.** Retro nhanh, dưới 30 phút, hướng hành động. Ba nhóm: START (hành vi/quy trình bắt đầu, 1-3 mục), STOP (hành vi/quy trình đang gây hại, 1-3 mục), CONTINUE (điều đang hiệu quả, 1-3 mục). Biến thể SST + AI: thêm cột Action gồm owner + due.
2. **4Ls: Liked / Learned / Lacked / Longed for.** Dùng cho retro phase, cân bằng chủ quan và khách quan. Liked: điều đã thích/đã tốt. Learned: kiến thức/nhận thức mới. Lacked: nguồn lực/hỗ trợ/độ rõ ràng cần mà không có. Longed for: cải thiện mong muốn cho phase sau.
3. **Sailboat.** Retro dự án, dễ trực quan hóa: thuyền đi từ Wind (gió đẩy) tới Island (đảo, tầm nhìn), dưới có Sun, Anchors, Rocks. Các phần: Sun (mục tiêu đã đạt, so với tiêu chí thành công trong charter), Wind (điều đẩy tiến lên: người hỗ trợ, yếu tố thuận lợi, quyết định tốt), Anchors (điều kéo chậm lại: ma sát quy trình, phụ thuộc, nợ), Rocks (rủi ro đã xảy ra, bất ngờ), Island (cải thiện mong muốn cho lần sau).
4. **DACI Timeline.** Dự án nặng quyết định (post-mortem release, gate abort). Theo dõi từng quyết định lớn trong bảng: Decision | Driver | Approver | Contributors | Informed | Outcome | Lesson. Ví dụ nguồn: duyệt một CR, kết quả +20md +7d trễ, bài học "khách hàng nên tham gia sớm hơn khi rà CR".
5. **Plus / Delta.** Hướng khách hàng, giọng chỉn chu. Chỉ hai cột: Plus (+) điều hiệu quả; Delta (Δ) điều sẽ thay đổi. Hai cột giúp sponsor/khách dễ nắm.
6. **Root Cause Analysis (5 Whys).** Dùng cho 1 sự cố/hold/abort nghiêm trọng. Mô tả sự cố rồi hỏi Why 1 tới Why 5 (gốc), sau đó ghi Root Cause (nguyên nhân cuối) và Systemic Fix (hành động xử lý gốc, không xử lý triệu chứng).
7. **Team Dynamics Retro.** Khi team căng thẳng, giao tiếp kém, có mẫu hành vi (có thể lấy dữ liệu từ phân tích cuộc họp). Gồm: mẫu cộng tác quan sát được (hành vi tích cực + tiêu cực); phản-mẫu giao tiếp (vd độc thoại dài, bàn giao mơ hồ); tín hiệu tin cậy (tin cậy cao / thấp); điểm sức khỏe team 1-10 (Psychological safety, Collaboration, Conflict handling); 1 thí nghiệm sẽ thử ở phase sau.
8. **Hybrid (mặc định cho retro dự án).** Kết hợp START/STOP/CONTINUE với 4 chiều: Process, Team, Customer, Technical, mỗi chiều có START/STOP/CONTINUE; tiếp theo là bảng Action Items cụ thể và mục Lessons for Catalog.

### Mẹo điều phối
1. An toàn trước: luật cơ bản "tôn trọng từng cá nhân, tập trung vào hệ thống/quy trình".
2. Mọi người đều có tiếng nói: xoay vòng để người hướng ngoại không lấn át.
3. Brainstorm im lặng 5 phút.
4. Bình chọn ưu tiên 3 dot vote, tập trung top 3.
5. Kết thúc bằng action: không có action thì coi như chưa retro.

## Template / mẫu đầu ra (rút gọn, giữ cấu trúc, cột, trường)
```
# Lessons Learned - <scope> (DRAFT)
> Nguồn: schedule + gates + status + cr + risk + ý kiến team
| Field | Value |   (Scope / Period / Held / Participants / Status)

## Numbers Summary
| Metric | Value |
(Schedule variance; Effort variance; Gates passed; CR processed;
 Risks closed; Hypercare incidents; Customer NPS - thiếu thì [NO_DATA])

## 4-Dimension Review
### Process - START / STOP / CONTINUE
### Team - START / STOP / CONTINUE
### Customer - START / STOP / CONTINUE
### Technical - START / STOP / CONTINUE

## Action Items
| # | Item | Owner | Due | Success Criteria |

## Lessons for Catalog
- L-YYYY-NNN: <tên bài học>. Mitigation: <hành động>.

## Sign
| Role | Sign | Date |   (để trống ⬜ chờ ký)
```
Checklist trước khi chốt: phạm vi + kỳ đã xác nhận; cả 4 chiều đều có START/STOP/CONTINUE; action có owner + due; số liệu thiếu ghi `[NO_DATA]`; đã thêm vào catalog; không có ngôn ngữ đổ lỗi.

## Lỗi thường gặp & lesson learned (sai gì -> hậu quả -> cách tránh)
| Sai | Hậu quả | Cách tránh |
|---|---|---|
| Retro thành buổi đổ lỗi | Phá vỡ psychological safety, các retro sau kém đi | Luật cơ bản tập trung hệ thống/quy trình |
| Action không có owner | Sẽ không ai làm | Ghi owner cho mọi action |
| Action không có hạn | Kéo dài mãi | Ghi due |
| "Chúng ta sẽ cải thiện giao tiếp" | Mơ hồ, không hành động được | Viết cụ thể kèm tiêu chí thành công |
| Dùng cùng một định dạng mỗi lần | Insight chững lại | Xoay vòng định dạng |
| Không có catalog | Bài học mất qua các dự án | Luôn ghi bài học vào catalog |
| Bỏ retro vì "không có thời gian" | Chính team cần retro nhất lại bỏ | Giữ nhịp retro theo quy mô |
| Tự điền số khi thiếu dữ liệu | Retro dựa trên số bịa | Ghi `[NO_DATA]`, bổ sung từ hồ sơ gốc |

Bài học chuẩn hóa trong ví dụ nguồn: dự án có mẫu "Basic Design vượt mãn tính" nên bổ sung đệm +1 ngày mỗi work package và nâng heuristic ước tính +25%.

## Ví dụ minh họa (ngắn, có số; dựng thì ghi "(ví dụ dựng)")
Rút gọn từ ví dụ trong nguồn (retro release <mã-release> v1.0; tên khách ẩn danh):
- Kỳ: 2026-06-01 đến 2026-10-07 (4 tháng); họp 2026-10-08; tham gia: PM, Tech Lead, BA Lead, QA Lead, <Customer PIC>.
- Numbers Summary: Schedule variance +7 ngày (M6 từ 2026-09-30 sang 2026-10-10); Effort variance +10.3% (162md thực tế vs 145md kế hoạch); Gates passed 6/6 (G2: 1 hold rồi pass); CR 3 (2 duyệt, 1 từ chối); Risks closed 8 trên 10 (2 còn mở, mức thấp); Hypercare: 0 P1, 2 P3; NPS 9/10. (Nguồn chưa rõ: ví dụ nguồn ghi +7 ngày nhưng 2026-09-30 sang 2026-10-10 là 10 ngày, và ghi +10.3% nhưng 162/145 tính ra khoảng +11.7%; giữ nguyên số của nguồn, đây là số minh họa không nhất quán.)
- Chiều Process: START đệm rà Basic Design +1 ngày mỗi WP, chạy giám sát tín hiệu hằng ngày thay vì chỉ hằng tuần; STOP chọn nhiều template lúc lập kế hoạch release (checklist dài); CONTINUE quy trình DRAFT-trước và template gate review.
- Action: AI-001 cập nhật heuristic Basic Design +25%, owner PM, hạn 2026-10-15, tiêu chí: có baseline ước tính mới.
- Catalog: `L-2026-001: BD chronic overrun +25% pattern. Mitigation: +1 day buffer per WP.`

## Tự kiểm tra (3-5 câu hỏi, đáp án ngắn ngay dưới)
1. Bốn chiều của Hybrid là gì? -> Process, Team, Customer, Technical; mỗi chiều có START/STOP/CONTINUE.
2. Sự cố nghiêm trọng thì retro khi nào, dùng định dạng nào? -> Trong vòng 48 giờ, Root Cause Analysis (5 Whys).
3. Action item hợp lệ cần những trường nào? -> Item, Owner, Due, Success Criteria; tối thiểu phải có owner và due.
4. Thiếu số liệu effort thì làm sao? -> Ghi `[NO_DATA]` (hoặc dùng ước tính từ báo cáo trạng thái nếu PM đồng ý), không bịa.
5. Dự án lớn (6+ tháng) đặt nhịp retro thế nào? -> Mini 2 tuần/lần (Plus/Delta) + cuối phase (4Ls) + cuối dự án (Sailboat).

## Liên quan (bài trước/sau)
- Trước: báo cáo trạng thái hằng tuần, gate review, quản lý rủi ro/issue, quản lý CR, hypercare, effort thực tế.
- Sau: Closeout (bài 02-closeout, retro dự án là đầu vào bắt buộc); báo giá dự án mới (catalog làm căn cứ); kickoff dự án mới (gieo rủi ro từ bài học).
- Câu hỏi nguồn còn bỏ ngỏ: catalog theo từng dự án hay tập trung toàn công ty; diễn đàn chia sẻ bài học giữa dự án; chính sách phản hồi ẩn danh; khách tham gia retro hay PM tổng hợp; theo dõi action item (hoãn).
