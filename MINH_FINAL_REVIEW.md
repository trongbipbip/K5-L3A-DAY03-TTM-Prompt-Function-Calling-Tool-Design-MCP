# Review cập nhật cuối của Minh — Tân, 10/11/2026

Commit được kiểm tra: `dfa7eaa`, nhánh `feature/eval-ui-report-03657`.
Đã có trên `origin/main` qua PR #9, merge commit `3c7ba2b` tại thời điểm fetch.
Review trong worktree riêng; không merge hoặc sửa main trong lần kiểm tra này.

## Kết quả xác nhận

- Toàn bộ test chạy lại: **131 passed, 0 failed, 0 skipped**, 1 warning plugin
  `anyio`; gồm 60 contract, 7 example, 59 tool và 5 UI cases.
- `version_log.csv` đã có 4 dòng `v0`, `v1`, `v2`, `v3`.
- Group run mới: `starter_v0/runs/v3_B_group_openai_20261110T125011759103.json`.
  Có 10 case: 7 PASS, 2 FAIL, 1 provider error; accuracy của runner là
  7/9 = 0.7778. Nếu tính cả error trong mẫu số thì là 7/10 = 0.70.
- Prompt/tools hashes trong group run và live transcript khớp artifact hiện tại.
- Có transcript thật 6 lượt:
  `starter_v0/transcripts/v3_openai_20261110T125044866247.transcript.json`.
  Có hỏi lại paper ID, đọc paper, hỏi xác nhận gửi và không gửi khi bị từ chối.
- Không có tool call `send` trong phiên live này.
- G01: model giữ nguyên `items`; tool báo `missing_url` và `missing_source`
  cho item thiếu metadata. Lỗi schema trước PR #7 đã được giải quyết ở case này.
- Replay offline `source_check` trên args trong log cho kết quả đúng như log;
  chưa phát hiện lỗi implementation mới của tool.
- Kiểm tra các mẫu credential phổ biến trong run/transcript được đọc không
  phát hiện key; đây không phải bảo đảm quét được mọi dạng secret.

## Findings còn lại

### P1 — G10 và live turn 6: model tự bổ sung nguồn, che mất missing_source

Input gốc item thứ ba không có `source`. Args model truyền cho `source_check`
lại thêm `source="blog.google"`. Tool vì vậy đánh dấu item này hợp lệ về metadata.
Nếu truyền nguyên input gốc, tool trả `missing_source` đúng như contract.

Đã xác minh ở cả group G10 và transcript live turn 6. Group evaluator vẫn ghi
PASS vì case chỉ chấm tên tool; kết quả đó **không chứng minh args đúng**.
Minh đã mô tả trung thực vấn đề trong REPORT B2/B3/B4.

Phụ trách tiếp: **Trọng** điều chỉnh prompt/routing để giữ nguyên `items`,
không suy diễn source từ URL; **Minh** chạy lại G10/live source-check bằng bản
artifact mới; **Tân** đối chiếu input gốc với args và replay tool để review lại.
Không tự thay đổi code tool nhằm đoán dữ liệu gốc: tool không có thông tin để
biết field nào do model tự thêm trước khi gọi.

### P2 — REPORT B5 còn ghi tổng test 122 thay vì 131

B5 vẫn trỏ `tools/source_check/pytest-output.txt` và mô tả 55 tool cases, trong
khi bản code mới có thêm 4 schema regression cases và 5 UI tests.

**Minh** cập nhật số hiện tại thành 131 (60 contract + 7 example + 59 tool +
5 UI; 42 source_check cases trong 59 tool cases), trỏ evidence mới. Nếu giữ số
122 thì phải ghi rõ là số lịch sử trước bản sửa schema/UI, không phải tổng cuối.
Evidence đã có trên main: `tools/source_check/schema-fix-test-output.txt`.

## Các phần chưa nên chốt là hoàn tất

- Group G02 còn provider error, G03 sai `sort_by`; G07 bị fail vì URL khác ID
  dù tool chấp nhận URL — report đã phân tích, không được đổi metric thành PASS.
- Live turn 3 dùng `lookup` cho yêu cầu arXiv và lỗi thiếu `TAVILY_API_KEY`;
  Trọng phụ trách routing `papers`, Minh chạy xác minh lại khi có bản sửa.
- Base suite hiện đo artifact tools cũ; report đã ghi rõ chưa đo lại base trên
  artifact tools cuối. Trọng quyết định lượt kiểm tra bản cuối và ghi đúng hash.
- Link UI demo và tên nhóm trong report còn placeholder; Minh hoàn thiện trước
  khi nộp. Các lỗi/giới hạn chưa sửa cần được giữ trong failure analysis.

## Bàn giao tiếp theo

1. Trọng xử lý model tự điền nguồn và routing arXiv; giữ nguyên evidence v0–v3.
2. Minh nhận artifact mới, chạy lại case/live liên quan và cập nhật REPORT B5.
3. Tân kiểm tra args thật, output tool và B5 sau lần bàn giao đó.

Đây là kết quả đọc log và chạy test offline. Không gọi lại model/API thật,
không tạo live transcript giả và chưa commit/push file review này.
