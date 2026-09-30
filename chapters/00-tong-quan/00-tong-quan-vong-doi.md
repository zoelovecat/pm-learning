---
title: Tổng quan vòng đời dự án, gate và tín hiệu
source: SKILL-MAP-SDLC.md, README.md, DATA-SOURCES.md
stage: Cross-cutting
level: cơ bản
prerequisites: []
---
# Tổng quan vòng đời dự án, gate và tín hiệu

## Mục tiêu học xong bạn làm được gì
- Kể đúng 10 giai đoạn của dự án và việc chính của PM ở từng giai đoạn.
- Nói được gate G1-G6 nằm ở đâu, ai duyệt, và vì sao gate dựa trên tín hiệu định lượng.
- Phân biệt việc làm theo nhịp (hằng ngày/tuần) với việc làm theo sự kiện và theo giai đoạn.

## Khi nào dùng
Học đầu tiên, và quay lại mỗi khi cần định vị "dự án đang ở đâu, việc tiếp theo là gì".

## Khái niệm cốt lõi
- **SDLC 10 giai đoạn**: 0 Pre-Project (báo giá) → 1 Initiation → 2 Planning → 3 Requirements → 4 Design → 5 Development → 6 Testing → 7 Release → 8 Hypercare → 9 Closure.
- **Milestone (M)**: mốc cần đạt. M1 Charter Approved, M2 SRS Approved, M3 BD (Basic Design) Approved, M4 Code Complete, M5a System Test Done, M5b UAT Sign-off, M6 Go-live, M7 Project Closed. M0 là mốc pre-project.
- **Gate (G)**: điểm ra quyết định cuối mỗi giai đoạn. G1 (Initiation, định tính), G2 (SRS), G3 (BD), G4 (code), G5 (UAT Sign-off), G6 (Go/No-go release). Lưu ý: bản đồ SDLC gốc chia G5 thành G5a (system test) và G5b (UAT), còn ma trận gate chỉ có một G5 = UAT Sign-off; khi chạy gate review hãy theo ma trận gate (nguồn chưa rõ cách hai tài liệu thống nhất). Gate thay câu hỏi mơ hồ "khi nào sang giai đoạn sau" bằng dữ liệu và ngưỡng rõ ràng, để quyết định không dựa vào ý kiến người có chức vụ cao nhất (HiPPO).
- **Tín hiệu QS-XX**: chỉ số định lượng gắn với từng giai đoạn/gate (ví dụ QS-REQ-01, QS-DSG-03, QS-TST-04). Chi tiết ở bài Tín hiệu (Ch6·01) và Gate review (Ch8·02).
- **Vòng học liên dự án**: lessons learned khi đóng dự án nuôi lại bước báo giá của dự án sau; effort thực tế thành benchmark; đội được giải phóng quay lại pool xếp người.

## Cách làm từng bước (đọc vòng đời như một PM)
Với mỗi giai đoạn nắm 4 thứ: việc cần làm, đầu ra, mốc, tín hiệu/gate.

| Giai đoạn | Việc chính của PM | Mốc/Gate | Tín hiệu chính |
|---|---|---|---|
| 0 Pre-Project | Ước lượng báo giá, dự báo năng lực đội, phân tích họp khám phá với khách | M0; quyết định GO / NO-GO | (chưa có) |
| 1 Initiation | Kickoff, lập charter + rủi ro ban đầu, chọn người theo RACI | M1 Charter Approved; G1 định tính (Sponsor + PM theo ma trận gate; bản đồ SDLC thêm Customer PIC nếu dự án ngoài) | — |
| 2 Planning | WBS, danh sách task, schedule + capacity + critical path, xếp người | Baseline schedule locked | E3 ≤ 10% (theo dõi hằng tuần từ giai đoạn này) |
| 3 Requirements | Chốt yêu cầu, checklist review, theo dõi tín hiệu | M2 SRS Approved; G2 (BA Lead + Customer PIC) | QS-REQ-01 ≥ 95%, QS-REQ-03 = 100% |
| 4 Design | Task BD, checklist design review | M3 BD Approved; G3 (Tech Lead + Customer PIC) | QS-DSG-03 ≤ 5% |
| 5 Development | Daily sync, CR, effort, rủi ro/issue, status tuần | M4 Code Complete; G4 (Tech Lead + QA Lead) | QS-DEV-cov ≥ 80%, QS-PRC-07 ≥ 90%, E3 ≤ 10% hằng tuần |
| 6 Testing | Task test, theo dõi lỗi, checklist test, UAT | M5a System Test Done; M5b UAT Sign-off (gate UAT: QA Lead + Customer PIC) | QS-TST-02 ≤ baseline, QS-TST-04 ≤ 2%, QS-TST-08 ≤ 5% |
| 7 Release | Release plan, checklist G6, chạy release, thông báo khách | G6 Go decision (PM + Sponsor + DevOps); M6 Go-live | QS-PRC-07 ≥ 90% |
| 8 Hypercare | Theo dõi sản xuất sau go-live, xử lý sự cố | Cửa sổ theo loại release: Major 7 ngày, Minor 3, Patch 1, Hotfix 24 giờ | Uptime ≥ 99.5%, error rate ≤ baseline + 0.5%, p95 latency ≤ baseline + 10%, 0 sự cố P1 |
| 9 Closure | Retro + lessons learned, chốt effort thực, báo cáo cuối cho khách, đóng dự án | M7 Project Closed (PM + Sponsor + Customer PIC + Support Lead) | — |

