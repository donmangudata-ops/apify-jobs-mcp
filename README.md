# Career page jobs and website tech stacks for AI agents (Apify MCP)

Connect Claude, Cursor, ChatGPT or any MCP client to live job data from company career pages, and to a website tech stack detector. Nothing to install. Both run on Apify's hosted MCP server at `mcp.apify.com`, pinned to my Apify Actors.

I built and maintain these Actors. They are paid per event, and every call is billed to your own Apify account at the prices below. There are no affiliate or referral parameters in any link here.

## Endpoints

| Server | URL | Registry name |
|---|---|---|
| Career page jobs | `https://mcp.apify.com/?tools=fetch-actor-details,conserving_celerytop/live-career-page-jobs-api,conserving_celerytop/tech-jobs-search` | `io.github.donmangudata-ops/career-page-jobs` |
| Website tech stack | `https://mcp.apify.com/?tools=fetch-actor-details,conserving_celerytop/website-tech-stack-detector` | `io.github.donmangudata-ops/website-tech-stack` |

Transport is Streamable HTTP. Sign-in is Apify OAuth, and the client opens a browser window the first time you connect. Clients without OAuth can send your Apify API token instead, as the header `Authorization: Bearer <token>` (Apify Console, Settings, API & Integrations). Never put the token in the URL.

## What the tools do

**ATS Jobs API** (`conserving_celerytop/live-career-page-jobs-api`)
Give it company names, websites or job board links. It returns every open job on each company's career page, read live when you ask, from Greenhouse, Lever, Ashby, Workday, Eightfold, Workable, Personio, Teamtailor and 14 more job boards. Title, department, location, pay range when listed, posted date and apply link. No login on the job boards, no personal data.

**Tech Jobs Search** (`conserving_celerytop/tech-jobs-search`)
Search the open jobs of 824 startups and tech, AI, remote-first and European companies by title, place, remote, seniority, salary and date. One row per matching job.

**Website Tech Stack Detector** (`conserving_celerytop/website-tech-stack-detector`)
Give it a list of websites. It loads each homepage once, respects robots.txt, and returns the CMS, ecommerce platform, analytics, frameworks, CDN, hosting and payment tools it finds, from 7,600+ open fingerprints.

`fetch-actor-details` is Apify's own tool. It lets the agent read each Actor's input fields before calling it.

## Prices (checked against the Apify Store on Sep 27, 2026)

| Actor | Free plan | Starter | Scale | Business |
|---|---|---|---|---|
| ATS Jobs API, per company, up to 1,000 jobs included | $0.045 | $0.0428 | $0.0405 | $0.036 |
| Tech Jobs Search, per 1,000 matching jobs | $1.15 | $1.15 | $1.05 | $1.00 |
| Website Tech Stack Detector, per 1,000 websites | $2.00 | $2.00 | $1.80 | $1.60 |

ATS Jobs API extras: $0.01 for each further 1,000 jobs of one company, $0.01 per 200 job descriptions on a few boards (JazzHR, Paylocity, Freshteam, JOIN, Workday, Eightfold), and $0.002 per 1,000 open jobs for a later "only new jobs" re-check. Each run also has an Apify start fee of $0.00005. The Actor pages on the Apify Store always show the current prices.

Examples on the Free plan: open jobs at 10 companies cost about $0.45. A search that returns 200 matching jobs costs about $0.23. Checking 500 websites costs about $1.

## Add it to a client

Claude Code:

```bash
claude mcp add --transport http career-page-jobs "https://mcp.apify.com/?tools=fetch-actor-details,conserving_celerytop/live-career-page-jobs-api,conserving_celerytop/tech-jobs-search"
```

Claude Desktop, Cursor, VS Code and other clients that read an `mcpServers` block:

```json
{
  "mcpServers": {
    "career-page-jobs": {
      "type": "http",
      "url": "https://mcp.apify.com/?tools=fetch-actor-details,conserving_celerytop/live-career-page-jobs-api,conserving_celerytop/tech-jobs-search"
    },
    "website-tech-stack": {
      "type": "http",
      "url": "https://mcp.apify.com/?tools=fetch-actor-details,conserving_celerytop/website-tech-stack-detector"
    }
  }
}
```

In claude.ai, add a custom connector with the same URL.

## Things to ask

- "Is Stripe hiring machine learning engineers in New York? Check their Greenhouse board."
- "List the open sales roles at Notion, Linear and Ramp, with location and apply link."
- "Find remote senior backend jobs posted in the last 7 days at AI companies."
- "Which of these 50 shop domains run on Shopify, and which use Klaviyo?"

## Limits

- Job data comes only from public career pages. The Actors do not log in anywhere and do not return people or contact details.
- Very long company lists are better run on the Actor directly (Apify API, schedules, n8n, Make) than through a chat.
- This repository holds no code. The MCP server is Apify's hosted server; this repo only documents the endpoints and holds the `server.json` files for the official MCP Registry.

## Links

- ATS Jobs API: https://apify.com/conserving_celerytop/live-career-page-jobs-api
- Tech Jobs Search: https://apify.com/conserving_celerytop/tech-jobs-search
- Website Tech Stack Detector: https://apify.com/conserving_celerytop/website-tech-stack-detector
- Apify MCP server docs: https://docs.apify.com/platform/integrations/mcp
- Blog: https://donmangu.hashnode.dev

For questions, or a job board that should be supported, open an issue here or email don.mangu.data@gmail.com.
