---
title: Báo cáo Daily - bản cho PM và bản chi tiết cả team
source: Daily report (Ch4·02)
stage: Development
level: trung bình
prerequisites: [Ch4·01]
---
# Báo cáo Daily - bản cho PM và bản chi tiết cả team

## Mục tiêu học xong bạn làm được gì
- Viết được báo cáo daily buổi sáng 3 phần (hôm qua làm gì / còn kẹt gì / rủi ro gì) mà mỗi dòng có bằng chứng và ghi công đúng người.
- Dựng được báo cáo chi tiết team: 4 bảng kiểm tra cho PM, danh sách "Quy trình" (thiếu logwork / thiếu estimate) và bảng tổng kết theo từng thành viên.
- Áp dụng bộ luật loại trừ việc không phải giao hàng, luật ghi công theo "người thực hiện", và 11 quy tắc phát hiện rủi ro tự động (R01-R11).
- Viết câu rủi ro/follow-up đọc lần đầu là hiểu: ticket nào + vấn đề gì + PM làm gì.

## Khi nào dùng (thời điểm, ai kích hoạt, điều kiện đầu vào)
- Mỗi sáng làm việc; PM kích hoạt. Dữ liệu là của **ngày hoạt động** (mặc định hôm qua); báo cáo dùng cho standup sáng ngày kế tiếp.
- Hai chế độ:
  - **PM summary** (mặc định): dùng cho standup sáng, PM tổng hợp team.
  - **Chi tiết team** (tên kỹ thuật `dev-detail`, nhưng phạm vi là mọi vai trò trong roster trừ PM: DEV, QA, BrSE...): checkpoint cho PM + bảng tổng kết.
- Đầu vào: mã dự án (Jira), ngày hoạt động, chế độ, tùy chọn gửi lên Teams. Cần có Jira; Bitbucket (PR) và roster (danh sách thành viên: vai trò, % phân bổ, ngày vào/ra) là tốt nhưng thiếu roster vẫn làm được (roster suy từ người có hoạt động trong Jira; ghi banner "Thiếu roster").
- Dự án chỉ dùng GitHub: không có PR qua Bitbucket -> ghi "-" hoặc "không có dữ liệu SCM", không bịa PR.
- Múi giờ báo cáo: Asia/Ho_Chi_Minh; cửa sổ = 00:00:00 đến 23:59:59 của ngày hoạt động.

## Khái niệm cốt lõi (định nghĩa, thuật ngữ, vì sao quan trọng)
- **activity_date** = ngày dữ liệu; **standup_date** = activity_date + 1 ngày. Tiêu đề PM summary dùng standup_date ("Báo cáo Daily buổi sáng - {standup_date}"), phụ đề ghi "Hoạt động ngày {activity_date}"; tên file theo activity_date (`{dự án}-{activity_date}-summary.md`). Ví dụ: hoạt động 15/06 -> tiêu đề ghi 16/06/2026.
- **Ghi công theo người thực hiện (performer), không theo assignee hiện tại.** Nếu userb chuyển Resolved rồi giao lại cho usera: công "Resolved" thuộc userb; usera chỉ được dòng "Nhận assign KEY" nếu cần. Vì assignee chỉ là trạng thái hiện tại, không chứng minh ai đã làm.
- **Nguồn bằng chứng và người được ghi công**:

  | Bằng chứng | Ghi công cho | Ví dụ dòng |
  |---|---|---|
  | Chuyển status trong cửa sổ (lịch sử thay đổi) | tác giả thay đổi | "Resolved KEY" |
  | Chỉ đổi assignee | tác giả thay đổi, dưới assignee mới | "Nhận assign KEY" |
  | Worklog bắt đầu trong cửa sổ | tác giả worklog | "Log 3h trên KEY" |
  | PR mở / merge / comment / approve | người thực hiện hành động đó (dòng thời gian hoạt động PR), merger có thể khác tác giả PR | "Mở PR / Merge PR / Comment PR / Approve PR repo#id" |
  | Tạo issue trong cửa sổ | reporter | "Tạo KEY" |
  | Chỉ có `updated`, không có changelog/worklog/PR | KHÔNG ghi công (hoặc lấy changelog trước) | - |
