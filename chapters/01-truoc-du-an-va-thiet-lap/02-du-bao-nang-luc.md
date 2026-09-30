---
title: Dự báo năng lực và nhu cầu nhân sự (capacity forecast)
source: Dự báo năng lực (Ch1·02)
stage: Pre-Project
level: trung bình
prerequisites: [Ch1·01]
---
# Dự báo năng lực nhân sự liên dự án (capacity forecast)

## Mục tiêu học xong bạn làm được gì
- Tính được khoảng trống (gap) giữa năng lực và nhu cầu theo đơn vị (SBU)/vai trò/tháng.
- Phân loại trạng thái Healthy / Underutilized / Overcommit / Critical theo ngưỡng.
- Đưa ra các phương án xử lý khi thiếu hoặc dư người, và lập báo cáo dự báo cho PM Lead/SBU Manager.

## Khi nào dùng (thời điểm, ai kích hoạt, điều kiện đầu vào)
- Khi cần trả lời "quý sau có rảnh không", "có cần tuyển thêm không", "có nên nhận thêm bid không". PM Lead hoặc SBU Manager kích hoạt; tần suất chạy chưa chốt (nguồn chưa rõ: hàng tháng / hàng quý / theo yêu cầu).
- Đầu vào bắt buộc: (1) chân trời dự báo 3/6/12 tháng; (2) lịch các dự án đang chạy kèm công số còn lại; (3) dữ liệu năng lực SBU (headcount, phân bổ). Thiếu thì dừng, không đoán năng lực.
- Đầu vào tùy chọn: các bid trong pipeline, bộ lọc SBU, xác suất thắng từng bid.
- Kết quả là bản NHÁP; con người quyết định tuyển / bỏ bid / điều chuyển, không làm tự động.

## Khái niệm cốt lõi (định nghĩa, thuật ngữ, vì sao quan trọng)
- **Capacity**: công số sẵn có của SBU/vai trò trong kỳ (md). **Committed**: công số còn lại đã cam kết cho dự án đang chạy. **Pipeline demand**: nhu cầu từ bid chưa thắng, tính có trọng số theo xác suất thắng.
- **Gap**: chênh lệch; dương là dư (bench), âm là thiếu (overcommit).
- **Weighted demand** = công số bid x xác suất thắng.
- 1 MM = 20 MD. Thời gian tuyển senior mặc định 2-3 tháng (senior khan hiếm).
- Vì sao quan trọng (giải thích thêm): thắng bid mà không có người làm hỏng dự án; ngược lại bench lâu là lãng phí.

## Cách làm từng bước (thủ công, đủ chi tiết để làm theo; kèm input/output)
1. **Xác nhận đầu vào**: chân trời (3/6/12 tháng), phạm vi (toàn công ty / một SBU / một vai trò). Kiểm tra có dữ liệu năng lực và ít nhất 1 dự án đang chạy có công số còn lại.
2. **Chọn tùy chọn**: có đưa pipeline hay không (không thì bỏ mục pipeline), bộ lọc SBU (mặc định tất cả), xác suất thắng từng bid (từ Sales/CRM hoặc PM tự nhập), ngưỡng xác suất đưa vào nhu cầu có trọng số (mặc định 40%).
3. **Kiểm tra**: khoảng thời gian không trùng kỳ đã dự báo trước; bộ lọc SBU hợp lệ; công số còn lại không âm và không vượt năng lực hiện tại một cách bất thường. Lịch nội bộ mâu thuẫn dữ liệu năng lực -> dừng và hỏi, không tự đối chiếu ngầm. Công số bid khác số trong CRM -> đánh dấu để chọn nguồn chuẩn.
4. **Thu thập dữ liệu**: năng lực theo kỳ và theo vai trò, danh sách người đang bench, dự báo tổng hợp; cộng công số còn lại theo vai trò theo tháng cho từng dự án đang chạy; với pipeline lấy công số, phân chia vai trò, giai đoạn bid, xác suất thắng. Ghi mốc thời gian lấy dữ liệu.
5. **Tính gap** theo công thức ở phần dưới, theo từng SBU/vai trò/tháng và tổng theo quý.
6. **Gắn trạng thái** theo ngưỡng; với mỗi mục đỏ, xin gợi ý tuyển dụng (SBU, vai trò, gap) và ghi thời gian tuyển 2-3 tháng.
7. **Lập báo cáo** theo thứ tự: metadata; tổng hợp theo SBU; chi tiết theo tháng; dự án đang chạy; pipeline có trọng số; cảnh báo overcommit (đỏ); bench (vàng); khuyến nghị (hành động - người chịu trách nhiệm - thời hạn); nguồn dữ liệu. Đặt cảnh báo đỏ/vàng TRƯỚC bảng khuyến nghị.
8. **Bàn giao nháp**: tóm tắt số SBU theo từng trạng thái, các gap lớn nhất, khuyến nghị tuyển; xác nhận phạm vi với PM Lead/SBU Manager; chưa tự kích hoạt tuyển, bỏ bid hay xử lý bench.

## Công thức, ngưỡng & tín hiệu (bảng: tên | công thức/điều kiện | ngưỡng | hành động khi vượt)
| Tên | Công thức / điều kiện | Ngưỡng | Hành động |
|---|---|---|---|
| Gap | gap[sbu][role][month] = capacity - committed_effort - (pipeline_demand x win_probability) | gap > 0 bench (vàng); gap < 0 overcommit (đỏ); gap ≈ 0 khỏe (xanh) | Theo trạng thái |
| Underutilized | net gap (md/quý) | > +50 | Hành động xử lý bench |
| Healthy | net gap | từ -10 đến +50 | Không cần |
| Overcommit | net gap | từ -10 đến -50 | Tuyển / thuê ngoài |
| Critical | net gap | < -50 | Hành động ngay |
| Xác suất thắng đưa vào | win_prob_threshold | mặc định 40% | Bid dưới ngưỡng loại khỏi nhu cầu có trọng số |
| Thời gian tuyển | hire lead time | 2-3 tháng (senior) | Ghi trong khuyến nghị |
| Đổi đơn vị | 1 MM | = 20 MD | |

