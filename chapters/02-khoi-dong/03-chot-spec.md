---
title: Sign-off spec - quản lý vòng review và theo dõi comment
source: Chốt spec (Ch2·03)
stage: Requirements
level: cơ bản
prerequisites: []
---
# Sign-off spec - quản lý vòng review và theo dõi comment

## Mục tiêu học xong bạn làm được gì
- Biến một đống comment rời rạc (biên bản họp, email, lời nói) thành danh sách "open item" chuẩn hóa, có mã, có người nêu, có mục spec liên quan.
- Phân loại từng item thành 4 nhóm Must-fix / Nice-to-have / Approved-as-is / Deferred và biết nhóm nào chặn sign-off.
- Kết luận spec đã `READY` hay còn `NOT READY` theo một ngưỡng duy nhất, rõ ràng.
- Dựng và duy trì một "review tracker" qua nhiều vòng review (R1, R2, ...).

## Khi nào dùng (thời điểm, ai kích hoạt, điều kiện đầu vào)
- Thời điểm: sau mỗi buổi/lượt review tài liệu spec (SRS hoặc basic design) với BA, khách hàng hoặc nội bộ, trước khi cho phép chuyển sang bước tách task.
- Người kích hoạt: PM (hoặc BA thay mặt PM).
- Đầu vào bắt buộc (thiếu một trong bốn thì dừng, yêu cầu bổ sung trước):
  1. Ít nhất 1 file spec cần review (một mục SRS hoặc basic design).
  2. Mã feature/module, ví dụ `F-PROJ-01` hoặc `MOD-AUTH` (định dạng `F-<PROJ>-NN` hoặc một slug).
  3. Danh sách reviewer kèm vai trò, ví dụ "Minh (BA), John (Client)" - tối thiểu 1 người.
  4. Comment thô (biên bản họp / email / PM tự gõ lại).
- Bối cảnh: đây là bước "khóa" spec, nên là điều kiện tiên quyết để sinh task (xem bài Spec thành task, Ch3·02).

## Khái niệm cốt lõi (định nghĩa, thuật ngữ, vì sao quan trọng)
- **Sign-off**: xác nhận chính thức rằng spec đủ tốt để làm tiếp. Trong quy trình này sign-off không phải cảm tính mà là kết quả của một ngưỡng đếm được.
- **Open item**: một ý kiến/câu hỏi/phản hồi cần được xử lý hoặc ghi nhận. Mỗi item có ID `RC-<feature-code>-<NNN>` (ví dụ `RC-F-AUTH-001`).
- **Review round**: vòng review, ký hiệu `R1`, `R2`... (số nguyên, bắt đầu từ 1).
- **4 nhóm item**:

| Nhóm | Mã | Định nghĩa | Tác động sign-off |
|---|---|---|---|
| Must-fix | M | Lỗi sai / thiếu thông tin bắt buộc / vi phạm business rule. Phải sửa trước khi sign-off | Chặn (block) |
| Nice-to-have | N | Cải thiện chất lượng tài liệu / UX / độ rõ ràng. Không ảnh hưởng logic. PM tự quyết có làm không | Không chặn |
| Approved-as-is | A | Reviewer xác nhận nội dung đúng, không cần đổi | Không chặn |
| Deferred | D | Ngoài scope hiện tại; đưa vào change request (CR) hoặc phase sau. Cần theo dõi riêng qua quy trình change request | Không chặn (nhưng cần CR nếu có tác động) |

- Vì sao quan trọng: tách bạch "phải sửa" với "nên sửa" giúp tránh cãi vô tận về việc khi nào spec xong; item Deferred được ghi lại thay vì mất dấu, tránh scope creep ngầm.

## Cách làm từng bước (thủ công, đủ chi tiết để làm theo; kèm input/output)
1. **Kiểm tra đầu vào.** Liệt kê file spec được review (tên file + số section nếu có), xác nhận mã feature hợp lệ, đếm reviewer. Xác nhận lại với các bên trước khi làm tiếp.
2. **Ghi metadata vòng review** (bắt buộc): mã feature/module, số vòng (`R1`, `R2`...), ngày review (`YYYY-MM-DD`), danh sách reviewer (tên + vai trò, ngăn cách bằng dấu phẩy).
   Tùy chọn (bỏ qua thì dùng mặc định): loại nguồn comment (mặc định `meeting-notes`), tên phiên review (mặc định `Spec Review R<N> — <feature-code>`), phiên bản spec được review (mặc định chưa biết - TBD).
   Loại nguồn comment gồm: `meeting-notes` (biên bản họp), `email` (chuỗi email từ khách hàng hoặc nội bộ), `direct-input` (PM nhập thẳng).