- **Việc không phải giao hàng (non-delivery)**: họp, đồng bộ khách, quản lý dự án, vận hành deploy. Không đưa vào báo cáo PM/leader. Quy tắc khớp: chuỗi con không phân biệt hoa thường trong `summary` của ticket.

  | Nhóm | Summary chứa (bất kỳ) |
  |---|---|
  | Họp | `mtg`, `họp`, ` hop`, `hop `, `meeting` |
  | Trao đổi khách | `trao đổi`, `trao doi`, `trao đổi với`, `đồng bộ với kh`, `họp kh`, `customer sync`, `sync khách` |
  | PM/admin | `quản lý dự án`, `quan ly du an`, `project management`, `quản lý team` |
  | Deploy ops | `deploy`, `deployment`, `triển khai`, `trien khai`, `review code & deploy`, `đẩy code`, `release lên` - **chỉ khi loại issue khác Bug** |

  Ví dụ loại: "MTG cụm dự án ... Q2", "Họp hàng tuần ...", "review code & deploy", "trao đổi với khách hàng về spec". Ví dụ giữ: task giao hàng, bug (kể cả bug liên quan deploy), coding/QA/spec không có từ khóa quản trị. Áp dụng bằng **hai lớp bắt buộc**: (1) lọc lại kết quả sau mọi truy vấn, (2) khuyến nghị thêm điều kiện loại trừ vào truy vấn. Riêng **giờ worklog vẫn cộng đủ** vào tổng giờ của thành viên (trách nhiệm giải trình).
- **Stale (không cập nhật)**: N = max(0, ngày báo cáo - ngày của `updated`) theo múi giờ báo cáo. N = 0 -> "cập nhật trong ngày"; ngược lại "{N} ngày không cập nhật".
- **Blocker của công ty (J2)** vì Jira của công ty không có status "Blocked": task (không phải Bug) ở status `Confirmming` (chờ khách/xác nhận; đúng chính tả hai chữ m) HOẶC Bug có status khác Done; luôn loại `Rejected` và `Pending`. Đây là ảnh chụp **hiện tại**, không lọc theo ngày báo cáo; cột "Người" = assignee.
- **Clickable link**: mọi mã Jira và PR trong báo cáo là link Markdown `[KEY](url)` / `[repo#id](url)` với nhãn thường (không backtick, không in URL). URL lấy từ hệ thống, không được bịa tên miền; không biết URL thì in mã trơn.

## Cách làm từng bước (thủ công, đủ chi tiết để làm theo; kèm input/output)
1. **Xác định dự án và khoảng thời gian.** Input: mã dự án, ngày hoạt động (mặc định hôm qua), chế độ. Output: cửa sổ 00:00-23:59, activity_date, standup_date. Mã dự án chưa đăng ký -> đăng ký trước (không đoán).
2. **Lấy roster** (vai trò, % phân bổ, ngày bắt đầu/kết thúc). Tên vai trò thường gặp: LTV, PM, Tester, BrSE, TL, BOD, PQA, SDM (vai trò kỹ thuật như Backend/Frontend/Mobile không nằm trong roster). Lưu ý: ngày kết thúc phân bổ hết hạn **không** tự loại thành viên khỏi dự án - kiểm tay.
3. **Thu thập hoạt động Jira.**
   - J1: issue có `updated` trong cửa sổ.
   - J2: blocker theo định nghĩa trên (lọc lại non-delivery).
   - J3: ảnh chụp "In Progress".
   - Với mỗi issue có đổi status/đổi assignee/xuất hiện trong danh sách worklog của ngày: đọc lịch sử thay đổi. Nếu quá 50 issue: ưu tiên issue có chuyển trạng thái kết thúc (Done, Resolved, Deployed, Rejected), tổng tối đa 80.
   - **Worklog phải đầy đủ**: ứng viên = J1 hợp với tìm theo ngày worklog; đọc worklog của **mọi** ứng viên (không chọn tập con "ưu tiên"), giới hạn 200 issue có ghi "(truncated)". Bất kỳ issue nào có worklog bắt đầu trong cửa sổ đều phải xuất hiện.
