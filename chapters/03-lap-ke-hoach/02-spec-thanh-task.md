---
title: Từ spec sang danh sách task (sinh task và bắt thay đổi tài liệu)
source: Spec thành task (Ch3·02)
stage: Planning
level: trung bình
prerequisites: [Ch2·03, Ch3·01]
---
# Từ spec sang danh sách task (sinh task và bắt thay đổi tài liệu)

## Mục tiêu học xong bạn làm được gì
- Từ SRS và basic design (thiết kế cơ bản) dựng được danh sách task đầy đủ theo 4 track: Dev, Test/QA, PM, Common.
- Áp dụng "Iron Law": mỗi task hoàn thành được trong không quá 1 man-day (md), biết cách tách nhỏ theo từng công đoạn.
- Đặt ID task, mô tả nguồn, dependency đúng chuẩn để truy vết và đo chất lượng theo function.
- Khi tài liệu đổi, so sánh phiên bản để sinh task delta và gắn tag rework / spec-change, từ đó nuôi các tín hiệu chất lượng.

## Khi nào dùng (thời điểm, ai kích hoạt, điều kiện đầu vào)
- Thời điểm: sau khi spec đã được sign-off (xem Chốt spec, Ch2·03); lại dùng mỗi khi spec thay đổi lớn hoặc có change request lớn (chế độ diff).
- Người kích hoạt: PM.
- File đầu vào bắt buộc: bảng feature `F-<PROJ>-<MOD>-NN` trong SRS §4; use case (SRS use-cases); chỉ mục màn hình (module + danh sách screen); các file màn hình `SCR-<PROJ>-*` với section đánh số §1-10.
- Tùy chọn: db-design (tác vụ schema), api-detail (tác vụ API binding).
- Tài liệu phải bám template chuẩn: SRS có bảng feature (id, tên, priority, mô tả, UC refs) + phân pha triển khai; screen có heading section đánh số cố định §1-10; db-design và api-detail có anchor ổn định. Không bám template (thiếu function ID hoặc heading) thì liệt kê chỗ lỗi và cảnh báo, không đoán.
- Chế độ `diff` chỉ chạy khi đã có danh sách task cũ kèm `spec_version` (ghi commit/phiên bản spec lúc sinh).

## Khái niệm cốt lõi (định nghĩa, thuật ngữ, vì sao quan trọng)
| Khái niệm | Vai trò |
|---|---|
| Function | `F-<PROJ>-<MOD>-NN`; đơn vị đo chất lượng |
| Module | Nhóm function/cluster; đơn vị lập lịch, gate, release |
| Stage | Công đoạn vòng đời; quyết định tín hiệu nào được nuôi |

4 track và mã công đoạn:
- **Dev** (theo function): `REQ` -> `BD` -> `DEV` -> `UT`.
- **Test/QA** (theo module): `TP` -> `TVP` -> `TC` -> `TE` -> `BV` -> `TR`.
  - `TVP` + `TC` nuôi QS-TST-09, QS-REQ-03 và đầu vào cho Inspector; `BV` nuôi QS-TST-08; `TR` nuôi QS-TST-02/04. Track PM nuôi QS-PRC-06/08, QS-PRC-02 và việc đánh giá gate.
- **PM** (theo template quy trình): `PM-KICKOFF`, `PM-PLAN`, `PM-TRACK`, `PM-GATE`, `PM-CLIENT`, `PM-RETRO`, `PM-OTHER`.
- **Common**: `COMM`.
- Vì sao có: logic sinh task một chỗ, chuẩn ở template tài liệu (đồng nhất); `function + stage` cho phép đo chất lượng một function qua mọi công đoạn (đo được); so sánh tài liệu cho ra delta và tag để có tín hiệu rework/churn gần như miễn phí (bắt thay đổi).
- Chú ý: "Est" (ước lượng) do PM điền, không do người sinh danh sách điền.

## Cách làm từng bước (thủ công, đủ chi tiết để làm theo; kèm input/output)
1. **Kiểm tra tài liệu.** Đủ các file bắt buộc chưa; có đúng template không. Trích: danh sách function (id, priority, phase, UC refs), module/cluster và số screen mỗi module.
2. **Xác thực.** Mọi feature ID đúng định dạng `F-<PROJ>-<MOD>-NN`? Heading section screen đọc được? Xác định được quan hệ screen <-> function qua tham chiếu chéo trong tài liệu? Không xác định được thì liệt kê để PM nối tay, không gán bừa. Phase trong SRS mâu thuẫn với module trong chỉ mục màn hình -> dừng và hỏi, không tự hòa giải. Nếu spec chỉ tới mức epic/module (không có chi tiết feature) thì ghi rõ task ở mức Module-level ("đo Module-level"), không ép xuống mức function.
3. **Quy đổi section thành task (Dev):**

