---
title: Đóng dự án chính thức (Project Closeout)
source: Closeout (Ch9·02)
stage: Closure
level: trung bình
prerequisites: [Ch6·03, Ch8·04, Ch9·01]
---
# Đóng dự án chính thức (Project Closeout)

## Mục tiêu học xong bạn làm được gì
- Kiểm tra dự án đã đủ điều kiện đóng (điều kiện tiên quyết và điều kiện PM phải xác nhận).
- Lập tài liệu closeout gồm 9 mục + phần ký (mục 10): phạm vi, tiến độ, effort/chi phí, chất lượng, rủi ro, bàn giao, nghiệm thu khách hàng, giải phóng team, lưu trữ.
- Ánh xạ chỉ số chất lượng (gate, tín hiệu QS-XX, sự cố hypercare, NPS) giữa mục tiêu trong charter và số thực tế.
- Chuẩn bị bàn giao cho team support mà không lộ thông tin bí mật.
- Biết đâu là việc PM làm tay ngoài tài liệu (đóng dự án trên hệ thống, giải phóng nhân sự, lưu trữ thật, thanh toán).

## Khi nào dùng (thời điểm, ai kích hoạt, điều kiện đầu vào)
- PM kích hoạt ở cuối vòng đời: sau khi mọi release đã phát hành, hypercare đã đóng, retro dự án đã xong. Kết quả là bản NHÁP chờ 4 bên ký cuối.
- Đầu vào BẮT BUỘC (thiếu thì dừng, không bịa kế hoạch/thực tế):

| Hồ sơ | Ghi chú |
|---|---|
| Charter | Phạm vi gốc |
| Tiến độ | Trạng thái milestone cuối |
| Các release | Tất cả đã phát hành |
| Kết quả gate G1-G6 | Từ gate review |
| Hypercare | Tất cả đã đóng |
| Retro dự án | Từ Lessons learned (Ch9·01) |
| Effort | Ảnh chụp cuối (không đủ nếu chỉ có bản stub) |
| Sổ rủi ro | Bản cuối |

- PM phải XÁC NHẬN trước khi làm tiếp: (1) khách hàng đã chấp nhận bằng lời hoặc email; (2) không còn rủi ro mức Critical/High đang mở. Chưa xác nhận thì dừng.
- PM nhận bàn giao giữa chừng thiếu charter/tiến độ/rủi ro: dựng lại bản tối thiểu trước. Gate, hypercare, retro, effort vẫn phải có từ nguồn chính thức, bản dựng lại chỉ là proxy/từng phần.

## Khái niệm cốt lõi
- **Closeout doc**: hồ sơ đóng dự án gồm final report, tài liệu bàn giao cho team support, checklist lưu trữ, nghiệm thu của khách, kế hoạch giải phóng team.
- **Chấp nhận (acceptance)**: khách xác nhận bằng lời/email (điều kiện để bắt đầu), sau đó ký chính thức theo phương thức đã chốt.
- **Cổng chất lượng G1-G6**: 6 gate của dự án; mục tiêu là qua đủ 6/6.
- **Tín hiệu chất lượng QS-XX**: các chỉ số chất lượng theo dõi suốt dự án (xem bảng ánh xạ bên dưới).
- **Realized as issue**: rủi ro đã xảy ra thành issue thật.
- **Handover**: bàn giao cho team support gồm quyền truy cập, runbook, backlog còn tồn, thời gian đi kèm (shadow).
- **Không lộ bí mật**: danh sách quyền truy cập production chỉ ghi tham chiếu kho bí mật (vault), tuyệt đối không ghi mật khẩu/khóa vào tài liệu.
- **Manual tick**: checklist lưu trữ do PM tự đánh dấu khi đã làm thật.

## Cách làm từng bước (thủ công, đủ chi tiết để làm theo; input/output)
1. **Kiểm tra hồ sơ đầu vào.** Đối chiếu bảng hồ sơ bắt buộc. Trích: mã + tên dự án từ charter; ID release đã phát hành và ngày đóng hypercare; tóm tắt gate pass/hold G1-G6; nơi để retro và effort.
2. **Xác nhận với khách và với sổ rủi ro.** Chưa có chấp nhận của khách, hoặc còn Critical/High mở: dừng, hoặc PM chủ động hoãn (defer) kèm lý do ghi rõ.
3. **Chốt thông tin.** Bắt buộc: mã + tên dự án; ngày nghiệm thu cuối (YYYY-MM-DD); cách khách ký (email / tài liệu có chữ ký / DocuSign); team support tiếp nhận (tên team + PIC). Tùy chọn (nếu bỏ qua): định dạng ký của khách (mặc định email); phạm vi bàn giao support (PM tự định: quyền truy cập, runbook, giai đoạn shadow); vị trí lưu trữ (chưa xác định: Git tag + ổ lưu trữ của công ty); ngày kích hoạt hóa đơn cuối (sau nghiệm thu, làm tay).
4. **Đối chiếu tính nhất quán.** Mọi release đã phát hành/xong? Mọi hypercare đã đóng? Số rủi ro Critical/High mở bằng 0? Có retro dự án? Xác nhận chấp nhận khớp thông tin PM nhập? Có mâu thuẫn giữa hồ sơ và lời PM thì dừng và hỏi, không tự dung hòa. Thiếu effort/gate thực tế cho mục bắt buộc thì ghi `[NO_DATA]`, không bịa số.
5. **Tổng hợp số liệu.**
   - Phạm vi: tính năng kế hoạch vs đã giao (từ charter + release + CR). Tiến độ: kế hoạch vs thực tế theo milestone.
   - Effort/chi phí: kế hoạch vs thực tế, biên lợi nhuận (margin), lấy bản effort mới nhất.
   - Chất lượng: gate G1-G6 pass/hold; giá trị cuối các tín hiệu QS-XX so với mục tiêu trong charter; sự cố hypercare P1/P2/P3; NPS do PM cung cấp (không bịa).
   - Rủi ro và bài học: tổng rủi ro nêu ra / đã đóng / xảy ra thành issue; action item retro và tham chiếu catalog.
   - Chuẩn bị bàn giao: danh sách truy cập production (không bí mật), backlog tồn/việc mở, giải phóng team theo vai trò.
   PM rà điểm nổi bật (kế hoạch vs thực tế, số việc mở) trước khi viết.
