---
title: Lập WBS gắn milestone với tín hiệu chất lượng (QS-XX)
source: WBS (Ch3·01)
stage: Initiation
level: trung bình
prerequisites: [Ch2·03]
---
# Lập WBS gắn milestone với tín hiệu chất lượng (QS-XX)

## Mục tiêu học xong bạn làm được gì
- Phân rã dự án thành cây 4 cấp Project -> Phase -> Deliverable -> Work Package (WP), có mã định danh nhất quán.
- Gắn mỗi milestone với một tín hiệu định lượng (QS-XX hoặc CPI/SPI) và ngưỡng, thay vì "xong là xong".
- Ánh xạ từng feature trong SRS sang các WP thiết kế / phát triển / kiểm thử, phát hiện feature "lạc" không có chỗ.
- Tự kiểm WBS bằng bộ quy tắc validate trước khi trình duyệt.

## Khi nào dùng (thời điểm, ai kích hoạt, điều kiện đầu vào)
- Thời điểm: giai đoạn khởi tạo/lập kế hoạch, sau khi có charter và/hoặc SRS; trước khi lập lịch (schedule) và tách task chi tiết.
- Người kích hoạt: PM.
- Cần ít nhất một trong ba nguồn: (1) SRS (ưu tiên): mô tả tổng quan + danh sách feature dạng `F-<PROJ>-<MOD>-NN`; (2) charter: scope (trong/ngoài) và các milestone mức cao; (3) PM tự liệt kê feature/deliverable. Cả ba đều thiếu thì dừng, không đoán.
- Dữ liệu bắt buộc: danh sách feature; loại hợp đồng (contract type) từ charter; tầm nhìn/vision (charter §1 hoặc phần giới thiệu SRS).
- Tùy chọn: ghi đè ngưỡng tín hiệu (mặc định dùng ngưỡng chuẩn bên dưới); bỏ bớt phase (mặc định đủ 7 phase).

## Khái niệm cốt lõi (định nghĩa, thuật ngữ, vì sao quan trọng)
| Khái niệm | Định nghĩa |
|---|---|
| Project | Đơn vị quản lý cao nhất (mã dự án, sponsor, go-live) |
| Phase | Pha vòng đời (7 phase chuẩn hoặc tập con) |
| Deliverable | Tài liệu/sản phẩm đo được ở cuối phase (SRS Approved, UAT Report...) |
| Work Package (WP) | Nhóm công việc cùng một deliverable; owner là một vai trò; ID `WP-<STAGE>-NN` |
| Milestone | Điểm kiểm tra có tín hiệu neo; tối thiểu 1 milestone mỗi phase |
| Signal anchor | Tín hiệu định lượng (QS-XX, hoặc CPI/SPI nếu PM chọn) gắn vào milestone để biết "đạt chưa" |

- Quy tắc nguồn: "tín hiệu phải gắn với kế hoạch" - milestone không có tiêu chí đo thì không kiểm soát được chất lượng.
- WBS chỉ tạo "ô chứa" (slot) WP; **không** sinh task chi tiết REQ/BD/DEV (việc của bước tách task) và **không** đặt lịch (việc của bước schedule).
- Feature ID chuẩn: `F-<PROJ>-<MOD>-NN`.

## Cách làm từng bước (thủ công, đủ chi tiết để làm theo; kèm input/output)
1. **Xác định chế độ nguồn.** Có SRS với danh sách feature -> dựa SRS. Không có nhưng có charter -> dựa charter. Không có cả hai -> hỏi PM scope. In tóm tắt (chế độ, số feature/deliverable, phase có thể bỏ) để PM xác nhận.
2. **Trích metadata.** Mã dự án, tên, go-live (từ phần giới thiệu SRS hoặc metadata charter); danh sách feature/deliverable (danh sách feature SRS hoặc scope charter); ngưỡng NFR (phần thuộc tính chất lượng SRS, nếu có); loại hợp đồng (metadata charter). Thiếu trường bắt buộc thì chặn, không làm tiếp.
3. **Hỏi PM những điểm cần chọn** (chỉ hỏi cái thực sự thiếu): loại hợp đồng nếu charter thiếu (bắt buộc); phase muốn bỏ (mặc định đủ 7); ghi đè ngưỡng (ví dụ dự án Internal R&D); dùng CPI/SPI thay QS-XX cho từng milestone (mặc định QS-XX). Cho PM xem bảng ngưỡng mặc định và hỏi có sửa không. Nếu bỏ phase (ví dụ không UAT chính thức) thì milestone test gộp vào M5a (System Test) hoặc PM chỉ định.
4. **Dựng WBS** theo trình tự: (a) 7 phase chuẩn (hoặc tập con); (b) mỗi phase 1-3 deliverable; (c) mỗi deliverable 1-N WP dạng `WP-<STAGE>-NN`; (d) ánh xạ feature -> WP (xem quy tắc dưới); (e) gắn milestone cuối phase + tín hiệu. Heuristic: phase dài hơn 4 tuần có thể thêm milestone giữa phase (PM xác nhận); feature chỉ backend thì cột Design WP là `—` và đánh dấu cảnh báo ở bảng coverage.
5. **Validate** (bảng dưới). Nếu có cảnh báo thì hỏi PM cách xử lý trước khi chốt.
6. **Chốt bản DRAFT v1** chờ PM duyệt; tóm tắt số phase, WP, feature đã phủ, mục còn mở.

