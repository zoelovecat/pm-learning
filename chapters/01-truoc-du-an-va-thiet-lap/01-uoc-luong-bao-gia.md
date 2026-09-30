---
title: Ước tính chào giá (bid) trước khi có dự án
source: Ước tính chào giá (Ch1·01)
stage: Pre-Project
level: trung bình
prerequisites: []
---
# Ước tính chào giá (bid): công số, chi phí, timeline và quyết định GO/NO-GO

## Mục tiêu học xong bạn làm được gì
- Từ một bản brief của khách, dựng được bảng ước tính công số (md) theo phase, cộng đệm (buffer) và markup rủi ro theo loại hợp đồng.
- Tính được giá chào (cost -> quote) với biên lợi nhuận (margin), đưa ra khoảng giá Low/Mid/High.
- Chiếu được timeline sơ bộ và kiểm tra năng lực (capacity) của đơn vị trước khi chào.
- Xếp hạng nhiều bid bằng WSJF/RICE/ICE/MoSCoW và ra khuyến nghị GO/HOLD/NO-GO.

## Khi nào dùng (thời điểm, ai kích hoạt, điều kiện đầu vào)
- Giai đoạn Pre-Project: chạy TRƯỚC khi có mã dự án và charter. Kích hoạt khi Sales nhận brief/RFP và cần báo giá ("ước tính dự án", "báo giá", "quote cho khách").
- Đầu vào bắt buộc: brief của khách (RFP/phạm vi), loại dự án (Web/Mobile/API/Migration/R&D), quy mô (S/M/L/XL), loại hợp đồng (Fixed-bid/T&M/Offshore/R&D). Thiếu brief thì dừng, nhờ Sales cung cấp; không đoán phạm vi.
- Đầu vào tùy chọn: rate card, lịch sử khách hàng, công số lịch sử của dự án tương tự, `margin_override`.
- Kết quả luôn là bản NHÁP để Sales và bên Delivery review; PM không tự gửi báo giá cho khách.

## Khái niệm cốt lõi (định nghĩa, thuật ngữ, vì sao quan trọng)
- **md (man-day) / MM (man-month)**: 1 MM = 20 MD, dùng nhất quán.
- **Phase distribution**: chia công số theo tỉ lệ chuẩn Requirements 8% / Design 18% / Development 50% / Testing 18% / Project Mgmt 6% (tổng 100%, là "subtotal" trước buffer).
- **System test** khoảng 30% công Dev (nằm trong phần Testing).
- **Buffer**: phần đệm cộng thêm theo loại hợp đồng; **risk markup**: phần cộng thêm theo bài học/rủi ro miền (vd banking).
- **Margin**: biên lợi nhuận cộng lên chi phí. Mặc định đề xuất 20%; Sales quyết định cuối cùng, phải ghi `margin_override` nếu đổi.
- **Quote range**: Low = cạnh tranh, buffer thấp; Mid = tiêu chuẩn (khuyến nghị); High = buffer thoải mái.
- Vì sao quan trọng: ước tính hụt là nguồn gốc của trễ/lỗ ở Fixed-bid (giải thích thêm); bid ước tính là nền cho charter (mục Scope, Nền tảng, Ước lượng công số, Schedule, Team).