| Nguồn (section) | Task sinh ra | Stage |
|---|---|---|
| SRS §4 feature + UC flow | Chốt AC + UC flow `{function}` | REQ |
| Screen §1-4 (Wireframe/Header/Actions/Tabs) | Thiết kế UI `{screen}` | BD |
| Screen §6 Data Source + api-detail | API/data binding `{screen}` | BD, DEV |
| Screen §7 Interactions | Implement tương tác `{screen}` | DEV |
| db-design (bảng liên quan) | Schema/migration `{function}` | BD, DEV |
| AC (từ REQ) | Unit test theo AC `{function}` | UT |

4. **Quy đổi cho Test/QA (theo module):**

| Nguồn | Task | Stage |
|---|---|---|
| Scope/lịch/môi trường/tiêu chí pass | Test Plan `{module}` | TP |
| AC + UC + screen §8 Lock + §9 Edge | Test Viewpoint `{module}` | TVP |
| Viewpoint + AC | Tạo & review testcase `{module}` | TC |
| Testcase | Thực thi e2e/manual `{module}` | TE |
| Bug từ TE | Verify bug `{module}` | BV |
| TE + BV + screen §10 Performance | Test Report `{module}` | TR |

5. **Thêm task PM/COMM** từ template quy trình (không đọc từ tài liệu thiết kế; số lượng co giãn theo số module):

| Task | Mã | Mức | Số lượng |
|---|---|---|---|
| Kickoff dự án | PM-KICKOFF | project | 1 |
| Plan + WBS + schedule | PM-PLAN | project | 1 |
| Theo dõi tiến độ + risk/issue | PM-TRACK | per module | = số module |
| Review gate G1-G5 | PM-GATE | per module | = số module |
| Báo cáo client + scope/resource | PM-CLIENT | project | 1 |
| Retrospective | PM-RETRO | per module | = số module |
| Mở rộng | PM-OTHER | project | tùy PM |
| Communication | COMM | project | 1 |

6. **Đặt dependency ("Depends on"):** Dev: `BD` phụ thuộc `REQ`, `DEV` phụ thuộc `BD`, `UT` phụ thuộc `DEV`. Test: `TVP` <- `TP`, `TC` <- `TVP`, `TE` <- `TC` + mọi `DEV` của module, `BV` <- `TE`, `TR` <- `BV`. PM: `PM-GATE` <- DEV + test của module; `PM-TRACK` chạy xuyên suốt.
7. **Tách nhỏ theo Iron Law** (bảng ở phần công thức). Parent `T-001` -> sub `T-001.1`, `T-001.2`. Không tách được thì cảnh báo và gợi ý viết lại task.
8. **Ghi bảng task** theo schema (dưới) + khối metadata. Nguyên tắc: Est để trống, Status mặc định `TODO`; không bịa AC/Est/dependency - thiếu thì để trống và ghi `⚠ cần PM`.
9. **Idempotent:** chạy lại vẫn theo Task ID; chỉ thêm task mới, giữ nguyên Est/Status PM đã điền.
10. **Chế độ diff (khi tài liệu đổi):** đọc `spec_version` cũ; so sánh tài liệu SRS/basic design giữa phiên bản cũ và hiện tại để tìm section đổi; phân loại:
   - Section/function **mới** -> bó task mới, tag `new`.
   - Section **đổi** -> rework, tag `spec-change` -> nuôi QS-REQ-01, QS-PRC-07.
   - §6/§7 đổi sau khi DEV đã in-progress/done -> tag `design-change-after-coding` -> nuôi QS-DSG-03, E3.
   - Section **xóa** -> tag `deprecated` (không xóa cứng, để audit).
   Nối thêm delta (giữ task cũ, Est/Status), cập nhật `spec_version`, và lập **Impact summary**: function bị đụng, tín hiệu được nuôi, số lượng rework/new/deprecated.

## Công thức, ngưỡng & tín hiệu
Iron Law (Q4.2): mỗi task phải hoàn thành trong <= 1md; ước lượng > 1md thì bắt buộc tách (no carry-over).

| Stage | md mặc định | Cách tách khi cần |
|---|---|---|
| REQ chốt AC | 0.5 | Theo từng AC |
| BD | S=0.5, M=1, L=1.5 | L nhiều state -> tách theo state |
| DEV | S=0.5, M=1, L=1.5 | Theo API / theo component |
| UT | 0.5 | Theo function class |
| TC | 0.5-1 | Theo nhóm test scenario |
| TE | 0.5-1 | Theo mỗi vòng trên mỗi module |

| Tag | Điều kiện | Tín hiệu nuôi |
|---|---|---|
| new | Section/function mới | — |
| rework / spec-change | Section đổi | QS-REQ-01, QS-PRC-07 |
| design-change-after-coding | §6/§7 đổi sau khi DEV in-progress/done | QS-DSG-03, E3 |
| deprecated | Section bị xóa | — (không xóa cứng) |

(nguồn chưa rõ: L với BD/DEV = 1.5md nhưng Iron Law nói <= 1md; nguồn ngầm hiểu tách tiếp, không nêu tiêu chí S/M/L.)

