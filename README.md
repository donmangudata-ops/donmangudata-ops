## Hi, I'm Don Mangu

I build small data tools on [Apify](https://apify.com/conserving_celerytop) that read public web data live, at the moment you run them. Most of them read open jobs from company career pages. One reads the technologies behind a website.

You pay per result, not per month. None of them need a login, an API key for the target site, or personal data.

- [Sales and hiring signals](#sales-and-hiring-signals)
- [Recruiting and job search](#recruiting-and-job-search)
- [Company and public data](#company-and-public-data)
- [Use them from AI agents](#use-them-from-ai-agents)
- [How pricing works](#how-pricing-works)
- [What data these tools touch](#what-data-these-tools-touch)

---

## Sales and hiring signals

Which of your accounts are hiring, for which team, and what changed since last week.

**[ATS Jobs API: Greenhouse & Lever Jobs, Ashby & Career Pages](https://apify.com/conserving_celerytop/live-career-page-jobs-api)**
Every open job at the companies you list, read live from their own job boards: Greenhouse, Lever, Ashby, Workday, Eightfold, Workable, Personio, Teamtailor, Recruitee, JOIN, Gem, Freshteam and 10 more (22 in all). Paste company names, websites or board links. It can return one summary row per company (open jobs, jobs posted in the last 7 and 30 days, top departments) or every job. Schedule it with "Only new jobs" to send new-job alerts to Slack.
Price: $0.01 per company, up to 1,000 jobs.

**[Live Jobs HTTP API: Greenhouse, Lever, Ashby, Workday](https://apify.com/conserving_celerytop/live-jobs-http-api)**
The same job data as ATS Jobs API, in one GET or POST request with the jobs in the response. Made for scripts, Clay and no-code tools that want an answer in one call instead of a run and a dataset.
Price: $0.01 per company, the same event prices as ATS Jobs API, plus Apify platform usage.

---

## Recruiting and job search

Find open roles, or track the career pages of the companies you care about.

**[Tech Jobs Search: Startup, AI & Remote Jobs](https://apify.com/conserving_celerytop/tech-jobs-search)**
Search the open jobs of 574 tech, AI, remote-first and European companies by title, place, remote, seniority, salary and date. The jobs are read live from their career pages when you run it. Companies with no match cost nothing.
Price: $1 per 1,000 matching jobs.

**[Greenhouse Jobs API: $0.045/Company, No Login](https://apify.com/conserving_celerytop/greenhouse-jobs-api)**
Every open job on a company's Greenhouse board, including roles that have been open a long time. Paste board links, names or websites. Title, department, location, pay ranges and apply link.
Price: $0.045 per company, up to 1,000 jobs.

**[Lever Jobs API: $0.045/Company, No Login](https://apify.com/conserving_celerytop/lever-jobs-api)**
Every open job on a company's Lever board. Title, team, location, job type, salary and apply link.
Price: $0.045 per company, up to 1,000 jobs.

**[Ashby Jobs API: $0.045/Company, No Login](https://apify.com/conserving_celerytop/ashby-jobs-api)**
Every open job on a company's Ashby board. Title, department, location, salary, job type and apply link.
Price: $0.045 per company, up to 1,000 jobs.

**[Workday Jobs API: $0.05/Company, No Login](https://apify.com/conserving_celerytop/workday-jobs-api)**
Every open job on a company's Workday career site, where the employer's robots.txt allows it. Paste career site links. Title, department, location, job type and apply link.
Price: $0.05 per company, up to 1,000 jobs. Full descriptions are optional, $0.01 per 200 jobs.

The four single-board Actors can be scheduled for new-job alerts. If your list mixes several job boards, ATS Jobs API reads all four of these boards plus 18 more at $0.01 per company.

---

## Company and public data

**[Website Tech Stack Detector: CMS & Analytics, No Login](https://apify.com/conserving_celerytop/website-tech-stack-detector)**
Give it a list of websites and it reports the CMS, ecommerce platform, analytics, frameworks, CDN, hosting and payment tools it finds on each homepage. One homepage request per site, robots.txt respected, 7,600+ open fingerprints. A result means a tool's tag was seen on the homepage. Tools that live behind a login, such as most CRMs, often do not show.
Price: $2 per 1,000 websites.

---

## Use them from AI agents

**Apify MCP server.** Any agent that speaks MCP (Claude, Cursor, VS Code, Codex and others) can call these Actors as tools through Apify's hosted MCP server. Add the Actors you want to the URL, for example:

```
https://mcp.apify.com/?tools=actors,docs,conserving_celerytop/live-career-page-jobs-api,conserving_celerytop/website-tech-stack-detector
```

Sign in with OAuth, or send your Apify token in an `Authorization: Bearer` header. Do not put a token in the URL. Setup guide: [docs.apify.com/platform/integrations/mcp](https://docs.apify.com/platform/integrations/mcp).

**Agent skills.** A free, MIT-licensed set of agent skills built on these Actors is coming soon.

---

## How pricing works

All of these Actors use Apify's pay per event model. You pay for what the run delivers, from your own Apify account, and there is no subscription to these tools. Apify's free plan includes a monthly usage credit, which covers small tests.

The main events:

- **Company lookup** (job Actors): charged once per company whose board was contacted. It includes up to 1,000 jobs. It is also charged when a board is empty, not found or fails, because the request was still made.
- **Extra 1,000 jobs**: only when one company has more than 1,000 open jobs.
- **Repeat monitor check**: $0.002 per later check of one company, per 1,000 open jobs on its board or part of them.
- **Description block**: $0.01 per 200 job descriptions, only on boards that need an extra request for them (Workday, Eightfold, JazzHR, Paylocity, Freshteam, JOIN). Other boards include descriptions at no extra cost.
- **Matching job** (Tech Jobs Search): $0.001 per job that matched your search.
- **Website analyzed** (Tech Stack Detector): $0.002 per homepage that loaded and was checked.
- **Actor start**: $0.00005 per GB of memory, once per run.

Examples at free-plan prices:

- Summaries for 200 target accounts with ATS Jobs API: 200 x $0.01 = **$2.00**.
- A weekly new-jobs check on the same 200 accounts, each with under 1,000 open jobs: 200 x $0.002 = **$0.40** a week.
- A Tech Jobs Search that returns 350 matching jobs: **$0.35**.
- 50 companies on the Greenhouse Jobs API: 50 x $0.045 = **$2.25**.
- 20 Workday companies with descriptions for 600 jobs: $1.00 + 3 x $0.01 = **$1.03**.
- The tech stack of 5,000 websites: **$10.00**.

Prices are lower on paid Apify plans (5% to 20% less on the main event). Each Store page shows the current prices, and the public API returns them without a token, for example `https://api.apify.com/v2/acts/conserving_celerytop~live-career-page-jobs-api`. The prices here were checked on September 26, 2026.

---

## What data these tools touch

- **Public data only.** Job boards and career pages that companies publish for anyone to read, and the public homepage of a website.
- **No personal data.** The Actors return jobs and technologies. They do not look up or collect data about people, such as recruiters or hiring managers. Job descriptions come through as the employer wrote them.
- **robots.txt respected.** Each source is read only where the site's robots.txt allows it. Where an employer can change its own robots.txt, as on Workday, it is read on every run and a site that disallows the path is skipped with a note in the output.
- **No login.** Nothing runs behind a sign-in, a paywall or a CAPTCHA.
- **Light load.** One request per board or homepage where the source allows it, instead of crawling whole sites.

You are responsible for how you use the data you collect, including the terms of the sites involved and the laws where you work. If you run a board or site and want it handled differently, open an issue on the Actor's page on Apify.

---

## Contact

Questions, bugs or a board I do not cover yet: open an issue on the Actor's Apify page.

All Actors: [apify.com/conserving_celerytop](https://apify.com/conserving_celerytop)
