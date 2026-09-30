---
title: Daily standup - chuẩn bị trước họp và ghi lại sau họp
source: Daily sync (Ch4·01)
stage: Development
level: cơ bản
prerequisites: []
---
# Daily standup - chuẩn bị trước họp và ghi lại sau họp

## Mục tiêu học xong bạn làm được gì
- Dựng được "bản tình hình" 1 trang trước buổi standup: blocker, việc xong hôm qua, việc đang làm hôm nay, việc quá hạn, việc mới phát sinh, hoạt động code.
- Xác định đúng cửa sổ thời gian (kể cả thứ Hai và sau kỳ nghỉ lễ) và chọn nguồn dữ liệu đáng tin cho từng loại thông tin.
- Ghi lại sau họp những thứ chỉ sinh ra trong họp (quyết định miệng, action item, blocker mới nêu) mà không làm mất bản đầu ngày.
- Nhận ra khi nào thiếu dữ liệu và ghi "không có dữ liệu" thay vì đoán.

## Khi nào dùng (thời điểm, ai kích hoạt, điều kiện đầu vào)
- Hằng ngày. PM là người kích hoạt.
- Chế độ **prep** (chuẩn bị): khoảng 8:30, trước standup. Đây là chế độ mặc định.
- Chế độ **capture** (ghi lại): ngay sau standup.
- Đầu vào tối thiểu: xác định được dự án (mã dự án, khóa Jira, khóa Bitbucket, mã dự án trong hệ thống nhân sự/roster) và có ít nhất một nguồn cho **cả** "task" và "blocker" (danh sách task local hoặc Jira). Không nguồn nào cho hai loại này thì bản standup vô nghĩa - dừng lại và kiếm nguồn.
- Chỉ làm cho **một dự án mỗi lần** (không chạy vòng nhiều dự án).
- Đây là bản chụp nhanh, tập trung vào blocker hơn là số đo. Muốn số đo sâu/xu hướng thì dùng báo cáo tuần (Status tuần (Ch7·01), `monitor-signal`); muốn gửi thông báo thì dùng Giao tiếp stakeholder (Ch7·03).

## Khái niệm cốt lõi (định nghĩa, thuật ngữ, vì sao quan trọng)
- **Standup snapshot**: bản chụp nhanh tình hình đầu ngày để cả nhóm họp ngắn mà có số liệu thật, không họp bằng cảm giác.
- **Hai thời điểm, hai chiều thông tin**:
  - Prep: hệ thống -> người (PM đọc). Là INPUT của cuộc họp. Nguồn: tự tổng hợp từ tài liệu/Jira/Bitbucket.
  - Capture: cuộc họp -> bản ghi (PM ghi). Là OUTPUT của cuộc họp. Nguồn: con người (ghi chú họp) - có thể bỏ qua; khi đó vẫn tự động so sánh ra blocker phát sinh.
  - Capture **nối thêm (append)** vào chính file prep cùng ngày: một file mỗi ngày = ảnh đầu ngày + kết quả họp. Không tạo file thứ hai, không ghi đè. Nếu không có file prep sáng thì tạo mới và ghi chú "(không có prep sáng)".
- **Chuỗi ưu tiên nguồn cho mỗi loại dữ liệu**: tài liệu local (nếu có) -> Jira/Bitbucket (dự phòng) -> nguồn khác đã cấu hình -> "không có dữ liệu". Thiếu tài liệu local **không** phải lý do dừng, chỉ là lý do đổi nguồn.

  | Loại dữ liệu | Tài liệu local | Dự phòng (hệ thống) |
  |---|---|---|
  | task (xong/đang làm/mới) | danh sách task | Jira |
  | quá hạn (overdue) | lịch (schedule) | Jira (`duedate` < hôm nay) |
  | rủi ro/vấn đề mới | sổ risk / sổ issue | Jira (`created` >= đầu cửa sổ) |
  | git | git local (nếu repo có) | Bitbucket (PR, commit) |
  | blocker | task có status = blocked | Jira |
