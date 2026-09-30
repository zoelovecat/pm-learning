# Lộ trình học PM (Kaopiz)

Giáo trình chưng cất từ 33 skill PM của Kaopiz (kinh nghiệm của người đi trước). Học theo thứ tự chương; mỗi bài 10-20 phút đọc + tự kiểm tra. Tổng 35 bài, khoảng 6-8 tuần nếu học 1 bài/ngày.

**Cách học mỗi bài:** đọc → làm phần "Tự kiểm tra" (che đáp án) → thử làm "Mẫu đầu ra" trên một dự án thật hoặc giả lập → ghi điểm vào [`progress.md`](./progress.md).

**Tra nhanh:** [`cheatsheet.md`](./cheatsheet.md) (công thức, ngưỡng, tín hiệu, gate) · [`glossary.md`](./glossary.md) (thuật ngữ).

## Sơ đồ thứ tự

```
Ch0 Tổng quan ─► Ch1 Trước dự án & thiết lập ─► Ch2 Khởi động ─► Ch3 Lập kế hoạch
                                                                        │
      Ch9 Đóng dự án ◄─ Ch8 Release & hypercare ◄─ Ch7 Báo cáo/họp ◄─ Ch6 Đo lường ◄─ Ch4 Điều hành ─ Ch5 Con người
```

Ch4 và Ch5 học sau Ch3; Ch6 cần Ch3 (schedule, effort) và Ch4 (rủi ro/CR). Ch8 (gate) cần Ch6 (tín hiệu, checklist).

## Chặng học

### Chặng A - Nền tảng (Ch0-Ch2, ~1 tuần)
| Bài | Cấp độ | Bạn học được |
|---|---|---|
| [Ch0 · 00 Tổng quan vòng đời](chapters/00-tong-quan/00-tong-quan-vong-doi.md) | cơ bản | 10 giai đoạn, gate G1-G6, tín hiệu, nhịp việc |
| [Ch1 · 01 Ước tính chào giá](chapters/01-truoc-du-an-va-thiet-lap/01-uoc-luong-bao-gia.md) | trung bình | Ước lượng effort/cost/timeline cho bid |
| [Ch1 · 02 Dự báo năng lực](chapters/01-truoc-du-an-va-thiet-lap/02-du-bao-nang-luc.md) | trung bình | Cân nhu cầu và nguồn nhân sự theo quý |
| [Ch1 · 03 Thiết lập PM](chapters/01-truoc-du-an-va-thiet-lap/03-thiet-lap-pm.md) | cơ bản | Đăng ký mã Jira/Bitbucket/Ksystem cho dự án |
| [Ch2 · 01 Kickoff](chapters/02-khoi-dong/01-kickoff.md) | | Charter, RACI, rủi ro ban đầu |
| [Ch2 · 02 Project plan](chapters/02-khoi-dong/02-project-plan.md) | | Kế hoạch dự án và bộ chỉ số |
| [Ch2 · 03 Chốt spec](chapters/02-khoi-dong/03-chot-spec.md) | cơ bản | Vòng review và sign-off spec |

### Chặng B - Lập kế hoạch (Ch3, ~1 tuần)
| Bài | Cấp độ | Bạn học được |
|---|---|---|
| [Ch3 · 01 WBS](chapters/03-lap-ke-hoach/01-wbs.md) | trung bình | Phân rã, milestone gắn tín hiệu QS-XX |
| [Ch3 · 02 Spec thành task](chapters/03-lap-ke-hoach/02-spec-thanh-task.md) | trung bình | Sinh task từ spec, hệ số effort, quy tắc task ≤ 1 md |
| [Ch3 · 03 Lập schedule](chapters/03-lap-ke-hoach/03-lap-schedule.md) | trung bình | Timeline, buffer, capacity, critical path |
| [Ch3 · 04 Sprint plan](chapters/03-lap-ke-hoach/04-sprint-plan.md) | cơ bản | Chọn task theo ưu tiên và capacity |
| [Ch3 · 05 Xếp người](chapters/03-lap-ke-hoach/05-team-match.md) | | Chấm điểm phù hợp kỹ năng/khả năng/năng lực |

