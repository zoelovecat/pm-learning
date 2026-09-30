---
title: Đánh giá cổng (Gate Review G1-G6)
source: Gate review (Ch8·02)
stage: Cross-cutting
level: trung bình
prerequisites: [Ch4·04, Ch6·01, Ch6·02, Ch8·01]
---
# Đánh giá cổng (Gate Review G1-G6)

## Mục tiêu học xong bạn làm được gì
- Chấm một cổng (G1-G6) bằng ba nguồn: tín hiệu (QS-XX so với ngưỡng), kết quả checklist và số rủi ro High/Critical đang mở.
- Áp ma trận quyết định để đề xuất GO / GO có rủi ro / HOLD / ABORT.
- Viết tài liệu gate review với điều kiện HOLD, ngày review lại, danh sách tiêu chí trượt khi ABORT.
- Hiểu vì sao PM chỉ "đề xuất", còn stakeholder mới là người ký.

## Khi nào dùng (thời điểm, ai kích hoạt, điều kiện đầu vào)
- Thời điểm: tại mỗi mốc (milestone) có cổng G1-G6, hoặc khi cần "go/no-go", "qualify release".
- Người kích hoạt: PM.
- Đầu vào bắt buộc (thiếu thì dừng, không bịa):
  - Mốc và tín hiệu neo (anchor) cho cổng (từ lịch/WBS).
  - Ảnh chụp tín hiệu hiện tại có ghi ngày.
  - Kết quả checklist của đúng cổng đó.
  - Sổ rủi ro (đếm High/Critical còn mở).
  - Ma trận người duyệt (RACI) từ charter.
- Không làm: tự chạy checklist/đo tín hiệu tại chỗ, sửa ngưỡng, tự ký, cập nhật trạng thái mốc trong lịch.

## Khái niệm cốt lõi (định nghĩa, thuật ngữ, vì sao quan trọng)
- Cổng (gate): điểm kiểm soát chất lượng tại milestone; kết quả là quyết định đi tiếp hay không.
- Ba quyết định: GO (đi tiếp), HOLD (duyệt có điều kiện, phải review lại), ABORT (dừng, tìm nguyên nhân gốc và lập lại kế hoạch).
- Trạng thái tín hiệu: ✅ đạt, 🟡 vàng (lệch nhẹ), 🔴 đỏ.
- Chính sách:
  - Người duyệt: mặc định theo RACI trong charter, có thể ghi đè.
  - Hết hạn HOLD: 5 ngày làm việc thì phải leo thang (escalate).
  - Nhật ký kiểm toán chỉ ghi thêm (append-only) và nguyên tắc "nhiều mắt" (multi-eyes): chỉ cảnh báo mềm, PM được ghi đè kèm lý do.
  - Ngưỡng tín hiệu điều chỉnh theo loại hợp đồng (ma trận còn ở dạng DRAFT trong tài liệu quy tắc giám sát tín hiệu).
- Chỉ đề xuất quyết định: người ký là các bên có thẩm quyền (bảng bên dưới).

## Cách làm từng bước (thủ công, đủ chi tiết để làm theo; kèm input/output)
1. Chuẩn bị đầu vào: tìm mốc cổng trong lịch (ngày, tín hiệu neo), tiêu chí cổng trong WBS, vai trò duyệt trong charter, đường dẫn ảnh chụp tín hiệu và kết quả checklist của cổng đó. Thiếu thì quay lại chạy bước upstream tương ứng (đo tín hiệu, chạy checklist, cập nhật rủi ro), không tự suy ra số.
2. Chốt thông tin: Gate ID (G1-G6), ngày review (mặc định hôm nay), ngày ảnh chụp tín hiệu, file kết quả checklist. Tùy chọn: ghi đè ma trận người duyệt, lý do multi-eyes, ngày review lại nếu dự kiến HOLD (mặc định +5 ngày làm việc).
3. Kiểm tra hợp lý:
   - Gate ID hợp lệ và khớp mốc trong lịch/WBS?
   - Ảnh chụp tín hiệu có ngày và đủ tín hiệu neo của cổng?
   - File checklist đúng cổng (ví dụ G4 dùng checklist G4)?
   - Có điều chỉnh ngưỡng theo loại hợp đồng trong charter chưa?
   - Chạy lại cùng cổng: xác nhận đường dẫn output (giữ mọi lần chạy).
   - Không khớp giữa cổng và kế hoạch: dừng, hỏi, không tự dung hòa. In tóm tắt tiêu chí (tín hiệu, checklist, người duyệt) và xác nhận.