4. **Thu thập hoạt động PR** (nếu có Bitbucket): tập ứng viên = PR MERGED có cập nhật trong cửa sổ + PR tạo trong cửa sổ + snapshot PR OPEN (bắt comment/approve trên PR đang chạy); tối đa 80 PR đọc dòng thời gian hoạt động (ghi "(PR activity truncated)" nếu cắt). Loại tài khoản bot (ví dụ bot review code) khỏi Phần 1; chỉ một dòng mỗi {người, repo, id, hành động}/ngày (nhiều comment -> "Comment PR repo#id (n comment)"). Trích mã Jira từ tiêu đề, mô tả, tên nhánh bằng mẫu `[A-Z][A-Z0-9_]+-\d+`. Luôn hỏi trạng thái MERGED và OPEN riêng (hỏi ALL có thể trả rỗng ở một số máy chủ).
5. **Ghép danh tính** giữa Jira - Bitbucket - roster: (1) email trùng chính xác (viết thường); (2) phần trước @ bỏ dấu chấm - độ tin cậy thấp; (3) chuẩn hóa tên bằng cách bỏ ký tự ngoài a-z0-9; (4) không khớp -> cờ `[IDENTITY_GAP]`. Kiểm tra PR-Jira: PR đã merge mà Jira vẫn In Progress -> cờ `[PR_JIRA_DRIFT]`.
6. **Chấm cờ rủi ro** (bảng R01-R11 ở dưới) và tính tỷ lệ tuân thủ worklog.
7. **Viết báo cáo** theo chế độ (xem Template). Kiểm tra câu chữ bằng câu hỏi: "Người chưa biết bối cảnh đọc câu này có hiểu ticket nào, vấn đề gì, cần làm gì không?".
8. **(Chỉ bản chi tiết team) Dựng các khối riêng**: Nhìn nhanh, 4 bảng checkpoint, Quy trình, Tổng kết nhanh, follow-up.
9. **Gửi Teams (tùy chọn)**: lưu file trước, rồi gửi nội dung qua webhook; nội dung cắt ở 25 000 ký tự thêm "...(truncated)". Không đưa địa chỉ webhook vào git. Thứ tự tìm webhook: tham số chỉ định > cấu hình dự án > cấu hình cũ > biến môi trường. Có thể báo lỗi dù tin vẫn vào kênh (máy chủ trả 202 "đã nhận") - kiểm tra kênh Teams.

### Chi tiết phần 4 bảng checkpoint của bản chi tiết team
Lọc lại non-delivery cho cả 4 bảng; luôn lấy `updated` để tính stale; sắp `duedate` tăng dần (bảng 4 sắp `resolved` giảm dần).
1. **Bug open**: loại = Bug và status thuộc {To Do, In Progress, Feedback, Resolved, Deployed, Confirmming}.
2. **Quá hạn**: `duedate` < ngày báo cáo và status thuộc allowlist {To Do, In Progress, Confirmming, Feedback, Resolved, Deployed}.
3. **Due 2 tuần tới**: `duedate` từ ngày báo cáo đến ngày báo cáo + 14, cùng allowlist. Ticket không có `duedate` phải được nêu rõ "no due date", không bỏ qua.
4. **Jira Task Done trong 10 ngày trước**: loại = Task, status hiện tại = Done, `resolved` >= ngày báo cáo - 10 ngày và < ngày báo cáo + 1 (ví dụ báo cáo 2026-09-08 -> từ 2026-08-29 đến trước 2026-09-09). Ưu tiên `resolved`; dự phòng "chuyển sang Done trong khoảng". **Không** dùng `updated` (comment/logwork trên ticket cũ đã Done gây dương tính giả) và không in changelog.
- Allowlist phải liệt kê tường minh; **không** dùng "status không thuộc Done/Rejected/Pending" vì nhóm "Done" của Jira vẫn có thể lộ Deployed/Resolved. Không bao giờ có Done, Rejected, Pending trong bảng 2-3.
- Cột: một cột `Jira / Status` (dòng 1 link KEY, dòng 2 status, nối bằng `<br>`, không xuống dòng thật), Due, Assignee, Summary. Stale: bảng 2 và 3 đặt trong ô Due (`{YYYY-MM-DD}<br>{stale}`); bảng 1 và 4 đặt ở dòng 3 của `Jira / Status`.

