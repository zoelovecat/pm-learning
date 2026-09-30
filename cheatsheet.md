# Cheatsheet PM Kaopiz (tra nhanh, dựng từ 35 bài)

Quy ước: cột "Bài" là mã chương-bài (ví dụ Ch6·01) để tra ngược. Số liệu chép nguyên từ bài, không làm tròn. "(nguồn chưa rõ)" = bài tự ghi còn mâu thuẫn/chưa chốt, xem mục 9. Mọi tài liệu PM lập ra đều ở trạng thái DRAFT chờ người có thẩm quyền duyệt; thiếu số thì ghi `[NO_DATA]`, không bịa.

## 1. Vòng đời, mốc và gate

### 1.1 Mười giai đoạn

| GĐ | Việc chính của PM | Mốc / Gate | Tín hiệu chính | Bài |
|---|---|---|---|---|
| 0 Pre-Project | Ước lượng báo giá, dự báo năng lực, phân tích họp khám phá | M0; GO / NO-GO | (chưa có) | Ch0, Ch1·01, Ch1·02 |
| 1 Initiation | Kickoff, charter, risk seed, RACI | M1 Charter Approved; G1 (định tính) | không có | Ch0, Ch2·01 |
| 2 Planning | WBS, task, schedule, capacity, critical path, xếp người | Baseline schedule locked | E3 ≤ 10% (theo dõi hằng tuần từ đây) | Ch0, Ch3·01-05 |
| 3 Requirements | Chốt yêu cầu, checklist review | M2 SRS Approved; G2 | QS-REQ-01 ≥ 95%, QS-REQ-03 = 100% | Ch0, Ch2·03 |
| 4 Design | Task BD, checklist design review | M3 BD Approved; G3 | QS-DSG-03 ≤ 5% | Ch0 |
| 5 Development | Daily sync, CR, effort, rủi ro/issue, status tuần | M4 Code Complete; G4 | QS-DEV-cov ≥ 80%, QS-PRC-07 ≥ 90%, E3 ≤ 10% | Ch0 |
| 6 Testing | Task test, bug, checklist test, UAT | M5a System Test Done; M5b UAT Sign-off (gate G5 = UAT; bản đồ SDLC gọi là G5a/G5b, ma trận gate chỉ có G5) (nguồn chưa rõ) | QS-TST-02 ≤ baseline, QS-TST-04 ≤ 2%, QS-TST-08 ≤ 5% | Ch0 |
| 7 Release | Release plan, checklist G6, release exec, báo khách | G6 Go decision; M6 Go-live | QS-PRC-07 ≥ 90% | Ch0, Ch8·01-03 |
| 8 Hypercare | Theo dõi sau go-live | Cửa sổ: Major 7 ngày, Minor 3, Patch 1, Hotfix 24 giờ | Uptime ≥ 99.5%, error rate ≤ baseline + 0.5%, p95 ≤ baseline + 10%, 0 P1 | Ch0, Ch8·04 |
| 9 Closure | Retro, lessons learned, chốt effort, báo cáo cuối, đóng | M7 Project Closed (PM + Sponsor + Customer PIC + Support Lead) | không có | Ch0, Ch9·01-02 |

Hypercare xong mà cần hotfix thì quay lại GĐ 7 với loại release = Hotfix. Tiếp quản PM giữa chừng: dựng lại hồ sơ (Ch5·04). Milestone: M1 Charter, M2 SRS, M3 BD, M4 Code Complete, M5a System Test, M5b UAT, M6 Go-live, M7 Closed (Ch0).

### 1.2 Gate G1-G6

| Gate | Tên | Ai quyết định | Tín hiệu bắt buộc | Checklist bắt buộc | Bài |
|---|---|---|---|---|---|
| G1 | Charter Approved | Sponsor + PM (Ch8·02); Sponsor + PM + Customer PIC nếu ngoài (Ch0) (nguồn chưa rõ) | không có | Project init | Ch8·02, Ch0 |
| G2 | SRS Approved | BA Lead + Customer PIC | QS-REQ-01 ≥ 95%; QS-REQ-03 = 100% | Requirements review | Ch8·02 |
| G3 | Basic Design Approved | Tech Lead + Customer PIC | QS-DSG-03 ≤ 5% | Design review | Ch8·02 |
| G4 | Code Complete | Tech Lead + QA Lead | QS-DEV-cov ≥ 80%; QS-PRC-07 ≥ 90% | Code review + UT | Ch8·02 |
| G5 | UAT Sign-off | QA Lead + Customer PIC | QS-TST-08 ≤ 5%; QS-TST-04 ≤ 2% | UAT | Ch8·02 |
| G6 | Go-live (Go/No-go) | PM + Sponsor + DevOps | QS-PRC-07 ≥ 90% | Pre-deploy + Rollback ready (Ch8·02); "all checklists pass" (Ch8·01) (nguồn chưa rõ) | Ch8·02, Ch8·01 |

Ngưỡng có thể điều chỉnh theo `contract_type` (Ch8·02, Ch6·01). Gate thay ý kiến bằng dữ liệu; chỉ PM đề xuất, stakeholder mới ký (ô phê duyệt để trống ⬜) (Ch8·02, Ch0).

### 1.3 Ma trận quyết định gate (Ch8·02)

| Tín hiệu | Checklist | Rủi ro High/Crit mở | Quyết định |
|---|---|---|---|
| Tất cả đạt | Tất cả đạt | 0 | GO |
| Tất cả đạt | Tất cả đạt | 1-2 | GO with risks (ký + kế hoạch giảm thiểu) |
| 1 tín hiệu vàng (lệch 5-10%) | Pass | ≤ 2 | HOLD (duyệt có điều kiện, đặt ngày review lại) |
| ≥ 1 tín hiệu đỏ | Bất kỳ | Bất kỳ | ABORT (tìm nguyên nhân gốc, lập lại kế hoạch qua CR) |
| Bất kỳ | ≥ 1 checklist fail mức Critical | Bất kỳ | ABORT (sửa checklist trước) |
| Pass | Pass kèm cảnh báo nhỏ | ≥ 3 High | HOLD (giảm thiểu trước) |

HOLD: review lại mặc định +5 ngày làm việc; quá hạn chưa đóng thì PM báo Sponsor. Checklist đề xuất: BLOCK (Critical fail > 0) / REVIEW (Standard fail > 20%) / READY (tất cả Pass) (Ch6·02). Tín hiệu chỉ đo, checklist chỉ Pass/Fail, gate review mới quyết (Ch6·01, Ch6·02).

## 2. Tín hiệu QS-XX và chỉ số công ty

### 2.1 QS-XX và E3

| Mã | Ý nghĩa | Công thức | Ngưỡng | Hành động | Bài |
|---|---|---|---|---|---|
| QS-REQ-01 | Tỉ lệ review yêu cầu đạt | reviewed_pass / total_reviewed × 100% | ≥ 95% (Fixed-bid) | gắn màu, cảnh báo | Ch6·01, Ch3·01 |
| QS-REQ-03 | Độ đầy đủ truy vết UC-feature-test | mapped_features / total_features × 100% | = 100% | như trên | Ch6·01, Ch3·01 |
| QS-DSG-03 | Tỉ lệ lỗi thiết kế | design_defects / total_design_items × 100% | ≤ 5% | như trên | Ch6·01 |
| QS-DEV-cov | Unit test coverage | covered_lines / total_lines × 100% | ≥ 80% | như trên | Ch6·01 |
| QS-PRC-07 | Tuân thủ quy trình | tasks_followed_process / total_tasks × 100% | ≥ 90% (ma trận Fixed-bid: ≥ 95%) (nguồn chưa rõ) | như trên | Ch6·01 |
| QS-TST-02 | Mật độ lỗi | defects / KLOC | ≤ baseline của dự án | như trên | Ch6·01, Ch3·01 |
| QS-TST-04 | Tỉ lệ lọt lỗi | post_release_defects / total_defects × 100% | ≤ 2% | như trên | Ch6·01 |
| QS-TST-08 | Tỉ lệ reopen | reopened_bugs / total_bugs × 100% | ≤ 5% | như trên | Ch6·01, Ch3·01 |
| QS-TST-09 | Độ phủ test (luồng/lỗi) | covered_flows / total_flows × 100% | không nêu | như trên | Ch6·01 |
| E3 | Chênh lệch effort | (actual − planned) / planned × 100% | ≤ 10% | vàng/đỏ, đào sâu | Ch6·01, Ch6·03 |
| QS-PRF-*, QS-OPS-* | Response time ≤ X ms; Uptime ≥ X% (X lấy từ NFR §7 SRS) | - | X từ NFR | theo dõi | Ch2·01 |

