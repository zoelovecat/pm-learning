---
title: Thực thi release và theo dõi rollback
source: Release exec (Ch8·03)
stage: Release
level: trung bình
prerequisites: [Ch8·01, Ch8·02]
---
# Thực thi release và theo dõi rollback

## Mục tiêu học xong bạn làm được gì
- Điều phối một đêm deploy production: kiểm tra điều kiện tiên quyết, đi từng bước còn lại, ghi log thực tế so với kế hoạch.
- Nhận ra điều kiện phải dừng và rollback, và biết ai quyết định.
- Lập được nhật ký thực thi (execution log) đúng cấu trúc, phân biệt bước "prereq" và bước "walk".
- Biết rõ PM điều phối và ghi log; DevOps/QA/DBA mới là người thực thi.

## Khi nào dùng (thời điểm, ai kích hoạt, điều kiện đầu vào)
- Thời điểm: đến cửa sổ deploy (window) đã ghi trong release plan.
- Người kích hoạt: PM.
- Điều kiện tiên quyết bắt buộc (thiếu thì dừng, không bịa kết quả gate/checklist):
  - Release plan (mục 5 lịch deploy, mục 6 rollback).
  - Kết quả G5 UAT Sign-off đã đạt.
  - G6 go/no-go = GO.
  - Checklist pre-deploy G6 đã đạt.
- Không làm: tự chạy lệnh deploy, chạy smoke test, gửi thông báo, làm lại UAT/G6, commit.

## Khái niệm cốt lõi (định nghĩa, thuật ngữ, vì sao quan trọng)
- Bước `prereq`: việc xong trước khi bắt đầu đi bước (UAT G5, checklist pre-deploy, G6 go/no-go, có thể cả code freeze/regression nếu đã xong). Chỉ kiểm tra, không đi lại.
- Bước `walk`: bước còn lại trong đêm deploy, PM hỏi và ghi kết quả từng bước (thường: DB migration, application deploy, smoke test, hypercare standby, customer notification).
- Nguyên tắc chính sách: không tự động deploy (PM chỉ điều phối và ghi log); múi giờ mặc định UTC+7; hỏi kết quả từng bước, không mặc định là thành công; UAT/G6 là điều kiện trước, không phải bước trong walk.
- Vì sao quan trọng: ghi log thực tế vs kế hoạch cho phép truy vết, đưa ra quyết định rollback có căn cứ và làm đầu vào cho hypercare và retro.

## Cách làm từng bước (thủ công, đủ chi tiết để làm theo; kèm input/output)
1. Xác minh điều kiện: lấy Release ID, cửa sổ, các bước mục 5, thủ tục và điều kiện rollback mục 6, quyết định và ngày của G5/G6, tóm tắt Pass/Fail của checklist pre-deploy. Xác nhận với các bên trước khi đi tiếp.
2. Chốt thông tin: Release ID (`R-<PROJ>-NN`), PM phụ trách, chế độ chạy (live hay chỉ dry-run ghi log). Tùy chọn: điều chỉnh điều kiện rollback (mặc định lấy từ plan), tần suất thông báo khách sau exec (mặc định lên lịch sau exec), danh sách người trực (DevOps + QA + DBA). Mặc định giả định: RTO 30 phút, UTC+7, cảnh báo multi-eyes mềm (PM + DevOps xác nhận).
3. Kiểm tra điều kiện tiên quyết (bảng dưới). Nếu G6 khác GO: dừng, không deploy production, chạy lại gate review. Xung đột giữa plan và gate: dừng và hỏi. Hỏi xác nhận bắt đầu: "Bắt đầu execute release `<release-id>`? Y/N"; trả lời N thì dừng, không tạo log dở.
4. Đi từng bước còn lại. Với mỗi bước: (a) thông báo bước (người phụ trách, giờ dự kiến, loại); (b) hỏi kết quả: success / fail / skip; (c) ghi giờ thực tế và ghi chú (nhánh, thời lượng, tham chiếu template...); (d) nếu fail, đối chiếu bảng rollback; khớp thì dừng và ghi bắt đầu rollback.
   - Điểm kiểm tra quan trọng: trước deploy (G6 GO đã xác minh ở bước 3, thiếu thì dừng); sau smoke test (kiểm tra điều kiện rollback + post-deploy validation); suốt cửa sổ (theo dõi điều kiện rollback đến hết window).
