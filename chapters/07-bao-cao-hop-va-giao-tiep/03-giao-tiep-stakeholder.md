---
title: Truyền thông với stakeholder theo từng đối tượng
source: Giao tiếp stakeholder (Ch7·03)
stage: Cross-cutting
level: trung bình
prerequisites: [Ch7·01]
---
# Truyền thông với stakeholder theo từng đối tượng

## Mục tiêu học xong bạn làm được gì
- Từ một tài liệu nguồn của PM (báo cáo trạng thái tuần, kết quả gate review, change request, kế hoạch release) viết được thông điệp đúng giọng và độ dài cho 7 đối tượng: sponsor, khách hàng, team, 3P team, newsletter, steering, Slack.
- Trích đúng sự kiện từ nguồn, không bịa số liệu, ghi rõ chỗ thiếu dữ liệu.
- Chạy quy trình 2 bước cho bản gửi khách hàng (nháp -> PM lọc thông tin nhạy cảm -> bản chính thức).

## Khi nào dùng (thời điểm, ai kích hoạt, điều kiện đầu vào)
- Khi cần gửi báo cáo cho sponsor, email khách hàng, thông báo release, cập nhật stakeholder, tóm tắt điều hành. PM kích hoạt; luôn là bản NHÁP để PM duyệt trước khi gửi (không tự gửi).
- Đầu vào bắt buộc: (1) ít nhất 1 tài liệu nguồn (báo cáo trạng thái tuần, biên bản gate, CR, kế hoạch release); (2) đối tượng nhận; (3) kỳ báo cáo (tuần ISO hoặc khoảng ngày); (4) danh sách stakeholder và mã/tên dự án từ hiến chương dự án (charter). Thiếu nguồn thì dừng, quay lại tạo tài liệu nguồn, không đoán.
- Tùy chọn (mặc định khi bỏ qua): yêu cầu/quyết định cụ thể cần nêu (lấy từ mục Asks/blockers/CR của nguồn); giọng riêng cho khách hàng (mặc định trang trọng); định dạng đầu ra (chỉ markdown).
- Giả định mặc định: tần suất truyền thông nội bộ hằng tuần, đối ngoại 2 tuần một lần; ghi họ tên đầy đủ trong bối cảnh nội bộ là chấp nhận được.

## Khái niệm cốt lõi (định nghĩa, thuật ngữ, vì sao quan trọng)
- Cùng một sự thật, mỗi đối tượng cần trọng tâm khác nhau: sponsor cần trạng thái + quyết định cần họ ra; khách hàng cần mốc + việc đang chờ phía họ + CR; team cần việc kế tiếp + chỗ cần hỗ trợ.
- **3P** = Progress / Plans / Problems: cập nhật ba phần đã làm, sẽ làm, vướng mắc.
- **`[NO_DATA]`**: nhãn đặt vào chỗ nguồn không có số liệu. Không ước lượng, không bịa.
- Mọi con số trong thông điệp phải truy ngược được về tài liệu nguồn.
- Quy tắc 2 bước cho khách hàng: bản nháp chứa mọi sự kiện -> PM đánh dấu mục nhạy cảm cần bỏ hoặc che -> tạo bản chính thức hoặc PM sửa trực tiếp -> không gửi khi chưa có PM duyệt.

## Cách làm từng bước (thủ công, đủ chi tiết để làm theo; kèm input/output)
1. Chọn tài liệu nguồn và xác nhận có đủ các phần cần: mã trạng thái, mốc, tín hiệu, rủi ro, blocker, CR, kế hoạch tuần tới. Danh sách stakeholder lấy từ hiến chương.
2. Xác định đối tượng, kỳ báo cáo, và các quyết định cần đối tượng đưa ra.
3. Kiểm tra trước khi viết: nếu là 3P hoặc newsletter thì dùng đúng khuôn riêng; nếu là khách hàng thì đánh dấu quy trình nháp -> duyệt -> chính thức; nếu nguồn thiếu phần cần cho đối tượng (ví dụ bảng mốc cho khách hàng) thì ghi `[NO_DATA]`; nếu là Slack thì giới hạn 280 ký tự; nếu nhiều nguồn mâu thuẫn nhau thì dừng và hỏi, không tự trộn.
4. Trích các trường cốt lõi từ nguồn: mã trạng thái (xanh/vàng/đỏ), điểm nổi bật/việc hoàn thành, tín hiệu cờ (từ mục mốc/tín hiệu hoặc QS-XX của gate), rủi ro High/Critical đang mở, blocker, CR đang chờ, kế hoạch tuần sau, yêu cầu/quyết định cần đối tượng ra.
5. Áp bảng ánh xạ theo đối tượng (bảng dưới) để chọn thông tin nào đi vào đâu.
6. Viết theo khuôn của đối tượng, khớp giọng và độ dài, đưa các quyết định cần thiết lên rõ ràng.
7. Đặt tên file theo dạng `<YYYY-MM-DD>-<đối-tượng>` (ví dụ 2026-08-26-sponsor). Trạng thái: NHÁP; bản khách hàng ghi đầu trang "DRAFT - PM review required".
8. Chạy checklist cuối rồi mới gửi. Không tự gửi email/Slack.