Nguồn số liệu: REQ-01/03 từ task list + ma trận truy vết; DSG-03 từ nhật ký review BD; DEV-cov từ CI; PRC-07 từ audit trail task; TST từ báo cáo test + bug tracker (Ch6·01). Task tag nuôi tín hiệu: spec-change nuôi QS-REQ-01, QS-PRC-07; design-change-after-coding nuôi QS-DSG-03, E3 (Ch3·02).

### 2.2 Màu tín hiệu (Ch6·01)

| Màu | Điều kiện (độ lệch so với ngưỡng) | Hành động |
|---|---|---|
| Xanh | = ngưỡng | ghi nhận |
| Vàng | lệch 5-10% | vào danh sách cảnh báo + hành động đề xuất |
| Đỏ | lệch > 10% | lên đầu file + hành động (người phụ trách, hạn) |

Đỏ kéo dài: mở rủi ro mới hoặc re-baseline qua CR. Khoảng lệch 0-5% và cách tính "lệch %" (nguồn chưa rõ).

### 2.3 Chỉ số công ty (TPL-SW-05-01 v1.7)

| Chỉ số | Công thức | LCL / Target / UCL | Owner | Bài |
|---|---|---|---|---|
| Bug rate | Bug nội bộ / công số thực tế (theo rank), Bug/MM | 3.55 / 4.57 / 8.4 | PM | Ch2·02, Ch6·01 |
| CSS | Theo công thức khảo sát CSS, điểm | 80 / 90 / 100 | Sales | Ch2·02, Ch6·01 |
| DRE | Bug nội bộ / (bug nội bộ + bug KH) | 0.94 / 0.98 / 1.0 | PQA | Ch2·02, Ch6·01 |
| Leakage | Tổng bug sau release / công số thực tế (theo rank), Bug/MM | 0 / 0.15 / 0.3 | PQA | Ch2·02, Ch6·01 |
| EE | (Re-estimate + CR charge) / MM × hệ số rank | 95% / 100% / 110% | PM | Ch2·02, Ch6·01 |
| Timeliness | SP đúng hạn / Tổng SP × 100% | 100% / 100% / 100% | PM | Ch2·02, Ch6·01 |
| Process Compliance | Tổng điểm TB các item PQA audit | 85 / 92.46 / 100 | PQA | Ch2·02, Ch6·01 |
| Correction Rate | Công số Correction (fix + verify bug) / công số thực tế (theo rank) | không có ngưỡng cố định | PM | Ch2·02, Ch6·01 |
| Tỉ lệ comment code | Số comment / LOC (LOC = dòng thay đổi) | không có ngưỡng cố định | TL | Ch2·02, Ch6·01 |
| Chất lượng testcase | (comment nội bộ + feedback KH) / total TC | không có ngưỡng cố định | TestLead | Ch2·02, Ch6·01 |
| Dự án Document: Feedback rate KH | Comment KH / số page (sheet Excel + page doc) | không có ngưỡng | PM | Ch2·02, Ch6·01 |

Cách đọc: Bug rate < 3.55 có thể test chưa kỹ, > 8.4 nghiêm trọng. DRE < 0.94 khách phát hiện quá nhiều bug. Leakage 0.15 ≈ 1 bug mỗi 7 MM, > 0.3 nghiêm trọng. EE < 95% vượt ước lượng, > 110% ước lượng dư (Ch6·01).

### 2.4 Ngưỡng theo loại hợp đồng (DRAFT chờ QA công ty) (Ch6·01)

| Tín hiệu | Fixed-bid | T&M | Offshore | R&D | Internal | Compliance |
|---|---|---|---|---|---|---|
| QS-REQ-01 | ≥ 95% | ≥ 90% | ≥ 92% | ≥ 85% | ≥ 90% | ≥ 100% |
| QS-DSG-03 | ≤ 5% | ≤ 7% | ≤ 6% | ≤ 10% | ≤ 7% | ≤ 3% |
| QS-DEV-cov | ≥ 85% | ≥ 75% | ≥ 80% | ≥ 70% | ≥ 75% | ≥ 90% |
| QS-PRC-07 | ≥ 95% | ≥ 88% | ≥ 90% | ≥ 80% | ≥ 88% | ≥ 95% |
| QS-TST-04 | ≤ 2% | ≤ 3% | ≤ 2.5% | ≤ 5% | ≤ 3% | ≤ 1% |
| E3 | ≤ 10% | ≤ 15% | ≤ 12% | ≤ 25% | ≤ 15% | ≤ 8% |
| CPI | ≥ 0.95 | ≥ 0.90 | ≥ 0.92 | ≥ 0.85 | ≥ 0.90 | ≥ 0.95 |
| SPI | ≥ 0.95 | ≥ 0.90 | ≥ 0.92 | ≥ 0.85 | ≥ 0.90 | ≥ 0.95 |

Đối chiếu 3 hệ (Ch6·01): DRE 0.94-1.0 ~ QS-TST-*; leakage ≤ 0.3 ~ QS-TST-04 ≤ 2%; EE 95-110% ~ E3 ≤ 10% ~ CPI ≥ 0.95; Timeliness 100% ~ SPI ≥ 0.95; Process Compliance 85-100 ~ QS-PRC-07 ≥ 90%.

## 3. Công thức tính