5. Viết log theo khung bên dưới. Kết quả có ba loại: ✅ SUCCESS (mọi bước quan trọng đạt -> hypercare + thông báo stakeholder); 🔴 ROLLBACK (điều kiện khớp hoặc fail nghiêm trọng -> ghi các bước rollback, mở post-mortem); 🟡 PARTIAL (window chưa xong, trạng thái LOG (in progress)). Mỗi dòng timeline có giờ dự kiến vs thực tế, biểu tượng kết quả, ghi chú; bước chưa xác nhận thì không giả định thành công.
6. Kết thúc: tóm tắt (kết quả, số bước đạt/fail, có rollback hay không). Nếu rollback thì gợi ý post-mortem/Lessons learned (Ch9·01). Không tự commit.

## Công thức, ngưỡng & tín hiệu
Kiểm tra trước khi thực thi:
| Kiểm tra | Nguồn | Chặn nếu fail |
|---|---|---|
| G5 UAT Sign-off | Tài liệu gate G5 | Có (chặn) |
| G6 pre-deploy checklist | Kết quả checklist G6 | Có |
| G6 final go/no-go = GO | Tài liệu gate G6 | Có |
| Rollback procedure ready | Release plan mục 6 | Có |
| Đã tới cửa sổ deploy | Plan mục 5 + PM xác nhận | Không hẳn (🟡): bắt đầu sớm được nếu PM xác nhận |
| Khách đã được báo | PM xác nhận | Không (🟡 cảnh báo) |
| Đội đang trực | PM xác nhận | Không (🟡 cảnh báo) |

Điều kiện rollback:
| Điều kiện | Hành động khi khớp |
|---|---|
| Critical bug > 30% người dùng trong 4h | DỪNG -> quy trình rollback |
| Suy giảm hiệu năng > 50% | DỪNG -> quy trình rollback |
| Customer escalation P1 | DỪNG -> PM quyết định |
| Sự cố toàn vẹn dữ liệu | DỪNG -> rollback ngay |

RTO mặc định 30 phút.

Loại bước và trường cần ghi:
| Bước | Người phụ trách thường | Vai trò | Trường log |
|---|---|---|---|
| Code freeze | Tech Lead | prereq nếu đã freeze | tên nhánh, giờ |
| Regression test | QA | prereq nếu đã xong | pass/fail, khoảng ngày |
| UAT sign-off | Khách + QA | prereq | tham chiếu G5 |
| Pre-deploy checklist | PM | prereq | tham chiếu checklist |
| G6 Final go/no-go | PM + Sponsor + DevOps | prereq | GO/HOLD |
| DB migration | DBA | walk | thời lượng, script |
| Application deploy | DevOps | walk | tham chiếu template |
| Smoke test | QA | walk | kết quả các đường quan trọng |
| Hypercare standby | Tất cả | walk | giờ bắt đầu window |
| Customer notification | PM | walk | đã lên lịch/đã gửi |

## Template / mẫu đầu ra (rút gọn, giữ cấu trúc và các cột/trường)
```markdown
# Release Execution Log — R-<PROJ>-NN
> Sources: release plan + PM step confirmations + rollback defaults
| Release ID | Window | Started | Ended | Result (✅ SUCCESS / 🔴 ROLLBACK) | PM | Status LOG (final) |
## Pre-execution Checks   | Check | Status | Note |
## Execution Timeline     | # | Step | Owner | Planned | Actual | Result | Note |
## Rollback Trigger Monitoring  | Trigger Condition | Status |
## Post-deploy Validation | Check | Result |
## Next Steps  1. hypercare / Giao tiếp stakeholder (Ch7·03) / Lessons learned (Ch9·01)
```
Trạng thái: LOG (final) hoặc LOG (in progress).

