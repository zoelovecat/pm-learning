---
title: Phân tích họp để tự coaching hành vi giao tiếp (Meeting Analyzer)
source: Phân tích họp (Ch7·02)
stage: Cross-cutting
level: trung bình
prerequisites: []
---
# Phân tích họp để tự coaching hành vi giao tiếp

## Mục tiêu học xong bạn làm được gì
- Từ bản ghi (transcript) một cuộc họp, đo được hành vi giao tiếp của chính bạn (hoặc người bạn coaching): tỉ lệ nói, độc thoại dài, ngắt lời, từ đệm, từ rào đón, kiểu câu hỏi, cách xử lý xung đột/blocker.
- So từng chỉ số với ngưỡng theo loại cuộc họp và biết cải thiện thế nào.
- Viết báo cáo coaching không phán xét: Tiếp tục / Bắt đầu / Dừng, kèm bằng chứng trích dẫn.

## Khi nào dùng (thời điểm, ai kích hoạt, điều kiện đầu vào)
- Sau các cuộc họp: standup, review, retro, customer sync, steering. PM (hoặc người muốn được coaching) kích hoạt.
- Khác báo cáo trạng thái hằng tuần: báo cáo trạng thái dựa trên số liệu dự án; bài này dựa trên hành vi thể hiện trong ngôn ngữ thật của cuộc họp.
- Đầu vào bắt buộc: (1) file transcript (định dạng .txt, .md, .vtt, .srt, .docx, .json, xuất từ các công cụ ghi âm họp); (2) xác định ai là "người được coaching" (focus speaker). Thiếu một trong hai thì dừng, không đoán người nói.
- Đầu vào nên có: nhãn người nói (thiếu thì chỉ đo được chỉ số tổng, giới hạn chỉ số theo từng người) và ngày họp (có thể suy từ tên file/nội dung).
- Tùy chọn (mặc định khi bỏ qua): loại cuộc họp (tự suy từ nội dung), chế độ bảo mật (tắt: trích dẫn nguyên văn), khoảng nhiều cuộc họp (chỉ 1 file), trích xuất action item (tắt), ngôn ngữ báo cáo (theo ngôn ngữ transcript).

## Khái niệm cốt lõi (định nghĩa, thuật ngữ, vì sao quan trọng)
- Coaching hành vi khác đánh giá con người: phản hồi phải nói về hành vi quan sát được, kèm bằng chứng, giọng không phán xét.
- 5 nhóm phân tích: (1) Speaking dynamics, (2) Filler và hedging, (3) Question pattern, (4) Action item extraction (tùy chọn), (5) Conflict/Blocker pattern.
- Filler (từ đệm), hedging (từ rào đón làm yếu câu quyết định), softener (từ làm mềm), leading question (câu hỏi dẫn dắt), ask/tell ratio (tỉ lệ hỏi so với nói).
- Chỉ số chỉ tính cho người được coaching, không gán ma sát của người khác cho họ.
- Không lưu toàn bộ transcript, chỉ trích đoạn ngắn làm bằng chứng (giảm rủi ro thông tin nhạy cảm).

## Cách làm từng bước (thủ công, đủ chi tiết để làm theo; kèm input/output)
1. Xác nhận file transcript đọc được và ai là người được coaching. Nếu ngày trong tên file mâu thuẫn ngày trong nội dung thì hỏi lại, không tự dàn xếp.
2. Chuẩn hóa transcript thành danh sách: người nói, mốc thời gian (giây), nội dung. Thiếu mốc thời gian thì bỏ các chỉ số về thời gian (độc thoại theo giây, ngắt lời), vẫn phân tích được phần text.
3. Với mỗi người nói, tính: số từ và % tổng; số lượt nói, độ dài lượt trung bình; độc thoại dài nhất; số lần ngắt lời; tỉ lệ filler; tỉ lệ hedging. Tính theo từ điển ở Module 2.
4. So với ngưỡng (bảng dưới). Chỉ điền cột "Example" (trích dẫn) cho dòng bị đánh dấu vượt ngưỡng.
5. Phân loại câu hỏi của người được coaching (mở / đóng / dẫn dắt / làm rõ), tính Ask %, % câu hỏi dẫn dắt, % câu hỏi đóng, so với mục tiêu theo loại họp.
6. (Chỉ khi người được coaching đồng ý) trích action item: tìm các mẫu kiểu "X sẽ làm Y trước [ngày]", "ai phụ trách", "due [ngày]", "[tên] take this"; đo owner rõ và due date rõ.
7. Tìm mẫu xung đột/blocker mà người được coaching là người nói hoặc bị nhắm tới.
8. Nếu có nhiều cuộc họp: so xu hướng từng chiều, ghi rõ chiều nào cải thiện, chiều nào thụt lùi.
9. Viết báo cáo theo mẫu ở dưới, trạng thái DRAFT chờ người được coaching xem lại; chạy checklist cuối.