## Công thức, ngưỡng & tín hiệu (bảng: tên | công thức/điều kiện | ngưỡng | hành động khi vượt)
Không có công thức. Có các giới hạn hình thức theo đối tượng:

| Đối tượng | Giọng | Độ dài | Trọng tâm |
|---|---|---|---|
| Sponsor | Điều hành, gạch đầu dòng | <= 1 trang | Trạng thái + yêu cầu quyết định + rủi ro |
| Khách hàng (PIC) | Trang trọng, chau chuốt | 1-2 trang | Tiến độ + mốc + CR |
| Team | Thân mật, việc trước | Ngắn | Việc tiếp theo + blocker |
| Team 3P | Có cấu trúc P/P/P | 1 trang | Cập nhật tuần của team |
| Newsletter | Bao hàm, dùng "chúng ta" | Đọc 3-5 phút | Thông báo liên nhóm |
| Steering | Chiến lược | Dàn ý 5-10 slide | Quyết định cần ra |
| Slack | Cực ngắn | <= 280 ký tự | Emoji + 1 dòng + link |

Ánh xạ nguồn sang thông điệp:
| Phần trong nguồn | Sponsor | Khách hàng | Team |
|---|---|---|---|
| Mã trạng thái | Tiêu đề | Bảng mốc | Dòng thắng lợi |
| Tín hiệu cờ | Gạch đầu dòng | Thành tựu | Blocker |
| Rủi ro High đang mở | Yêu cầu (asks) | Việc đang chờ phía khách hàng | Cần trợ giúp |
| Blocker | Asks | Nêu tác động | Người phụ trách + escalate |
| CR đang chờ | Yêu cầu quyết định | Mục CR | - |
| Kế hoạch tuần sau | Triển vọng | - | Danh sách tập trung |

Giới hạn hình thức 3P: mỗi phần <= 5 gạch đầu dòng; mỗi gạch <= 2 dòng; tổng <= 1 màn hình. Newsletter: dưới 1000 từ là lý tưởng, mỗi mục 100-200 từ, đoạn 2-4 câu.

Tần suất gợi ý:
| Đối tượng (3P) | Tần suất | Độ dài |
|---|---|---|
| Line manager / PM Lead | Hằng tuần, cuối chiều thứ Sáu | 1 trang |
| Cuối tuần của phòng ban | Hằng tuần, sáng thứ Hai | 1 trang |
| Cá nhân | Hằng tuần, review Chủ nhật | nửa trang |
| Tổng hợp nhiều team | 2 tuần một lần | tối đa 2 trang |

| Newsletter | Tần suất |
|---|---|
| Toàn công ty | Hằng tuần hoặc 2 tuần một lần |
| Theo đơn vị (SBU) | Hằng tháng |
| Theo dự án | Mỗi milestone |
| Hướng khách hàng | Hằng quý |

## Template / mẫu đầu ra (rút gọn, giữ cấu trúc và các cột/trường)
Sponsor: `Sponsor Brief - Tuần NN <mã dự án>` -> Status (xanh/vàng/đỏ + 1 câu) -> Headlines (3-5 gạch) -> Asks (quyết định sponsor cần ra) -> Outlook -> ký tên PM.

Khách hàng: `Weekly Progress Report - <mã dự án>` + kỳ báo cáo -> Lời chào PIC -> Milestone Status (bảng Milestone | Target Date | Status) -> Achievements -> Pending from Customer (nêu mục, ngày yêu cầu, hạn cần có để tránh ảnh hưởng mốc) -> Change Requests (nêu tác động: công số, số ngày trễ, chi phí, đính kèm phân tích) -> lời kết.