| Nhóm | Công thức | Bài |
|---|---|---|
| Đổi đơn vị | 1 MM = 20 MD = 160 MH; Tổng MM = Tổng MD / 20; 1 md = 8 mh | Ch0, Ch2·01, Ch3·03, Ch6·03 |
| Giá chào | cost_per_role = effort_md × daily_rate; subtotal = tổng; customer_quote = subtotal × (1 + margin), margin mặc định 20% | Ch1·01 |
| Timeline bid | working_days = total_effort_md / (team_size × utilization); calendar_duration = working_days + buffer_days + UAT window | Ch1·01 |
| WSJF | CoD / Job Size; CoD = User-Business Value + Time Criticality + Risk Reduction & Opportunity Enablement (thang 1, 2, 3, 5, 8, 13, 20) | Ch1·01 |
| RICE | (Reach × Impact × Confidence) / Effort (person-month) | Ch1·01 |
| ICE | (Impact × Confidence × Ease) / 3, mỗi thành phần 1-10 | Ch1·01 |
| Điểm tổng hợp bid | Final = w1×WSJF + w2×RICE + w3×Strategic Fit + w4×Resource Match (ví dụ 0.35 / 0.25 / 0.25 / 0.15) | Ch1·01 |
| Gap năng lực | gap = capacity − committed_effort − (pipeline_demand × win_probability); weighted demand = công số bid × xác suất thắng | Ch1·02 |
| Utilization lịch | Planned (md) / SBU Capacity; cảnh báo > 100% (OVER) hoặc < 50% (UNDER) | Ch3·03 |
| Buffer lên đường găng | Cộng buffer % theo hợp đồng (ví dụ nguồn: 65 ngày + 10 = 75 với 15%) | Ch3·03 |
| Utilization sprint | effort_committed(role) / capacity_available(role) × 100% | Ch3·04 |
| Velocity check | \|effort_selected − velocity_actual\| / velocity_actual > 20% thì cảnh báo; velocity_ratio = actual / planned | Ch3·04 |
| Team match single | score = w_skill×skill_match + w_avail×avail_norm + w_comp×competency_norm; mặc định 0.5 / 0.3 / 0.2 | Ch3·05 |
| skill_match, avail_norm, competency_norm | avg(min(level_actual/level_required, 1.0)); avail_pct/100; avg(skill_level/5) | Ch3·05 |
| Mức rảnh | avail_pct = max(0, 100 − tổng trừ tải); timeestimate: load_pct += min(50, giờ ước × 5) | Ch3·05 |
| Team match batch | jira_avail_pct = max(0, 100 − jira_load); initial_avail_pct = min(jira_avail_pct, participation_rate); effort_pct_equiv = effort_md × 10 | Ch3·05 |
| Điểm batch | assign_score = w_role×role_fit + w_avail×avail_fit + w_level×level_fit, mặc định 0.35 / 0.45 / 0.20; level_fit = min(proxy_level/expect_level, 1.0); balanced: adjusted = assign_score − 0.05 × số task đã gán | Ch3·05 |
| EVM cơ bản | EV = planned × % hoàn thành; AC = actual; PV = planned đến hiện tại; CPI = EV/AC; SPI = EV/PV | Ch6·01, Ch6·03 |
| Variance | actual − planned; Variance % = (actual − planned) / planned × 100% | Ch6·03 |
| EAC / ETC / VAC (EVM) | EAC = AC_total + (BAC − EV_total) / CPI; ETC = EAC − AC_total; VAC = BAC − EAC (âm = vượt ngân sách) | Ch6·03 |
| EAC / ETC (hệ số chênh lệch) | ETC = Σ(planned task còn lại × variance factor); EAC = actual_to_date + ETC; ví dụ 96 + 64 = 160 md, VAC −15 md | Ch6·03 |
| SPI / SV proxy (tuần) | SPI = actual_tasks_done / planned_tasks_this_week; SV = actual_tasks_done − planned_tasks_this_week | Ch7·01 |
| E3 (3 dạng) | (actual − planned)/planned × 100% (Ch6·01, Ch6·03); actual% − planned% (Ch7·01 bản chính) (nguồn chưa rõ) | Ch6·01, Ch7·01 |
| % complete, forecast tuần | done/total × 100; weeks_left = remaining_tasks / avg_velocity; projected_end = hôm nay + weeks_left × 7 ngày (avg 4 tuần gần nhất) | Ch7·01 |
| EAC / ETC (tuần) | EAC = actual_effort_to_date + remaining_tasks × avg effort remaining; ETC = EAC − actual_effort_to_date | Ch7·01 |
| Scope growth | (features_added − features_removed) / total_original × 100; current = original + added − removed | Ch6·04 |
| Effort baseline | effort_current = effort_original + effort_delta; effort_delta_% = effort_delta / effort_original × 100; version v<major>.<số CR duyệt> | Ch6·04 |
| Scope creep tuần | unplanned_tasks_in_progress / total_in_progress × 100 | Ch7·01 |
| Chi phí CR (T&M) | cost delta = effort delta (md) × đơn giá (ví dụ $400/md) | Ch4·03 |
| MM_used (Base) | Σ[(logwork_jira − OT_chưa_hệ_số + OT_đã_hệ_số) × hệ_số_rank] / 8 / 20 | Ch2·02, Ch6·01 |
| MM_used (Labor) | TH1 và TH3: / 8 / số ngày đi làm thực tế; TH2: / 8 / 20 | Ch2·02 |
| EE | (Re-estimate + CR charge) / MM_used × hệ số rank | Ch2·02, Ch6·01 |
| Risk score nâng cao | score = probability × impact × category_weight; EMV = probability × financial_impact | Ch4·04 |
| Trọng số nhóm rủi ro | Technical 1.2, Resource 1.1, Schedule 1.0, Financial 1.4, Scope 1.1, Dependency 1.0, Operations 1.0, Compliance 1.2, Safety 1.3 | Ch4·04 |
| Chiến lược theo score | ≥ 18 AVOID; 12-18 MITIGATE; 8-12 TRANSFER; < 8 ACCEPT (biên chồng nhau, nguồn chưa rõ) | Ch4·04 |
| Chỉ số rủi ro tuần | Mitigation velocity = closed / raised; Action completion % = DONE / (tổng − CANCELLED), mẫu 0 thì in "— (0 action)" | Ch4·04 |
| Checklist pass rate | Pass / (Total − N/A) × 100% | Ch6·02 |
| Worklog compliance | logged_people / active_people × 100 (logged = worklog ≥ 0.5 giờ) | Ch4·02 |
| Stale | N = max(0, ngày báo cáo − ngày updated) | Ch4·02 |
| Bug triage | Working set = tổng − Rejected; genuine bug = OPEN − SPEC_GAP; % đóng = round(CLOSED/TOTAL×100) | Ch6·05 |
| Bảng số liệu HTML | thanh module: MOD_TOTAL/TOTAL×100 và MOD_OPEN/TOTAL×100 | Ch6·05 |
| Meeting | Ask % (theo loại họp), câu hỏi dẫn dắt %, đóng %, filler/phút, hedging/phút | Ch7·02 |
| Ngưỡng hypercare | p95 ≤ baseline × 1.10 (ví dụ 180 → 198 ms); error ≤ baseline + 0.5% (0.3% → 0.8%); phiên ≥ baseline − 10% (1000 → 900) | Ch8·04 |

## 4. Ngưỡng cảnh báo theo chủ đề