## Công thức, ngưỡng & tín hiệu (bảng: tên | công thức/điều kiện | ngưỡng | hành động khi vượt)
| Tên | Công thức/điều kiện | Ngưỡng | Hành động khi vượt |
|---|---|---|---|
| Dominance | 1 người nói chiếm % tổng số từ | > 60% | Dominance: cân lại thời lượng nói, mời người khác |
| Độc thoại dài | Một lượt nói liên tục | > 60 giây hoặc > 200 từ (cờ) | Ngắt nhịp, hỏi lại người nghe |
| Lecture mode | Số độc thoại > 200 từ của người được coaching | > 2 lần | Chuyển sang hỏi thay vì giảng |
| Ngắt lời | Lượt nói bắt đầu trong vòng 2 giây sau người trước | tần suất cao | Dấu hiệu vỡ nhịp hội thoại (nguồn chưa rõ: "cao" là bao nhiêu) |
| Filler rate | Số từ đệm mỗi phút | > 5/phút | Cần luyện nói |
| Hedging rate | Số từ rào đón mỗi phút trong ngữ cảnh ra quyết định | > 3/phút | Thiếu tự tin, nói thẳng quyết định |
| Ask % lệch mục tiêu | Ask % so với khoảng mục tiêu theo loại họp | lệch > 10 điểm ngoài khoảng | Thấp: quá nhiều "tell"; cao: có thể thiếu quyết đoán khi cần chốt (tùy ngữ cảnh) |
| Câu hỏi dẫn dắt | % trên tổng câu hỏi | > 20% | Đổi thành câu hỏi mở |
| Câu hỏi đóng | % trên tổng câu hỏi | > 50% | Thêm follow-up "Vì sao/Cụ thể như nào" |
| Owner rõ (action item) | % action item có owner rõ | mục tiêu 90% | Cờ: thiếu owner, bàn giao mập mờ lặp lại |
| Due date rõ (action item) | % có deadline rõ | mục tiêu 80% | Như trên |

Mục tiêu Ask % theo loại họp:
| Loại họp | Ask % lý tưởng |
|---|---|
| Standup | 30-40% |
| Review | 50%+ |
| Decision | 20-30% ask |
| Customer sync | 40-50% |

Từ điển (Module 2):
- Filler tiếng Việt: ờ, à, kiểu, kiểu như, thì là, đại loại, cái này. Filler tiếng Anh: uh, um, like, you know.
- Hedging: có lẽ, tôi nghĩ là, không chắc nhưng, I think, maybe.
- Softener: chỉ là, một chút, có thể (chỉ tính khi lặp quá nhiều).

Bốn loại câu hỏi (Module 3):
| Loại | Ví dụ | Rủi ro nếu lạm dụng |
|---|---|---|
| Mở | "Anh nghĩ sao về...?" | Không có (đây là mục tiêu chính) |
| Đóng | có/không | Giới hạn thảo luận, thiếu chi tiết |
| Dẫn dắt | "Đúng không?" | Dẫn câu trả lời, giảm tín hiệu thật |
| Làm rõ | "Ý anh là... đúng chứ?" | Quá nhiều: chưa nghe kỹ lần đầu |

Mẫu xung đột/blocker (Module 5, chỉ khi người được coaching là người nói hoặc bị nhắm tới):
| Mẫu | Tín hiệu | Mức | Cách cải thiện |
|---|---|---|---|
| Né tránh | "để bàn sau", "discuss offline" lặp cùng vấn đề | Trung bình | Nêu bước tiếp theo cụ thể ngay trong họp, tránh hoãn lặp |
| Thời điểm escalate | blocker được nêu, nhiều lượt sau mới escalate | Cao | Escalate ngay khi blocker rõ tác động |
| Phòng thủ | "tôi đã làm rồi" | Trung bình | Trả lời bằng dữ kiện/số liệu thay vì giọng phòng thủ |
| Đồng ý quá sớm | agree quá nhanh | Thấp | Xác nhận hiểu đúng bằng 1 câu làm rõ trước khi đồng ý |

## Template / mẫu đầu ra (rút gọn, giữ cấu trúc và các cột/trường)
```
# Meeting Analysis - <chủ đề> <ngày>
(Chú giải nguồn ở đầu file)
| Field | Value |  -> Date / Type / Participants / Duration / User focus / Status (DRAFT)

## Coaching Summary   (đặt ngay sau phần thông tin chung; 3-5 mục mỗi loại, mỗi mục 1 ví dụ)
| Category | Item | Example |
| CONTINUE | ... | "[mốc thời gian] người nói: ..." |
| START    | ... | ... |
| STOP     | ... | ... |

## Speaking Dynamics (<người được coaching>)
1-2 câu nhận xét chung, rồi bảng: Metric | Value | Status | Example
(filler và hedging là các dòng trong bảng này)

## Question Pattern (<người được coaching>)
1-2 câu nhận xét chung, rồi bảng: Metric | Value | Status | How to improve

## Action Items (chỉ khi đã chọn bật)   Action | Owner | Due | Clear?
## Conflict / Blocker (<người được coaching>)   Pattern | Signal | Severity | How to improve
## Cross-meeting trend (nếu N > 1)
```
Gợi ý "How to improve" cho câu hỏi: Ask % thấp -> đổi phát biểu thành câu hỏi mở ("Tôi nghĩ X" -> "Anh nghĩ gì về X?"); dẫn dắt cao -> đổi "Đúng không?" thành "Anh thấy sao?"; đóng cao -> thêm "Vì sao"/"Cụ thể như nào".