Team: `Team Update - Tuần NN` -> Wins -> Need help -> Next week focus -> PM.

Slack (<= 280 ký tự): `<emoji trạng thái> <mã>-W<tuần>: headline. blocker. link nguồn`.

Steering (dàn ý 8 slide): 1 Tiêu đề; 2 Tóm tắt điều hành; 3 Burn-up mốc; 4 Bảng tín hiệu; 5 Rủi ro hàng đầu; 6 Quyết định cần ra; 7 30 ngày tới; 8 Asks.

3P (khuôn đầy đủ):
```
# 3P Update - <kỳ>     Team/Project | Reporter | Date
## Progress   - [đã xong] <việc> - 1 dòng bối cảnh + số liệu (tùy chọn: điểm đáng khoe)
## Plans      - <ưu tiên> - owner, ETA (3 mục)
## Problems   - blocker (tác động, cần hỗ trợ gì); rủi ro (khả năng, giảm thiểu); câu hỏi mở (cần ai quyết)
                (không có thì ghi "None this period - green light.")
## Metrics (tùy chọn)  Metric | This Period | Last | Trend
```
Tổng hợp nhiều team: mỗi team 1 khối (P1/P2/P3), cuối cùng có "Cross-team Asks (for sponsor)" dạng checklist quyết định/nguồn lực cần.
Biến thể: khách hàng (trang trọng hơn, thay "we" bằng tên team, bỏ tiếng lóng nội bộ, thêm mục "customer ask", ít gạch đầu dòng hơn); chỉ kỹ sư (thân mật, dùng thuật ngữ thoải mái); lãnh đạo cấp cao (câu đầu là HEADLINE trạng thái, TLDR trước chi tiết, nêu hàm ý chiến lược).

Newsletter (khuôn): tiêu đề + tagline 1 dòng -> Trong số này -> Headlines (2-4 câu, dẫn bằng tác động, kèm link) -> Bảng số liệu (3-5 chỉ số kể được câu chuyện: Metric | Value | Context) -> Thắng lợi -> Con người (mới vào, chuyển vị trí, chia tay) -> Cập nhật sản phẩm/dự án (kèm biểu tượng trạng thái) -> Sắp tới (sự kiện/hạn/mốc) -> Spotlight (tùy chọn) -> Nên đọc -> Mẹo -> lời kết + kênh phản hồi.

Quy tắc văn phong: 3P dùng thể chủ động; P1 quá khứ, P2 tương lai, P3 hiện tại; "we" cho team, "I" cho cá nhân. Ưu tiên số hơn tính từ ("+12% conversion" hơn "significant improvement"); dẫn link bằng chứng (PR, tài liệu, ticket); trung thực, mang tính xây dựng (vấn đề đi kèm đề nghị hỗ trợ, không than phiền), đổ lỗi cho hệ thống chứ không cho người. Newsletter: bắt đầu bằng tin quan trọng nhất, dùng "chúng ta", chủ động, cụ thể hơn trừu tượng, thuật ngữ kỹ thuật giữ tiếng Anh (release, milestone, KPI); bản nội bộ tiếng Việt, bản hướng khách hàng tiếng Anh hoặc song ngữ.

Checklist cuối: mọi con số truy ngược được về nguồn; `[NO_DATA]` ở chỗ nguồn thiếu; giọng khớp đối tượng; đã dùng đúng khuôn 3P/newsletter; bản khách hàng đã gắn cờ NHÁP chờ PM; không tự gửi.

## Lỗi thường gặp & lesson learned (lấy từ nguồn, mỗi ý: sai gì -> hậu quả -> cách tránh)
Bảng anti-pattern 3P:
| Sai | Vì sao hỏng | Cách tốt hơn |
|---|---|---|
| "Made progress on X" | Mơ hồ, tiến bao nhiêu? | "Shipped 8/10 sub-tasks of <tính năng>" |
| "Working on stuff" ở mục Plans | Nghe như không có kế hoạch | Ưu tiên cụ thể có hạn ("close M3 BD by Fri") |
| Giấu vấn đề ở P3 | Bất ngờ về sau, mất lòng tin | Nêu sớm, kèm đề nghị hỗ trợ |
| Khối văn bản dài | Không ai đọc | Gạch đầu dòng dễ lướt |
| Không có số | Khó so sánh giữa các tuần | Thêm 2-3 số chính |
| Cùng một khuôn mỗi tuần | Nhàm, bị bỏ qua | Đổi phần mở đầu, giữ cấu trúc |
| Liệt kê cuộc họp thay vì việc | Tốn thời gian lãnh đạo | Liệt kê kết quả, không liệt kê hoạt động |