| Chủ đề | Cảnh báo (vàng) | Đỏ / hành động | Bài |
|---|---|---|---|
| Tín hiệu QS | lệch 5-10% | lệch > 10% | Ch6·01 |
| Effort E3 | 10-15% (bản effort variance) | > 15%; CPI < 0.85 nghiêm trọng, leo thang | Ch7·01, Ch6·03 |
| E3 (actual% − planned%) | −5% đến −10% | < −10% (hoặc milestone slip) | Ch7·01 |
| CPI / SPI (chuẩn) | dưới ngưỡng hợp đồng (mặc định ≥ 0.90 T&M, ≥ 0.95 Fixed-bid) | SPI < 0.9 đèn đỏ tuần; SPI < 0.7 họp khẩn PM + Sponsor | Ch6·01, Ch7·01 |
| SPI proxy tuần | 0.9-1.0 | < 0.9 | Ch7·01 |
| SV proxy tuần | −1 đến −2 | ≤ −3 | Ch7·01 |
| Overdue | 1-2 task ≤ 3 ngày | ≥ 3 task hoặc > 3 ngày | Ch7·01 |
| Blocker (tuần) | 1-2 | ≥ 3 hoặc chặn milestone | Ch7·01 |
| Scope creep (tuần) | > 10% (ứng viên > 10% thì vàng) | > 20% (PM xác nhận trước khi đi tiếp) | Ch7·01 |
| Forecast trễ | 1-7 ngày (cách khác: < 1 tuần) | > 7 ngày (cách khác: ≥ 1 tuần) | Ch7·01 |
| Issue tác động cao mở | 3-5 ngày | > 5 ngày, leo thang Tech Lead | Ch7·01 |
| Vượt chronic theo stage | - | ≥ 5 task cùng stage, chênh lệch TB > 10% | Ch6·03 |
| Nút thắt vai trò | chênh lệch theo vai trò > 50% | xem vai trò/tải, không đổ lỗi cá nhân | Ch6·03 |
| Sprint capacity | utilization ≥ 90% WARN | > 100% OVER (hỏi PM: cắt / tăng capacity / dời sprint) | Ch3·04 |
| Sprint velocity | - | lệch > 20% so với velocity_actual | Ch3·04 |
| Capacity tuần lịch | - | utilization > 100% OVER hoặc < 50% UNDER | Ch3·03 |
| Gap năng lực (md/quý) | Underutilized > +50; Overcommit −10 đến −50 | Critical < −50 | Ch1·02 |
| Healthy | −10 đến +50 | - | Ch1·02 |
| Bug rate | < 3.55 (test chưa kỹ) | > 8.4 nghiêm trọng | Ch6·01 |
| DRE / leakage | DRE < 0.94 | leakage > 0.3 | Ch6·01 |
| Bug triage: bug KH | < 10% chỉ Medium/Low = QA tốt | > 30% kèm Critical/High = cổng QA chưa đủ | Ch6·05 |
| Bug triage: quy trình | Resolved + DEV quá 4h; Done + QA; Deployed + DEV; thiếu 1 trong 4 trường bắt buộc | cờ vi phạm | Ch6·05 |
| Checklist | Standard fail > 20% = REVIEW | Critical fail > 0 = BLOCK | Ch6·02 |
| Gate | 1 tín hiệu vàng (5-10%) = HOLD | ≥ 1 đỏ hoặc Critical checklist fail = ABORT; HOLD > 5 ngày làm việc leo thang | Ch8·02 |
| Release: cửa sổ | window lệch go-live charter > 2 tuần thì gắn cờ | - | Ch8·01 |
| Rollback | - | Critical bug > 30% người dùng trong 4h; hiệu năng suy giảm > 50%; customer escalation P1; DB migration hỏng dữ liệu; RTO 30 phút | Ch8·01, Ch8·03 |
| Hypercare | vượt ngưỡng = Watch | P1 = Alert, dừng thường kỳ; uptime < 99.5%; p95 > baseline + 10%; error > baseline + 0.5%; phiên < baseline − 10%; bug KH > 2 P1/ngày; lọt critical ≠ 0 | Ch8·04 |
| Rủi ro: Likelihood | L < 30%; M 30-70%; H > 70% | - | Ch4·04 |
| Rủi ro: xu hướng | Mitigation velocity < 0.5; exposure > 2 lần baseline | Action completion < 50% với High/Critical; action quá hạn (đỏ); DONE thiếu Evidence (vàng) | Ch4·04 |
| Daily report R01-R11 | xem 4.1 | xem 4.1 | Ch4·02 |
| Họp (coaching) | Dominance > 60% từ; độc thoại > 60 giây hoặc > 200 từ; filler > 5/phút; hedging > 3/phút | lecture mode: > 2 độc thoại > 200 từ | Ch7·02 |
| CR (mức nghiêm trọng) | xem 4.2 | xem 4.2 | Ch4·03 |
| Action item retro | thiếu owner/deadline | không chấp nhận "Team", "ASAP" | Ch7·04 |
| Bàn giao / closeout | - | Critical/High mở ≠ 0 thì không đóng; cần 4 chữ ký | Ch9·02 |

### 4.1 Cờ daily report (Ch4·02)

| Mã | Mức | Điều kiện |
|---|---|---|
| R01 GHOST | đỏ | phân bổ ≥ 10%, không hoạt động Jira/Bitbucket trong cửa sổ |
| R02 BUS_FACTOR | đỏ | một người ≥ 70% PR merged + cập nhật Jira (cuộn 7 ngày) |
| R03 WORKLOG_GAP | vàng | có PR/commit nhưng 0 worklog hôm qua |
| R04 WORKLOG_TEAM | vàng | tuân thủ worklog team < 50% |
| R05 ALLOCATION_EXPIRED | đỏ | ngày kết thúc phân bổ < hôm nay mà vẫn hoạt động |
| R06 PR_JIRA_DRIFT | vàng | PR đã merge mà Jira không thuộc {Done, Resolved, Deployed} |
| R07 STALE_PR | vàng | PR OPEN không hoạt động > 24h |
| R08 BLOCKER_AGING | vàng | blocker không đổi > 2 ngày làm việc |
| R09 UNASSIGNED_WIP | vàng | In Progress không có assignee |
| R10 IDENTITY_GAP | vàng | không ghép được người dùng với roster |
| R11 OVERALLOCATED | vàng | tổng phân bổ qua các dự án > 100% |

### 4.2 Mức nghiêm trọng CR (Ch4·03)

| Mức | Lịch | Effort | Chi phí | Đề xuất |
|---|---|---|---|---|
| Trivial | 0 ngày | < 1 md | < $500 | APPROVE (Trivial/Low, giá trị rõ) |
| Low | 1-3 ngày | 1-5 md | $500-$2k | APPROVE |
| Medium | 4-10 ngày | 5-15 md | $2k-$10k | APPROVE kèm điều kiện (giá trị rõ) |
| High | 11-30 ngày | 15-40 md | $10k-$50k | APPROVE kèm re-plan (giá trị Critical); DEFER (giá trị không rõ) |
| Critical | > 30 ngày | > 40 md | > $50k | REJECT, thương lượng lại phạm vi (vượt ngân sách) |

## 5. Quy tắc cố định

