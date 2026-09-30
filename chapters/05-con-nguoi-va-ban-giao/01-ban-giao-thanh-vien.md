---
title: Bàn giao công việc khi thành viên nghỉ việc hoặc chuyển dự án
source: Bàn giao thành viên (Ch5·01)
stage: Cross-cutting
level: trung bình
prerequisites: [Ch5·02]
---
# Bàn giao công việc khi thành viên nghỉ việc hoặc chuyển dự án

## Mục tiêu học xong bạn làm được gì
- Chạy đúng quy trình bàn giao 8 bước khi một thành viên rời hoặc chuyển dự án, biết bước nào PM làm, bước nào thuộc Giám đốc, HR, Sales/AM.
- Lập được bản kế hoạch bàn giao theo mẫu TPL-HR-14-01 (tổng quan, ma trận 13 mục, đầu việc, ticket, tài liệu, môi trường/truy cập, lịch, ghi chú, lịch sử).
- Theo dõi trạng thái bàn giao (DRAFT, Approved, In-progress, Confirmed, Rejected) và biết điều kiện để xác nhận đóng.
- Tránh các lỗi nhạy cảm: ghi mật khẩu vào tài liệu, biến bản bàn giao thành lệnh giao việc, nhầm bàn giao thành viên với đóng dự án.

## Khi nào dùng (thời điểm, ai kích hoạt, điều kiện đầu vào)
- Kích hoạt khi có thành viên nghỉ việc (resign), chuyển dự án (transfer) hoặc lý do khác (other).
- Người soạn: PM, phối hợp với người bàn giao. Người phê duyệt mặc định là PM; có thể là GĐ SBU / GĐ chi nhánh / GD Solution.
- Thông tin bắt buộc trước khi lập kế hoạch: định danh dự án; người bàn giao (tên + vai trò); lý do (resign/transfer/other); ngày hiệu lực (định dạng YYYY-MM-DD).
- Người nhận: nếu đã biết thì ghi; nếu chưa có thì ghi "chưa xác định" (TBD) và đánh dấu cần tuyển/bổ sung nhân sự (không dừng quy trình).
- Nếu ngày hiệu lực đã ở quá khứ thì phải hỏi lại PM xác nhận.
- Phân biệt: member VÀO dự án -> bài Onboarding brief (Ch5·02); member RA/CHUYỂN -> bài này; đóng CẢ dự án -> quy trình closeout (không dùng bài này).

## Khái niệm cốt lõi (định nghĩa, thuật ngữ, vì sao quan trọng)
- **TPL-HR-14-01**: mẫu Excel "Kế hoạch và nội dung công việc bàn giao" v1.0 của công ty. Bài này chuyển từng sheet sang một phần của tài liệu Markdown.
- **Nội dung cần bàn giao**: trọng tâm là những gì người nhận cần được giải thích (tài liệu, danh sách ticket đang phụ trách, rủi ro, quyền truy cập, lịch trao đổi) chứ không phải việc phân công.
- **Kiểm kê (inventory) chỉ đọc**: liệt kê ticket Jira đang mở của người bàn giao để giải thích. Không cập nhật, không reassign, không tự gán Jira. Không có cột "Suggested Receiver" hay câu lệnh "giao cho X" vì dễ bị hiểu nhầm là đã giao việc. Việc đổi assignee (nếu cần) làm thủ công, ngoài bản kế hoạch.
- **Người bàn giao / Người nhận**: có thể 1 người nhận hoặc nhiều (1 -> N). Khi nhiều người nhận, ghi ở phần thông tin chung và buổi trao đổi; nhóm nội dung A/B/C chỉ để bao quát khi trình bày, không phải gán chủ sở hữu.
- **Nguyên tắc bảo mật**: không ghi mật khẩu, token, private key, OTP seed. Chỉ ghi "credential: see <đường dẫn vault>".
- Vì sao quan trọng: bàn giao thiếu -> mất tri thức dự án, ticket bị bỏ rơi; bàn giao ghi mật khẩu -> rò rỉ bảo mật.

## Cách làm từng bước (thủ công, đủ chi tiết để làm theo; kèm input/output)