Quy tắc ánh xạ feature -> WP:
- Mỗi `F-<PROJ>-<MOD>-NN` -> ít nhất 1 `WP-DEV-NN` (Development) + ít nhất 1 `WP-TST-02-NN` (testcase).
- Có UI/UX -> `WP-DSG-02-NN` (Design). API mới -> `WP-DSG-04-NN`. Thay đổi schema -> `WP-DSG-03-NN`.
- Feature không map được với thiết kế (chỉ backend) -> đánh dấu cảnh báo trong bảng Feature -> WP Coverage.

## Công thức, ngưỡng & tín hiệu
Bảng neo tín hiệu mặc định (PM xác nhận trước khi gắn):

| Phase | Milestone | Tín hiệu | Ngưỡng | Ghi chú |
|---|---|---|---|---|
| Initiation | Charter Approved | — | — | Không có tín hiệu định lượng |
| Requirements | SRS Approved | QS-REQ-01 | >= 95% | tỉ lệ pass khi review yêu cầu |
| Requirements | SRS Approved | QS-REQ-03 | 100% | truy vết UC <-> feature <-> test |
| Design | Basic Design Approved | QS-DSG-03 | <= 5% | tỉ lệ lỗi thiết kế |
| Development | Code Complete | QS-DEV-cov | >= 80% | độ phủ unit test |
| Development | Code Complete | QS-PRC-07 | >= 90% | tuân thủ quy trình theo tuần |
| Testing | System Test Done | QS-TST-02 | <= baseline của dự án | mật độ lỗi |
| Testing | UAT Sign-off | QS-TST-08 | <= 5% | tỉ lệ reopen |
| Testing | UAT Sign-off | QS-TST-04 | <= 2% | tỉ lệ lọt lỗi (leak) |
| Release | Go-live | QS-PRC-07 | >= 90% | tuân thủ quy trình release |
| Closure | Project Closed | — | — | retrospective định tính |

Tín hiệu lặp hằng tuần (phase Dev/Test): **E3 (effort variance) <= 10%**.

Quy tắc validate:
| Kiểm tra | Nếu fail |
|---|---|
| Mỗi phase có >= 1 milestone | Cảnh báo |
| Milestone phase 2-6 có tín hiệu neo | Cảnh báo |
| Feature SRS đã map vào WP | Liệt kê feature lạc / cảnh báo backend-only |
| Trường bắt buộc có ghi nguồn | Không được chốt nếu thiếu |

## Template / mẫu đầu ra (rút gọn, giữ cấu trúc và các cột/trường)
Bảng phase template (7 phase):

| # | Phase | Deliverable mặc định | WP mặc định |
|---|---|---|---|
| 1 | Initiation | Charter, WBS, Risk Seed | WP-INIT-01 Charter, WP-INIT-02 Stakeholder map |
| 2 | Requirements | SRS final, Traceability matrix | WP-REQ-01 UC detail, WP-REQ-02 NFR confirm, WP-REQ-03 Trace matrix |
| 3 | Design | Basic Design, DB Design, API Detail | WP-DSG-01 Architecture, WP-DSG-02 Screen, WP-DSG-03 DB, WP-DSG-04 API |
| 4 | Development | Source code, Unit test report | WP-DEV-NN theo feature, WP-DEV-INT integration |
| 5 | Testing | Test plan, Testcase, ST report, UAT report | WP-TST-01..04 |
| 6 | Release | Deploy plan, Release note, Go-live | WP-REL-01..03 |
| 7 | Closure | Lessons learned, Handover | WP-CLO-01 Retro, WP-CLO-02 Handover |

Khung tài liệu WBS:
```
# WBS — <Tên dự án> (<MÃ>) (DRAFT)
| Project Code | Generated | Source (SRS/charter) | Contract Type | Phases (7 full) | Status DRAFT v1 |
## 1. Phase & Milestone Summary   (Phase | Milestone | Signal Anchor | Threshold) + dòng Weekly anchor: E3 <= 10%
## 2. Work Breakdown   (mỗi phase: Deliverables, Milestone; bảng WP ID | Title | Owner role | Maps to [feature])
## 3. Feature -> WP Coverage   (Feature | Design WP | Dev WP | Test WP | Status: Covered / thiếu Design - backend-only?)
## 4. Validation   (các mục pass/cảnh báo)
## Checklist sau khi lập: giả định cần PM kiểm | TBD | PM đã xác nhận
```
Quy ước ID WP: `WP-<STAGE>-NN` (hậu tố `-NN` theo feature nếu cần); có thể thêm mã dự án `WP-KM-DEV-NN` nếu nhiều dự án chung một kho - khi đó ghi rõ là PM yêu cầu.