- **Nguyên tắc "không bịa số"**: thiếu dữ liệu -> ghi `[NO_DATA]` cho mục đó. Chỉ dừng toàn bộ khi cả task và blocker đều không có nguồn.
- **Trạng thái tài liệu**: luôn là bản nháp (DRAFT) chờ PM duyệt; không tự động gửi thông báo, không commit.
- **Ký hiệu nguồn** (giúp người đọc biết dữ liệu đến từ đâu): tài liệu / hệ thống (Jira, Bitbucket) / quy tắc cố định của công ty / PM xác nhận / giả định / chưa có (TBD). Mỗi mục nên ghi rõ nguồn.

## Cách làm từng bước (thủ công, đủ chi tiết để làm theo; kèm input/output)
1. **Xác định dự án và nguồn.** Input: tên/mã dự án. Xác định khóa Jira, khóa Bitbucket, mã dự án trong roster. Người dùng đôi khi gõ tên repo thay vì mã dự án: khi đó tìm repo, lấy dự án cha, giới hạn git về đúng repo đó, nhưng nhớ rằng Jira/roster là cấp dự án còn git là cấp repo (nêu rõ chênh lệch này và xác nhận với PM).
2. **Kiểm tra nguồn nào dùng được cho từng loại** và lập bảng "loại - nguồn dùng - trạng thái" (ví dụ tasks/overdue/blockers lấy từ Jira; git từ Bitbucket; risk từ sổ risk, nếu chưa có file thì dự phòng Jira). Xác nhận với mình/PM trước khi làm tiếp.
3. **Chọn chế độ và cửa sổ thời gian.**
   - Mặc định: prep.
   - Cửa sổ mặc định = ngày chạy + **ngày làm việc liền kề trước đó** (không cố định 24 giờ). Thứ Hai gộp thứ Sáu + cuối tuần; sau kỳ nghỉ lễ gộp cả ngày nghỉ. Dùng số ngày làm việc/tuần = 5 và lịch nghỉ lễ (lịch nghỉ lễ của hệ thống, dự phòng lễ Việt Nam).
   - Nếu tự đổi cửa sổ khác mặc định thì phải xác nhận lại khoảng đó trước khi phân tích.