### Chặng C - Điều hành hằng ngày (Ch4-Ch5, ~1.5 tuần)
| Bài | Cấp độ | Bạn học được |
|---|---|---|
| [Ch4 · 01 Daily sync](chapters/04-dieu-hanh-hang-ngay/01-daily-sync.md) | cơ bản | Chuẩn bị và ghi lại standup |
| [Ch4 · 02 Daily report](chapters/04-dieu-hanh-hang-ngay/02-daily-report.md) | trung bình | Báo cáo daily cho PM và cả team |
| [Ch4 · 03 Change request](chapters/04-dieu-hanh-hang-ngay/03-change-request.md) | trung bình | Từ diff spec đến quyết định CR |
| [Ch4 · 04 Rủi ro & issue](chapters/04-dieu-hanh-hang-ngay/04-risk-issue.md) | | EMV, vòng đời rủi ro, xử lý issue |
| [Ch5 · 01 Bàn giao thành viên](chapters/05-con-nguoi-va-ban-giao/01-ban-giao-thanh-vien.md) | trung bình | Ma trận bàn giao 13 mục |
| [Ch5 · 02 Onboarding brief](chapters/05-con-nguoi-va-ban-giao/02-onboarding-brief.md) | cơ bản | Brief đọc trước cho người mới |
| [Ch5 · 03 Onboarding todo](chapters/05-con-nguoi-va-ban-giao/03-onboarding-todo.md) | cơ bản | Checklist theo vai trò |
| [Ch5 · 04 Tiếp quản PM](chapters/05-con-nguoi-va-ban-giao/04-tiep-quan-pm.md) | nâng cao | Dựng lại hồ sơ khi nhận dự án giữa chừng |

### Chặng D - Đo lường và báo cáo (Ch6-Ch7, ~1.5 tuần)
| Bài | Cấp độ | Bạn học được |
|---|---|---|
| [Ch6 · 01 Tín hiệu](chapters/06-do-luong-va-kiem-soat/01-tin-hieu-signal.md) | trung bình | QS-XX, chỉ số công ty, CPI/SPI và ngưỡng |
| [Ch6 · 02 Checklist](chapters/06-do-luong-va-kiem-soat/02-checklist.md) | cơ bản | Checklist Pass/Fail cho gate, phase, release |
| [Ch6 · 03 Effort actuals](chapters/06-do-luong-va-kiem-soat/03-effort-actuals.md) | trung bình | EVM, E3, dự báo EAC |
| [Ch6 · 04 Scope baseline](chapters/06-do-luong-va-kiem-soat/04-scope-baseline.md) | cơ bản | Baseline phạm vi tích lũy |
| [Ch6 · 05 Bug triage](chapters/06-do-luong-va-kiem-soat/05-bug-triage.md) | trung bình | Phân loại và báo cáo bug |
| [Ch7 · 01 Status tuần](chapters/07-bao-cao-hop-va-giao-tiep/01-status-weekly.md) | | Báo cáo tình trạng hằng tuần |
| [Ch7 · 02 Phân tích họp](chapters/07-bao-cao-hop-va-giao-tiep/02-phan-tich-hop.md) | trung bình | Tự coaching hành vi giao tiếp |
| [Ch7 · 03 Giao tiếp stakeholder](chapters/07-bao-cao-hop-va-giao-tiep/03-giao-tiep-stakeholder.md) | trung bình | Truyền thông theo từng đối tượng |
| [Ch7 · 04 Sprint retro](chapters/07-bao-cao-hop-va-giao-tiep/04-sprint-retro.md) | | Retro và kho lesson learned |

### Chặng E - Release và đóng dự án (Ch8-Ch9, ~1 tuần)
| Bài | Cấp độ | Bạn học được |
|---|---|---|
| [Ch8 · 01 Release plan](chapters/08-release-va-hypercare/01-release-plan.md) | trung bình | Kế hoạch release, template N-N |
| [Ch8 · 02 Gate review](chapters/08-release-va-hypercare/02-gate-review.md) | trung bình | G1-G6, ma trận ngưỡng |
| [Ch8 · 03 Release exec](chapters/08-release-va-hypercare/03-release-exec.md) | trung bình | Thực thi release, rollback |
| [Ch8 · 04 Hypercare](chapters/08-release-va-hypercare/04-hypercare.md) | trung bình | Theo dõi sau go-live |
| [Ch9 · 01 Lessons learned](chapters/09-dong-du-an/01-lessons-learned.md) | | 8 định dạng retro, catalog |
| [Ch9 · 02 Closeout](chapters/09-dong-du-an/02-closeout.md) | | Đóng dự án M7 |

## Kiểm tra cuối chặng
Sau mỗi chặng, chọn một dự án (thật hoặc giả lập) và tự làm các đầu ra của chặng theo mục "Mẫu đầu ra". Nhờ pm-mentor (xem `SKILL.md`) chấm và hỏi thi thử.

## Dùng như một skill
Sao thư mục này vào `~/.claude/skills/pm-learning` (hoặc tạo link) để gọi `/pm-learning`: nó dạy từng bài, hỏi kiểm tra, và cập nhật `progress.md`. Không cài cũng được: chỉ cần đọc các file.