Hypercare kết thúc khi hết cửa sổ và mọi chỉ số xanh; nếu cần hotfix thì quay lại giai đoạn 7 với loại release = Hotfix. Không bỏ hypercare: nó là cầu nối giữa release và đóng dự án.

Tiếp quản dự án đang chạy mà thiếu tài liệu quản lý: dựng lại (bootstrap) lịch, trạng thái, gate, rủi ro, CR (và charter) từ hệ thống quản lý dự án trước khi đóng dự án (bài Tiếp quản PM, Ch5·04).

## Nhịp việc theo tần suất
| Tần suất | Việc |
|---|---|
| Hằng ngày (giai đoạn 5-9) | Daily sync đầu ngày |
| Hằng tuần | Status weekly (chiều thứ Sáu), signal monitor, effort actuals (variance) |
| Theo sự kiện | Change request, rủi ro/issue, phân tích họp, checklist trước gate, thông báo cho từng nhóm stakeholder, tiếp quản PM |
| Theo giai đoạn/gate | Checklist trước gate, gate review cuối giai đoạn |
| Một lần/dự án | Kickoff, lessons learned, closeout |
| Một lần/giai đoạn | WBS, danh sách task, gate G1-G6 |
| Một lần/release | Release plan, release exec, hypercare |
| Liên dự án | Ước lượng báo giá (trước mỗi bid), dự báo năng lực (hằng quý hoặc trước khi cam kết bid; do PM Lead chạy) |

## Nguyên tắc dữ liệu (rút từ registry nguồn dữ liệu)
- Nguồn dữ liệu có 5 loại: tài liệu dự án (PM chỉnh), quy tắc Kaopiz (KHÓA, chỉ QA đổi), hệ thống ngoài, nhập tay từ PM, và số tự tính.
- Trường dữ liệu chia 3 mức: BẮT BUỘC (thiếu thì dừng, quay về bước trước), TÙY CHỌN (hỏi PM, có thể để TBD), TỰ ĐIỀN (lấy mặc định Kaopiz).
- Quy tắc cố định hay gặp: 1 MM = 20 MD = 160 MH; tuần theo ISO 8601 (Thứ Hai-Chủ Nhật); múi giờ mặc định UTC+7; 5 ngày làm việc/tuần; task ≤ 1 md và không chuyển sang ngày sau.
- Hệ số ước lượng mặc định theo loại việc: REQ 0.5; BD/DEV cỡ S = 0.5, cỡ M = 1; UT 0.5; TC/TE 0.5-1.
- Buffer theo loại hợp đồng (bản nháp): Fixed-bid 15%, T&M 10%, Offshore 20%, R&D 25%, Internal 10%, Compliance 20%.
- Công thức CPI, SPI theo chuẩn EVM: CPI = EV/AC, SPI = EV/PV.
- Ngưỡng mặc định E3 = 10%.

## Lỗi thường gặp & lesson learned
- Bỏ qua hypercare để đóng dự án sớm -> lỗi sản xuất tràn sang giai đoạn đóng -> giữ cửa sổ theo loại release.
- Quyết định qua gate theo cảm tính -> tranh cãi và làm lại -> luôn có tín hiệu định lượng và checklist trước gate.
- Không nạp lessons learned cho báo giá dự án sau -> lặp lại lỗi ước lượng -> đưa effort thực và lessons vào benchmark.

## Ví dụ minh họa (ví dụ dựng)
Dự án đang ở giai đoạn 3 (Requirements). Tuần này QS-REQ-01 = 92% (ngưỡng ≥ 95%). Kết luận: chưa đủ điều kiện G2; PM đẩy BA hoàn thiện phần thiếu, chạy lại checklist, chưa xin M2.

## Tự kiểm tra
1. Gate nào là gate Go/No-go release và ai duyệt? — G6; PM + Sponsor + DevOps.
2. Cửa sổ hypercare của bản Minor là bao lâu? — 3 ngày (Major 7, Patch 1, Hotfix 24 giờ).
3. Kể ngưỡng tín hiệu của giai đoạn Requirements. — QS-REQ-01 ≥ 95%, QS-REQ-03 = 100%.
4. 1 MM bằng bao nhiêu MD, MH? — 20 MD = 160 MH.
5. Việc nào PM làm mỗi chiều thứ Sáu? — Status weekly.

## Liên quan
Xem `curriculum.md` cho thứ tự học; bài chi tiết từng việc nằm trong thư mục lessons.
