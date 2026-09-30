---
title: Thiết lập registry dự án (mã Jira, Bitbucket, ksystem)
source: Thiết lập PM (Ch1·03)
stage: Initiation
level: cơ bản
prerequisites: []
---
# Thiết lập registry dự án: một lần cho mỗi dự án

## Mục tiêu học xong bạn làm được gì
- Biết một dự án cần "đăng ký" những định danh nào (Jira, Bitbucket, mã dự án trong hệ thống quản lý nhân sự/dự án ksystem) để các báo cáo và theo dõi sau này dùng chung.
- Chuẩn hóa mã dự án đúng quy ước và xử lý đúng khi dự án đã có hoặc chưa có bản ghi.
- Giữ an toàn thông tin cấu hình (webhook, quyền file).

## Khi nào dùng (thời điểm, ai kích hoạt, điều kiện đầu vào)
- Khi khởi tạo một dự án mới ("setup dự án", "cấu hình dự án mới", "chưa có config cho dự án này"), hoặc khi cần cập nhật định danh của dự án đã có. Chỉ làm một lần cho mỗi dự án; sau đó mọi báo cáo/theo dõi dùng lại.
- PM kích hoạt. Đầu vào: mã hoặc tên dự án; PM biết Jira project key và Bitbucket project key.
- Việc này KHÔNG bao gồm: tạo Jira project, tạo repo Bitbucket, sửa dữ liệu trên ksystem, hay đưa file cấu hình vào git.

## Khái niệm cốt lõi (định nghĩa, thuật ngữ, vì sao quan trọng)
- **Registry (sổ đăng ký dự án)**: một file cấu hình chung (`projects.yaml`, thư mục cấu hình riêng của người dùng) lưu định danh từng dự án. Có thể đổi vị trí bằng biến môi trường. Tự tạo lần đầu khi ghi; PM không phải tạo tay.
- Ba trường bắt buộc: `jira_key`, `bitbucket_project_key`, `ksystem_project_code`.
- Trường tùy chọn: `name` (tên hiển thị, tự lấy từ ksystem, có thể ghi đè), `bitbucket_repos` (danh sách repo cụ thể; để trống = tự khám phá theo project key), `teams_webhook_url` (địa chỉ nhận thông báo Microsoft Teams), `docs_root` (thư mục tài liệu cục bộ).
- Quy ước mã: ksystem thường có dấu gạch dưới (ví dụ `PROJA_01`); Jira thường không có (ví dụ `PROJA`); mã Bitbucket thường là tiền tố ngắn (ví dụ `PRJA`). Khóa trong registry = mã dự án viết hoa, bỏ khoảng trắng.
- Vì sao quan trọng: nhiều hoạt động quản lý (báo cáo ngày, báo cáo tuần, giám sát tín hiệu, công số thực tế) cần biết dự án nằm ở đâu trên từng hệ thống; một nơi đăng ký duy nhất tránh nhập lặp và nhập sai (giải thích thêm).

## Cách làm từng bước (thủ công, đủ chi tiết để làm theo; kèm input/output)
1. **Xác định dự án**: lấy mã từ chính câu yêu cầu, hoặc từ ngữ cảnh đang làm việc, không rõ thì hỏi. Chuẩn hóa: bỏ khoảng trắng, viết hoa (`proja` -> `PROJA`).
2. **Tra cứu ksystem**: tìm theo tên/mã dự án. Nhiều kết quả thì chọn một; không thấy thì thử biến thể có/không có gạch dưới (`PROJA` <-> `PROJA_01`); vẫn không thấy thì ghi nhận "không tìm thấy" và tự nhập ở bước sau. Lấy: `code` -> `ksystem_project_code`, `name` -> `name`; các thông tin khác (phòng ban, loại Project Base / Labor / Nội bộ, ngày bắt đầu/kết thúc, PM) chỉ để đối chiếu, không lưu. Cho PM xem lại mã, tên, loại, thời gian, PM và xác nhận.
3. **Kiểm tra đã đăng ký chưa**: nếu khóa đã tồn tại thì chế độ CẬP NHẬT (hiển thị giá trị hiện có, chỉ đổi trường PM sửa, để trống là giữ nguyên); chưa có thì chế độ TẠO MỚI.
4. **Thu thập trường còn thiếu** (chỉ hỏi cái chưa có): nhóm bắt buộc hỏi cùng lúc (Jira project key; Bitbucket project key; mã ksystem chỉ hỏi nếu tra cứu không ra); nhóm tùy chọn hỏi một lần (repo cụ thể, phân tách bằng dấu phẩy; Teams webhook; thư mục tài liệu cục bộ). Bỏ trống repo -> danh sách rỗng (tự khám phá); bỏ trống webhook/docs_root -> không lưu trường đó.
5. **Xác nhận trước khi ghi**: hiện bản xem trước toàn bộ, webhook che thành `***`, repo rỗng ghi "(auto-discover)". PM từ chối thì hủy, không ghi gì.
6. **Ghi (upsert)**: hợp nhất vào registry. Thiếu trường bắt buộc hoặc JSON lỗi thì quay lại bước 4 để nhập lại.
7. **Kiểm tra sau khi ghi**: đọc lại bản ghi, đủ 3 trường bắt buộc; nếu báo không tìm thấy thì kiểm tra quyền file. Không in webhook ra màn hình.