| Quy tắc | Giá trị | Bài |
|---|---|---|
| Đơn vị effort | 1 MM = 20 MD = 160 MH; 1 md = 8 mh | Ch0, Ch3·03 |
| Tuần / múi giờ | ISO 8601 Thứ Hai-Chủ Nhật, `YYYY-Www`; 5 ngày làm việc/tuần; UTC+7 (báo cáo daily: Asia/Ho_Chi_Minh) | Ch0, Ch7·01, Ch4·02 |
| Task | ≤ 1 md, không chuyển sang ngày sau (Iron Law); > 1 md phải tách T-001.1, T-001.2 | Ch0, Ch3·02 |
| Hệ số ước lượng | REQ 0.5; BD/DEV S=0.5, M=1, L=1.5; UT 0.5; TC 0.5-1; TE 0.5-1; BV 0.5; TP/TVP/TR 1 mỗi loại | Ch0, Ch3·02, Ch3·03 |
| Effort PM mặc định | PM-KICKOFF 2; PM-PLAN 3; PM-TRACK 0.5/tuần; PM-GATE 1/gate; COMM 0.5/tuần | Ch3·03 |
| Buffer theo hợp đồng (DRAFT) | Fixed-bid 15%; T&M 10%; Offshore 20%; R&D 25%; Internal 10%; Compliance 20% | Ch0, Ch3·03 |
| Buffer bid | Fixed-bid +15%, T&M +10%, Offshore +20%, R&D +25%; miền mới không lịch sử +10% extra; banking +10% tổng; lesson L-2026-001 +25% phase Design | Ch1·01 |
| Phase distribution (bid) | Requirements 8% / Design 18% / Development 50% / Testing 18% / Project Mgmt 6%; system test ≈ 30% công Dev | Ch1·01, Ch2·01 |
| Quy mô bid | S 40-80 md (1-3 tháng); M 100-160 md (3-6 tháng); L 160-350 md (6-12 tháng); XL 350+ md (12+ tháng); điều chỉnh ±20% | Ch1·01 |
| Margin bid | mặc định 20%; Sales quyết, ghi `margin_override` nếu đổi | Ch1·01 |
| Ngưỡng E3 | 10% | Ch0 |
| Sprint | mặc định 2 tuần = 10 ngày làm việc; 1 md ≈ 10% (sprint 2 tuần), sprint 1 tuần PM đặt 8 | Ch3·04, Ch3·05 |
| Chọn task sprint | High → Medium → Low, cùng ưu tiên theo Task ID | Ch3·04 |
| Hypercare | Major 7 ngày, Minor 3, Patch 1, Hotfix 24 giờ (review Hotfix mỗi 4h, còn lại hằng ngày); không rõ loại thì mặc định Major 7 ngày | Ch0, Ch8·01, Ch8·04 |
| RTO rollback | 30 phút; người quyết định rollback: PM (tham vấn Tech Lead + Sponsor) | Ch8·01 |
| Escalation rủi ro (chưa xử lý sau) | Critical 1 ngày (lên Sponsor ngay); High 3 ngày (PM Lead / Sponsor hàng tuần); Medium 7 ngày (xem báo cáo tuần); Low 14 ngày (xem hàng tháng); có thể ghi đè theo dự án | Ch4·04 |
| Escalation trong RACI | L1 mâu thuẫn đội: PM trong tuần; L2 nguồn lực/scope/rủi ro: PM Lead + SBU Manager trong 3 ngày; L3 chiến lược/khách hàng: Sponsor + Director trong 1 ngày; L4 khủng hoảng: CEO + Legal | Ch2·01 |
| Hold gate | review lại +5 ngày làm việc; quá hạn thì PM báo Sponsor | Ch8·02 |
| Mỗi việc chỉ 1 A | RACI: nhiều R/C/I được, không ô trống; chỉ ghi vai trò, không ghi tên | Ch2·01 |
| Rủi ro seed | Fixed-bid mặc định 8; T&M mặc định 6; thêm phần Offshore/R&D/Internal | Ch2·01 |
| Sign-off spec | READY khi số Must-fix Open = 0 (kể cả chưa có item M nào) | Ch2·03 |
| Baseline lịch | lưu bản cũ `schedule-v{N}-YYYYMMDD` hoặc `schedule.v<N>.md`; chỉ ghi lịch mới sau khi sponsor ký CR | Ch3·03, Ch4·03 |
| Nguồn thiếu dữ liệu | Ghi `[NO_DATA]`/⏳ TBD, không bịa; mâu thuẫn nguồn thì dừng và hỏi | toàn giáo trình |
| Daily window | ngày chạy + ngày làm việc liền kề trước (Thứ Hai gộp cuối tuần); overdue standup không tính Resolved/Deployed | Ch4·01 |
| Ghi công | theo người thực hiện (changelog), không theo assignee hiện tại | Ch4·01, Ch4·02 |
| Blocker Jira công ty | (không phải Bug + status Confirmming) hoặc (Bug + status khác Done); loại Rejected/Pending | Ch4·01, Ch4·02 |
| Team match | trọng số single 0.5/0.3/0.2, batch 0.35/0.45/0.20; loại nếu avail_pct < effort_pct hoặc score < 0.5; cảnh báo nếu < 5 người đạt; ghi `[PROXY]` khi level suy từ chức danh | Ch3·05 |
| Trừ tải ticket | In Progress/In Review/Testing −25%; To Do/Open có duedate trong timeline −15%; Confirmming/chờ KH −10%; ticket cập nhật trong 90 ngày | Ch3·05 |
| Capacity forecast | xác suất thắng đưa vào mặc định 40%; tuyển senior 2-3 tháng; điều chuyển SBU cần 2 SBU Manager; không khuyến nghị làm thêm giờ | Ch1·02 |
| Retro | mỗi nhóm 1-5 mục (sprint) hoặc 1-3 mục START/STOP/CONTINUE (lessons); brainstorm im lặng 5 phút; 3 dot vote; retro sự cố nghiêm trọng trong 48 giờ (5 Whys) | Ch7·04, Ch9·01 |
| Nhịp retro | nhỏ < 3 tháng: cuối phase + cuối dự án; vừa 3-6 tháng: cuối mỗi phase; lớn 6+ tháng: mini 2 tuần/lần + cuối phase + cuối dự án | Ch9·01 |
| Bảo mật | không ghi mật khẩu/token/khóa; chỉ "see vault: <đường dẫn>"; webhook che `***`; registry quyền `600`, không commit | Ch1·03, Ch5·01, Ch9·02 |
| Onboarding | brief hiển thị top 3 rủi ro, tối đa 3 milestone; standup đầu = ngày bắt đầu + 1 ngày làm việc; hạn D1, D2, W1 | Ch5·02, Ch5·03 |
| Tiếp quản PM | cửa sổ status 12 tuần ISO; phân trang 50; policy skip-existing (mặc định) | Ch5·04 |
| CM Plan riêng | dự án ≥ 10MM hoặc ≥ 3 member; nhỏ hơn ghi inline mục 17 | Ch2·02 |
| Chi phí phát sinh mặc định | đi lại 5.000.000; công tác phí 30.000.000; thiết bị 15.000.000; teambuilding 5.000.000; tổng 55.000.000 VND | Ch2·02 |
| Mã định danh | Charter `<PROJ>-YYYY-NNN`; Bid `BID-YYYY-NNN`; Feature `F-<PROJ>-<MOD>-NN`; Release `R-<PROJ>-NN`; Risk `R-<CAT>-NN`; Issue `ISSUE-NNN`; Action `MA-NNN`/`RA-NNN`; CR `CR-<NN>`; Lesson `L-YYYY-NNN`; Review item `RC-<feature>-NNN` | Ch1·01, Ch2·01, Ch2·03, Ch4·03, Ch4·04, Ch8·01, Ch9·01 |
| Ma trận Level rủi ro (L × I) | Low: Low/Low/Medium/High; Medium: Low/Medium/High/Critical; High: Medium/High/Critical/Critical (cột Impact Low/Medium/High/Critical) | Ch4·04 |
| Calibrate Impact scope/estimate | Fixed-bid Critical; T&M giờ thực tế Medium; T&M MM cam kết High; Offshore Medium; Internal R&D Medium (bản nháp) | Ch4·04 |

## 6. Nhịp việc

| Nhịp | Việc | Bài |
|---|---|---|
| Hằng ngày (GĐ 5-9) | Daily sync đầu ngày (prep ~8:30, capture sau họp); daily report sáng; kiểm effort task ≤ 1md; hypercare snapshot mỗi ngày (Hotfix mỗi 4h) | Ch0, Ch4·01, Ch4·02, Ch6·03, Ch8·04 |
| Hằng tuần | Status weekly (chiều thứ Sáu, Friday EOD); signal monitor; effort actuals (variance); REVIEW sổ rủi ro; scope creep; 3P line manager (cuối chiều thứ Sáu) | Ch0, Ch7·01, Ch6·01, Ch6·03, Ch4·04, Ch7·03 |
| Sprint (2 tuần) | Sprint plan đầu sprint; Sprint retro cuối sprint | Ch3·04, Ch7·04 |
| Theo sự kiện | Change request; rủi ro/issue mới; ESCALATE; phân tích họp; checklist trước gate; thông báo stakeholder; bàn giao/onboarding thành viên; tiếp quản PM; bug triage; scope baseline (mỗi CR duyệt) | Ch0, Ch4·03, Ch4·04, Ch5·01-04, Ch6·05, Ch6·04 |
| Theo giai đoạn / gate | Checklist trước gate; Gate review cuối GĐ; WBS, task list, schedule (một lần/giai đoạn); retro cuối phase | Ch0, Ch6·02, Ch8·02, Ch9·01 |
| Một lần / dự án | Setup registry; Kickoff/charter; Project plan; chốt spec; lessons learned; closeout | Ch1·03, Ch2·01-03, Ch9·01, Ch9·02 |
| Một lần / release | Release plan → gate G5/G6 → release exec → hypercare | Ch8·01-04 |
| Liên dự án | Ước lượng bid (trước mỗi bid); dự báo năng lực (PM Lead chạy; hằng quý hoặc trước khi cam kết bid) | Ch0, Ch1·01, Ch1·02 |
| Tần suất truyền thông | 3P cuối tuần phòng ban sáng thứ Hai; cá nhân Chủ nhật; tổng hợp nhiều team 2 tuần; newsletter công ty tuần hoặc 2 tuần, SBU tháng, dự án mỗi milestone, khách hàng quý; nội bộ hằng tuần, đối ngoại 2 tuần | Ch7·03 |
| Sales-AM | họp cùng 1 KH ít nhất 1 tháng/1 lần | Ch2·01 |
| PQA | kiểm toán hàng quý (và theo milestone) | Ch2·02 |

