# SEO monitor suite (n8n)

Three interconnected n8n workflows for monitoring a Russian-market e-commerce
site's SEO health: uptime/content auditing, monthly reporting with keyword
cannibalization detection, and brand visibility tracking across AI answer
engines (GEO/AIO).

## Workflows

| Folder | Purpose | Trigger |
|---|---|---|
| [`daily-weekly/`](./daily-weekly) | Uptime + content-drift monitoring | Daily / Monday 09:00 |
| [`monthly-anticannibal/`](./monthly-anticannibal) | Monthly SEO report + keyword cannibalization engine | 1st of month / weekly |
| [`ai-visibility/`](./ai-visibility) | Brand visibility across Yandex GenSearch, GPT, Gemini, Qwen | Manual / monthly 10th |

## Architecture

All three workflows read/write a single Google Sheet used as a shared state
store, keyed per-run so reruns don't repeat paid API calls:

`Daily_Log`, `Weekly_Log`, `Monthly_Log`, `Daily_Monitor`, `Baseline_Metrics`,
`Master_Briefs`, `Owner_Map`, `Cannibalization_State`, `Cannibalization_History`,
`Query_Discovery`, `SEO_Page_Snapshot`, `SEO_Run_State`, `SEO_Change_Log`,
`SERP_Query_State`, `SERP_Query_History`, `AI_Visibility_State`, `AI_Visibility_History`

Data sources: Yandex Webmaster, Yandex Metrika, Google Search Console,
SerpApi (live SERP checks), Yandex GenSearch / OpenRouter (Qwen, GPT,
Gemini). Charts render via quickchart.io. Reports deliver to Telegram,
archive to Google Drive.

TODO: diagram.

## Stack

- n8n (self-hosted / cloud)
- Google Sheets as state store
- Telegram for report delivery
- Yandex Webmaster API, Yandex Metrika, Google Search Console
- SerpApi (SERP tracking), OpenRouter (Qwen/GPT/Gemini), Yandex GenSearch

## Setup

1. Import the workflow JSON from the relevant folder into n8n.
2. Fill in n8n credentials for: Google Sheets, Google Drive, Telegram, OpenAI/OpenRouter.
3. Open each `Config` / `Config — ...` code node and replace the placeholder
   values (`YOUR_GOOGLE_SHEET_ID`, `YOUR_SERPAPI_KEY`, etc. — see `.env.example`).
4. Set up the required Google Sheet tabs (see each workflow's README).

## Related writeups

- TODO: link master Habr article
- TODO: link per-workflow Habr articles

## License

MIT — see [LICENSE](./LICENSE).
