# TTM · Research Agent

Research agent tiếng Việt cho Day 03: chọn tool, thực thi, lưu bằng chứng và
đánh giá prompt qua nhiều phiên bản. Có giao diện Streamlit, 11 tool và bộ
kiểm thử offline.

**[Báo cáo đầy đủ](starter_v0/artifacts/REPORT.md)** ·
**[Mục lục bằng chứng](docs/EVIDENCE_INDEX.md)** ·
**[Thành viên](TEAM.md)** · **[Checklist cuối](TEAM_HANDOFF_CHECKLIST.md)**

## Kết quả bản nộp

| Hạng mục | Kết quả | Bằng chứng |
|---|---|---|
| Contract, unit và UI tests | **131 passed · 0 failed · 0 skipped** | [Output cuối](starter_v0/artifacts/verification/pytest-final.txt) |
| Base eval v4 | **19/20 · 95%** | [Run base](starter_v0/runs/v4_B_base_openai_20261110T145359081439.json) |
| Group eval v4 | **8/10 PASS**, 1 FAIL, 1 provider error | [Run group](starter_v0/runs/v4_B_group_openai_20261110T145702253546.json) |
| Review arguments thủ công | **7/10** nếu tính thêm G10 sai arguments là FAIL | [REPORT B2–B3](starter_v0/artifacts/REPORT.md#b3-team-eval-cases) |
| Eval nhóm | 5 single-turn + 5 multi-turn | [10 case](starter_v0/data/eval_group.json) |
| Live chat | 3 phiên; phiên v3 có 6 lượt, bổ sung kiểm tra p1/v4 | [Transcripts](starter_v0/transcripts) |

Runner loại provider error khỏi mẫu số nên accuracy group trong JSON là
8/9 = 0.8889. Bảng trên dùng đủ 10 case. Nhóm chấp nhận mức 7/10 sau review;
các lỗi còn lại được giữ nguyên trong báo cáo và log.

## Chạy nhanh

Yêu cầu Python 3.10+. Bản nộp kiểm tra với Python 3.14.3. PowerShell:

```powershell
cd starter_v0
python -m venv .venv
.venv\Scripts\Activate.ps1
python -m pip install -r requirements.txt
Copy-Item .env.example .env
```

Chỉ copy mẫu khi chưa có `.env`. Điền key riêng trên máy theo
[hướng dẫn cấu hình](TOOL-SETUP.md). Evidence cuối của nhóm dùng:

```dotenv
OPENAI_API_KEY=your_groq_key
OPENAI_BASE_URL=https://api.groq.com/openai/v1
```

`openai` là adapter OpenAI-compatible cho endpoint Groq; model cuối là
`openai/gpt-oss-120b`.

```powershell
python -m pytest -v
python scripts/preflight_provider.py --provider openai --model openai/gpt-oss-120b
python -m streamlit run app.py
```

Mở **http://localhost:8501**. Trong sidebar chọn **Provider: openai**,
**Model: openai/gpt-oss-120b**, **Version label: v4**. UI hiện tool calls,
arguments, kết quả và tùy chọn lưu transcript. Chưa triển khai UI public;
repo này là link nộp mã nguồn, báo cáo và evidence.

Test chạy offline, không cần key; preflight/chat cần key thật. Tool web/Twitter
cần key dịch vụ riêng, xem [TOOL-SETUP.md](TOOL-SETUP.md).

## Tool và giới hạn

`clarify` · `timeline` · `social_search` · `lookup` · `fetch` · `format` ·
`send` · `policy` · `papers` · `paper_text` · **`source_check`** (nhóm thêm).

`source_check` kiểm tra metadata trích dẫn, không xác minh sự thật hoặc uy tín
nguồn. Schema cho phép item thiếu URL/source để tool báo lỗi. Model đôi khi
tự thêm `source` trước khi gọi tool; đây là giới hạn còn lại ở G10, được ghi rõ
trong report. Không dùng kết quả này như xác nhận tính đúng của nội dung.

## Chạy lại bản cuối

Chạy trong `starter_v0/`, có key tương ứng trong `.env`:

```powershell
python run_eval.py --provider openai --model openai/gpt-oss-120b --version v4 --suite base --eval-cases data/eval_base.json
python run_eval.py --provider openai --model openai/gpt-oss-120b --version v4 --suite group --eval-cases data/eval_group.json
python chat.py --provider openai --model openai/gpt-oss-120b --version v4
```

Các lệnh tạo run/transcript mới. Output model có thể khác giữa các lần chạy;
kết quả đã nộp nằm trong các file được dẫn ở bảng trên.

## Cấu trúc và bàn giao

```text
starter_v0/
  app.py                 Streamlit UI
  agent.py, chat.py      Agent và vòng gọi tool
  providers/             Adapter model
  tools/                 11 tool và contract TOOL.md
  tests/                 Contract, unit và UI regression tests
  data/                  Base, group và extension eval
  artifacts/             Report, prompt, schema, version log, test evidence
  runs/                  Run JSON thật và snapshot baseline
  transcripts/           Live evidence
docs/                    Mục lục evidence và tài liệu tham chiếu
```

Cả ba thành viên nộp cùng link repo nhánh `main`. Có thể tải
[ZIP của main](https://github.com/trongbipbip/K5-L3A-DAY03-TTM-Prompt-Function-Calling-Tool-Design-MCP-/archive/refs/heads/main.zip)
nếu nơi nộp yêu cầu file. Không đưa `.env`, key thật, `.venv` hoặc cache vào bài.

Đề bài gốc: [Lab instructions](docs/LAB_INSTRUCTIONS.md).
Phân công: [TASK_ASSIGNMENT.md](TASK_ASSIGNMENT.md).
Lịch sử bàn giao: [docs/archive](docs/archive).