## Lỗi thường gặp & lesson learned
- Đi lại UAT/G6 trong lúc đi bước -> trùng lặp, dễ mâu thuẫn -> chỉ kiểm tra ở bước điều kiện tiên quyết, đi phần còn lại.
- Mặc định bước thành công -> log sai, bỏ lỡ tín hiệu rollback -> hỏi và ghi kết quả từng bước.
- Bắt đầu deploy khi G6 chưa GO -> đi ngược cổng chất lượng -> dừng và chạy lại gate review.
- Chỉ ghi giờ dự kiến -> mất khả năng phân tích -> luôn ghi giờ thực tế cạnh dự kiến.
- Ngưng theo dõi rollback sau smoke test -> sự cố muộn không bị bắt -> theo dõi điều kiện đến hết window.
- Chưa báo khách/đội chưa trực mà vẫn đi -> chỉ là cảnh báo, không chặn nhưng phải ghi rõ trong log.

## Ví dụ minh họa
Ví dụ từ nguồn (release Major, window 2026-09-30 22:00 → 2026-10-01 02:00, kết thúc thực tế 00:45, ✅ SUCCESS): G5 passed 2026-09-23; checklist G6 passed 2026-09-30 20:00. Timeline: (1) DB migration DBA 22:00 -> 22:18 ✅ (TPL-MIG-DB); (2) Application deploy DevOps 22:20 -> 22:35 ✅ (TPL-STD-WEB); (3) Smoke test QA dự kiến 23:00, thực tế 22:40 -> 23:15 ✅; (4) Hypercare standby 00:00 ✅, hypercare 7d; (5) Customer notification 09:00 ngày 2026-10-01, đang lên lịch ⏳. Cả 4 điều kiện rollback "không kích hoạt". Post-deploy: p95 latency 180ms so với mục tiêu ≤ 200ms. Bước tiếp: thông báo khách, hypercare 7 ngày, retro ngày 2026-10-08.

## Tự kiểm tra
1. Những bước nào là prereq, không đi lại trong lúc deploy? -> UAT sign-off (G5), pre-deploy checklist, G6 final go/no-go (và code freeze/regression nếu đã xong).
2. Điều kiện nào yêu cầu rollback ngay và điều kiện nào PM quyết định? -> Toàn vẹn dữ liệu bị hỏng: rollback ngay; customer escalation P1: PM quyết định; bug critical > 30% người dùng trong 4h và hiệu năng suy giảm > 50%: dừng và chạy quy trình rollback.
3. Nếu G6 không phải GO thì làm gì? -> Dừng, không deploy production, chạy lại gate review.
4. Khách chưa được báo thì có chặn deploy không? -> Không, chỉ cảnh báo (🟡).
5. Ba loại kết quả của log? -> SUCCESS, ROLLBACK, PARTIAL (log đang chạy).

## Liên quan
- Trước: Release plan (Ch8·01) (lịch và rollback), Gate review (Ch8·02) (G5, G6), checklist pre-deploy G6.
- Sau: Hypercare (Ch8·04) (bắt đầu sau khi exec thành công), Giao tiếp stakeholder (Ch7·03) (thông báo khách), Lessons learned (Ch9·01) (retro sau release).
- Chỗ nguồn chưa rõ: (1) Nguồn còn để mở: script deploy do DevOps sở hữu, công cụ giám sát (Datadog hay canary), mức tự động hóa rollback, tham số múi giờ. (2) "Bắt đầu sớm" so với window: nguồn chỉ nói cho phép nếu PM xác nhận, không nêu giới hạn thời gian.