## 7. Mẫu đầu ra chính (mục bắt buộc, 1 dòng)

| Tài liệu | Mục bắt buộc | Bài |
|---|---|---|
| Bid Estimate (DRAFT) | Bảng thông tin; 1 Scope; 2 Effort (Phase/%/md, Subtotal, Buffer, Risk markup, TOTAL); 3 Cost + quote Low/Mid/High; 4 Timeline; 5 Capacity Check; 6 Top 5 Risks; 7 Win/Loss (GO/HOLD/NO-GO); 8 Sales Action Items | Ch1·01 |
| Capacity Forecast | Metadata; Summary SBU; Per-month; Active Projects; Pipeline (weighted); Overcommit Alerts; Bench; Recommendations (Action/Owner/Timeline); Data Sources | Ch1·02 |
| Registry dự án | jira_key, bitbucket_project_key, ksystem_project_code (bắt buộc); tùy chọn name, bitbucket_repos, teams_webhook_url, docs_root | Ch1·03 |
| Project Charter TPL-SM-02-01 v1.3 | Metadata + 11 mục: (1) Nội dung, (2) KH, (3) Bối cảnh, (4) Scope, (5) Nền tảng, (6) Schedule, (7) Ước lượng, (8) Team, (9) Tư liệu KH, (10) Sản phẩm bàn giao, (11) Điều kiện thỏa thuận + Approval + phụ lục Sales/AM | Ch2·01 |
| RACI | mức dự án, feature, tài liệu, truyền thông; mỗi việc 1 A; kèm 4 mức escalation | Ch2·01 |
| Risk register (khởi điểm) | ID, Title, Category, Likelihood, Impact, Level, Mitigation, Owner (+ Closed Risks) | Ch2·01 |
| Project Plan TPL-SW-05-01 v1.7 | Bìa + lịch sử + 22 mục (thông tin chung, chỉ số LCL/Target/UCL, tailoring 11 PROC, review, test, ước tính, milestone, truyền thông, rủi ro, PQA, nhân sự, CM, đào tạo…) + 3 bảng rà 🤖/⏳/💭 + Sign-off PM/Giám đốc SBU-CTO/PQA | Ch2·02 |
| Spec Review Tracker | Metadata (feature, round R<N>, date, reviewers, source, Sign-off Status); Open Items (ID, Description, Section Ref, Raised By, Category M/N/A/D, Status); Summary | Ch2·03 |
| WBS | 7 phase; deliverable; WP `WP-<STAGE>-NN`; milestone + signal anchor; Feature→WP Coverage; Validation | Ch3·01 |
| Task list | ID, Function, Module, Stage, Title, Description, Source, AC, Depends on, Est, Status, Tags + metadata spec_version | Ch3·02 |
| Schedule | Milestone & Signal Anchor; Task Schedule; Critical Path (+ buffer); Capacity Check; Roles Summary | Ch3·03 |
| Sprint NN | Sprint Goal (chép nguyên văn PM); Capacity Summary; Sprint Backlog; Excluded Tasks | Ch3·04 |
| Team Match | Single: Top Candidates + Score breakdown + Conflicts; Batch: Assign by task + Plan by member + Unassigned | Ch3·05 |
| Daily Sync | Blockers (đầu file); Done Yesterday; In Progress; Overdue; New Today; Git Activity; Quick Asks; (capture) Standup Capture | Ch4·01 |
| Daily report | PM summary: 1 Hôm qua làm gì; 2 Block/vướng; 3 Rủi ro; Red Flags; Số liệu nhanh. Chi tiết team: Nhìn nhanh; 4 bảng checkpoint; Quy trình; Tổng kết nhanh | Ch4·02 |
| Change Request | Field; 1 Spec Diff; 2 Impact (Schedule/Effort/Risk/Quality/Resource); 3 Severity; 4 Recommended Decision; 5 Sponsor Approval; 6 If Rejected | Ch4·03 |
| Risk / Issue log | Active Risks 14 cột; Mitigation Actions 7 cột; Closed Risks 4 cột; Active Issues 11 cột; Resolution Actions | Ch4·04 |
| Member Handover Plan TPL-HR-14-01 | Thông tin; §1 Tổng quan; §2 Ma trận 13 mục; §3 Đầu việc; §4 Kiểm kê ticket; §5 Tài liệu; §6 Môi trường; §7 Lịch bàn giao; §8 Ghi chú; Lịch sử | Ch5·01 |
| Onboarding brief | 1 Overview; 2 Phase & Milestones; 3 Assigned Tasks; 4 Top 3 Risks; 5 Key Contacts; 6 Links; 7 Day 1 Checklist | Ch5·02 |
| Onboarding todo | 12 trường (id, group, task, role, assignee, support, location, location_url, priority, due, status, note); 4 nhóm A/B/C/D | Ch5·03 |
| Bộ hồ sơ seed (tiếp quản PM) | banner synced-from; schedule; status/YYYY-WW; gates (proxy); risk; cr + INDEX; (closeout) charter + effort; SYNC-MANIFEST | Ch5·04 |
| Signal Snapshot | Metadata; Alerts (đỏ lên đầu); Signal Status; Trend; Suggested Actions (Owner/Target); Data Sources | Ch6·01 |
| Checklist Run | Metadata; Summary (Total/Pass/Fail/N-A/Critical/Pass rate); Items by Section; Critical Fails; Reviewer Sign | Ch6·02 |
| Effort Actuals | Summary (Planned/Actual/Variance/E3/CPI/SPI/EAC/VAC); Variance Breakdown (Phase/Role/Stage); Pattern Found; Forecast; Recommended Actions | Ch6·03 |
| Scope Baseline | Metadata; Summary Stats; Original Contract Scope; CR Delta Table; Current Scope | Ch6·04 |
| Bug Triage (8 phần) | KPI Summary; theo module; Category; Customer vs Internal; hành động bug Open; tuân thủ; Spec gap chờ PM; khuyến nghị | Ch6·05 |
| Weekly Status | Summary; Forecast; 2 Progress; 3 Signal; 4 Milestone; 5a Risks; 5b Issues; 6 Next week; 10 Recommended Actions | Ch7·01 |
| Meeting Analysis | Coaching Summary (CONTINUE/START/STOP); Speaking Dynamics; Question Pattern; (Action Items); Conflict/Blocker; Cross-meeting trend | Ch7·02 |
| Thông điệp stakeholder | Sponsor ≤ 1 trang; Khách 1-2 trang; Team ngắn; 3P mỗi phần ≤ 5 gạch, mỗi gạch ≤ 2 dòng; Newsletter 3-5 phút; Steering 5-10 slide (8 slide mẫu); Slack ≤ 280 ký tự | Ch7·03 |
| Sprint Retro | Sprint Info; Went Well; Didn't Go Well (+ gợi ý AI-01…AI-15); Blockers; Carry-forward; Action Items (owner + deadline) | Ch7·04 |
| Release Plan | 1 Templates; 2 Scope; 3 Gate Criteria G1-G6; 4 Readiness; 5 Deploy Schedule; 6 Rollback Plan; 7 Open items | Ch8·01 |
| Gate Review | 1 Criteria Check (Signals, Checklists, Risk); 2 Proposed Decision; 3 Stakeholder Approval; 4 Action items | Ch8·02 |
| Release Execution Log | Pre-execution Checks; Execution Timeline (prereq/walk); Rollback Trigger Monitoring; Post-deploy Validation; Next Steps | Ch8·03 |
| Hypercare Log | Signal Health; Daily Snapshots; Incidents Log (ID, Severity, RTO); Customer Feedback; Exit Criteria; Next Steps | Ch8·04 |
| Lessons Learned | Numbers Summary; 4-Dimension Review (Process, Team, Customer, Technical × START/STOP/CONTINUE); Action Items (Owner, Due, Success Criteria); Lessons for Catalog `L-YYYY-NNN`; Sign | Ch9·01 |
| Project Closeout | 1 Scope; 2 Schedule; 3 Effort/Cost; 4 Quality; 5 Risk; 6 Handover; 7 Customer Sign-off; 8 Team Release; 9 Archive Checklist; 10 Sign-off (PM, Sponsor, Customer PIC, Support Lead) | Ch9·02 |