3. **Tách comment thành item.** Mỗi item phải đủ 4 trường:
   - `ID` tự sinh `RC-<feature-code>-<NNN>`;
   - `Description`: diễn đạt lại ngắn gọn, ngôn ngữ trung lập;
   - `Raised by`: tên reviewer (lấy từ danh sách ở bước 2);
   - `Section ref`: mục spec liên quan (ví dụ `§3.2`, `UC-LOGIN`, `ERD users`).
   Quy tắc tách: mỗi câu hỏi/phản hồi riêng biệt là 1 item (không gom); câu lặp/paraphrase cùng ý thì gộp và ghi `(raised by: A, B)`; không rõ section thì ghi `§UNKNOWN` và hỏi lại ở bước phân loại; không rõ reviewer thì ghi `Unnamed` và đánh dấu.
   Sau khi tách, đưa bảng item cho mọi người xem và hỏi "có item nào bị bỏ sót không?".
4. **Phân loại từng item** (M / N / A / D). Dấu hiệu gợi ý trong câu chữ:

| Dấu hiệu trong comment | Gợi ý |
|---|---|
| "sai", "thiếu", "không đúng", "must", "required" | M |
| "nên", "có thể", "đề xuất", "nice to have" | N |
| "OK", "đồng ý", "approved", "confirmed" | A |
| "phase 2", "sau", "CR", "ngoài scope" | D |

   Item không rõ nhóm: nêu item + gợi ý + lý do, rồi hỏi người có thẩm quyền chọn. Không tự gán nhóm cho item mơ hồ khi chưa xác nhận. Nếu ý kiến của người review mâu thuẫn với gợi ý dấu hiệu, dừng lại hỏi.
5. **Lập tracker**: điền metadata, bảng Open Items, bảng Summary đếm theo nhóm (tổng / open / closed), và trạng thái sign-off. Gắn nhãn phiên bản `DRAFT v1` và số vòng.
6. **Kết luận & bàn giao.** Chạy checklist cuối (bên dưới). Nếu còn Must-fix open: sửa xong rồi làm vòng kế (round +1). Nếu Must-fix open = 0: spec sẵn sàng cho bước sinh task. Item Deferred có tác động thì mở change request.
- Vòng mới: tăng số vòng thêm 1, giữ nguyên ID item cũ, thêm item mới với ID tiếp theo (không đánh số lại).

## Công thức, ngưỡng & tín hiệu
| Tên | Công thức/điều kiện | Ngưỡng | Hành động khi vượt |
|---|---|---|---|
| Sign-off status | Đếm số item nhóm M có trạng thái Open | > 0 → `NOT READY`; = 0 → `READY` (kể cả khi chưa có item M nào) | NOT READY: sửa rồi chạy vòng tiếp (round +1). READY: chuyển sang bước sinh task |
| Item Deferred | Nhóm D | Không chặn sign-off | Mở CR nếu có tác động đến scope |

## Template / mẫu đầu ra (rút gọn, giữ cấu trúc và các cột/trường)
```
# Spec Review Tracker — <feature-code> (DRAFT v1)
| Field | Value |
| Feature / Module | <feature-code> |
| Review Round | R<N> |
| Review Date | YYYY-MM-DD |
| Reviewers | <name (role), ...> |
| Comment Source | <meeting-notes / email / direct-input> |
| Sign-off Status | NOT READY / READY |
| Generated | YYYY-MM-DD |

Chú giải nguồn comment: Meeting notes / Email / Direct PM input

## Open Items
| ID | Description | Section Ref | Raised By | Category | Status | Notes |
| RC-<code>-001 | <mô tả> | §X.Y | <reviewer> | M / N / A / D | Open / Closed | |

## Summary
| Category | Count | Open | Closed |
| Must-fix (M) / Nice-to-have (N) / Approved-as-is (A) / Deferred (D) / Total |
Sign-off Status: NOT READY — X Must-fix item(s) còn Open.

## Checklist sau khi lập: (1) mục do người lập tự giả định cần PM kiểm; (2) mục còn TBD chờ dữ liệu; (3) mục PM đã xác nhận
```
Ghi chú nguồn số liệu: mỗi trường nên đánh dấu nguồn (từ tài liệu / quy tắc nội bộ / PM xác nhận / giả định / TBD) để người duyệt biết chỗ nào cần kiểm.