### Quy trình 8 bước của công ty (RACI)
| # | Công việc | Vai trò | Tài liệu | PM làm gì |
|---|---|---|---|---|
| 1 | Thông báo chuyển giao công việc | GĐ SBU / GĐ CN Đà Nẵng / GD Solution | - | Ghi vào kế hoạch |
| 2 | Thông báo kế hoạch tuyển dụng / điều chỉnh nhân sự | GĐ ... | - | Đánh dấu "cần tuyển" nếu chưa có người nhận |
| 3 | Xem xét có thông báo cho KH không? | Sales/AM | - | Ghi quyết định; nếu Có thì soạn nháp thông báo |
| 3a | Thông báo cho khách hàng (nếu Có) | Sales/AM | - | Chỉ soạn nháp; Sales/AM gửi |
| 4 | Xác định thông tin + kế hoạch bàn giao | Người bàn giao / PM | TPL-HR-14-01 | Lập kế hoạch |
| 5 | Xem xét và phê duyệt | PM / GĐ SBU / GĐ CN / GD Solution | TPL-HR-14-01 | Trình duyệt; từ chối thì quay lại bước 4 |
| 6 | Trao đổi kế hoạch và công việc cần bàn giao | Người nhận / Người bàn giao / PM | TPL-HR-14-01 | Tổ chức buổi trao đổi, cập nhật trạng thái trong/sau buổi |
| 7 | Đánh giá nhân sự | PM / GĐ ... | - | Ngoài phạm vi bài này (chỉ nhắc) |
| 8 | Xác nhận tình trạng bàn giao | PM | TPL-HR-14-01 | Xác nhận đóng |

Bảng theo dõi 8 bước dùng trạng thái: Pending | Done | N/A | Skipped.

### Thực hiện chi tiết
1. **Thu thập thông tin (theo nhóm)**: (Q1) người bàn giao (tên, vai trò, tài khoản Jira/email), người nhận (mỗi người: tên, vai trò, module/task nhận), lý do, ngày hiệu lực; (Q2) có thông báo khách hàng không (mặc định No), Sales/AM phụ trách, kênh/tông giọng (mặc định Teams / email formal); (Q3) kênh liên lạc, lịch họp cần theo dõi, repo Git và có chuyển quyền master không, vị trí vault (chỉ hỏi đường dẫn, không hỏi mật khẩu); (Q4) khoảng thời gian bàn giao (mặc định bắt đầu = hôm nay, hạn = ngày hiệu lực), người duyệt (mặc định PM).
2. **Kiểm tra hợp lệ**: người bàn giao có tên + vai trò; mỗi người nhận có tên + vai trò; khi chia 1->N thì ít nhất 1 người có phạm vi công việc; ngày hợp lệ; tài liệu không chứa mật khẩu/token/khóa. Nếu PM dán mật khẩu vào chat thì không ghi vào file, nhắc dùng vault.
3. **Tập hợp nội dung**:
   - Tổng quan dự án: tên, khách hàng, mô tả, thời gian, đặc thù (từ charter hoặc hệ thống quản lý dự án).
   - Ticket của người bàn giao (chỉ đọc). Truy vấn Jira mẫu: `project = <khóa dự án> AND assignee = <người bàn giao> AND statusCategory != Done ORDER BY priority DESC, updated DESC`. Mỗi ticket ghi: key, tóm tắt, trạng thái, hạn (nếu có), ghi chú nội dung cần bàn giao. Không có Jira thì dùng danh sách task hoặc PM tự liệt kê (vẫn chỉ là kiểm kê).
   - Đầu việc: từ lịch, ghi chép hằng ngày, PM (đầu mục, thời gian, người liên quan, URL, mô tả).
   - Tài liệu: phân loại Spec / Design / Report / Other.
   - Môi trường: chỉ URL + tài khoản/vai trò + ghi chú vault.
   - Lịch bàn giao: gợi ý 4 hạng mục Kickoff (trao đổi kế hoạch), Walkthrough (tài liệu + flow), Pairing (task đang mở), Confirm (xác nhận tình trạng). Ước lượng giờ do PM hoặc tự ước.
   - Khác: issue/rủi ro chưa xử lý, working flow nội bộ và với khách hàng.
4. **Đặt tên file**: `<dự-án>-<người-bàn-giao-kebab>-to-<người-nhận-kebab>-<YYYY-MM-DD>.md`. Nhiều người nhận: `-to-multi-`; chưa có: `-to-tbd-`. Cập nhật/duyệt/xác nhận thì ghi đè cùng file (trừ khi cần bản mới `-r2`).
5. **Trình duyệt (bước 5)**: gửi cho người duyệt. Từ chối -> chỉnh sửa, trạng thái về DRAFT rồi trình lại.
6. **Trao đổi (bước 6)**: sau buổi họp, cập nhật từng mục ma trận; ghi ticket còn mở vào cột Note; thêm dòng vào Lịch sử.
7. **Xác nhận (bước 8)**: chỉ khi kế hoạch đã Approved và mọi mục bắt buộc trong ma trận là Done hoặc N/A (kèm ghi chú). Thiếu thì liệt kê khoảng trống và cập nhật tiếp.
8. **Thông báo khách hàng (nếu Có)**: soạn nháp gồm đối tượng nhận (đầu mối khách hàng), hạn gửi, điểm nhấn (ai thay, từ ngày nào). PM/Sales gửi; người soạn không tự gửi.