## Cách làm từng bước (thủ công, đủ chi tiết để làm theo; kèm input/output)
1. **Đọc brief, rút thông tin**: số tính năng (màn hình/module) ước lượng thô, yêu cầu phi chức năng (hiệu năng, bảo mật, tuân thủ), tích hợp, dấu hiệu miền nghiệp vụ. Tóm tắt lại và xác nhận với PM/Sales.
2. **Thu thập metadata**: Bid ID dạng `BID-YYYY-NNN` (lấy số kế tiếp), tên khách + miền, loại dự án, quy mô, loại hợp đồng, gợi ý tech stack, khung thời gian bắt đầu dự kiến.
3. **Kiểm tra nhất quán**: Bid ID chưa trùng; brief không mâu thuẫn với loại/quy mô/hợp đồng PM khai. Có mâu thuẫn thì hỏi lại, không tự dung hòa. Có thể kiểm tra sơ bộ năng lực đơn vị; không có dữ liệu thì ghi `[NO_DATA]`, không chặn.
4. **Chọn công số nền** theo quy mô (bảng ở phần Công thức), điều chỉnh ±20% dựa trên dự án lịch sử giống (miền, công nghệ, quy mô). Nếu không có lịch sử, ghi `[NO_DATA]` và dùng khoảng nền theo quy mô.
5. **Chia theo phase** bằng tỉ lệ 8/18/50/18/6 -> ra subtotal.
6. **Cộng buffer** theo loại hợp đồng (+ thêm 10% nếu miền mới không có lịch sử) rồi **markup rủi ro** theo bài học (vd banking +10% tổng). Liệt kê top 3-5 rủi ro kèm dự phòng.
7. **Tính chi phí**: chia vai trò theo tỉ lệ mặc định (điều chỉnh theo bid), `cost_per_role = effort_md x daily_rate`, cộng thành subtotal, `customer_quote = subtotal x (1 + margin)`. Đơn giá phải lấy từ rate card hoặc PM cung cấp, tuyệt đối không tự bịa.
8. **Timeline**: `working_days = total_effort_md / (team_size x utilization)`; `calendar_duration = working_days + buffer_days + UAT window`. Nhớ cộng cửa sổ UAT và go-live.
9. **Kiểm tra capacity**: so năng lực khả dụng của đơn vị với công số bid theo từng tháng. Xung đột với pipeline đã cam kết thì cảnh báo đỏ và gợi ý dời ngày bắt đầu.
10. **Phân tích thắng/thua & khuyến nghị**: điểm mạnh, rủi ro, GO/HOLD/NO-GO. Nếu nhiều bid cùng lúc thì xếp hạng bằng WSJF (xem phần dưới).
11. **Chốt bản nháp**: chạy checklist cuối (phần Template), gửi Sales + Delivery review. Không gửi báo giá cho khách khi chưa được duyệt.

## Công thức, ngưỡng & tín hiệu (bảng: tên | công thức/điều kiện | ngưỡng | hành động khi vượt)
| Tên | Công thức / điều kiện | Ngưỡng | Hành động |
|---|---|---|---|
| Phase % | Req / Design / Dev / Test / Mgmt | 8% / 18% / 50% / 18% / 6% (=100%) | Dùng làm subtotal trước buffer |
| System test | ≈ 30% công Dev | 30% | Tính trong phần Testing |
| Quy mô S | 1-3 tháng lịch | 40-80 md | Nền; điều chỉnh ±20% theo lịch sử |
| Quy mô M | 3-6 tháng | 100-160 md | như trên |
| Quy mô L | 6-12 tháng | 160-350 md | như trên |
| Quy mô XL | 12+ tháng | 350+ md | như trên |
| Buffer Fixed-bid | cộng % lên subtotal | +15% | |
| Buffer T&M | | +10% | |
| Buffer Offshore | | +20% | |
| Buffer R&D | | +25% | |
| Miền mới (không lịch sử) | cộng thêm | +10% extra | |
| Markup bài học L-2026-001 | BD lặp nhiều màn hình | +25% phase Design | |
| Markup banking compliance | ISO27001/audit | +10% tổng + vai trò security | |
| Tích hợp "mãn tính" (API khách trễ) | | không tính %, xử lý bằng rủi ro + điều khoản SLA | |
| Cost | `cost_per_role = effort_md x daily_rate`; `subtotal = sum` | | |
| Quote | `customer_quote = subtotal x (1 + margin)` | margin mặc định 20% | Ghi `margin_override` nếu Sales đổi |
| Timeline | `working_days = total_effort_md/(team_size x utilization)` | M ≈ 5 FTE blended | + buffer_days + UAT |
| Đổi đơn vị | 1 MM | = 20 MD | |

Tỉ lệ vai trò mặc định (điều chỉnh theo bid): PM 6%, Tech Lead 10%, BA 8%, Designer 12% (UI nặng), Backend Dev 25%, Frontend Dev 22%, QA 15%, Security audit 2% (nếu có compliance) = 100%.