## 8. Top lỗi hay gặp (mỗi bài 1-2 ý)

| Bài | Lỗi quan trọng nhất |
|---|---|
| Ch0 | Bỏ hypercare để đóng sớm; quyết gate bằng cảm tính thay vì tín hiệu + checklist; không nạp lessons vào báo giá sau |
| Ch1·01 | Tự đoán phạm vi/bịa đơn giá khi thiếu brief/rate card; quên UAT/go-live và capacity khi tính lịch; gửi báo giá chưa qua Sales + Delivery review |
| Ch1·02 | Cộng nguyên công số bid mà không nhân xác suất thắng; quên thời gian tuyển 2-3 tháng; tự kích hoạt tuyển/bỏ bid |
| Ch1·03 | Đoán Jira/Bitbucket key; commit registry/webhook vào git hoặc hiện webhook rõ |
| Ch2·01 | Nhiều A trên một việc; ghi tên người vào RACI; đoán khi thiếu SRS; NFR không có tiêu chí thành công (`[NEEDS_CONFIRM]`) |
| Ch2·02 | Bỏ hạng mục quy trình bắt buộc mà không có lý do (X kèm lý do); đổi tùy ý LCL/Target/UCL cố định; tính MM đội VN kèm BrSE Nhật |
| Ch2·03 | Tự đoán nhóm item mơ hồ nên READY sai; đánh số lại ID ở vòng mới; bỏ qua item Deferred (scope creep ngầm) |
| Ch3·01 | Milestone phase 2-6 không gắn tín hiệu; nhét task chi tiết vào WBS; tự đổi ngưỡng mặc định |
| Ch3·02 | Task > 1md không tách; bịa AC/Est/dependency (để trống + `⚠ cần PM`); xóa cứng task của section bị bỏ (dùng `deprecated`) |
| Ch3·03 | Dùng heuristic cũ REQ:1/BD:2/DEV:3; bỏ tuần OVER capacity; sửa đè lịch cũ khi có CR (phải archive) |
| Ch3·04 | Tự bỏ task khi vượt capacity không hỏi PM; tính utilization theo cả đội thay vì từng vai trò; paraphrase sprint goal |
| Ch3·05 | Coi level suy từ chức danh là thật (phải ghi `[PROXY]`); bỏ qua trần participation; tin điểm số tuyệt đối |
| Ch4·01 | Hardcode nhánh `develop`; đưa Resolved/Deployed vào overdue standup; ghi công theo assignee; ghi đè file prep khi capture |
| Ch4·02 | Ghi công theo assignee; đọc worklog chỉ một tập con ticket; dùng `updated` thay `resolved` cho Task Done; văn phong hành chính khó hiểu |
| Ch4·03 | Sửa lịch chính trước khi sponsor ký; bỏ chiều chất lượng (QS-REQ-03, QS-DEV-cov); quên đưa rủi ro phát sinh vào sổ risk |
| Ch4·04 | Mitigation "monitor" (chấp nhận trá hình), Owner là "team"; để OPEN khi hậu quả đã xảy ra (phải ESCALATE); thêm action quên cập nhật cột Actions của cha |
| Ch5·01 | Dán mật khẩu vào kế hoạch (chỉ "see vault"); thêm cột "giao cho X" làm hiểu nhầm đã assign; tự duyệt/tự gửi khách |
| Ch5·02 | Bắt buộc có charter/WBS mới làm (dự án giữa chừng lấy từ nguồn thật); lấy mốc từ Jira chưa cập nhật; liệt kê toàn bộ task cho người mới |
| Ch5·03 | Bịa URL/DB hoặc chép mật khẩu (ghi ⏳ TBD); gộp nhiều người vào một file; nhầm checklist với brief |
| Ch5·04 | Coi proxy gate là gate chính thức; ghi đè hồ sơ PM tự viết (mặc định skip-existing); đoán status code |
| Ch6·01 | Hard-code/ghi đè ngầm ngưỡng; bịa số khi thiếu nguồn; coi signal là quyết định go/no-go; Bug rate thấp hơn LCL bị hiểu là tốt |
| Ch6·02 | Bỏ bằng chứng cho mục Critical; tự chấm/ký thay reviewer; ghi đè kết quả lần chạy cũ |
| Ch6·03 | Chỉ cộng tổng không tìm nguyên nhân; đổ lỗi cá nhân thay vì vai trò/tải; lẫn md và mh; tự sửa ước lượng gốc thay vì CR |
| Ch6·04 | Đưa CR chưa duyệt vào baseline; tự sửa charter (baseline là lớp cộng dồn); đếm hai lần feature thêm ở nhiều CR |
| Ch6·05 | Báo cáo khi mới lấy trang đầu (> 50 phải lấy hết); để Rejected lẫn phân tích; đổi issue type trước rồi mới comment |
| Ch7·01 | Gộp Risk và Issue một bảng; có đỏ mà không có Recommended Action; chia cho 0 khi velocity = 0 (ghi `[NO_DATA]`) |
| Ch7·02 | Gán xung đột của người khác cho người được coaching; lưu cả transcript; đoán focus speaker |
| Ch7·03 | Bịa/ước lượng số khi nguồn thiếu; gửi khách khi chưa qua PM; tự trộn hai nguồn mâu thuẫn |
| Ch7·04 | Action mơ hồ, owner "Team", deadline "ASAP"; quên carry-forward; ép gán gợi ý AI không khớp |
| Ch8·01 | Chặn plan vì chưa có UAT (G5 chỉ snapshot/`[NO_DATA]`); ngầm giả định template; tự chế mã template |
| Ch8·02 | Tự chạy checklist/đo tín hiệu lúc review; tự ký/điền sẵn phê duyệt; HOLD không có ngày review lại |
| Ch8·03 | Bắt đầu deploy khi G6 chưa GO; mặc định bước thành công (phải hỏi từng bước); ngưng theo dõi rollback sau smoke test |
| Ch8·04 | Mở hypercare khi exec chưa thành công; không có baseline; ghi đè nhật ký; tiếp tục thường kỳ khi có P1 |
| Ch9·01 | Retro thành đổ lỗi; action không owner/hạn; không có catalog; tự điền số khi thiếu |
| Ch9·02 | Đóng khi còn Critical/High mở hoặc chưa có chấp nhận của khách; bịa plan/actual; ghi bí mật trong danh sách truy cập; tự ký thay các bên |

## 9. Điểm nguồn chưa rõ / mâu thuẫn (cần xác nhận)