6. **Viết closeout doc** theo mẫu ở dưới; đầu mỗi mục lớn ghi nguồn số liệu; trạng thái "DRAFT - pending final sign"; nếu catalog bài học có bài mới thì thêm ghi chú danh mục.
7. **Hậu kiểm và bàn giao.** Rà checklist sau khi viết; chờ 4 người ký (PM / Sponsor / Customer PIC / Support Lead). Việc tiếp theo: gửi báo cáo cuối cho sponsor/khách (email hoặc deck).
8. **Việc PM tự làm ngoài tài liệu** (tài liệu này không tự làm): chuyển trạng thái dự án sang đóng trên hệ thống; giải phóng nhân sự với HR/quản lý SBU; thực thi lưu trữ thật; kích hoạt thanh toán/hóa đơn.
- Input: hồ sơ dự án + xác nhận của khách. Output: closeout doc DRAFT + checklist lưu trữ.

## Công thức, ngưỡng & tín hiệu (bảng: tên | công thức/điều kiện | ngưỡng | hành động khi vượt; không có thì ghi "Không có")

| Tên | Công thức / điều kiện | Ngưỡng | Hành động khi vượt |
|---|---|---|---|
| Gates passed | Số gate qua / tổng | Mục tiêu 6/6 (G1-G6) | Ghi trạng thái từng gate, nêu hold |
| Rủi ro Critical/High mở | Đếm trong sổ rủi ro | Phải bằng 0 để đóng | Dừng, hoặc PM hoãn có lý do rõ ràng |
| QS-REQ-01 | Giá trị cuối so với mục tiêu | Mục tiêu lấy từ tiêu chí thành công trong charter | Ghi Status đạt/không đạt |
| QS-DSG-03 | Giá trị cuối | Mục tiêu từ charter | như trên |
| QS-DEV-cov | Giá trị cuối | Mục tiêu từ charter | như trên |
| QS-TST-04 | Giá trị cuối | Mục tiêu: nhỏ hơn hoặc bằng 2% | Ghi Status; nêu nguyên nhân nếu vượt |
| QS-PRC-07 | Giá trị cuối | Mục tiêu: lớn hơn hoặc bằng 90% | như trên |
| Sự cố hypercare | Đếm P1/P2/P3 theo nhật ký hypercare | Không đặt ngưỡng | Ghi số lượng |
| Customer NPS | PM cung cấp | Không đặt ngưỡng | Không bịa; thiếu ghi `[NO_DATA]` |
| Số bên ký | PM, Sponsor, Customer PIC, Support Lead | 4 chữ ký | Chưa đủ thì giữ trạng thái DRAFT |

(nguồn chưa rõ: ý nghĩa cụ thể từng mã QS-XX không được định nghĩa trong hai thư mục này; chỉ có mục tiêu ở bảng trên. Tham khảo bài về tín hiệu chất lượng.)
(nguồn chưa rõ: nguồn ghi "9 sections + sign-off" nhưng đánh số 1-10, trong đó 10 là Sign-off.)