Checklist cuối: xác nhận phạm vi trước khi phân tích sâu; mục Action Items chỉ có khi đã bật; không lưu transcript đầy đủ; có ví dụ trích dẫn cho mọi dòng bị cờ; tôn trọng chế độ bảo mật (diễn đạt lại thay vì trích nguyên văn); giọng không phán xét; không commit git.

## Lỗi thường gặp & lesson learned (lấy từ nguồn, mỗi ý: sai gì -> hậu quả -> cách tránh)
- Chỉ đưa số liệu thô, không kèm nhận xét chung -> người đọc không biết rút ra gì -> luôn có 1-2 câu tổng kết trước mỗi bảng.
- Đặt takeaway ở cuối sau hàng loạt bảng -> người đọc mệt trước khi tới kết luận -> để Coaching Summary ở đầu.
- Tách bằng chứng (quote) thành mục riêng -> không rõ bằng chứng của chỉ số nào -> gắn quote vào cột Example của dòng bị cờ.
- Gán conflict giữa hai người khác cho người được coaching -> phản hồi oan -> chỉ tính khi họ là người nói hoặc bị nhắm tới.
- Bản cũ chỉ đếm % loại câu hỏi mà không đánh giá -> không hành động được -> có ngưỡng và cột How to improve.
- Trộn việc theo dõi action item vào coaching -> lệch phạm vi (theo dõi task thuộc nhóm báo cáo/họp hằng ngày) -> để tùy chọn, mặc định tắt.
- Đoán ai là người được coaching, hoặc tự dàn xếp khi ngày file và ngày nội dung mâu thuẫn -> kết quả sai người/sai buổi -> dừng và hỏi.
- Lưu cả transcript -> rủi ro thông tin nhạy cảm -> chỉ trích đoạn ngắn.
- Câu hỏi mở của nguồn chưa chốt: có nên bỏ tên trước khi phân tích, từ điển filler theo phương ngữ Bắc/Nam, mốc mặc định của tổ chức, cửa sổ so nhiều buổi (4 tuần hay 1 quý), họp song ngữ.

## Ví dụ minh họa (1 ví dụ ngắn có số, lấy hoặc dựng từ nguồn; nếu dựng thì ghi "(ví dụ dựng)")
(ví dụ dựng) Họp quyết định 20 phút. PM nói 780 từ trên tổng 1200 từ = 65% > 60% -> cờ dominance. Filler 130 lần / 20 phút = 6.5/phút > 5/phút -> cần luyện. 10 câu hỏi của PM: 3 câu dẫn dắt (30% > 20%) -> cờ; Ask % = 35%, ngoài khoảng 20-30% của họp Decision 5 điểm nên chưa vượt ngưỡng lệch 10 điểm. Coaching Summary: STOP "Đúng không?" cuối ý kiến; START chốt bước tiếp theo bằng câu hỏi mở; CONTINUE tóm tắt quyết định cuối họp.

## Tự kiểm tra (3-5 câu hỏi có đáp án ngắn ngay dưới, dựa trên chính nội dung bài)
1. Ngưỡng nào cho thấy một người "lecture mode"?
   - Người được coaching có hơn 2 lần độc thoại dài hơn 200 từ.
2. Họp review, Ask % của bạn là 35%. Có vấn đề không?
   - Mục tiêu review là 50%+; lệch 15 điểm, vượt ngưỡng lệch 10 điểm, nghĩa là nói nhiều hơn hỏi.
3. Filler và hedging có ngưỡng nào?
   - Filler > 5/phút; hedging > 3/phút trong ngữ cảnh ra quyết định.
4. Vì sao cột Example chỉ điền ở dòng bị cờ?
   - Gắn bằng chứng cụ thể vào chỉ số vi phạm, tránh feedback trừu tượng và giảm lượng dữ liệu nhạy cảm.
5. Khi nào xuất mục Action Items?
   - Chỉ khi đã đồng ý bật ở bước thu thập thông tin; mặc định tắt.

## Liên quan (bài trước/sau trong quy trình, tên thư mục skill khác)
- Kết nối: báo cáo trạng thái tuần (khác về dữ liệu), Giao tiếp stakeholder (Ch7·03) (action item thành cập nhật cho các bên), Sprint retro (Ch7·04) (mẫu lặp qua nhiều cuộc họp đưa vào retro), họp hằng ngày (transcript standup làm nguồn), quản lý rủi ro/issue (mục escalation/blocker, tùy chọn).
