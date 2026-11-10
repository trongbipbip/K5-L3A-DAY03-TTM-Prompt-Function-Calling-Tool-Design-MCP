# Cấu hình môi trường và model

Chạy tại `starter_v0/` với môi trường Python đã kích hoạt và cài
`requirements.txt`. Mỗi máy tự tạo `.env` từ `.env.example`; không ghi đè file
đã có key và không commit key thật.

## Provider dùng trong evidence cuối

```dotenv
OPENAI_API_KEY=your_groq_key
OPENAI_BASE_URL=https://api.groq.com/openai/v1
```

CLI dùng `--provider openai --model openai/gpt-oss-120b`. `openai` là adapter
OpenAI-compatible; endpoint và key thuộc Groq. Trong UI chọn cùng provider/model
và label `v4`. Version label chỉ ghi nhãn, không tự chọn model hoặc đổi prompt.

```powershell
python scripts/preflight_provider.py --provider openai --model openai/gpt-oss-120b
python chat.py --provider openai --model openai/gpt-oss-120b --version v4
```

Không thêm biến `OPENAI_MODEL` rồi kỳ vọng CLI tự đọc: chọn model bằng
`--model` hoặc ô Model của UI. UI mặc định có thể chọn provider khác; cần chọn
đúng trước khi gửi câu hỏi.

## Key của từng tool

| Tool | Biến môi trường | Khi thiếu |
|---|---|---|
| `lookup` | `TAVILY_API_KEY` | Trả error dict, không có kết quả web |
| `fetch` | `FIRECRAWL_API_KEY` | Trả error dict, không đọc được URL |
| `timeline`, `social_search` | `RAPIDAPI_KEY`; host mặc định trong mẫu | Trả error dict, không có dữ liệu Twitter/X |
| `papers`, `paper_text` | Không cần key; có thể đặt `ARXIV_USER_AGENT` | Vẫn cần mạng để gọi arXiv; có rate-limit |
| `send` | `TELEGRAM_BOT_TOKEN`, `TELEGRAM_CHAT_ID` | Không gửi được; chỉ gọi khi đã có xác nhận |
| `clarify`, `format`, `policy`, `source_check` | Không cần key | Chạy local |

Evidence live ưu tiên arXiv và tool local do máy chạy chưa cấu hình key
web/Twitter. Telegram chưa gửi thật; evidence xác nhận hành vi hỏi lại và không
gửi khi người dùng từ chối.

## Chọn provider khác

| CLI provider | Key / cấu hình |
|---|---|
| `openrouter` | `OPENROUTER_API_KEY`, model theo `--model` |
| `openai` với endpoint mặc định | `OPENAI_API_KEY`; bỏ `OPENAI_BASE_URL` Groq trước khi dùng key OpenAI |
| `gemini` | `GEMINI_API_KEY` |
| `anthropic` | `ANTHROPIC_API_KEY` |
| `ollama` | Server local; có thể đặt `OLLAMA_BASE_URL`, `OLLAMA_MODEL` |

Các phép so sánh trong report dùng cùng provider/model; không gộp metric
Gemini cũ vào kết quả Groq. Test offline không cần provider:

```powershell
python -m pytest -v
```