Bảng anti-pattern newsletter:
| Sai | Vì sao hỏng | Cách tốt hơn |
|---|---|---|
| Lời mở đầu biên tập dài | Người đọc bỏ | Mở bằng headline |
| Số liệu chôn ở cuối | Mất thông tin chính | Dẫn bằng số tác động |
| Chỉ tự khen | Giống tuyên truyền | Pha thắng lợi với thách thức minh bạch |
| Không có bước tiếp theo | Người đọc không biết làm gì | Luôn có phần "sắp tới" |
| Chỉ ảnh lãnh đạo | Xa cách với team | Tôn vinh người đóng góp |
| Bản mẫu lặp lại | Nhàm | Đổi cấu trúc theo quý |
| Văn phong hành chính nhân sự | Máy móc, xa | Viết như nói với đồng nghiệp |

Các lỗi chung: bịa hoặc ước lượng số khi nguồn thiếu (dùng `[NO_DATA]`); gửi khách hàng khi chưa qua PM; tự trộn hai nguồn mâu thuẫn (phải hỏi); không chỉ rõ quyết định cần đối tượng ra.

## Ví dụ minh họa (1 ví dụ ngắn có số, lấy hoặc dựng từ nguồn; nếu dựng thì ghi "(ví dụ dựng)")
Từ nguồn (ẩn danh), Sponsor Brief tuần 34 của <tên-dự-án>:
- Status: vàng, At Risk - 1 blocker, 1 tín hiệu vượt ngân sách.
- Headlines: M2 SRS duyệt đúng hạn (QS-REQ-01 = 96%); QS-DEV-cov 76% (mục tiêu 80%); T-018 bị chặn 4 ngày do khách hàng chưa xác nhận API; chênh lệch effort 10.3%.
- Asks: (1) duyệt CR-002 (đã chờ 5 ngày, mở rộng phạm vi +20md); (2) hỗ trợ escalate với khách hàng lúc 14:00.
- Outlook: M3 BD duyệt mục tiêu 2026-09-08 nếu T-018 giải quyết trong tuần; go-live 2026-09-30 có nguy cơ trễ +1 tuần nếu T-018 trượt.
Cùng dữ kiện thành Slack: `🟡 KM-W34: M2 xong. 1 blocker (T-018 API khách hàng) - escalation 14h. DEV-cov 76%, đẩy UT. Plan: M3 close W36. Chi tiết: <link nguồn>`. Với khách hàng: bảng mốc (M3 Basic Design 2026-09-08: đang làm, 5/7 module xong), mục "Pending from Customer" nêu xác nhận 5 API endpoint, cần trước 2026-08-28; CR-003 chờ duyệt: +20md, +7 ngày, chi phí thêm $8,000.

## Tự kiểm tra (3-5 câu hỏi có đáp án ngắn ngay dưới, dựa trên chính nội dung bài)
1. Nguồn không có số chênh lệch effort. Bạn viết gì?
   - `[NO_DATA]`, không ước lượng.
2. Giới hạn ký tự của tin Slack và nội dung tối thiểu?
   - <= 280 ký tự: emoji trạng thái + 1 dòng headline/blocker + link nguồn.
3. Ba chữ P là gì và thì động từ của từng phần?
   - Progress (quá khứ), Plans (tương lai), Problems (hiện tại).
4. Quy trình bản gửi khách hàng?
   - Nháp đủ sự kiện -> PM đánh dấu mục nhạy cảm -> bản chính thức -> chỉ gửi khi PM duyệt.
5. Rủi ro High đang mở nên đi vào đâu trong thông điệp cho sponsor và cho khách hàng?
   - Sponsor: mục Asks; khách hàng: mục việc đang chờ phía khách hàng.

## Liên quan (bài trước/sau trong quy trình, tên thư mục skill khác)
- Nguồn vào: báo cáo trạng thái tuần, gate review, change request, kế hoạch release, hiến chương dự án (kickoff), họp hằng ngày (nguồn cho Slack).
- Liên quan: Phân tích họp (Ch7·02) (action item từ họp thành cập nhật), Sprint retro (Ch7·04) (thông tin spotlight cho newsletter), Bug triage (Ch6·05).
