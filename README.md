## Live job data from company career pages, for sales, recruiting and AI agents

See which companies are hiring, for which team, and what changed since last week. Each tool below reads public job boards or homepages at the moment you run it, and you pay per result.

All tools run on [Apify](https://apify.com/conserving_celerytop). No login to any job board, no personal data, no monthly fee. Every block below is copy-paste ready once you set `APIFY_TOKEN` (Apify Console, Settings, API & Integrations).

- [What's new](#whats-new)
- [Sales and hiring signals](#sales-and-hiring-signals)
- [Recruiting and job search](#recruiting-and-job-search)
- [Company data](#company-data)
- [Use them from AI agents](#use-them-from-ai-agents)
- [Code examples](#code-examples)
- [Prices](#prices)
- [What data these tools touch](#what-data-these-tools-touch)

---

## What's new

- **Sep 26, 2026.** One Actor per job board: Greenhouse, Lever, Ashby and Workday Jobs API. Also new: Website Tech Stack Detector.
- **Sep 25, 2026.** Tech Jobs Search: one search across 574 tech, AI and remote-first companies. Live Jobs HTTP API: jobs in one GET request.
- **Coming soon.** Four free, MIT-licensed agent skills for account research, hiring signals, competitor hiring and job search. Company Hiring Signals: one row per company with a 0 to 100 hiring score, for Clay or a sheet ($0.06 per company).

---

## Sales and hiring signals

**[ATS Jobs API](https://apify.com/conserving_celerytop/live-career-page-jobs-api)**
Know which of your accounts are hiring, and for which team, before you reach out. Paste company names, websites or job board links. Get every open job, or one summary row per company with jobs posted in the last 7 and 30 days. Reads Greenhouse, Lever, Ashby, Workday and 18 more job boards. Put it on a schedule to get only new jobs in Slack.
Price: see the Store page.

```bash
curl -X POST "https://api.apify.com/v2/acts/conserving_celerytop~live-career-page-jobs-api/run-sync-get-dataset-items?maxTotalChargeUsd=0.30" \
  -H "Authorization: Bearer $APIFY_TOKEN" -H "Content-Type: application/json" \
  -d '{"companies": ["https://boards.greenhouse.io/stripe", "https://jobs.lever.co/palantir"], "postedSince": "7 days"}'
```

**[Live Jobs HTTP API](https://apify.com/conserving_celerytop/live-jobs-http-api)**
Get a company's open jobs in one request, with the jobs in the response. Made for scripts, Clay and no-code tools. Same data as ATS Jobs API.
Price: see the Store page.

```bash
curl -H "Authorization: Bearer $APIFY_TOKEN" \
  "https://conserving-celerytop--live-jobs-http-api.apify.actor/?companies=stripe,linear.app&postedSince=7%20days"
```

---

## Recruiting and job search

**[Tech Jobs Search](https://apify.com/conserving_celerytop/tech-jobs-search)**
Find fresh jobs at 574 tech, AI, remote-first and European companies in one search. Filter by title, place, remote, seniority, salary and date. Every result was open when you ran it. Companies with no match cost nothing.
Price: $1 per 1,000 matching jobs; $1.15 from October 11, 2026.

```bash
curl -X POST "https://api.apify.com/v2/acts/conserving_celerytop~tech-jobs-search/run-sync-get-dataset-items?maxTotalChargeUsd=0.12" \
  -H "Authorization: Bearer $APIFY_TOKEN" -H "Content-Type: application/json" \
  -d '{"titleIncludes": ["product designer"], "location": "Berlin", "postedSince": "30 days", "maxResults": 100}'
```

**Track one job board.** If all your companies use the same job board, these Actors read it directly. Each returns title, team, location and the apply link, plus pay where the board shows it. Each can send new-job alerts on a schedule.

| Actor | Paste | Price |
|---|---|---|
| [Greenhouse Jobs API](https://apify.com/conserving_celerytop/greenhouse-jobs-api) | Greenhouse board links, names or websites | $0.045 per company, up to 1,000 jobs; $0.10 from October 11, 2026 |
| [Lever Jobs API](https://apify.com/conserving_celerytop/lever-jobs-api) | Lever board links | $0.045 per company, up to 1,000 jobs; $0.10 from October 11, 2026 |
| [Ashby Jobs API](https://apify.com/conserving_celerytop/ashby-jobs-api) | Ashby board links | $0.045 per company, up to 1,000 jobs; $0.10 from October 11, 2026 |
| [Workday Jobs API](https://apify.com/conserving_celerytop/workday-jobs-api) | Workday career site links | $0.05 per company, up to 1,000 jobs; $0.10 from October 11, 2026 |

```bash
curl -X POST "https://api.apify.com/v2/acts/conserving_celerytop~greenhouse-jobs-api/run-sync-get-dataset-items?maxTotalChargeUsd=0.30" \
  -H "Authorization: Bearer $APIFY_TOKEN" -H "Content-Type: application/json" \
  -d '{"companies": ["https://boards.greenhouse.io/dropbox", "https://job-boards.greenhouse.io/duolingo"]}'
```

Swap `greenhouse-jobs-api` for `lever-jobs-api`, `ashby-jobs-api` or `workday-jobs-api`, with links from that board.

---

## Company data

**[Website Tech Stack Detector](https://apify.com/conserving_celerytop/website-tech-stack-detector)**
See what a list of websites runs before you pitch them: CMS, ecommerce platform, analytics, frameworks, CDN, hosting and payments. One homepage request per site. A result means the tool's tag was on the homepage. Tools behind a login, like most CRMs, often do not show.
Price: $2 per 1,000 websites.

```bash
curl -X POST "https://api.apify.com/v2/acts/conserving_celerytop~website-tech-stack-detector/run-sync-get-dataset-items?maxTotalChargeUsd=0.10" \
  -H "Authorization: Bearer $APIFY_TOKEN" -H "Content-Type: application/json" \
  -d '{"websites": ["pypi.org", "crates.io"]}'
```

---

## Use them from AI agents

Any agent that speaks MCP (Claude, Cursor, VS Code, Codex and others) can call these Actors as tools through Apify's hosted MCP server. Add this URL as an MCP server:

```
https://mcp.apify.com/?tools=actors,docs,conserving_celerytop/live-career-page-jobs-api,conserving_celerytop/tech-jobs-search,conserving_celerytop/website-tech-stack-detector
```

Sign in with OAuth, or send your Apify token in an `Authorization: Bearer` header. Never put a token in the URL. Setup guide: [docs.apify.com/platform/integrations/mcp](https://docs.apify.com/platform/integrations/mcp).

Agent skills built on these Actors are coming soon.

---

## Code examples

Python, curl and MCP setup for Claude, Cursor, VS Code and ChatGPT. MIT licensed.

- [ats-jobs-api-python](https://github.com/donmangudata-ops/ats-jobs-api-python): every open job at the companies you list, from Python.
- [tech-jobs-search-api](https://github.com/donmangudata-ops/tech-jobs-search-api): search AI, startup and remote tech jobs from Python.
- [live-jobs-http-api-examples](https://github.com/donmangudata-ops/live-jobs-http-api-examples): company jobs in one GET request.

---

## Prices

You pay per event from your own Apify account. There is no subscription. Apify's free plan includes a monthly credit that covers small tests. Prices are lower on the Scale and Business plans.

- **Per company** (job Actors): once per company whose board was read, up to 1,000 jobs. Also charged when a board is empty or not found, because the request was still made.
- **Per matching job** (Tech Jobs Search): only jobs that matched your search.
- **Per website** (Tech Stack Detector): only homepages that loaded.
- **Later checks** of the same company for new jobs cost much less than the first one.

Every Store page shows the current prices. `maxTotalChargeUsd` in the blocks above caps what a run can cost.

---

## What data these tools touch

- **Public data only.** Job boards and career pages that companies publish for anyone, and the public homepage of a website.
- **No personal data.** The Actors return jobs and technologies. They do not collect data about people, such as recruiters or hiring managers.
- **robots.txt respected.** A site that disallows the path is skipped, with a note in the output.
- **No login.** Nothing runs behind a sign-in, a paywall or a CAPTCHA.
- **Light load.** One request per board or homepage where the source allows it.

You are responsible for how you use the data, including the terms of the sites involved and the laws where you work. If you run a board or site and want it handled differently, open an issue on the Actor's Apify page.

---

Questions, bugs or a job board I do not cover yet: open an issue on the Actor's Apify page.

If one of these saved you time, star the code example you used, or follow this account for the next tool.