Lệnh của công cụ hỗ trợ (nếu dùng): `list` (liệt kê khóa), `get` (đọc một bản ghi), `exists` (mã thoát 0 = có, 1 = không), `upsert` (ghi/hợp nhất từ JSON), `path` (in đường dẫn file).

## Công thức, ngưỡng & tín hiệu (bảng: tên | công thức/điều kiện | ngưỡng | hành động khi vượt)
Không có công thức/ngưỡng chất lượng. Các quy tắc cứng:
| Quy tắc | Điều kiện | Hành động |
|---|---|---|
| Trường bắt buộc | jira_key, bitbucket_project_key, ksystem_project_code | Thiếu -> ghi bị từ chối |
| Không bịa key | Không chắc Jira/Bitbucket key | Luôn hỏi PM |
| Không commit | projects.yaml, teams_webhook_url | Không đưa vào git |
| Quyền file | Sau mỗi lần ghi | Tự đặt quyền `600` |

Giá trị mặc định trong công cụ (nguồn công cụ, không phải quy trình): múi giờ báo cáo `Asia/Ho_Chi_Minh`; tối thiểu worklog `0.5` giờ; ngưỡng một người đóng góp chiếm `0.70` (nguồn chưa rõ ý nghĩa nghiệp vụ chi tiết).

## Template / mẫu đầu ra (rút gọn, giữ cấu trúc và các cột/trường)
```
registry_key: PROJA            # mã viết hoa
name: <tên hiển thị>            # từ ksystem, có thể ghi đè
jira_key: <PROJA>               # bắt buộc
bitbucket_project_key: <PRJA>   # bắt buộc
ksystem_project_code: <PROJA_01># bắt buộc
bitbucket_repos: []             # [] = tự khám phá
teams_webhook_url: <ẩn>         # tùy chọn, bỏ trống thì không lưu
docs_root: <đường dẫn thư mục>  # tùy chọn
```
Checklist xong việc: bản ghi có đủ 3 trường bắt buộc; đúng file đăng ký; webhook không lộ; gợi ý bước tiếp theo phù hợp trạng thái dự án (mới hay đang chạy).

## Lỗi thường gặp & lesson learned (lấy từ nguồn, mỗi ý: sai gì -> hậu quả -> cách tránh)
- Đoán Jira key / Bitbucket key -> báo cáo trỏ nhầm hệ thống -> luôn hỏi PM.
- Nhầm dạng mã (có/không gạch dưới) giữa ksystem và Jira -> không tra cứu được -> thử cả hai dạng, PM xác nhận mã Jira ở bước nhập.
- Commit file registry hoặc webhook vào git -> lộ địa chỉ nhận thông báo -> không commit; quyền file 600.
- Hiện webhook rõ khi xem trước -> lộ bí mật -> che `***`.
- Ghi đè cả bản ghi khi cập nhật -> mất giá trị cũ -> để trống là giữ nguyên.

## Ví dụ minh họa (1 ví dụ ngắn có số, lấy hoặc dựng từ nguồn; nếu dựng thì ghi "(ví dụ dựng)")
(ví dụ dựng theo mẫu nguồn) PM nhập `proja` -> chuẩn hóa `PROJA`. ksystem trả `PROJA_01`, "Project Alpha Phase 2", loại Labor, 2026-06-01 -> 2026-09-30. PM nhập Jira `PROJA`, Bitbucket `PRJA`, repo `proja-backend, proja-frontend` -> lưu `["proja-backend","proja-frontend"]`, bỏ trống webhook. Bản ghi cuối có đủ 3 trường bắt buộc.

Trạng thái sau đăng ký (theo nguồn): các hoạt động dùng ngay được: báo cáo ngày, đồng bộ ngày, báo cáo tuần, giám sát tín hiệu, công số thực tế. Cần thêm tài liệu trước: lập lịch (cần WBS + danh sách task), phân tích chênh lệch công số mức task (cần lịch).

## Tự kiểm tra (3-5 câu hỏi có đáp án ngắn ngay dưới, dựa trên chính nội dung bài)
1. Ba trường bắt buộc? -> jira_key, bitbucket_project_key, ksystem_project_code.
2. Bỏ trống danh sách repo thì sao? -> Lưu rỗng và tự khám phá repo theo project key.
3. Khi dự án đã có trong registry, làm gì? -> Chế độ cập nhật: hiển thị giá trị hiện có, để trống = giữ nguyên.
4. Hai điều KHÔNG được làm với cấu hình? -> Không commit registry/webhook vào git; không tự đoán Jira/Bitbucket key.
5. Quyền file registry sau khi ghi? -> 600.

## Liên quan (bài trước/sau trong quy trình, tên thư mục skill khác)
- Sau: Kickoff (Ch2·01) (charter và risk seed), rồi WBS, Lập schedule (Ch3·03); các skill báo cáo hàng ngày/tuần và theo dõi tín hiệu dùng registry này (Daily report (Ch4·02), Daily sync (Ch4·01), Status tuần (Ch7·01), Tín hiệu (Ch6·01), Effort actuals (Ch6·03)).