### Chuyển trạng thái của kế hoạch
```
DRAFT -> Approved (duyệt)
DRAFT -> Rejected (từ chối) -> chỉnh -> DRAFT
Approved -> In-progress (khi bắt đầu trao đổi)
In-progress -> Confirmed (xác nhận đóng)
```
Duyệt chỉ áp dụng khi kế hoạch đang DRAFT hoặc Rejected (đã chỉnh); không duyệt lại khi đã Confirmed. Khi duyệt: ghi người duyệt + ngày, không sửa nội dung trừ khi được yêu cầu. Chuyển trạng thái không hợp lệ thì dừng và hỏi lại.

## Công thức, ngưỡng & tín hiệu
Không có công thức hay ngưỡng số. Các điều kiện pass/fail đáng nhớ:

| Tên | Điều kiện | Ngưỡng | Hành động khi vi phạm |
|---|---|---|---|
| Điều kiện xác nhận đóng | Kế hoạch đã Approved; mọi mục bắt buộc ở ma trận là Done hoặc N/A (kèm note) | Không còn mục bắt buộc Pending | Liệt kê khoảng trống, cập nhật tiếp |
| Kiểm tra bảo mật | Không có password/token/private key trong file | 0 | Xóa, thay bằng "see vault: <path>" |
| Ngày hiệu lực | Định dạng ISO hợp lệ | Không ở quá khứ | Nếu quá khứ thì hỏi PM xác nhận |

## Template / mẫu đầu ra (rút gọn, giữ cấu trúc và các cột/trường)
Tiêu đề: "Member Handover Plan - <Từ> -> <Đến>". Chú giải nguồn: 📄 file dự án · 📋 quy tắc/TPL-HR-14-01 · 🌐 hệ thống · 💭 PM cung cấp · 🤖 tự sinh · ⏳ chưa có.

Bảng thông tin: Project | Template (TPL-HR-14-01 v1.0) | Người bàn giao (vai trò) | Người nhận (hoặc multi/TBD) | Lý do | Ngày hiệu lực | Approver | Notify KH (Yes/No) | Jira policy (chỉ kiểm kê, không cập nhật/reassign/tự gán) | Prepared by | Status (DRAFT) | Created.

Bảng theo dõi 8 bước: `# | Bước | Owner | Status | Note` (bước 4 = Done ngay khi có tài liệu này; bước 7 ghi "ngoài phạm vi").

§1 Tổng quan dự án: Tên dự án, KH, Mô tả, Thời gian dự án, Đặc thù.

§2 Ma trận trạng thái bàn giao: cột `No. | Description | BG status | Người BG | Receive status | Người nhận | Note`. Trạng thái: Pending / In-progress / Done / N/A. 13 mục chuẩn:

| No. | Mô tả | Gợi ý điền |
|---|---|---|
| 1 | Các công việc cần thực hiện | Liên kết §3 + §7 |
| 2 | Project document | §5 |
| 3 | Project Report | Báo cáo tuần/tháng, trạng thái |
| 4 | Project JIRA | Link board + khóa dự án |
| 5 | Project tickets | Ticket tồn đọng/quan trọng (§4) |
| 6 | GIT | Link repo + có chuyển quyền master không |
| 7 | (dự phòng, bỏ qua nếu trống trong mẫu) | - |
| 8 | Communication Channel | Teams/Slack/email |
| 9 | Meeting schedule | Lịch team/khách hàng cần theo |
| 10 | Project resources | Người, môi trường, công cụ |
| 11 | Important issues | Issue/rủi ro chưa xử lý |
| 12 | Working flow | Flow nội bộ + với khách |
| 13 | Other notes | QA, AF, Sales, lưu ý khác |

(Nguồn chưa rõ: mục 7 không có nội dung; mẫu output bỏ dòng 7, đánh số 1-6 rồi 8-13.)

