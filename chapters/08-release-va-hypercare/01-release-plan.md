---
title: Lập kế hoạch release (Release Plan)
source: Release plan (Ch8·01)
stage: Release
level: trung bình
prerequisites: [Ch2·01, Ch3·03]
---
# Lập kế hoạch release (Release Plan)

## Mục tiêu học xong bạn làm được gì
- Lập một bản Release Plan hoàn chỉnh (7 mục) cho một đợt bàn giao lên production, ở trạng thái DRAFT chờ stakeholder ký.
- Chọn được bộ template release phù hợp (một release có thể áp nhiều template) và gộp checklist của chúng đúng quy tắc.
- Gắn tiêu chí cổng G1-G6 vào release, biết vì sao G5 (UAT) không được chặn khi mới lập kế hoạch.
- Định nghĩa được điều kiện rollback, người quyết định, RTO và khoảng hypercare mặc định.

## Khi nào dùng (thời điểm, ai kích hoạt, điều kiện đầu vào)
- Thời điểm: trước khi deploy, khi đã có charter, lịch dự án và danh sách feature đã hoàn thành (hoặc sắp hoàn thành). Thường lập trước UAT.
- Người kích hoạt: PM (ví dụ khi cần "lập release plan", "chọn template release", "release window", "release readiness").
- Đầu vào bắt buộc (thiếu là dừng, không đoán):
  - Danh sách feature và trạng thái (task list).
  - Mốc lịch (milestone), đặc biệt M5 UAT và M6 go-live.
  - Ngày go-live mục tiêu và loại hợp đồng (trong charter).
  - Danh mục template release (DB công ty; nếu chưa có thì dùng danh mục dự phòng bên dưới).
- Đầu vào tùy chọn: WBS (đối chiếu deliverable), kết quả gate G5 nếu đã có, sổ rủi ro/issue để chụp "readiness".
- Ngoài phạm vi bài này: chạy gate review, chạy checklist, thực thi deploy, theo dõi tín hiệu thời gian thực.

## Khái niệm cốt lõi (định nghĩa, thuật ngữ, vì sao quan trọng)
| Khái niệm | Định nghĩa |
|---|---|
| Release | Đợt bàn giao feature lên production. ID dạng `R-<PROJ>-NN`. |
| Template | Bộ quy trình + checklist + gate của công ty; mỗi template có mã. |
| Scope | Các feature `F-<PROJ>-NN` go-live trong release. |
| Gate criteria | Điều kiện G1-G6 (tín hiệu + checklist). Việc chấm gate làm ở bước gate review, không phải ở đây. |
| Window | Khung thời gian deploy (ngày + giờ; bị ràng buộc bởi khách hàng). |
| Rollback trigger | Điều kiện kích hoạt quay lui sau deploy. |
| Quan hệ N-N | 1 release áp nhiều template; checklist gộp = hợp (union), loại trùng theo ID item, ưu tiên Critical > Standard. |

Vì sao quan trọng: kế hoạch release chốt sẵn "thế nào là sẵn sàng" và "khi nào phải lùi" trước khi áp lực deploy ập tới. Nguyên tắc chính sách:
- Múi giờ window: PM đặt theo từng dự án; mặc định UTC+7 (Asia/Ho_Chi_Minh).
- Lập plan trước UAT: G5 không bắt buộc lúc plan; có kết quả thì chụp lại, thiếu thì ghi `[NO_DATA]`, không chặn, không bịa pass/fail.
- Nguồn template chuẩn (SSOT) là DB của công cụ quản lý; nếu chưa kết nối phải cảnh báo và dùng danh mục dự phòng, không tự chế mã template lạ.

## Cách làm từng bước (thủ công, đủ chi tiết để làm theo; kèm input/output)
1. Kiểm tra đầu vào. Thu thập: ngày go-live mục tiêu + loại hợp đồng (charter), các mốc M5/M6 và ràng buộc window (lịch), feature nào đã done/đang test (task list). Tóm tắt số feature done, các mốc, nguồn template (DB hay dự phòng) rồi xác nhận với chính mình/stakeholder trước khi đi tiếp. Thiếu file bắt buộc: dừng và quay lại tài liệu upstream (charter, lịch, danh sách task).
2. Chốt thông tin release.
   - Bắt buộc: Release ID (đề xuất `R-<PROJ>-NN` kế tiếp), loại release (Major / Minor / Patch / Hotfix), cửa sổ deploy mục tiêu (ngày + giờ).
   - Tùy chọn (có mặc định): template (gợi ý theo loại release, PM xác nhận), múi giờ (UTC+7), customer-facing (mặc định Yes nếu hợp đồng với khách), chi tiết giờ deploy (PM nhập).
   - Giả định mặc định: mốc tín hiệu G6 = QS-PRC-07 ≥ 90% và các checklist pass; hypercare Major 7 ngày / Minor 3 ngày / Patch 1 ngày / Hotfix 24h; RTO rollback 30 phút; thông báo nội bộ chỉ soạn bản markdown.