4. **Kiểm tra trước khi phân tích**: mã dự án khớp; token nguồn hợp lệ (chỉ `doc`, `jira`, `bitbucket`, `ksystem`); nếu cùng một loại có cả tài liệu và hệ thống thì theo ưu tiên đã khai; nếu nguồn ưu tiên là tài liệu mà tài liệu cũ hơn cửa sổ (ví dụ chưa cập nhật hôm nay) thì gắn cờ nhẹ "tài liệu có thể cũ, cân nhắc lấy từ hệ thống" - **PM quyết**, không tự đổi nguồn.
5. **Thu thập trạng thái (chế độ prep)** - mỗi khối áp bộ lọc loại trừ việc không phải giao hàng (họp, đồng bộ khách, quản lý dự án, deploy - xem bài Daily report, Ch4·02):
   - **Blocker**: từ danh sách task status = blocked; nếu dùng Jira của công ty (không có status "Blocked") thì dùng đại diện: dự án = X, status không thuộc {Rejected, Pending}, và ((loại issue khác Bug và status = Confirmming) hoặc (loại issue = Bug và status khác Done)); sắp theo priority giảm dần; người = assignee. Đánh 🔴 nếu blocker **mới** (chuyển vào Confirmming/bug-open trong cửa sổ, kiểm bằng lịch sử thay đổi), còn lại 🟡 (tồn từ trước).
   - **Xong hôm qua**: task chuyển sang Done/Resolved/Deployed trong cửa sổ; ghi công cho **người thực hiện chuyển trạng thái** (author trong lịch sử thay đổi), không phải assignee hiện tại. Nếu hệ thống không hỗ trợ lọc theo chuyển trạng thái: lấy issue có `updated` trong cửa sổ rồi đọc lịch sử từng issue, giữ issue có chuyển trạng thái kết thúc trong cửa sổ (giới hạn khoảng 30, ghi chú "(truncated)"). Kèm số commit và PR đã merge.
   - **Đang làm hôm nay**: status "In Progress" hoặc "To Do", sắp theo `duedate` tăng dần (nếu dùng tài liệu: việc lập kế hoạch cho hôm nay).
   - **Quá hạn**: `duedate` < hôm nay và status thuộc {To Do, In Progress, Confirmming, Feedback}; số ngày trễ = hôm nay - duedate; chủ = assignee. **Loại Resolved/Deployed** khỏi danh sách quá hạn của standup (khác báo cáo cho quản lý): standup chỉ cần việc còn phải làm; đã kiểm chứng rằng gồm cả Resolved gây nhiễu nặng (một dự án có 37 issue, đa số đã xong nhưng duedate cũ).
   - **Mới hôm nay**: issue tạo từ đầu cửa sổ đến hết hôm nay; ghi công cho reporter; tách bug mới và task mới theo loại issue; đếm risk mới và issue mới.
   - **Hoạt động git**: (a) PR đã merge - lấy 25 PR mới nhất trạng thái MERGED rồi lọc phía client theo thời điểm cập nhật trong cửa sổ (định dạng thời gian của hệ thống có thể không phải ISO, cần parse); (b) PR đang mở - đếm "chờ review", PR cũ hơn cửa sổ gắn cờ nhẹ; (c) commit - xác định nhánh tích hợp **theo dữ liệu, không giả định tên nhánh** (xem lỗi thường gặp), lấy 25 commit gần nhất rồi lọc client-side theo ngày commit trong cửa sổ và nhóm theo tác giả.
   - **Tên người**: nếu có roster thì đổi username thành tên hiển thị (so khớp email chính xác, rồi phần trước @, rồi chuẩn hóa chuỗi); không có roster thì để username và ghi banner cảnh báo.
6. **Sinh file** `<ngày>.md` theo mẫu (xem mục Template). Blocker đặt ngay sau bảng thông tin đầu file. Mỗi section có dòng nguồn. Thiếu dữ liệu -> `[NO_DATA]`. Status = DRAFT.
7. **Sau họp (capture)**:
   - Tự động, không cần input: chạy lại truy vấn blocker, so với danh sách blocker trong file prep cùng ngày -> ra "blocker mới nêu trong standup".
   - Nếu PM có ghi chú họp: cấu trúc thành bảng Chủ đề / Quyết định-Action / Người phụ trách / Hạn; cờ item thiếu người phụ trách hoặc hạn. Nếu PM bỏ qua hoàn toàn: bảng ghi `[NO_DATA] no capture input`.
   - Nối vào file prep, không ghi đè.
8. **Kết thúc**: đọc lại bản tóm tắt (số blocker, quá hạn, git; nguồn đã dùng), chạy checklist cuối. Nếu có blocker mới 🔴: in banner "NEW BLOCKER - báo standup channel" và (tùy chọn) soạn 1 dòng để PM **tự copy** sang Teams/Slack. Không tự gửi.

## Công thức, ngưỡng & tín hiệu (bảng: tên | công thức/điều kiện | ngưỡng | hành động khi vượt)
| Tên | Công thức / điều kiện | Ngưỡng | Hành động |
|---|---|---|---|
| Cửa sổ ngày | ngày chạy + ngày làm việc liền kề trước; 5 ngày làm việc/tuần; gộp cuối tuần/lễ | - | Đổi cửa sổ -> xác nhận lại |
| Blocker (Jira công ty) | (loại != Bug và status = Confirmming) hoặc (Bug và status != Done), loại Rejected/Pending | - | Liệt kê đầu file |
| Blocker mới 🔴 vs cũ 🟡 | có chuyển trạng thái vào Confirmming/bug-open trong cửa sổ | - | 🔴: banner + escalation; 🟡: theo dõi |
| Số ngày trễ | hôm nay - duedate | > 0 | Đưa vào bảng quá hạn (chủ + số ngày) |
| Status tính quá hạn | To Do, In Progress, Confirmming, Feedback (KHÔNG gồm Resolved/Deployed) | - | - |
| Giới hạn truy vấn dự phòng | khoảng 30 issue đọc lịch sử; PR/commit lấy 25 gần nhất | - | Ghi "(truncated)" |
| 0 commit / 0 PR | - | - | Ghi "0 commits / 0 PR (cửa sổ ...)" |