4. Tổng hợp:
   - Tín hiệu: lọc tín hiệu neo của cổng, so sánh thực tế với mục tiêu, gán ✅ / 🟡 / 🔴. Chưa có ảnh chụp: chạy đo tín hiệu trước; chỉ dùng số cũ nếu PM xác nhận.
   - Checklist: cộng Pass / Fail / N-A và số lỗi Critical. Chưa có: chạy checklist trước.
   - Rủi ro: lọc mức High/Critical, trạng thái Open, đếm.
   - Tra ma trận quyết định (bên dưới) ra đề xuất.
5. Viết tài liệu theo khung bên dưới. Phần phê duyệt của stakeholder để trống (⬜). Trạng thái: DRAFT (đề xuất: ...).
   - GO: mọi tiêu chí đạt; ghi gợi ý cổng kế tiếp.
   - HOLD: nêu tiêu chí trượt, điều kiện để được duyệt có điều kiện, ngày review lại (mặc định +5 ngày làm việc).
   - ABORT: liệt kê đủ mọi tiêu chí trượt, kích hoạt lập lại kế hoạch (qua change request) và quyết định của Sponsor.
6. Bàn giao: tóm tắt đề xuất, số tiêu chí trượt, ngày review lại nếu HOLD. Với ABORT, cảnh báo rõ và hỏi có chạy lại với dữ liệu mới hơn không. Không cập nhật mốc trong lịch, không tự ký.

## Công thức, ngưỡng & tín hiệu
Ma trận cổng:
| Gate | Tên | Tín hiệu bắt buộc | Checklist bắt buộc | Người quyết định |
|---|---|---|---|---|
| G1 | Charter Approved | — | Project init checklist | Sponsor + PM |
| G2 | SRS Approved | QS-REQ-01 ≥ 95%, QS-REQ-03 = 100% | Requirements review checklist | BA Lead + Customer PIC |
| G3 | Basic Design Approved | QS-DSG-03 ≤ 5% | Design review checklist | Tech Lead + Customer PIC |
| G4 | Code Complete | QS-DEV-cov ≥ 80%, QS-PRC-07 ≥ 90% | Code review + UT checklist | Tech Lead + QA Lead |
| G5 | UAT Sign-off | QS-TST-08 ≤ 5%, QS-TST-04 ≤ 2% | UAT checklist | QA Lead + Customer PIC |
| G6 | Go-live | QS-PRC-07 ≥ 90% | Pre-deploy + Rollback ready | PM + Sponsor + DevOps |

Ngưỡng thực tế có thể điều chỉnh theo `contract_type`.

Ma trận quyết định:
| Tín hiệu | Checklist | Rủi ro High/Crit đang mở | Quyết định | Hành động |
|---|---|---|---|---|
| Tất cả đạt | Tất cả đạt | 0 | 🟢 GO | Ký và sang giai đoạn tiếp |
| Tất cả đạt | Tất cả đạt | 1-2 | 🟢 GO with risks | Ký + kế hoạch giảm thiểu |
| 1 tín hiệu 🟡 (lệch 5-10%) | Pass | ≤ 2 | 🟡 HOLD | Duyệt có điều kiện, đặt ngày review lại |
| ≥ 1 tín hiệu 🔴 | Bất kỳ | Bất kỳ | 🔴 ABORT | Không đi tiếp, tìm nguyên nhân gốc, lập lại kế hoạch |
| Bất kỳ | ≥ 1 checklist fail mức Critical | Bất kỳ | 🔴 ABORT | Sửa checklist trước |
| Pass | Pass kèm ⚠ nhỏ | ≥ 3 High | 🟡 HOLD | Giảm thiểu trước |

Chính sách HOLD: review lại mặc định +5 ngày làm việc; quá hạn mà chưa đóng thì leo thang (PM báo Sponsor); đầu ra phải nhắc PM đặt ngày review lại.

## Template / mẫu đầu ra (rút gọn, giữ cấu trúc và các cột/trường)
```markdown
# Gate Review — G<n> <tên> — DRAFT
| Field | Value |  (Gate, Project, Release, Review Date, PM, Status = DRAFT (proposed: HOLD/GO/ABORT))
## 1. Criteria Check
### Signals   | Signal | Actual | Target | Status |
### Checklists | Checklist | Items | Pass | Fail | N/A | Status |   + dòng "Failing item"
### Risk Status | ID | Title | Level | Status |   + "Open High/Critical: n"
## 2. Proposed Decision   (lý do; điều kiện trong 5 ngày làm việc; Re-review date)
## 3. Stakeholder Approval | Role | Name | Decision (⬜ Approve / Reject) | Sign Date | Note |
## 4. Action items  (- [ ] ...)
```
Biến thể GO: "All criteria met" + mục "Next phase" (kích hoạt gate kế tiếp). Biến thể ABORT: liệt kê Failing criteria, "Root cause investigation required", kích hoạt re-plan (change request để đặt lại baseline; Sponsor quyết định tiếp tục/tạm dừng/hủy).

