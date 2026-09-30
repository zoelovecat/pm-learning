---
title: Hypercare - theo dõi sau release
source: Hypercare (Ch8·04)
stage: Hypercare
level: trung bình
prerequisites: [Ch8·03]
---
# Hypercare - theo dõi sau release

## Mục tiêu học xong bạn làm được gì
- Chạy một cửa sổ hypercare đúng độ dài theo loại release và lập nhật ký hằng ngày.
- So sánh tín hiệu production với baseline trước deploy bằng các ngưỡng cụ thể.
- Ghi sự cố (mức độ, RTO) và phản hồi khách; đặt cờ 🟢 / 🟡 / 🔴 và biết khi nào leo thang.
- Kiểm tra tiêu chí thoát và quyết định đóng hypercare.

## Khi nào dùng (thời điểm, ai kích hoạt, điều kiện đầu vào)
- Thời điểm: ngay sau khi deploy thành công, mỗi ngày trong cửa sổ hypercare (mô tả gốc nói "7-30 ngày"; thực tế bảng cửa sổ bên dưới).
- Người kích hoạt: PM.
- Điều kiện bắt buộc: log thực thi release ở trạng thái thành công; ảnh chụp tín hiệu baseline trước deploy; sổ rủi ro hiện hành; loại release (Major/Minor/Patch/Hotfix).
- Không làm: sửa bug, tự rollback (chỉ khuyến nghị), bịa số liệu (thiếu thì `[NO_DATA]`).

## Khái niệm cốt lõi (định nghĩa, thuật ngữ, vì sao quan trọng)
- Hypercare: giai đoạn giám sát chặt sau go-live để phát hiện sớm suy giảm so với baseline trước deploy.
- Baseline: giá trị tín hiệu chụp trước deploy, làm chuẩn so sánh.
- Trạng thái hằng ngày: 🟢 Stable (mọi tín hiệu trong ngưỡng) / 🟡 Watch / 🔴 Alert.
- Sự cố có mức độ P1-P4; P1 critical dừng mọi sinh hoạt hằng ngày và chuyển sang ứng phó khẩn cấp.
- Nhật ký chỉ ghi thêm (append-only): mỗi ngày thêm một phần, không ghi đè lịch sử.
- Vì sao quan trọng: đây là lưới an toàn cuối trước khi đóng release và mở retro.

## Cách làm từng bước (thủ công, đủ chi tiết để làm theo; kèm input/output)
1. Kiểm tra đầu vào: trạng thái exec (thành công / thất bại / một phần), thời điểm deploy, Release ID + version, loại release để lấy độ dài cửa sổ, ngày và giá trị baseline. Thiếu thì quay lại các bước upstream (thực thi release, đo tín hiệu, cập nhật rủi ro).
2. Chốt: Release ID và "ngày thứ mấy" trong cửa sổ (tính từ ngày deploy hoặc PM ghi đè). Tùy chọn: độ dài cửa sổ ghi đè, kênh sự cố (Slack/Jira/PagerDuty), kênh phản hồi khách (email/khảo sát/ticket). Mặc định: cửa sổ theo loại release; tiêu chí thoát 0 P1, tín hiệu ổn định, không có escalation; cảnh báo qua kênh thông báo công cụ (tương lai), tạm dùng markdown.
3. Kiểm tra hợp lý:
   - Exec thất bại/một phần: không mở hypercare, xem lại Release exec (Ch8·03) hoặc rollback.
   - Không xác định được loại release: hỏi (mặc định Major 7 ngày).
   - Baseline cũ hơn 1 ngày trước deploy? Nguồn ghi "Baseline snapshot trước deploy ≥ 1 ngày? Quá cũ" -> gắn cờ, PM xác nhận dùng tiếp hoặc đo lại. (Nguồn chưa rõ: ý nghĩa chính xác của ngưỡng "≥ 1 ngày".)
   - Ngày hiện tại ngoài cửa sổ: chuyển sang kiểm tra thoát, không thêm ngày mới.
   - Có P1 critical đang mở: dừng thường kỳ, chuyển ứng phó khẩn cấp (hotfix hoặc rollback).
   - Mâu thuẫn giữa log exec và release plan (version/ngày): dừng và hỏi.