## Template / mẫu đầu ra (rút gọn, giữ cấu trúc và các cột/trường)
```
# Daily Sync - <YYYY-MM-DD> (<thứ>)
| Field | Value |  Project | Mode (prep/capture) | Reported (giờ) | Window (từ -> đến, "ngày làm việc liền kề") | Status (ví dụ: 1 new blocker)
> Sources: (Jira + Bitbucket + tự động ...)
## Blockers (need attention today)   - 🔴 KEY (người) - mô tả, kẹt N ngày -> hành động; 🟡 KEY - phụ thuộc, parked
## Done Yesterday (<ngày>)           - danh sách issue chuyển Done/Resolved; số commit, số PR merged
## In Progress Today                 - KEY (người) - việc
## Overdue Tasks                     | Issue | Owner | Days late | Note |
## New Today                         - N risk mới - M issue mới: KEY (người) - mô tả
## Git Activity (cửa sổ ngày làm việc) - N commits (theo người) - nhánh; PR merged: repo#id; PR open: #id (review pending)
## Quick Asks                        - việc cần PM xử lý (ví dụ escalate khách 14:00)
--- capture (nối thêm) ---
## Blocker nêu trong standup (diff vs prep sáng)
## Standup Capture   | Topic | Decision / Action | Owner | Due |
```
Checklist cuối: blocker đầu file; quá hạn có số ngày trễ + chủ; git đúng cửa sổ hoặc `[NO_DATA]`; mỗi mục ghi nguồn; thiếu dữ liệu -> `[NO_DATA]`; capture nối đúng file prep; DRAFT, không commit.

## Lỗi thường gặp & lesson learned (lấy từ nguồn, mỗi ý: sai gì -> hậu quả -> cách tránh)
- Đoán cứng nhánh git là `develop` -> báo 0 commit dù repo có hoạt động (repo thực tế dùng `main` + một nhánh khác, không có `develop`/`master`) -> xác định động: lấy tập nhánh đích của PR gần đây cộng {main, develop, master}, thử lấy 1 commit mỗi nhánh, bỏ nhánh không tồn tại, **chọn nhánh có commit mới nhất**. Đừng chọn theo "nhánh đích phổ biến nhất" (đã gặp repo PR nhắm nhánh khác nhưng commit thật ở `main`).
- Dùng tham số khoảng thời gian (since/until) khi lấy commit từ Bitbucket Data Center -> lỗi "Not found" khi khoảng rỗng -> luôn lấy commit gần đây rồi lọc phía client.
- Đưa Resolved/Deployed vào danh sách quá hạn -> danh sách nhiễu, che mất việc thật -> loại chúng khỏi standup.
- Ghi công theo assignee hiện tại -> sai người (người khác đã làm xong rồi giao lại) -> đọc lịch sử thay đổi và ghi công cho người chuyển trạng thái.
- Coi thiếu tài liệu local là lỗi cứng -> skill/PM dừng vô ích -> chỉ đổi sang nguồn dự phòng; chỉ dừng khi cả task lẫn blocker đều không có nguồn.
- Tin tài liệu cũ -> blocker cũ -> có cờ "tài liệu có thể cũ", để PM quyết.
- Gộp capture bằng cách ghi đè file prep -> mất ảnh đầu ngày -> luôn nối thêm.
- Tự gửi thông báo blocker -> ngoài phạm vi và rủi ro nhầm kênh -> chỉ hiện banner + 1 dòng để PM copy.
- Ghi số liệu khi hệ thống không trả dữ liệu -> báo cáo sai -> `[NO_DATA]`.
- Hạn chế đã biết: credit PR merged theo **tác giả** (không có thông tin người merge trong công cụ dùng ở đây); nếu không parse được thời gian cập nhật thì giữ PR và ghi "(time unparsed)".