Checklist sau khi viết: Gate ID khớp mốc; tín hiệu từ ảnh chụp có ngày; checklist là kết quả có sẵn (không chạy lại tại chỗ); quyết định khớp ma trận; HOLD có ngày review lại + điều kiện; ABORT liệt kê hết tiêu chí trượt; bảng phê duyệt để trống (⬜); trạng thái DRAFT.

## Lỗi thường gặp & lesson learned
- Tự chạy checklist/đo tín hiệu ngay lúc review -> số liệu không có nguồn, khó kiểm chứng -> dùng kết quả đã ghi ngày từ bước đo và bước chạy checklist.
- Dùng số tín hiệu cũ mà không nói -> quyết định trên dữ liệu lỗi thời -> phải có ngày ảnh chụp, PM xác nhận nếu dùng cũ.
- Tự ký / điền sẵn phê duyệt -> phá vai trò kiểm soát -> để trống ⬜.
- HOLD không có ngày review lại và điều kiện -> HOLD kéo dài vô hạn -> luôn đặt +5 ngày làm việc và liệt kê điều kiện, quá hạn thì leo thang.
- ABORT chỉ nêu một lý do -> mất manh mối nguyên nhân -> liệt kê đủ mọi tiêu chí trượt.
- Lệch cổng với kế hoạch mà tự dung hòa -> sai lệch ngầm -> dừng và hỏi.
- Bỏ qua ngưỡng theo hợp đồng -> chấm sai -> đối chiếu `contract_type` trong charter.

## Ví dụ minh họa
Ví dụ từ nguồn (biến thể HOLD, cổng G4): QS-DEV-cov 76% so với ≥ 80% (thiếu 4%) -> 🟡; QS-PRC-07 92% so với ≥ 90% -> ✅. Checklist code review: 12 mục, 11 pass, 0 fail, 1 N/A -> Pass; checklist unit test: 8 mục, 7 pass, 1 fail (UT-CHK-04: coverage module Release ≥ 80% nhưng thực tế 72%) -> 🟡. Rủi ro High đang mở: 1 (R-007). Đề xuất: 🟡 HOLD, điều kiện trong 5 ngày làm việc: QS-DEV-cov ≥ 80%; UT-CHK-04 pass; R-007 cập nhật bằng chứng giảm thiểu. Re-review 2026-09-02 (review ngày 2026-08-26). Action: thêm 8% unit test coverage cho module Release, PM theo dõi hằng ngày, chạy lại gate review G4 vào 2026-09-02. (Nguồn chưa rõ: "8%" thêm coverage không suy ra chính xác từ 72% và 80%, ghi nguyên như nguồn.)

## Tự kiểm tra
1. Cổng G2 cần những ngưỡng tín hiệu nào? -> QS-REQ-01 ≥ 95% và QS-REQ-03 = 100%.
2. Một tín hiệu 🟡 (lệch 5-10%), checklist pass, 2 rủi ro High mở: quyết định gì? -> 🟡 HOLD (điều kiện: ≤ 2 rủi ro).
3. Chỉ cần 1 checklist fail mức Critical thì kết quả là gì? -> 🔴 ABORT, sửa checklist trước.
4. HOLD quá hạn thì xử lý ra sao? -> Mặc định review lại +5 ngày làm việc; quá hạn chưa đóng thì PM báo Sponsor (leo thang).
5. Ai ký quyết định G6? -> PM + Sponsor + DevOps.

## Liên quan
- Trước: Tín hiệu (Ch6·01) (tín hiệu), Checklist (Ch6·02) (checklist), Rủi ro & issue (Ch4·04) (rủi ro), wbs/Lập schedule (Ch3·03) (tiêu chí và mốc), Release plan (Ch8·01) (bối cảnh G4-G6).
- Sau: Change request (Ch4·03) (khi ABORT -> lập lại baseline), Status tuần (Ch7·01) (báo cáo trạng thái cổng), Release exec (Ch8·03) (G5/G6 là điều kiện tiên quyết trước khi deploy).
- Chỗ nguồn chưa rõ: (1) Ma trận quyết định không phủ mọi tổ hợp (ví dụ tín hiệu đạt hết + checklist đạt + ≥ 3 rủi ro High; hoặc 🟡 với > 2 rủi ro; hoặc checklist fail không Critical); (2) thiếu định nghĩa số chính xác cho "lệch 5-10%" (đo tương đối hay tuyệt đối); (3) các câu hỏi mở của nguồn: quá hạn HOLD có tự động thành ABORT không; ai ký từng cổng; ảnh chụp tín hiệu khóa tại thời điểm review hay dùng mới nhất; có cần chế độ nhiều cổng song song.