4. Thu thập tín hiệu hôm nay so với baseline (bảng ngưỡng). Ghi sự cố: mức P1-P4, thời gian, mô tả, cách xử lý, RTO. Ghi phản hồi khách: tích cực / tiêu cực / báo bug, kèm ngày, nguồn, ghi chú, gắn ID sự cố nếu có. Đặt cờ: vượt ngưỡng 🟡 Watch hoặc 🔴 Alert (đề xuất hotfix/rollback); có P1 thì 🔴 và dừng; mọi thứ trong ngưỡng thì 🟢.
5. Viết nhật ký: cập nhật bảng Signal Health, thêm phần Daily Snapshot cho ngày hôm nay, gộp tích lũy Incidents Log và Customer Feedback, cập nhật Exit Criteria (N/N ngày), ghi Next Steps.
6. Kết thúc ngày: tóm tắt (Day X of Y, cờ, số tín hiệu vượt ngưỡng, số P1 đang mở). Vượt ngưỡng: cảnh báo, đề xuất hành động (hotfix qua release plan loại Hotfix hoặc khuyến nghị rollback). Hết cửa sổ và tiêu chí thoát đạt: đóng hypercare và làm retro.

## Công thức, ngưỡng & tín hiệu
Cửa sổ theo loại release:
| Loại | Cửa sổ | Review |
|---|---|---|
| Major (vN.0) | 7 ngày | Hằng ngày |
| Minor (v.X) | 3 ngày | Hằng ngày |
| Patch | 1 ngày | Hằng ngày |
| Hotfix | 24h | Mỗi 4h |

Ngưỡng tín hiệu so với baseline:
| Tín hiệu | Nguồn | Ngưỡng | Hành động khi vượt |
|---|---|---|---|
| Uptime | Công cụ giám sát/APM | ≥ 99.5% | 🟡 Watch hoặc 🔴 Alert; đề xuất hotfix/rollback |
| p95 latency | Công cụ giám sát | ≤ baseline + 10% | như trên |
| Error rate | Logs / APM | ≤ baseline + 0.5% | như trên |
| Phiên người dùng hoạt động | Analytics | ≥ baseline - 10% | như trên |
| Bug do khách báo | Kênh support | ≤ 2 P1/ngày | như trên |
| Lọt lỗi critical | Bug tracker | 0 | như trên |

Leo thang và dừng:
| Điều kiện | Hành động |
|---|---|
| Tín hiệu vượt ngưỡng | Báo PM; đề xuất hotfix (release plan loại Hotfix) hoặc khuyến nghị rollback |
| Sự cố P1 critical | Dừng thường kỳ; ứng phó khẩn cấp |
| Hết cửa sổ và tất cả xanh | Đóng hypercare; chạy Lessons learned (Ch9·01) |
| Xong snapshot ngày | Ghi thêm bản nháp, không ghi đè |

Tiêu chí thoát: 0 sự cố P1 critical trong cửa sổ; mọi tín hiệu trong ngưỡng; không có escalation từ khách; hoàn thành snapshot hằng ngày (N/N ngày).

## Template / mẫu đầu ra (rút gọn, giữ cấu trúc và các cột/trường)
```markdown
# Hypercare Log — R-<PROJ>-NN (Major) — Day X of Y
> Sources: exec log + Tín hiệu (Ch6·01) + PM incident input
| Release | Deployed | Hypercare window (N days → end date) | Current day | Status 🟢 Stable / 🟡 Watch / 🔴 Alert |
## Signal Health (Day X)   | Signal | Baseline (pre-deploy) | Current | Status |
## Daily Snapshots         ### Day 1 (date) - incidents, feedback, notes
## Incidents Log           | ID | Date | Severity | Description | Resolution | RTO |
## Customer Feedback       | Date | From | Type | Note |
## Exit Criteria           - [ ] items
## Next Steps
```
Append-only: mỗi ngày thêm phần mới.
Checklist sau khi viết: baseline có ngày cụ thể; so sánh có `[NO_DATA]` nếu thiếu; sự cố có severity + RTO; tiêu chí thoát theo dõi N/N ngày; lịch sử cũ giữ nguyên.