3. Kiểm tra hợp lý (validate).
   - Cửa sổ deploy lệch ngày go-live charter > 2 tuần: gắn cờ.
   - Feature trong scope chưa `done`: liệt kê cảnh báo, hỏi có hoãn sang release sau không.
   - Template chưa nạp từ DB: cảnh báo và dùng danh mục dự phòng.
   - Loại Hotfix nhưng lại chọn Major (không khớp): dừng, hỏi lại.
   - Scope PM chọn mâu thuẫn với trạng thái task list: dừng, hỏi, không tự dung hòa.
   - G5 chưa có: gắn cờ + `[NO_DATA]`, không chặn.
4. Tổng hợp nguồn.
   - Charter: loại hợp đồng gợi ý template, ngày go-live để kiểm window.
   - Lịch: M5 UAT, M6 go-live cho lịch gate.
   - Task list: lọc `done` (cộng phần PM xác nhận in-test/hoãn) thành mục Scope.
   - Chọn template: liệt kê template hợp loại release, PM chọn nhiều (multi-select) và xác nhận trước khi dựng gate; gộp theo quy tắc N-N.
   - Nếu chụp readiness có tín hiệu đỏ: hỏi PM có hoãn release trước khi viết plan.
5. Viết plan theo khung 7 mục (xem phần Template). Đầu trang có chú giải nguồn; mỗi mục lớn có dòng "Nguồn". Thiếu dữ liệu tín hiệu ghi `[NO_DATA]`, không bịa. Mục 7 "Open items" lấy từ các lỗ hổng (feature chưa done, tín hiệu vàng, rủi ro High).
6. Dừng và bàn giao: in tóm tắt (số feature trong scope, số template, số gate đang chờ, readiness đỏ/vàng), để trạng thái **DRAFT v1** chờ stakeholder ký, chạy checklist cuối, không tự commit.

Checklist sau khi viết:
- Mọi trường bắt buộc có nguồn.
- Danh sách template đã xác nhận với PM (không ngầm giả định).
- Scope khớp trạng thái done trong task list.
- Gate cover G1-G6 (G5 chỉ snapshot hoặc `[NO_DATA]`).
- Readiness có `[NO_DATA]` khi thiếu tín hiệu.
- Status = DRAFT v1.

## Công thức, ngưỡng & tín hiệu
| Tên | Công thức/điều kiện | Ngưỡng | Hành động khi vượt |
|---|---|---|---|
| Lệch window vs go-live | Ngày window so với `target_go_live` charter | > 2 tuần | Gắn cờ để PM xử lý |
| G1 Charter | Project-level, kickoff đã duyệt | Checklist G1-charter | Thường đã Passed; vẫn ghi trong plan (gate review có thể chạy lại) |
| G2 SRS Approved | QS-REQ-01; QS-REQ-03 | QS-REQ-01 ≥ 95%; QS-REQ-03 = 100% | Checklist G2-srs |
| G3 BD Approved | QS-DSG-03 | ≤ 5% | Checklist G3-bd |
| G4 Code Complete | QS-DEV-cov; QS-PRC-07 | QS-DEV-cov ≥ 80%; QS-PRC-07 ≥ 90% | Checklist G4-code |
| G5 UAT Sign-off | QS-TST-08; QS-TST-04 | QS-TST-08 ≤ 5%; QS-TST-04 ≤ 2% | Checklist G5-uat; lúc plan chỉ snapshot |
| G6 Go-live | QS-PRC-07 và mọi checklist | QS-PRC-07 ≥ 90%, all checklists pass | Checklist G6-golive |
| Rollback: bug nghiêm trọng | Critical bug | > 30% người dùng trong 4h sau deploy | Kích hoạt rollback |
| Rollback: hiệu năng | Suy giảm so với baseline | > 50% | Kích hoạt rollback |
| Rollback: khách hàng | Customer escalation | P1 | Kích hoạt rollback |
| Rollback: dữ liệu | DB migration làm hỏng dữ liệu | Có xảy ra | Kích hoạt rollback |
| RTO | Thời gian phục hồi mục tiêu | 30 phút | Ghi vào plan |
| Hypercare | Theo loại release | Major 7d / Minor 3d / Patch 1d / Hotfix 24h | Ghi vào plan |

Người quyết định rollback: PM (tham vấn Tech Lead + Sponsor).

Danh mục template dự phòng (không tự thêm mã ngoài danh sách):
| Mã | Tên | Loại | Khi áp dụng |
|---|---|---|---|
| TPL-STD-WEB | Standard Web Release | All | Deploy web chuẩn |
| TPL-STD-API | Standard API Release | All | Deploy API service |
| TPL-MIG-DB | DB Migration Release | Major/Minor | Đổi schema DB |
| TPL-HOTFIX | Hotfix Release | Hotfix | Bug critical trên prod |
| TPL-CUSTOMER-A | Customer A Compliance | Customer-specific | Yêu cầu riêng của khách |
| TPL-INT-3RD | Third-party Integration | Major | Tích hợp hệ thống ngoài |