### Các mô hình ưu tiên bid (đa bid)
| Mô hình | Công thức | Ghi chú |
|---|---|---|
| WSJF | CoD / Job Size; CoD = User-Business Value + Time Criticality + Risk Reduction & Opportunity Enablement | Thang Fibonacci 1, 2, 3, 5, 8, 13, 20 |
| RICE | (Reach x Impact x Confidence) / Effort | Reach 100/1000/10000/100000; Impact 0.25/0.5/1.0/2.0/3.0; Confidence 100%/80%/50%; Effort = person-month |
| ICE | (Impact x Confidence x Ease) / 3 | mỗi thành phần thang 1-10 |
| MoSCoW | Must 60% / Should 20% / Could 10% / Won't 10% tổng phạm vi | thỏa thuận phạm vi, cắt scope, chia phase (M=Phase 1, S=Phase 2, C=Phase 3) |
| Kano | Must-be / Performance / Excitement / Indifferent / Reverse | chiến lược đầu tư từng nhóm |
| Điểm tổng hợp | Final = w1 x WSJF + w2 x RICE + w3 x Strategic Fit + w4 x Resource Match | ví dụ w1=0.35, w2=0.25, w3=0.25, w4=0.15 |
| Strategic Fit (chấm 1-5) | Phù hợp chiến lược công ty 0.3; Tận dụng chuyên môn miền 0.2; Giá trị quan hệ KH 0.2; Xây năng lực 0.15; Định vị thị trường 0.15 | |

Hướng dẫn chấm WSJF:
- User-Business Value: 1 = cải tiến nhỏ, ít người dùng; 5 = giá trị đáng kể, nhóm người dùng chính; 13 = giá trị cao, khác biệt chiến lược; 20 = sống còn, khách yêu cầu.
- Time Criticality: 1 = không áp lực; 5 = áp lực cuối quý; 13 = hạn cam kết với khách; 20 = hạn pháp lý/hợp đồng.
- Risk Reduction/Opportunity: 1 = không; 5 = giảm 1 rủi ro đã biết; 13 = mở khóa 2-3 phụ thuộc; 20 = nền tảng cho nhiều việc sau.
- Job Size: 1 = ≤ 1 sprint / ≤ 10 md; 5 = 2-3 sprint / 30-50 md; 13 = cả quý / 100-150 md; 20 = nhiều quý / > 200 md.

Chọn mô hình: đánh giá bid -> WSJF; tính năng trong sprint/release -> WSJF hoặc RICE; phân loại nhanh backlog -> ICE; go/no-go danh mục -> MoSCoW + WSJF; phân bổ nguồn lực nhiều bid -> xếp hạng WSJF; roadmap quý -> RICE.

## Template / mẫu đầu ra (rút gọn, giữ cấu trúc và các cột/trường)
Tài liệu "Bid Estimate - <BID-ID> (DRAFT)":
- Bảng thông tin: Bid ID | Customer | Domain | Project Type | Estimated Size | Contract Type | Tech Stack | Tentative Start | margin_override (trống = 20%) | Generated | Status (DRAFT - Sales + Delivery review).
- 1. Scope Summary (từ brief): số màn hình, số vai trò, tích hợp, tuân thủ.
- 2. Effort: bảng Phase | % | Effort (md); dòng Subtotal, Buffer, Risk markup, TOTAL; mục Historical reference (dự án tương tự và công số thực tế).
- 3. Cost: bảng Role | Effort (md) | Daily Rate | Cost; Subtotal, Margin, Customer quote; Quote range Low/Mid/High.
- 4. Timeline: Phase | Effort | Duration (theo FTE) | Cumulative.
- 5. Capacity Check: SBU | Cap | Committed | Available; ghi chú vàng/đỏ.
- 6. Top 5 Risks: Risk | L | I | Mitigation.
- 7. Win/Loss: Strengths, Risks, Recommendation (GO/HOLD/NO-GO).
- 8. Sales Action Items (checkbox).

Ánh xạ sang charter khi thắng bid (template charter TPL-SM-02-01): Scope summary -> mục 4 Scope; Tech stack -> mục 5 Nền tảng phát triển; Effort Bậc 1/2/3 -> mục 7 Ước lượng công số; Timeline -> mục 6 Schedule; Team composition -> mục 8 Phương án thực hiện.

Checklist trước khi giao bản nháp: brief đã xác nhận; ghi rõ phase % và buffer; rate lấy từ nguồn chính thức (không bịa); có `margin_override` nếu khác 20%; tham chiếu lịch sử hoặc `[NO_DATA]`; đã chạy hoặc đánh dấu `[NO_DATA]` cho capacity check; trạng thái DRAFT; chưa gửi khách.

