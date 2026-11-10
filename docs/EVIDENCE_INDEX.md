# Mục lục bằng chứng

Bản nộp dùng prompt **v4**, tools sau PR #7, model Groq `openai/gpt-oss-120b`.

## Evidence chính

- [REPORT](../starter_v0/artifacts/REPORT.md)
- [Version log](../starter_v0/artifacts/version_log.csv)
- [Test cuối](../starter_v0/artifacts/verification/pytest-final.txt)
- [Rà soát gói nộp](../starter_v0/artifacts/verification/submission-audit.txt)
- [Base v4 — 19/20](../starter_v0/runs/v4_B_base_openai_20261110T145359081439.json)
- [Group v4 — 8/10 tự động, 7/10 khi tính thêm G10 sai args](../starter_v0/runs/v4_B_group_openai_20261110T145702253546.json)
- [Probe lặp source_check](../starter_v0/runs/v4_source_check_repeat_probe.txt)

Không sửa log cũ. Run lỗi kết nối/provider được giữ và đánh dấu ở bảng dưới; không dùng các run không đo được để kết luận accuracy.

## Toàn bộ run JSON

| Run | Model | PASS / đo được | Provider errors |
|---|---|---|---|
| [pr3_B_base_openai_20261110T115022673494.json](../starter_v0/runs/pr3_B_base_openai_20261110T115022673494.json) | `openai/gpt-oss-120b` | 17/20 | 0 |
| [pr3_B_group_openai_20261110T115325390297.json](../starter_v0/runs/pr3_B_group_openai_20261110T115325390297.json) | `openai/gpt-oss-120b` | 6/8 | 2 |
| [v0_B_base_gemini_20261110T105830047307.json](../starter_v0/runs/v0_B_base_gemini_20261110T105830047307.json) | `gemini-3.5-flash` | 0/0 | 20 |
| [v0_B_base_gemini_20261110T110115259745.json](../starter_v0/runs/v0_B_base_gemini_20261110T110115259745.json) | `gemini-3.5-flash` | 0/0 | 20 |
| [v0_B_base_gemini_20261110T110404621050.json](../starter_v0/runs/v0_B_base_gemini_20261110T110404621050.json) | `gemini-3.5-flash` | 18/19 | 1 |
| [v0_B_base_openai_20261110T114359700556.json](../starter_v0/runs/v0_B_base_openai_20261110T114359700556.json) | `openai/gpt-oss-120b` | 13/20 | 0 |
| [v0_B_group_openai_20261110T115628292321.json](../starter_v0/runs/v0_B_group_openai_20261110T115628292321.json) | `openai/gpt-oss-120b` | 6/9 | 1 |
| [v1_B_base_openai_20261110T121418398315.json](../starter_v0/runs/v1_B_base_openai_20261110T121418398315.json) | `openai/gpt-oss-120b` | 18/20 | 0 |
| [v2_B_base_openai_20261110T121718628052.json](../starter_v0/runs/v2_B_base_openai_20261110T121718628052.json) | `openai/gpt-oss-120b` | 0/0 | 20 |
| [v2_B_base_openai_20261110T122124813813.json](../starter_v0/runs/v2_B_base_openai_20261110T122124813813.json) | `openai/gpt-oss-120b` | 18/20 | 0 |
| [v3-final-p1_B_base_openai_20261110T141810057021.json](../starter_v0/runs/v3-final-p1_B_base_openai_20261110T141810057021.json) | `openai/gpt-oss-120b` | 19/20 | 0 |
| [v3-final-p1_B_group_openai_20261110T142154758429.json](../starter_v0/runs/v3-final-p1_B_group_openai_20261110T142154758429.json) | `openai/gpt-oss-120b` | 8/9 | 1 |
| [v3-final_B_base_openai_20261110T141124707959.json](../starter_v0/runs/v3-final_B_base_openai_20261110T141124707959.json) | `openai/gpt-oss-120b` | 19/20 | 0 |
| [v3_B_base_openai_20261110T122544614376.json](../starter_v0/runs/v3_B_base_openai_20261110T122544614376.json) | `openai/gpt-oss-120b` | 17/19 | 1 |
| [v3_B_group_openai_20261110T122840577449.json](../starter_v0/runs/v3_B_group_openai_20261110T122840577449.json) | `openai/gpt-oss-120b` | 6/8 | 2 |
| [v3_B_group_openai_20261110T125011759103.json](../starter_v0/runs/v3_B_group_openai_20261110T125011759103.json) | `openai/gpt-oss-120b` | 7/9 | 1 |
| [v4_B_base_openai_20261110T145359081439.json](../starter_v0/runs/v4_B_base_openai_20261110T145359081439.json) | `openai/gpt-oss-120b` | 19/20 | 0 |
| [v4_B_group_openai_20261110T145702253546.json](../starter_v0/runs/v4_B_group_openai_20261110T145702253546.json) | `openai/gpt-oss-120b` | 8/9 | 1 |

## Live transcripts

| Phiên | Số lượt | Artifact |
|---|---|---|
| [v3-final-p1_openai_20261110T143232383389.transcript.json](../starter_v0/transcripts/v3-final-p1_openai_20261110T143232383389.transcript.json) | 2 | `v3-final-p1+pb768ae4b5c47+tfe7f33e09197` |
| [v3_openai_20261110T125044866247.transcript.json](../starter_v0/transcripts/v3_openai_20261110T125044866247.transcript.json) | 6 | `v3+p39c95958ae7e+tfe7f33e09197` |
| [v4_openai_20261110T145738372871.transcript.json](../starter_v0/transcripts/v4_openai_20261110T145738372871.transcript.json) | 1 | `v4+p15d09dc21db5+tfe7f33e09197` |

Phiên v3 có 6 lượt, gồm hỏi lại, đọc paper, yêu cầu gửi và từ chối gửi. Các phiên p1/v4 kiểm tra lại routing và giới hạn tự thêm nguồn; không coi các phiên khác hash là cùng artifact.

## Tool và lịch sử

- [Contract source_check](../starter_v0/tools/source_check/TOOL.md)
- [Schema regression trước sửa](../starter_v0/tools/source_check/schema-regression-before.txt)
- [Test sau sửa schema](../starter_v0/tools/source_check/schema-fix-test-output.txt)
- [Đề bài gốc](LAB_INSTRUCTIONS.md)
- [Lịch sử bàn giao](archive/TEAM_HANDOFF_HISTORY.md)