| # | Điểm | Bài |
|---|---|---|
| 1 | Ví dụ bid: bảng nguồn margin 20% = 16,638 và quote = 83,188 USD; công thức cho 66,550 × 20% = 13,310, quote 79,860 (83,188 ứng margin 25%). Dùng công thức | Ch1·01 |
| 2 | Ví dụ WSJF: cột Rank ghi BID-042 = 1 trong khi BID-045 (2,38) cao nhất; ICE ghi 7,7 và 5,7 (trung bình cộng) trong khi công thức cho 168 và 45 | Ch1·01 |
| 3 | Tần suất chạy dự báo năng lực: hàng tháng / hàng quý / theo yêu cầu (Ch0: hằng quý hoặc trước khi cam kết bid) | Ch1·02 |
| 4 | Ví dụ gap: dòng tháng 1 Frontend −10 gắn đỏ trong khi −10 thuộc Healthy (ngưỡng theo md/quý); bid 048 xác suất 30% < ngưỡng 40% vẫn có trong ví dụ | Ch1·02 |
| 5 | Ý nghĩa nghiệp vụ của ngưỡng một người đóng góp 0.70 trong công cụ registry | Ch1·03 |
| 6 | RACI có hai chữ A (UAT sign-off: QA Lead và Customer PIC; Gate review và Release decision: Sponsor và Customer PIC) mâu thuẫn quy tắc 1 A; ma trận L × I → Level không nêu ở Ch2·01 | Ch2·01 |
| 7 | Hành động cụ thể khi chỉ số vượt LCL/UCL; ngày đi làm thực tế đúng bằng 20 không thuộc TH nào; EE_numerator có/không "× hệ số rank"; PROC-SW-09 dùng cho cả Fix bug và Quản lý CR | Ch2·02 |
| 8 | Milestone M5a chưa định nghĩa đủ (skeleton chỉ M1, M2, M4); E3 ghi "Phase 3-6" vs "phase Dev/Test"; QS-DEV-cov là ký hiệu đặc biệt; WP-TST-01..04 vs WP-TST-02-NN | Ch3·01 |
| 9 | BD/DEV cỡ L = 1.5 md trong khi Iron Law ≤ 1 md (không nêu tiêu chí S/M/L); PM-GATE ghi "G1-G5" trong khi WBS tham chiếu "G2-G6" | Ch3·02 |
| 10 | Tỉ lệ buffer còn DRAFT chờ QA; công thức cộng buffer lên đường găng (65 + 10 = 75 với 15%, suy luận làm tròn 9.75); công thức "Min FTE (avg)" | Ch3·03 |
| 11 | velocity_ratio không dùng trong ngưỡng nào; utilization đúng 100% xếp WARN (vì ≥ 90%); cách chia tỉ lệ effort task đa stage | Ch3·04 |
| 12 | Trọng số single (0.5/0.3/0.2) khác batch (0.35/0.45/0.20); "cap trước khi trừ" của timeestimate; ví dụ ghi 0.92 nhưng phép tính đúng 0.93; role_fit ≥ 0.2 thực tế không loại ai; PQA2+ L3-L4 không tiêu chí | Ch3·05 |
| 13 | Giờ báo cáo mẫu 09:30 vs prep ~8:30; không có quy tắc đặt dòng Status trong mẫu | Ch4·01 |
| 14 | GHOST/DATA trong ví dụ gắn cho phân bổ 5% và 1% trong khi R01 cần ≥ 10%; ví dụ dùng "8/10 commit" cho bus factor; bảng non-delivery ngắn hơn bảng chuẩn; luật `{stale}` bảng 2-3 vs 1+4 (v1.17.2); công cụ PR khác Ch4·01 | Ch4·02 |
| 15 | Ma trận severity CR không nói cách tổng hợp khi các cột lệch (ví dụ CR-003: +7 ngày, +20md, $8,000 → kết luận Medium); heuristic quyết định không phủ mọi tổ hợp; đơn vị "$"; 5 câu hỏi mở của nguồn | Ch4·03 |
| 16 | Bảng calibrate Impact theo hợp đồng còn DRAFT chưa qua QA; "exposure > 2× baseline" không định nghĩa; Severity issue chỉ 3 mức (không Critical); dải score 12-18 và 8-12 chồng biên; L/M/H (%) vs thang 1-5 không quy đổi; ví dụ 1/8 DONE ghi 12% (đúng 12.5%) | Ch4·04 |
| 17 | Mục 7 của ma trận 13 mục bàn giao không có nội dung (mẫu output đánh số 1-6 rồi 8-13) | Ch5·01 |
| 18 | Chưa có cơ chế hết hạn/phiên bản cho onboarding brief | Ch5·02 |
| 19 | Schema onboarding todo liệt kê 12 trường không có `done_date` nhưng dữ liệu mẫu có | Ch5·03 |
| 20 | E3 "Weekly: E3 ≤ 10%" trong mẫu lịch tiếp quản không được định nghĩa trong các file seed | Ch5·04 |
| 21 | Khoảng lệch 0-5% không gán màu; "lệch %" hiểu là tương đối (QS-DEV-cov 76% vs 80% ghi −5% vẫn đỏ); QS-PRC-07 ≥ 90% (bảng đối chiếu/ví dụ) vs ≥ 95% (Fixed-bid ma trận); dự án Labor 3 trường hợp không chi tiết; QS-REQ-03 không có hàng trong ma trận | Ch6·01 |
| 22 | "Standard fail > 20%" tính trên số mục Standard hay tổng; trạng thái trung gian (Standard fail ≤ 20% nhưng > 0) không nêu; ví dụ 3/26 ≈ 11.5% vẫn ghi REVIEW | Ch6·02 |
| 23 | Hai công thức EAC/ETC (EVM chuẩn vs hệ số chênh lệch) chưa chọn; E3 ở đây khác nghĩa với Ch7·01; ví dụ Summary EAC 162 md, +12%, VAC −17 vs Forecast EAC 160, −15 (~10%) | Ch6·03 |
| 24 | Không có ngưỡng cảnh báo scope growth (10%/20% ở báo cáo tuần là khái niệm khác); tổng delta 3 dòng mẫu +3 md vs Summary +9 md, Modified = 2 | Ch6·04 |
| 25 | E3 có hai định nghĩa (actual% − planned% với ngưỡng −5%/−10%; effort variance 10%/15%); biên SPI = 1.0 (> 1.0 xanh vs ≥ 1.0 xanh); overdue vàng 1-2 vs 1-3 ngày; "lệch" tín hiệu theo điểm % hay tỷ lệ; forecast hai cách; ma trận đèn bản hai thêm điều kiện signal | Ch7·01 |
| 26 | Tần suất ngắt lời "cao" là bao nhiêu | Ch7·02 |
| 27 | Ma trận quyết định gate không phủ mọi tổ hợp (ví dụ đạt hết + ≥ 3 High; vàng + > 2 High; checklist fail không Critical); "lệch 5-10%" tuyệt đối hay tương đối; ví dụ thêm "8%" coverage không suy được từ 72% và 80% | Ch8·02 |
| 28 | G6: "all checklists pass" (Ch8·01) vs chỉ QS-PRC-07 ≥ 90% + Pre-deploy + Rollback ready (Ch8·02); câu hỏi mở: ID release `R-<PROJ>-NN` hay semver, quy tắc gộp union/intersect, RTO 30 phút thực tế | Ch8·01 |
| 29 | Giới hạn thời gian cho "bắt đầu sớm" so với window (chỉ cần PM xác nhận) | Ch8·03 |
| 30 | Hypercare: mô tả gốc "7-30 ngày" vs bảng 7 ngày / 3 / 1 / 24h; "bug do khách báo ≤ 2 P1/ngày" vs tiêu chí thoát "0 P1" và P1 dừng thường kỳ; uptime ≥ 99.5% vừa tuyệt đối vừa "vs baseline"; ngưỡng baseline "≥ 1 ngày" quá cũ | Ch8·04 |
| 31 | "4Ls + Anchor" không mô tả riêng "Anchor"; ví dụ +7 ngày nhưng 2026-09-30 → 2026-10-10 là 10 ngày; +10.3% nhưng 162/145 ≈ +11.7% | Ch9·01 |
| 32 | Ý nghĩa từng mã QS-XX không được định nghĩa trong chương 8-9 (xem Ch6·01); "9 sections + sign-off" nhưng đánh số 1-10 | Ch9·02 |
| 33 | G1 người duyệt: Sponsor + PM (Ch8·02) vs Sponsor + PM + Customer PIC nếu ngoài (Ch0) — chênh lệch giữa hai bài, không được bài tự đánh dấu | Ch0, Ch8·02 |