### Chi tiết phần "Quy trình" (thiếu logwork / thiếu origin estimate)
Không phải bảng; gom theo assignee hiện tại, chỉ là ảnh chụp trạng thái hiện tại, **không đọc changelog**, cùng cửa sổ `updated` trong 2 tháng lịch kết thúc ở ngày báo cáo (`updated` >= ngày báo cáo - 2 tháng và <= ngày báo cáo; ví dụ báo cáo 2026-09-08 -> từ 2026-07-08).
- **Danh sách 1 - chưa có logwork**: loại Bug hoặc Sub-task; status hiện tại thuộc {Done, Resolved, Deployed}; không có worklog (`timespent` rỗng; dự phòng đọc worklog thấy rỗng); áp loại trừ non-delivery. Không coi "0h trong ngày báo cáo" là thiếu nếu ticket có worklog trước đó.
- **Danh sách 2 - chưa có origin estimate**: mọi loại, mọi status; có worklog (`timespent` > 0 - không dùng "không rỗng" vì `0m` không có dòng worklog vẫn bị coi là không rỗng); Original Estimate rỗng hoặc bằng 0/0h (ticket có estimate > 0 thì loại); **không** áp loại trừ non-delivery (họp/admin/deploy vẫn nằm trong danh sách này).
- Hiển thị: tiêu đề `### {Tên} ({n})` (n = số mã duy nhất của hợp hai danh sách), dưới đó các dòng "Chưa có logwork: ..." và "Chưa có origin estimate: ..." (bỏ dòng rỗng). Nhóm sắp giảm dần theo số ticket, "Unassigned" cuối. Cả hai rỗng -> "**Không có.**". Giới hạn 200 mỗi danh sách với "(truncated)".
- Vai trò PM: **nhắc thành viên** logwork/điền estimate; PM không tự sửa Jira.

## Công thức, ngưỡng & tín hiệu (bảng: tên | công thức/điều kiện | ngưỡng | hành động khi vượt)
| Mã | Mức | Tag | Điều kiện | Ghi chú/hành động |
|---|---|---|---|---|
| R01 | 🔴 | GHOST | thành viên roster có phân bổ >= 10%, không có hoạt động Jira và không có Bitbucket trong cửa sổ | xác nhận có đang làm việc không |
| R02 | 🔴 | BUS_FACTOR | một người >= 70% số PR merged + cập nhật Jira (cuộn 7 ngày) | chia việc/pair (ngưỡng mặc định `single_contributor_threshold` = 0.70) |
| R03 | 🟡 | WORKLOG_GAP | có PR/commit nhưng 0 worklog hôm qua | nhắc log giờ |
| R04 | 🟡 | WORKLOG_TEAM | tỷ lệ tuân thủ worklog của team < 50% | nhắc cả team |
| R05 | 🔴 | ALLOCATION_EXPIRED | ngày kết thúc phân bổ (roster) < hôm nay mà vẫn hoạt động | cập nhật phân bổ |
| R06 | 🟡 | PR_JIRA_DRIFT | PR đã merge mà Jira liên kết không thuộc {Done, Resolved, Deployed} | đồng bộ Jira |
| R07 | 🟡 | STALE_PR | PR OPEN không hoạt động > 24h | nhắc review |
| R08 | 🟡 | BLOCKER_AGING | ticket blocker J2 (Confirmming không phải Bug, hoặc bug mở) không đổi > 2 ngày làm việc | follow-up |
| R09 | 🟡 | UNASSIGNED_WIP | ticket In Progress không có assignee | giao người |
| R10 | 🟡 | IDENTITY_GAP | người dùng Bitbucket/Jira không ghép được với roster | bổ sung ánh xạ |
| R11 | 🟡 | OVERALLOCATED | tổng phân bổ qua các dự án > 100% (nhiều dự án) | điều chỉnh |