## Ví dụ minh họa (1 ví dụ ngắn có số, lấy hoặc dựng từ nguồn; nếu dựng thì ghi "(ví dụ dựng)")
Ví dụ mẫu trong nguồn (dữ liệu giả, dự án PROJA, thứ Ba 2026-08-26, cửa sổ 2026-08-25 -> 2026-08-26):
- Blocker: 🔴 PROJA-018 (usera) - khách chưa xác nhận API spec, kẹt 4 ngày -> escalate 14:00; 🟡 PROJA-022 (userb) phụ thuộc PROJA-018, parked.
- Xong hôm qua: PROJA-015, -016, -017 (3 issue Done/Resolved); 5 commit, 2 PR merged.
- Quá hạn: PROJA-018, chủ usera, trễ 4 ngày (đúng là blocker).
- Mới: 0 risk, 1 issue (PROJA-025 - dựng môi trường test).
- Git: 5 commit (usera 2, userb 2, userc 1); 2 PR merged (#47, #48); 1 PR open (#50, chờ review).
- Capture sau họp: blocker mới PROJA-030 (userc) chưa có trong bản sáng; bảng: "PROJA-018 escalation -> họp khách 14:00 - PM - 2026-08-26", "Test env -> DevOps xác nhận capacity - userd - 2026-08-27".

## Tự kiểm tra (3-5 câu hỏi có đáp án ngắn ngay dưới, dựa trên chính nội dung bài)
1. Hôm nay là thứ Hai, cửa sổ standup mặc định là gì?
   - Ngày chạy + ngày làm việc liền kề trước (tức thứ Sáu), gộp cả cuối tuần.
2. Hai chế độ prep và capture khác nhau ở chiều thông tin và nguồn thế nào?
   - Prep: hệ thống -> PM, nguồn tự tổng hợp, là input họp. Capture: họp -> bản ghi, nguồn là PM (tùy chọn), là output; nối thêm vào file prep cùng ngày.
3. Việc nào KHÔNG được tính vào danh sách quá hạn của standup, và vì sao?
   - Resolved/Deployed - vì standup chỉ cần việc còn phải làm, gồm chúng gây nhiễu.
4. Khi không tìm thấy dữ liệu cho mục "risk mới" thì làm gì? Khi nào thì được dừng cả bản standup?
   - Ghi `[NO_DATA]` cho mục đó; chỉ dừng khi cả task và blocker đều không có nguồn.
5. Vì sao không được hardcode nhánh `develop` khi đếm commit?
   - Repo có thể dùng nhánh khác (ví dụ `main`); phải chọn nhánh có commit mới nhất trong số các ứng viên.

## Liên quan (bài trước/sau trong quy trình, tên thư mục skill khác)
- Anh em: Daily report (Ch4·02) (bản chi tiết hơn, cùng nguồn Jira/Bitbucket); Status tuần (Ch7·01) (gộp daily thành báo cáo tuần); Giao tiếp stakeholder (Ch7·03) (gửi thông báo).
- Nguồn tài liệu tùy chọn: danh sách task (Spec thành task, Ch3·02), lịch (Lập schedule, Ch3·03), sổ risk/issue (Rủi ro & issue, Ch4·04).
- Cần đăng ký dự án trước (Thiết lập PM, Ch1·03).
- Nguồn chưa rõ: mẫu ví dụ ghi giờ báo cáo 09:30 trong khi quy định nói prep chạy khoảng 8:30 (không mâu thuẫn quy tắc, chỉ là giờ minh họa); dòng "Status" trong mẫu (ví dụ "1 new blocker") không có quy tắc chính thức cách đặt.