Checklist cuối trước khi giao:
- Mọi trường bắt buộc đều có ghi nguồn.
- Mọi item đủ ID / Description / Section ref / Raised by / Category.
- Không còn item mơ hồ chưa được xác nhận nhóm.
- Trạng thái sign-off tính đúng ngưỡng (Must-fix open = 0 thì READY).
- Chú giải nguồn comment hiển thị đúng loại đầu vào.
- Tài liệu ở trạng thái DRAFT v1.

## Lỗi thường gặp & lesson learned (lấy từ nguồn, mỗi ý: sai gì -> hậu quả -> cách tránh)
- Gộp nhiều ý kiến vào một item -> không đếm/đóng được từng ý, tracker sai -> mỗi câu hỏi/phản hồi riêng là 1 item.
- Không gộp các ý lặp -> item trùng làm phình số lượng -> gộp, ghi `(raised by: A, B)`.
- Tự đoán nhóm cho item mơ hồ -> có thể bỏ sót Must-fix nên trạng thái READY sai -> hỏi người có thẩm quyền, không tự gán.
- Bỏ trống Section ref hoặc Raised by -> không truy vết được -> dùng `§UNKNOWN`/`Unnamed`, đánh dấu và xử lý ở bước phân loại.
- Đánh số lại ID ở vòng mới -> mất liên kết với comment cũ -> giữ ID cũ, thêm ID mới nối tiếp.
- Tự sửa spec hoặc tự tạo task trong lúc review -> nhầm vai trò; tracker chỉ theo dõi, việc sửa spec và sinh task là bước khác.
- Bỏ qua item Deferred -> scope creep ngầm -> ghi lại và mở CR nếu có tác động.

## Ví dụ minh họa (1 ví dụ ngắn có số, lấy hoặc dựng từ nguồn; nếu dựng thì ghi "(ví dụ dựng)")
(ví dụ dựng) Feature `F-AUTH`, R1, reviewer: <BA-1> (BA), <Client-1> (Client). Sau họp có 6 item: 2 M (đều Open), 2 N, 1 A, 1 D. Summary: Total 6, M open = 2 → `NOT READY — 2 Must-fix item(s) còn Open`. Sau khi sửa spec, R2: giữ 6 ID cũ, thêm `RC-F-AUTH-007`; hai item M chuyển Closed và không có M mới → M open = 0 → `READY`.

## Tự kiểm tra (3-5 câu hỏi có đáp án ngắn ngay dưới, dựa trên chính nội dung bài)
1. Điều kiện nào để trạng thái là `READY`?
   - Số item Must-fix còn Open = 0 (kể cả khi chưa có item M nào).
2. Item "Deferred" có chặn sign-off không? Cần làm gì thêm?
   - Không chặn; nhưng cần theo dõi riêng qua change request nếu có tác động.
3. Sang vòng review mới, ID item được xử lý thế nào?
   - Tăng số vòng lên 1, giữ nguyên ID cũ, item mới lấy ID tiếp theo.
4. Comment chứa "phase 2" hoặc "ngoài scope" gợi ý nhóm nào? Nếu comment mơ hồ thì sao?
   - Nhóm D; item mơ hồ thì hỏi người có thẩm quyền chọn, không tự gán.
5. Một item phải có đủ những trường nào?
   - ID, Description, Raised by, Section ref (rồi thêm Category, Status).

## Liên quan (bài trước/sau trong quy trình, tên thư mục skill khác)
- Trước: bước kickoff (nguồn chỉ nhắc "kickoff" là upstream: charter/SRS phải tồn tại trước).
- Sau: Spec thành task (Ch3·02) (sinh task từ spec đã duyệt, chạy lại sau sign-off); quy trình change request (khi item Deferred làm đổi scope).
- Song song: WBS (Ch3·01).