| Chỉ số | Công thức | Ngưỡng |
|---|---|---|
| Tuân thủ worklog | active_people = số người có hoạt động Jira hoặc Bitbucket trong cửa sổ; logged_people = số người có worklog_hours >= `worklog_minimum_hours` (mặc định 0.5); compliance = logged_people / active_people x 100 | R04: < 50% |
| Cửa sổ Quy trình | `updated` trong 2 tháng lịch đến ngày báo cáo | - |
| Bảng "Done 10 ngày" | `resolved` trong [ngày báo cáo - 10, ngày báo cáo] | - |
| Số ngày stale | max(0, ngày báo cáo - ngày `updated`) | N = 0 -> "cập nhật trong ngày" |
| Giới hạn hiển thị | Phần 1: tối đa 8 người hoạt động nhiều nhất (phần còn lại gộp 1 dòng "không hoạt động"); tối đa 3-5 bullet/người; Phần 2: tối đa 15 dòng + "(+N more)"; Nhìn nhanh: tối đa 15 mã Task Done rồi "(+N)"; Follow-up 1-5 mục | - |

## Template / mẫu đầu ra (rút gọn, giữ cấu trúc và các cột/trường)
**A. PM summary**
```
# Báo cáo Daily buổi sáng - {standup_DD/MM/YYYY} ({tên dự án})
> Hoạt động ngày {activity_DD/MM/YYYY} | Jira + Bitbucket + roster | TZ: Asia/Ho_Chi_Minh
## 1. Hôm qua đã làm gì
### {Tên} - {Vai trò} ({phân bổ}%)
- [{DỰ ÁN}] {động từ} [KEY](url) / Mở|Merge|Comment|Approve PR [repo#id](url) {bằng chứng}
**Không có hoạt động ghi nhận:** {tên hoặc "Không"}
## 2. Còn block / vướng mắc ở đâu không?
| Người | Issue | Trạng thái | Mô tả ngắn |   (Mô tả ngắn: tiếng Việt tự nhiên, <= ~15 từ; ai chờ gì)
**PR đang chờ review > 24h:** [repo#id] - tác giả - reviewer - {giờ}h
(Nếu J2 rỗng: "Không có ticket Confirmming (non-bug) hoặc bug chưa Done. N PR đang mở...")
## 3. Có rủi ro nào team cần thảo luận không?
| Mức | Rủi ro | Chi tiết | Đề xuất hành động |   (🔴/🟡; Chi tiết = sự kiện + hệ quả có link; Đề xuất = 1 việc cụ thể)
## Red Flags (tự động)  - [GHOST]/[BUS_FACTOR]/[WORKLOG]/[ALLOCATION]/[PROCESS]/[DATA] ...
**Số liệu nhanh:** {active}/{total} active | {pr_opened} PR opened | {pr_merged} PR merged | {pr_review_actions} PR comment+approve | {jira_updates} issues updated | {compliance}% worklog
```
Sắp xếp Phần 2: `Confirmming` trước, sau đó bug theo priority giảm dần.

**B. Chi tiết team**
```
# Báo cáo chi tiết team - {DD/MM/YYYY} ({dự án})
## Nhìn nhanh
- Bug open: n; Quá hạn: n (Confirmming / chờ KH: n; không assignee: n); Due 2 tuần tới: n
- Jira Task Done trong 10 ngày trước: [KEY], ... (hoặc "Không có.")
- Quy trình: n ticket (chưa logwork n1; chưa origin estimate n2) - {assignee}: {count}, ...
- Member nên nhắc: {tên} - {lý do ngắn}. PM nhắc member dọn Jira / logwork; PM không tự chuyển status.
## Điểm cần nhìn cho PM   (4 bảng: | Jira / Status | Due | Assignee | Summary |)
## Quy trình              (### {Tên} ({n}) - Chưa có logwork: ... - Chưa có origin estimate: ...)
## Tổng kết nhanh
| Member | Role | Tasks (worklog) | Worklog | PR merged | PR open | Bug open |
**Rủi ro cần follow-up:** 1. [KEY] - {vấn đề}. {PM nhắc ...}.
```
Quy tắc bảng tổng kết: mỗi thành viên roster **trừ vai trò PM** (kể cả người 0 hoạt động) một dòng; Tasks = mã có worklog trong cửa sổ, đã loại non-delivery, "-" nếu không có; Worklog = tổng giờ; PR merged = PR **do thành viên tạo** và merge trong cửa sổ; PR open = PR do thành viên tạo, trạng thái OPEN tại thời điểm chạy (không lọc ngày); luôn ghi `{repo}#{id}` (không bao giờ chỉ `#id` khi dự án có > 1 repo); Bug open = mã bug từ bảng Bug open có assignee là thành viên. **Không** in tường thuật từng người (Nội dung task, Cause, How fixed), không in ghi chú nguồn dữ liệu, không liệt kê file thay đổi.