## Lỗi thường gặp & lesson learned
- Mở hypercare khi exec chưa thành công -> theo dõi trên nền sai -> chỉ mở khi log exec thành công.
- Không có baseline -> không biết "xấu đi" là bao nhiêu -> chụp tín hiệu trước deploy, ghi ngày.
- Bịa chỉ số khi thiếu dữ liệu -> quyết định sai -> ghi `[NO_DATA]`.
- Ghi đè nhật ký -> mất lịch sử sự cố -> luôn thêm mục mới mỗi ngày.
- Tiếp tục thường kỳ khi có P1 -> chậm ứng phó -> P1 thì dừng thường kỳ, chuyển khẩn cấp.
- Sự cố không có RTO/severity -> khó rút bài học -> luôn ghi cả hai.

## Ví dụ minh họa
(ví dụ dựng) Release Major, hypercare 7 ngày, ngày 3/7. Baseline: p95 latency 180ms -> ngưỡng ≤ 180 + 10% = 198ms; hôm nay đo 190ms -> đạt. Uptime 99.7% (≥ 99.5%) đạt. Error rate baseline 0.3% -> ngưỡng ≤ 0.8%; hôm nay 0.4% đạt. Phiên hoạt động baseline 1000 -> ngưỡng ≥ 900; hôm nay 950 đạt. 1 sự cố P3 đã xử lý. Cờ 🟢 Stable; tiêu chí thoát tiến độ 3/7 ngày.

## Tự kiểm tra
1. Cửa sổ hypercare của Minor và Hotfix là bao lâu, review ra sao? -> Minor 3 ngày review hằng ngày; Hotfix 24h review mỗi 4h.
2. Ngưỡng p95 latency và error rate so với baseline? -> p95 ≤ baseline + 10%; error rate ≤ baseline + 0.5%.
3. Khi có sự cố P1 critical đang mở thì làm gì? -> Dừng thường kỳ, chuyển ứng phó khẩn cấp (hotfix hoặc rollback).
4. Bốn tiêu chí thoát là gì? -> 0 P1 critical; mọi tín hiệu trong ngưỡng; không escalation khách; hoàn thành snapshot N/N ngày.
5. Vì sao nhật ký hypercare là append-only? -> Để giữ lịch sử từng ngày, không bị ghi đè.

## Liên quan
- Trước: Release exec (Ch8·03), Release plan (Ch8·01) (loại release), Tín hiệu (Ch6·01) (baseline), Rủi ro & issue (Ch4·04).
- Sau: Lessons learned (Ch9·01) (retro release sau khi đóng hypercare), Release plan (Ch8·01) loại Hotfix (nếu cần vá khẩn), Rủi ro & issue (Ch4·04) (ghi sự cố thành issue).
- Chỗ nguồn chưa rõ: (1) Mô tả gốc nói "7-30 ngày" nhưng bảng chỉ có 7 ngày / 3 ngày / 1 ngày / 24h. (2) Ngưỡng "Bug do khách báo ≤ 2 P1/ngày" có vẻ mâu thuẫn với tiêu chí thoát "0 P1" và quy tắc "P1 dừng thường kỳ"; nguồn không giải thích cách hòa giải. (3) Uptime ≥ 99.5% được ghi cả là ngưỡng tuyệt đối lẫn "vs baseline". (4) Câu hỏi mở của nguồn: công cụ giám sát chuẩn, kênh sự cố, kênh phản hồi khách, chính sách ghi đè cửa sổ, SLA uptime/RTO chuẩn.