§3 Đầu việc: `NO | Đầu mục | Thời gian | Người liên quan | URL | Mô tả | Note`.
§4 Kiểm kê ticket: `NO | Jira key/Epic | Nội dung cần bàn giao | Status | Due | Note` (đầu phần ghi rõ: không cập nhật, không gán).
§5 Tài liệu: `NO | Tên tài liệu | Phân loại | Lưu trữ | URL | Mô tả | Note`.
§6 Môi trường & truy cập: `No | Môi trường | URL | Account/role | Credential | Note`, cột Credential = "see vault: <đường dẫn>".
§7 Lịch bàn giao: `Category | Task | Assignee | Estimate (h) | Start | Due | Note` với 4 hạng mục Kickoff / Walkthrough / Pairing / Confirm.
§8 Ghi chú khác: working flow; issue/rủi ro; ghi chú QA / AF / Sales.
Lịch sử: `Date | Member | Description` (chỉ thêm, không sửa).
Checklist rà soát cuối file: (1) việc bên soạn tự giả định cần PM kiểm; (2) mục chờ dữ liệu; (3) bảo mật (không có password/token); (4) mục PM đã xác nhận.

## Lỗi thường gặp & lesson learned (lấy từ nguồn, mỗi ý: sai gì -> hậu quả -> cách tránh)
- Dán mật khẩu vào bản kế hoạch -> rò rỉ bảo mật -> chỉ ghi đường dẫn vault.
- Ghi cột "Suggested Receiver" hoặc "giao cho X" trong danh sách ticket -> người đọc hiểu nhầm là đã assign -> chỉ ghi nội dung cần giải thích; đổi assignee làm thủ công ngoài kế hoạch.
- Bịa danh sách task khi không lấy được Jira -> sai phạm vi bàn giao -> ghi [NO_DATA] và nhờ PM cung cấp danh sách.
- Tự duyệt hoặc tự gửi khách hàng -> vượt thẩm quyền -> chỉ soạn nháp, người có thẩm quyền duyệt/gửi.
- Dùng quy trình đóng dự án để bàn giao một thành viên -> sai vòng đời -> xem mục "Khi nào dùng".
- Bỏ phần nào đó khi thiếu dữ liệu -> người rà soát mất checklist -> giữ nguyên phần, ghi [NO_DATA].
- Quên mục GIT (mục 6) -> không rõ repo và quyền master -> ghi rõ repo và có chuyển quyền master hay không; quyết định đó thuộc bên có thẩm quyền.

## Ví dụ minh họa (1 ví dụ ngắn có số, lấy hoặc dựng từ nguồn; nếu dựng thì ghi "(ví dụ dựng)")
(Ví dụ dựng, dựa trên ví dụ synthetic trong nguồn) BE <Member A> nghỉ việc ngày 2026-07-31, người nhận <Member B> (BE), không thông báo khách hàng. PM lập file `<dự-án>-<member-a>-to-<member-b>-2026-07-13.md`, trạng thái DRAFT. §4 có 5 ticket Jira đang mở của A; §2 mọi mục Pending; theo dõi 8 bước thì bước 4 = Done, bước 5 = Pending; §6 ghi "credential: see vault: <vault>". Sau buổi họp: mục Document, JIRA, GIT = Done; 2 ticket còn Pending ghi vào Note; thêm dòng Lịch sử. Ngày 2026-07-15 GĐ duyệt -> Approved. Khi đủ Done -> Confirmed, bước 8 = Done.

## Tự kiểm tra (3-5 câu hỏi có đáp án ngắn ngay dưới, dựa trên chính nội dung bài)
1. Người nhận chưa xác định thì làm gì? -> Ghi TBD, đánh dấu cần tuyển/bổ sung nhân sự, vẫn tiếp tục lập kế hoạch.
2. Điều kiện để xác nhận (Confirmed)? -> Kế hoạch đã Approved và mọi mục bắt buộc ở ma trận là Done hoặc N/A có ghi chú.
3. Vì sao không có cột "Suggested Receiver"? -> Dễ bị hiểu là đã assign; Jira chỉ kiểm kê, không cập nhật/reassign.
4. Thông tin đăng nhập được ghi thế nào? -> Chỉ "credential: see <vault>"; tuyệt đối không mật khẩu/token/khóa.
5. Bước nào ngoài phạm vi kế hoạch? -> Bước 7 Đánh giá nhân sự (chỉ nhắc).

## Liên quan (bài trước/sau trong quy trình, tên thư mục skill khác)
- Anh em: Onboarding brief (Ch5·02) (người nhận mới vào), Onboarding todo (Ch5·03).
- Sau đó: thông báo khách hàng (Giao tiếp stakeholder, Ch7·03), Xếp người (Ch3·05) (bổ sung người), Daily sync (Ch4·01) / Status tuần (Ch7·01), Rủi ro & issue (Ch4·04) (nếu bàn giao trễ).
- Không thay thế: closeout (đóng cả dự án); Tiếp quản PM (Ch5·04) (PM tiếp quản giữa chừng, đồng bộ dữ liệu).