## Template / mẫu đầu ra (rút gọn, giữ cấu trúc và các cột/trường)
```markdown
# Release Plan — R-<PROJ>-NN (<version>) — DRAFT
> Sources: charter + schedule + task-list + PM release meta + gate defaults
| Field | Value |
| Release ID | R-<PROJ>-NN |
| Project | <CODE> |
| Type | Major |
| Target Window | YYYY-MM-DD HH:MM → HH:MM (Asia/Ho_Chi_Minh) |
| Customer-facing | Yes |
| Status | DRAFT v1 |

## 1. Templates Applied (N-N)      | # | Template Code | Name | Lý do áp |
## 2. Scope — Features Released    | Feature ID | Title | Status | Module |
## 3. Gate Criteria                | Gate | Name | Date | Criteria | Status |
## 4. Pre-release Readiness (snapshot) | Item | Status | Note |
## 5. Deploy Schedule              | Step | Time | Owner | Action |
## 6. Rollback Plan  (Trigger conditions / Decision maker: PM / RTO target: 30 phút)
## 7. Open items (PM xử lý trước release)  - [ ] ...
```
Bản mẫu đầy đủ trong nguồn có 3 template áp N-N, 6 feature scope, bảng G1-G6, chuỗi deploy 8 bước, các điều kiện rollback.

## Lỗi thường gặp & lesson learned
- Chặn kế hoạch vì chưa có kết quả UAT -> không lập được plan đúng hạn -> G5 chỉ cần snapshot hoặc `[NO_DATA]`; đánh giá G5 thật để cho bước gate review/pre-exec.
- Ngầm giả định template -> checklist sai bộ -> luôn cho PM multi-select và xác nhận trước khi dựng gate.
- Gộp checklist bằng cách chọn một trong nhiều template -> sót item -> gộp theo hợp, loại trùng theo ID, Critical thắng Standard.
- Tự chế mã template khi DB chưa sẵn sàng -> không truy vết được -> cảnh báo rõ, chỉ dùng danh mục dự phòng.
- Đưa feature chưa done vào scope -> release hứa quá tay -> lọc `done`, hỏi hoãn phần còn lại.
- Bịa tín hiệu readiness -> quyết định sai -> thiếu thì `[NO_DATA]`.
- Tự dung hòa xung đột giữa scope PM chọn và task list -> sai lệch ngầm -> dừng và hỏi.
- Không nhập múi giờ -> nhầm giờ deploy -> mặc định UTC+7 nhưng ghi rõ trong Target Window.

## Ví dụ minh họa
(ví dụ dựng) Release Minor `R-<PROJ>-02`, đặt window 22:00 → 02:00 (Asia/Ho_Chi_Minh). Charter ghi go-live mục tiêu cách window 3 tuần -> vượt ngưỡng 2 tuần -> gắn cờ và hỏi PM. Có 1 trong 7 feature chưa done -> đưa vào mục 7 và hỏi hoãn. Có đổi schema DB -> chọn TPL-STD-WEB + TPL-MIG-DB; checklist gộp theo hợp. G5 chưa có -> ghi `[NO_DATA]`. Hypercare mặc định Minor = 3 ngày; RTO 30 phút; trạng thái DRAFT v1.

## Tự kiểm tra
1. Vì sao G5 không phải điều kiện bắt buộc khi lập release plan? -> Vì plan được lập trước UAT; có kết quả thì chụp, thiếu thì `[NO_DATA]`, không chặn và không bịa.
2. Cửa sổ deploy lệch bao nhiêu so với go-live charter thì phải gắn cờ? -> Hơn 2 tuần.
3. Điều kiện rollback mặc định gồm những gì? -> Critical bug > 30% người dùng trong 4h; hiệu năng suy giảm > 50% so với baseline; customer escalation P1; dữ liệu hỏng do DB migration.
4. Quy tắc gộp checklist khi một release áp nhiều template? -> Hợp (union), loại trùng theo ID item, ưu tiên Critical > Standard.
5. Hypercare mặc định theo loại release? -> Major 7d, Minor 3d, Patch 1d, Hotfix 24h.

## Liên quan
- Trước: kickoff (charter), Lập schedule (Ch3·03), Spec thành task (Ch3·02) (danh sách feature), wbs.
- Sau: Gate review (Ch8·02) (chấm G1-G6), Release exec (Ch8·03) (thực thi deploy theo mục 5 và 6), Hypercare (Ch8·04) (cửa sổ sau deploy), Status tuần (Ch7·01) (readiness trong báo cáo tuần).
- Ghi chú nguồn chưa rõ: (1) Nguồn còn liệt kê các câu hỏi mở chưa trả lời: ID release `R-<PROJ>-NN` hay semver; G1 có tự động pass khi kickoff duyệt; quy tắc gộp union/intersect/priority; Hotfix nên có quy trình riêng hay type=Hotfix bỏ G1-G3; RTO 30 phút có đủ thực tế. (2) Mục tiêu G6 ở đây ghi "all checklists pass", trong khi bài Gate review (Ch8·02) ghi G6 chỉ cần QS-PRC-07 ≥ 90% cùng checklist Pre-deploy và Rollback ready.