## Lỗi thường gặp & lesson learned (lấy từ nguồn, mỗi ý: sai gì -> hậu quả -> cách tránh)
- Ghi công theo assignee -> ghi sai người (ví dụ người đã Resolved rồi giao lại) -> đọc lịch sử thay đổi, ghi công cho tác giả thay đổi.
- Ghi "Merge PR" cho tác giả PR khi người merge là người khác -> sai công -> lấy người thực hiện từ dòng thời gian hoạt động PR.
- Chỉ lấy tập con ticket khi đọc worklog -> bỏ sót giờ làm -> đọc worklog của mọi ứng viên.
- Dùng "worklog không rỗng" để xác định có worklog -> `0m` bị tính nhầm -> dùng `timespent` > 0 và lọc bỏ worklog rỗng (sửa ở v1.18.1).
- Dùng `updated` để tìm Task Done gần đây -> ticket cũ có comment mới bị tính -> dùng `resolved`.
- Dùng "không thuộc Done/Rejected/Pending" -> lộ Deployed/Resolved -> allowlist tường minh.
- Đưa Rejected/Pending hoặc backlog "In Progress" chung chung vào Phần 2 -> nhiễu -> chỉ dùng điều kiện J2.
- Mã Jira bọc backtick trong link (`` [`KEY`](url) ``) hoặc in URL trần -> xem trước Markdown hiện URL thô, hỏng link -> nhãn thường `[KEY](url)`.
- Văn phong hành chính khó hiểu: `close wave`, `handoff`, `bàn giao test từ ...`, `bandwidth`, `snapshot`, `drift`, `bus factor` (trong văn xuôi) -> người đọc phải đoán -> viết lại bằng ngôn ngữ thường ("PR đã merge nhưng Jira chưa Done", "tại thời điểm báo cáo"). Thẻ Red Flag như `[BUS_FACTOR]` thì được.
- Nối hai ticket không liên quan trong một câu chỉ vì cùng người hoặc cùng ngày đóng -> tạo quan hệ giả -> chỉ nối khi có bằng chứng Jira: cha/con (sub-task), `blocks`, cùng epic đã nêu. Mỗi ticket một bullet rủi ro riêng.
- Đưa ticket đã Done vào follow-up rủi ro (chụp giữa ngày) -> rủi ro giả -> chỉ ticket còn mở.
- Chạy `state: ALL` lấy PR trên một số máy chủ -> rỗng -> hỏi MERGED và OPEN riêng.
- Tìm dự án trong roster chỉ bằng tên -> có thể ra dự án không liên quan -> luôn xác minh bằng trường mã dự án (code).
- Đưa thông tin thật (khóa dự án, tên người, mã roster, tên repo, webhook) vào tài liệu dùng chung hoặc git -> lộ dữ liệu -> chỉ dùng placeholder (PROJA, usera); dữ liệu thật để ở cấu hình cục bộ, không commit.
- Tìm status "Blocked" trong Jira của công ty -> không có status này nên Phần 2 trống sai -> dùng định nghĩa J2.
- Ngày kết thúc phân bổ trong roster hết hạn không tự loại thành viên khỏi dự án -> kiểm tay (cờ R05).