## Template / mẫu đầu ra (rút gọn, giữ cấu trúc, cột, trường)
```
# Project Closeout - <CODE> <name> - DRAFT
> Nguồn: charter + schedule + gates + effort + xác nhận ký của PM
| Field | Value |
Project Code | Project Name | Sponsor | PM | SBU | Contract Type | Period (start -> end) | Status: DRAFT - pending final sign

## 1. Scope Delivered      | Feature | Plan | Status | Note |
## 2. Schedule Final       | Milestone | Original Plan | Final Actual | Variance |
## 3. Effort/Cost Final    | Metric | Plan | Actual | Variance |
## 4. Quality Summary      | Metric | Target | Actual | Status |
## 5. Risk Final           | Total raised | Closed | Realized as issue |
## 6. Handover
   ### Support Team Taking Over / ### Production Access / ### Known Open Items / ### Runbook
## 7. Customer Sign-off    | Item | Status | Sign Date |   (UAT, go-live, final acceptance, invoice)
## 8. Team Release Plan    | Role | Person | Release Date | Next assignment |
## 9. Archive Checklist    - [ ] ...
## 10. Sign-off            | Role | Name | Sign | Date |   (PM, Sponsor, Customer PIC, Support Lead)
Portfolio note: tham chiếu catalog bài học
```
Nội dung mặc định của Archive Checklist:
- [ ] Source code: gắn tag `vX.Y.Z-final` + khóa bảo vệ nhánh
- [ ] Toàn bộ tài liệu quản lý dự án chuyển lên ổ lưu trữ của công ty theo thư mục `/projects/<CODE>/`
- [ ] Bản chụp cuối SRS, basic design
- [ ] Charter, baseline tiến độ + bản cuối
- [ ] Mọi tài liệu và checklist gate review
- [ ] Sổ rủi ro cuối + Lessons learned (Ch9·01)
- [ ] Closeout doc + chứng từ ký của khách
- [ ] Báo cáo cuối dạng PDF cho sponsor

Checklist sau khi viết: hypercare + retro đã đóng; kế hoạch vs thực tế có nguồn (thiếu thì `[NO_DATA]`); danh sách truy cập không chứa bí mật (chỉ tham chiếu vault); archive checklist do PM tự tick; trạng thái DRAFT chờ 4 chữ ký.

## Lỗi thường gặp & lesson learned (sai gì -> hậu quả -> cách tránh)
| Sai | Hậu quả | Cách tránh |
|---|---|---|
| Đóng khi còn Critical/High mở | Rủi ro nghiêm trọng bị bỏ lại cho team support | Đếm về 0, hoặc hoãn có lý do và người chấp nhận |
| Chưa có chấp nhận của khách mà đã lập closeout | Tài liệu vô nghĩa, tranh chấp nghiệm thu | Xác nhận lời/email trước |
| Bịa số plan/actual khi thiếu effort hoặc gate | Báo cáo cuối sai, mất uy tín | Ghi `[NO_DATA]`, bổ sung hồ sơ gốc |
| Chỉ có bản effort stub/proxy | Mục 3 không đủ tin cậy | Lấy effort chính thức |
| Ghi mật khẩu/khóa trong danh sách truy cập | Lộ bí mật | Chỉ ghi tham chiếu vault |
| Coi tài liệu = đã lưu trữ/đã giải phóng người | Việc thật không xảy ra | PM tự thực hiện và tự tick |
| Mâu thuẫn giữa hồ sơ và lời PM bị bỏ qua | Sai lệch âm thầm | Dừng và làm rõ |
| Tự ký thay các bên | Sai quy trình | Chỉ 4 bên ký |

## Ví dụ minh họa (ngắn, có số; dựng thì ghi "(ví dụ dựng)")
(ví dụ dựng) Dự án <tên-dự-án> có 2 release, hypercare cả hai đã đóng, retro dự án xong. Bảng Quality Summary:
- Gates passed: Target 6/6, Actual 6/6 (G2 từng hold rồi pass), Status đạt.
- QS-TST-04: Target nhỏ hơn hoặc bằng 2%, Actual 1.5%, đạt. QS-PRC-07: Target lớn hơn hoặc bằng 90%, Actual 88%, không đạt, ghi lý do trong Note.
- Hypercare: 0 P1, 0 P2, 2 P3. Customer NPS: `[NO_DATA]` vì PM chưa có khảo sát.
- Còn 1 rủi ro High mở nên chưa thể đóng: PM hoặc xử lý về 0, hoặc hoãn có lý do và ghi rõ người chấp nhận.

## Tự kiểm tra (3-5 câu hỏi, đáp án ngắn ngay dưới)
1. Hai điều PM phải xác nhận trước khi làm closeout? -> Khách đã chấp nhận (lời/email) và không còn rủi ro Critical/High mở.
2. Ai ký closeout? -> PM, Sponsor, Customer PIC, Support Lead (4 chữ ký).
3. Mục tiêu QS-TST-04 và QS-PRC-07? -> QS-TST-04 nhỏ hơn hoặc bằng 2%; QS-PRC-07 lớn hơn hoặc bằng 90%.
4. Danh sách truy cập production ghi thế nào? -> Chỉ ghi tham chiếu vault, không ghi bí mật.
5. Tài liệu closeout có tự giải phóng nhân sự và lưu trữ không? -> Không, PM tự làm và tự tick checklist.

## Liên quan (bài trước/sau)
- Trước: 01-lessons-learned (retro dự án), hypercare, gate review, effort thực tế, quản lý rủi ro/issue, kickoff (charter), lập tiến độ, kế hoạch/thực hiện release.
- Sau: báo cáo cuối cho sponsor/khách (truyền thông stakeholder); phân công lại người vừa được giải phóng (ghép team).
- Câu hỏi nguồn còn bỏ ngỏ: quy ước đường dẫn lưu trữ; kích hoạt hóa đơn cuối và bàn giao thanh toán; catalog lịch sử tập trung; ký bằng PDF/email/DocuSign; giai đoạn support shadow 1 tuần có đủ không.