## Template / mẫu đầu ra (rút gọn, giữ cấu trúc và các cột/trường)
Schema bảng task:
```
| ID | Function | Module | Stage | Title | Description | Source | AC | Depends on | Est | Status | Tags |
```
- ID: `{function}-{STAGE}-{NN}`, ví dụ `F-KM-REL-04-DEV-01`.
- Source: `doc-path#anchor @doc-version` (commit ngắn lúc sinh).
- Description: trích/tóm tắt section nguồn, không bịa.
- AC: tham chiếu AC; thiếu thì để trống + `⚠ cần PM`.
- Tags: `new` / `rework` / `spec-change` / `design-change-after-coding` / `deprecated`.

Khối metadata đầu file: `spec_version` (commit ngắn), `generated_at` (ngày), `source_docs` (srs/, basic_design/).

Các mục cuối: "Dev track - Function X", "Test track - Module Y", "PM track", rồi checklist "cần PM" (ví dụ Screen không map function; AC trống trên task REQ) và "giả định" (ví dụ số task PM = số module).

Checklist trước khi giao: metadata `spec_version` đúng; mọi function có chuỗi REQ->UT (hoặc ghi rõ lý do bỏ); mọi module có chuỗi TP->TR; không task nào > 1md chưa tách; Est còn trống để PM điền trước khi lập lịch; chế độ diff có Impact summary + tag đúng.

## Lỗi thường gặp & lesson learned (lấy từ nguồn, mỗi ý: sai gì -> hậu quả -> cách tránh)
- Đoán khi tài liệu thiếu/lệch template -> task sai gốc -> dừng, liệt kê chỗ lỗi, yêu cầu hoàn thiện tài liệu.
- Gán bừa screen cho function khi không có tham chiếu chéo -> task sai chủ -> liệt kê để PM nối tay.
- Tự hòa giải mâu thuẫn phase (SRS) vs module (screen index) -> sai lịch/gate -> dừng và hỏi.
- Ép task xuống function-level khi spec chỉ tới epic/module -> số liệu đo sai -> ghi rõ Module-level.
- Task > 1md không tách -> khó theo dõi, trễ dồn -> tách sub-task.
- Bịa AC, Est hoặc dependency -> lập lịch/đo lường sai -> để trống và ghi `⚠ cần PM`.
- Xóa cứng task của section đã bị bỏ -> mất dấu vết audit -> gắn `deprecated`.
- Chạy lại sinh task mà ghi đè Est/Status PM đã điền -> mất công PM -> chạy idempotent theo Task ID.
- Ghi đè file task đang do PM sở hữu ngoài ý muốn -> kiểm tra đường dẫn xuất trước.
- (nguồn chưa rõ: PM-GATE ghi "G1-G5" ở đây, còn WBS (Ch3·01) tham chiếu gate "G2-G6" - chưa rõ có mâu thuẫn không.)

## Ví dụ minh họa (1 ví dụ ngắn có số, lấy hoặc dựng từ nguồn; nếu dựng thì ghi "(ví dụ dựng)")
(ví dụ dựng theo nguồn) Function `F-KM-REL-04` thuộc module REL. Dev track: `F-KM-REL-04-REQ-01` (0.5 md, tag `new`) -> BD -> DEV -> UT. Project có 3 module -> PM-TRACK, PM-GATE, PM-RETRO mỗi loại 3 task; PM-KICKOFF, PM-PLAN, PM-CLIENT, COMM mỗi loại 1 task. Tuần sau screen §7 (Interactions) đổi khi DEV đã in-progress -> tag `design-change-after-coding`, nuôi QS-DSG-03 và E3; Impact summary ghi 1 function bị đụng.

## Tự kiểm tra (3-5 câu hỏi có đáp án ngắn ngay dưới, dựa trên chính nội dung bài)
1. Iron Law của task là gì và làm gì khi vi phạm?
   - Mỗi task <= 1md; nếu > 1md thì tách thành sub-task (T-001.1...), không tách được thì cảnh báo và gợi ý viết lại.
2. `TE` phụ thuộc vào những gì?
   - `TC` và mọi `DEV` của module.
3. Section §6/§7 đổi sau khi DEV bắt đầu thì gắn tag gì và nuôi tín hiệu nào?
   - `design-change-after-coding`; nuôi QS-DSG-03 và E3.
4. Ai điền Est và trạng thái mặc định của task?
   - PM điền Est (để trống lúc sinh); Status mặc định `TODO`.
5. Số task PM-TRACK, PM-GATE, PM-RETRO?
   - Mỗi loại bằng số module.

## Liên quan (bài trước/sau trong quy trình, tên thư mục skill khác)
- Trước: Chốt spec (Ch2·03), WBS (Ch3·01) (chạy song song, không thay thế task list).
- Sau: Lập schedule (Ch3·03) (lập lịch sau khi PM điền Est), Xếp người (Ch3·05) (gán người), Sprint plan (Ch3·04); theo dõi tín hiệu (Tín hiệu, Ch6·01) từ tag; change request lớn -> chạy lại chế độ diff.
