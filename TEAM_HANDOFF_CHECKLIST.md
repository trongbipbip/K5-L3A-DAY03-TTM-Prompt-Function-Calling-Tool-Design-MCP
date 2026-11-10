# Chốt bài nộp — nhóm TTM

Bản rà soát: 10/11/2026. Code/model giữ ở **v4**; chỉ dọn tài liệu và cấu trúc
cho bản nộp. Lịch sử công việc giữ tại [docs/archive](docs/archive).

## Kết quả kiểm tra

- [x] Có đủ ba thành viên và phân công trong [TEAM.md](TEAM.md).
- [x] Tool `source_check` có implementation, contract, registry và YAML đồng bộ.
- [x] Đã sửa schema để nhận item thiếu URL/source, kèm 4 regression cases.
- [x] Toàn bộ test bản cuối: **131 passed, 0 failed, 0 skipped**.
- [x] Có baseline và các vòng v1–v3, thêm đo bản cuối v4; version log dẫn run JSON.
- [x] Group suite đủ 10 case: **5 single-turn + 5 multi-turn**.
- [x] Group v4: **8/10 tự động**; **7/10** nếu tính thêm G10 sai args là FAIL.
- [x] Có live transcript thật: phiên v3 6 lượt, bổ sung kiểm tra p1 và v4.
- [x] Có UI Streamlit, hướng dẫn chạy local và 5 UI tests offline.
- [x] REPORT A, B1–B6 có nội dung/evidence; bonus model local ghi rõ không làm.
- [x] Đã review B5: test count 131, metadata-only, evidence trước/sau schema fix.
- [x] Các lỗi còn lại được giữ trong report; không đổi nhãn PASS hoặc sửa log.

Test evidence: [pytest-final.txt](starter_v0/artifacts/verification/pytest-final.txt).
Run/transcript index: [EVIDENCE_INDEX.md](docs/EVIDENCE_INDEX.md).

## Hoàn tất phần từng người

| Thành viên | Đầu ra đã bàn giao | Trạng thái |
|---|---|---|
| Trọng | Baseline, prompt/routing, base eval v0–v3, version log | Đã có trên main |
| Tân | Tool mới, unit/schema regression tests, review args live và B5 | Hoàn thành; giới hạn model được công khai |
| Minh | 10 case eval, UI, live chat, report, thí nghiệm v4 | Đã có trên main |

## Giới hạn được chấp nhận khi chốt

- G10: model có thể tự thêm `source` trước khi gọi tool; runner chỉ chấm routing.
  Khi review thủ công, không coi đây là arguments đúng. Tool không thể biết
  field nào do model thêm vì không nhận được input gốc để đối chiếu.
- G02 còn provider error; G07 khác URL/ID nên runner FAIL, có manual analysis.
- Group runner loại provider error khỏi mẫu số: 8/9 trong JSON không phải 8/10.
- UI chạy local; chưa có hosting public. Repo/link ZIP là nơi nộp mã nguồn và
  bằng chứng. Cách chạy nằm ở README; không bịa link demo.
- Không phải mọi máy thành viên đã preflight riêng. Evidence model thực tế
  thuộc các môi trường chạy được ghi trong run/transcript; không xác nhận setup
  cả ba máy nếu chưa có bằng chứng.

Nhóm chấp nhận mức **7/10 sau review** để nộp. Không tiếp tục tối ưu chỉ để cố
đạt 10/10. Các thử nghiệm mới sau khi nộp cần ghi version và evidence riêng.

## Cách nộp chung

Cả ba thành viên dùng [repo main](https://github.com/trongbipbip/K5-L3A-DAY03-TTM-Prompt-Function-Calling-Tool-Design-MCP-/tree/main)
hoặc [ZIP của main](https://github.com/trongbipbip/K5-L3A-DAY03-TTM-Prompt-Function-Calling-Tool-Design-MCP-/archive/refs/heads/main.zip).
Giữ nguyên `starter_v0/` cùng `artifacts/`, `runs/`, `transcripts/` và `tests/`.
Không đưa `.env`, key, `.venv`, cache hoặc PDF tải về vào bài nộp.