Các ngưỡng gap là heuristic theo nguồn.

Phương án khi overcommit:
1. Tuyển (thời gian 2-3 tháng).
2. Thuê ngoài / đối tác tạm.
3. Từ chối bid có WSJF x xác suất thắng thấp nhất (xem bài Ước tính chào giá, Ch1·01).
4. Điều chuyển giữa SBU (cần 2 SBU Manager xác nhận).
5. Cross-train từ SBU đang bench sang SBU thiếu kỹ năng (SBU Manager quyết; người lập dự báo chỉ đề xuất).
6. Làm thêm giờ - không khuyến nghị (rủi ro với chỉ số E3).

## Template / mẫu đầu ra (rút gọn, giữ cấu trúc và các cột/trường)
"Capacity Forecast - <kỳ>":
- Metadata: Generated | Horizon | Scope | Include pipeline (kèm ngưỡng) | Status (DRAFT).
- Summary: SBU | Capacity (md/Q) | Committed | Pipeline | Net | Status.
- Per-month detail: SBU | Cap | Committed | Pipeline | Net.
- Active Projects: Project | Status | Effort remaining trong kỳ.
- Pipeline Demand (weighted): Bid | Stage | Effort | Win prob | Weighted.
- Overcommit Alerts (đỏ): mỗi SBU thiếu kèm các phương án.
- Bench (vàng): hành động đề xuất (vd cross-train).
- Recommendations: # | Action | Owner | Timeline.
- Data Sources: mốc thời gian lấy dữ liệu, số dự án đã quét, số bid.

Checklist: chân trời và phạm vi đã xác nhận với PM Lead; gap tính theo SBU (và vai trò nếu có); đỏ nêu trước khuyến nghị; ghi thời gian tuyển 2-3 tháng; ghi mốc thời gian dữ liệu; trạng thái DRAFT; không tự kích hoạt tuyển / từ chối bid.

## Lỗi thường gặp & lesson learned (lấy từ nguồn, mỗi ý: sai gì -> hậu quả -> cách tránh)
- Đoán năng lực khi thiếu dữ liệu -> dự báo vô nghĩa -> dừng, lấy dữ liệu hoặc để PM cung cấp.
- Lịch dự án và dữ liệu năng lực mâu thuẫn mà tự dàn xếp ngầm -> sai lệch không ai biết -> hỏi và chốt nguồn chuẩn.
- Cộng nguyên công số bid mà không nhân xác suất thắng -> nhu cầu bị thổi phồng -> luôn dùng weighted demand.
- Quên thời gian tuyển 2-3 tháng -> tuyển quá trễ -> ghi lead time vào khuyến nghị.
- Dùng làm thêm giờ để bù thiếu -> rủi ro (E3) -> không khuyến nghị.
- Tự kích hoạt tuyển / bỏ bid -> vượt thẩm quyền -> chỉ đề xuất, người có thẩm quyền quyết.

## Ví dụ minh họa (1 ví dụ ngắn có số, lấy hoặc dựng từ nguồn; nếu dựng thì ghi "(ví dụ dựng)")
Từ nguồn (Q1): Banking: capacity 600, committed 480, pipeline 80 -> net 40, Healthy. Frontend: 720 - 600 - 150 = -30, Overcommit. Backend: 900 - 750 - 200 = -50, Overcommit (đúng biên -50). QA: 540 - 380 - 60 = +100, Underutilized. Đề xuất nguồn: tuyển 1 FE + 2 BE, từ chối một bid, cross-train 2 người QA sang BE hybrid.
Weighted: BID-2026-042 145 md x 60% = 87 md; BID-2026-048 50 md x 30% = 15 md.
(nguồn chưa rõ: dòng chi tiết tháng 1 của Frontend là 240 - 200 - 50 = -10 và gắn đỏ, trong khi -10 thuộc khoảng Healthy của bảng ngưỡng; ngưỡng tính theo md/quý nên không nên áp thẳng cho từng tháng. Bid 048 xác suất 30% thấp hơn ngưỡng 40% nhưng vẫn có trong bảng ví dụ.)

## Tự kiểm tra (3-5 câu hỏi có đáp án ngắn ngay dưới, dựa trên chính nội dung bài)
1. Viết công thức gap. -> capacity - committed_effort - (pipeline_demand x win_probability).
2. Net gap -30 md/quý thuộc trạng thái nào và làm gì? -> Overcommit (từ -10 đến -50): tuyển / thuê ngoài; dưới -50 là Critical.
3. Ngưỡng xác suất thắng mặc định để đưa bid vào nhu cầu có trọng số? -> 40%.
4. Thời gian tuyển senior mặc định? -> 2-3 tháng.
5. Điều chuyển người giữa hai SBU cần gì? -> 2 SBU Manager xác nhận.

## Liên quan (bài trước/sau trong quy trình, tên thư mục skill khác)
- Trước: Ước tính chào giá (Ch1·01) (nguồn nhu cầu pipeline), Lập schedule (Ch3·03) (nguồn cam kết theo dự án).
- Sau: Xếp người (Ch3·05) (sau khi tuyển, xếp người vào dự án), Kickoff (Ch2·01) (năng lực ảnh hưởng quy mô dự án).