## Lỗi thường gặp & lesson learned (lấy từ nguồn, mỗi ý: sai gì -> hậu quả -> cách tránh)
- Tự đoán phạm vi khi thiếu brief -> ước tính lệch hoàn toàn -> dừng, yêu cầu Sales cung cấp brief.
- Tự bịa đơn giá -> báo giá sai/không kiểm chứng được -> lấy từ rate card hoặc PM; chưa có thì ghi TBD.
- Bỏ qua miền mới và bài học lịch sử -> thiếu công số (vd thiết kế lặp nhiều màn hình cần +25% Design; banking cần +10% và vai trò security) -> tra catalog bài học/retro.
- Tích hợp với hệ thống khách trễ (API) -> không xử lý được bằng % công số -> đưa vào rủi ro + điều khoản SLA trong hợp đồng.
- Quên UAT/go-live khi tính lịch -> lịch quá lạc quan -> luôn cộng cửa sổ UAT.
- Không kiểm tra capacity -> thắng bid nhưng thiếu người khi chồng dự án khác -> so capacity theo tháng, cảnh báo đỏ và dời ngày bắt đầu.
- Anti-pattern ưu tiên: quyết theo ý kiến người lương cao nhất (HiPPO), mọi thứ đều Must (MoSCoW vô nghĩa), tự tin 100% mọi ước tính (giấu rủi ro), chấm WSJF không có mốc neo (điểm trôi), ưu tiên một lần rồi bỏ (lỗi thời trong 1 quý) -> dùng dữ liệu, chấm có neo, ưu tiên lại mỗi quý.
- Gửi báo giá khi chưa qua Sales + Delivery review -> cam kết ngoài kiểm soát -> chỉ giao bản DRAFT.

## Ví dụ minh họa (1 ví dụ ngắn có số, lấy hoặc dựng từ nguồn; nếu dựng thì ghi "(ví dụ dựng)")
Từ nguồn (BID-2026-042, Web banking, quy mô M, Fixed-bid, ISO27001): subtotal 110-130 md -> buffer Fixed-bid +15% = +17-20 md -> markup banking +10% = +11-13 md -> tổng 138-163 md. Chọn 145 md, subtotal chi phí 66,550 USD. Timeline ~5 tháng với 5 FTE. Khoảng giá Low 78k | Mid 83k | High 90k, khuyến nghị GO ở mức Mid 83k.
(nguồn chưa rõ: bảng nguồn ghi Margin (20%) = 16,638 và quote = 83,188 USD; theo công thức 66,550 x 20% = 13,310 và quote = 79,860, còn 83,188 ứng với margin 25%. Con số mâu thuẫn với công thức; khi học hãy dùng công thức.)

Ví dụ WSJF từ nguồn (3 bid): BID-042 (13+5+5=23, size 13 -> 1,77); BID-045 (8+8+3=19, size 8 -> 2,38); BID-048 (5+1+8=14, size 13 -> 1,08). Kết luận nguồn: BID-045 có WSJF cao nhất, theo đuổi trước nếu năng lực hạn chế.
(nguồn chưa rõ: cột Rank ghi BID-042 = 1 trong khi BID-045 mới có WSJF cao nhất; cột Rank không khớp điểm.)
Ghi chú số học nguồn: ví dụ ICE ghi 7,7 cho (7x9x8)/3 và 5,7 cho (9x5x3)/3, nhưng theo công thức là 168 và 45; 7,7 và 5,7 là trung bình cộng của ba thành phần (nguồn chưa rõ công thức nào đúng). Ví dụ RICE khớp công thức: 333, 500, 800.

## Tự kiểm tra (3-5 câu hỏi có đáp án ngắn ngay dưới, dựa trên chính nội dung bài)
1. Phase distribution mặc định là gì? -> Requirements 8%, Design 18%, Development 50%, Testing 18%, Project Mgmt 6%.
2. Buffer theo loại hợp đồng? -> Fixed-bid +15%, T&M +10%, Offshore +20%, R&D +25%, miền mới không lịch sử thêm +10%.
3. Công thức giá chào? -> cost_per_role = effort_md x daily_rate; customer_quote = subtotal x (1 + margin), margin mặc định 20%, Sales quyết định cuối.
4. Ai quyết định margin và phải ghi gì khi đổi? -> Sales; ghi `margin_override`.
5. Tính WSJF thế nào? -> WSJF = CoD / Job Size, CoD = Value + Time Criticality + Risk Reduction/Opportunity; thang 1, 2, 3, 5, 8, 13, 20.

## Liên quan (bài trước/sau trong quy trình, tên thư mục skill khác)
- Sau: Dự báo năng lực (Ch1·02) (dự báo năng lực, khuyến nghị bỏ bid), Kickoff (Ch2·01) (bid thắng thì làm charter từ estimate), Xếp người (Ch3·05) (lập đội).
- Tham chiếu: Lessons learned (Ch9·01) (bài học lịch sử để markup).