## Lỗi thường gặp & lesson learned (lấy từ nguồn, mỗi ý: sai gì -> hậu quả -> cách tránh)
- Lập WBS khi thiếu cả SRS, charter, danh sách feature -> đoán scope, WBS sai gốc -> dừng, hỏi PM scope.
- Milestone không gắn tín hiệu -> không biết đạt hay chưa -> mọi milestone phase 2-6 phải có tín hiệu (hoặc CPI/SPI).
- Nhét task chi tiết vào WBS -> WBS phình, lẫn với task list -> chỉ tạo slot WP.
- Feature backend-only bị bỏ ngỏ cột Design -> bị hiểu là thiếu thiết kế -> ghi `—` và cảnh báo để PM xác nhận.
- Tự đổi ngưỡng mặc định mà không hỏi -> lệch chuẩn -> luôn cho PM xem và xác nhận bảng ngưỡng.
- Bỏ phase mà quên chỉ rõ milestone test gộp vào đâu -> mất neo tín hiệu -> gộp vào M5a (System Test) hoặc PM chỉ định.
- Có change request thay đổi phạm vi -> WBS lỗi thời -> chạy lại WBS để cập nhật độ phủ WP.
- (nguồn chưa rõ: "M5a (System Test)" - đánh số milestone M1..M5a không được định nghĩa đầy đủ; skeleton chỉ liệt kê M1, M2, M4.)
- (nguồn chưa rõ: E3 ghi là "Phase 3-6" trong skeleton nhưng "phase Dev/Test" trong bảng - Dev/Test tương ứng phase 4-5 theo phase template.)
- (nguồn chưa rõ: QS-DEV-cov là ký hiệu đặc biệt không theo dạng QS-XXX-NN.)
- (nguồn chưa rõ: WP test được ghi `WP-TST-01..04` ở phase template nhưng `WP-TST-02-NN` cho testcase ở phần mapping.)
- Phase Release (phase 6) có milestone Go-live neo QS-PRC-07; Closure (phase 7) và Initiation không có tín hiệu định lượng - khớp với quy tắc "phase 2-6".

## Ví dụ minh họa (1 ví dụ ngắn có số, lấy hoặc dựng từ nguồn; nếu dựng thì ghi "(ví dụ dựng)")
Từ mẫu của nguồn: dự án mã `KM-2026-001`, hợp đồng Fixed-bid, 7 phase. Milestone `M2 SRS Approved` neo `QS-REQ-01 >= 95%` và `QS-REQ-03 = 100%`; `M4 Code Complete` neo `QS-DEV-cov >= 80%` và `QS-PRC-07 >= 90%`. Coverage: `F-KM-REL-01` có Design WP `WP-DSG-02-01`, Dev WP `WP-DEV-01`, Test WP `WP-TST-02-01` -> Covered; `F-KM-API-03` không có Design WP, Dev `WP-DEV-03`, Test `WP-TST-02-03` -> cảnh báo "Thiếu Design - backend-only?" để PM xác nhận.

## Tự kiểm tra (3-5 câu hỏi có đáp án ngắn ngay dưới, dựa trên chính nội dung bài)
1. Ngưỡng tín hiệu mặc định cho milestone SRS Approved là gì?
   - QS-REQ-01 >= 95% và QS-REQ-03 = 100%.
2. Tín hiệu lặp hằng tuần trong phase Dev/Test và ngưỡng?
   - E3 (effort variance) <= 10%.
3. Feature chỉ backend xử lý thế nào trong bảng coverage?
   - Design WP ghi `—`, đánh dấu cảnh báo để PM xác nhận backend-only.
4. Mỗi phase cần tối thiểu gì, và milestone phase nào bắt buộc có tín hiệu?
   - Tối thiểu 1 milestone/phase; milestone phase 2-6 phải có tín hiệu neo.
5. Mỗi feature `F-<PROJ>-<MOD>-NN` cần ít nhất những WP nào?
   - >= 1 `WP-DEV-NN` và >= 1 `WP-TST-02-NN`; thêm WP Design nếu có UI/UX, API mới hoặc thay đổi schema.

## Liên quan (bài trước/sau trong quy trình, tên thư mục skill khác)
- Trước: charter/kickoff; Chốt spec (Ch2·03) (spec đã duyệt).
- Sau: Spec thành task (Ch3·02) (đổ task vào WP-DEV-NN, WP-TST-02-NN), Lập schedule (Ch3·03) (lịch từ milestone + tín hiệu), Xếp người (Ch3·05) (đưa người vào vai trò owner WP).
- Về sau: theo dõi tín hiệu (Tín hiệu, Ch6·01) và change request (chạy lại WBS).