## Ví dụ minh họa (1 ví dụ ngắn có số, lấy hoặc dựng từ nguồn; nếu dựng thì ghi "(ví dụ dựng)")
Từ ví dụ mẫu trong nguồn (dữ liệu giả, PROJA, hoạt động 04/06 -> tiêu đề 05/06/2026):
- Phần 1: usera merge 4 PR (ví dụ 121, 122, 123, 120); userc tạo 4 bug (PROJA-344..347); 4 người không có hoạt động ghi nhận.
- Phần 2: PROJA-340 (Confirmming - chờ khách xác nhận spec), PROJA-346 và PROJA-347 (bug chưa Done). Task `To Do` không phải bug **không** vào bảng; Pending/Rejected không bao giờ vào.
- Phần 3: 🔴 bus factor - usera = 80% PR merged (8/10 commit, 4/5 PR); 🟡 worklog - 1/4 thành viên active có worklog (25%) (thấp hơn 50% nên đúng R04); 🟡 ghost - userd được giao 4 bug, 0 commit/PR.
- Số liệu nhanh: 3/12 active | 4 PR merged | 8 issues updated | 25% worklog.
Ví dụ viết câu rủi ro:
- Sai: `PROJA-200` - Due 23/06; cần bàn giao test từ close wave PROJA-150.
- Đúng: [PROJA-200] - Due 23/06, userc chưa có worklog; PM confirm lịch test trước deadline. Và: [PROJA-180] - Confirmming quá due 17/06; PM follow-up khách hàng xác nhận.

## Tự kiểm tra (3-5 câu hỏi có đáp án ngắn ngay dưới, dựa trên chính nội dung bài)
1. Hoạt động ngày 15/06, tiêu đề PM summary ghi ngày nào và tên file theo ngày nào?
   - Tiêu đề ghi 16/06/2026 (activity_date + 1); tên file theo 15/06.
2. Một ticket được userb Resolved rồi giao lại cho usera, hôm qua ai được ghi công "Resolved"?
   - userb (tác giả thay đổi trong changelog); usera chỉ có thể có "Nhận assign".
3. Điều kiện nào khiến ticket vào Phần 2 (blocker)?
   - Không phải Bug + status Confirmming, hoặc Bug + status khác Done; loại Rejected và Pending.
4. Ticket có 3h worklog nhưng chưa có Original Estimate nằm ở danh sách nào của "Quy trình", và có bị lọc non-delivery không?
   - Danh sách 2 (chưa có origin estimate); không bị lọc non-delivery.
5. Điều kiện R02 và R04 là gì?
   - R02: một người >= 70% PR merged + cập nhật Jira (cuộn 7 ngày). R04: tuân thủ worklog của team < 50%.

## Liên quan (bài trước/sau trong quy trình, tên thư mục skill khác)
- Bài trước/cùng nguồn: Daily sync (Ch4·01) (snapshot nhanh trước standup); cả hai dùng lại bộ luật loại trừ non-delivery và ghi công.
- Dự án cần đăng ký trước: Thiết lập PM (Ch1·03).
- Sau đó: Status tuần (Ch7·01), Giao tiếp stakeholder (Ch7·03).
- Nguồn chưa rõ / mâu thuẫn:
  - Ví dụ mẫu (PROJB) gắn [GHOST] cho thành viên phân bổ 5% và [DATA] cho 1%, trong khi luật R01 nói phân bổ >= 10% mới tính GHOST (ví dụ có thể cũ hơn luật).
  - Ví dụ mẫu dùng "8/10 commit" trong bus factor trong khi luật cho biết commit theo nhánh nằm ngoài phạm vi báo cáo.
  - Bảng non-delivery trong tài liệu tham chiếu ngắn hơn bảng chuẩn (bảng chuẩn ở đây lấy từ bước Jira); nếu lệch, dùng bảng đầy đủ.
  - Luật về "{stale}" ở bảng 2-3 vs bảng 1+4 do nhiều lần sửa (v1.17.2); dùng quy tắc hiện hành ở trên.
  - Nguồn đề cập phiên bản 1.18.1; công cụ đọc PR ở đây (có thông tin người merge) khác công cụ ở bài Daily sync (Ch4·01) (không có), nên mức chi tiết PR khác nhau giữa hai bài.
