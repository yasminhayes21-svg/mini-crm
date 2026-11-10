# Mini CRM

A one-file CRM for a small business development team: each rep sees their territory, their clients and their prospect pipeline, unowned clients wait in an assignment queue, and AI suggests and qualifies new prospects.

I built the original for a sales team that had no shared view of who owned which client or which prospects were already being worked. It is in use there. This is a generic copy with made-up reps and companies, so it can be shown publicly.

**Open `index.html` in a browser.** No install, no account, no server.

## What it does

| Area | What a rep can do |
|---|---|
| **Rep picker** | Choose your name and open your territory, client count and pipeline. |
| **My prospects** | Track each prospect as New, Contacted, Meeting booked or Not interested, with a note. Counts per status at the top. |
| **AI suggestions** | Ask for eight prospects that resemble your clients, optionally narrowed by industry and country. Existing clients and prospects are excluded, and anything already in the CRM is dropped again on arrival. |
| **Qualify** | Score one prospect out of 100 on industry, size, market and buying signals, with a tier and a next step. If the model knows little about the company, the result says so. |
| **My clients** | See your accounts and move one back to the pool. |
| **Assignment queue** | Clients without an owner, grouped by country, with the rep whose territory it is. New clients are added here and badged "New". |

## Run it

1. Download or clone the repo and open `index.html`.
2. Pick a rep. The sample data loads on first open.
3. For the AI buttons, open **Settings** and paste a Gemini API key, free from Google AI Studio. Everything else works without one.

Settings also holds what your company sells and your ideal customer, which the AI uses to judge fit, plus **Export data** and **Reset sample data**.

## How it is built

- **One HTML file**, plain JavaScript, no framework or build step.
- **Data stays in the browser** (localStorage). The production version keeps the same records in a shared Airtable base so the whole team sees one pipeline; the storage is two functions, `load()` and `save()`, so it can point at any backend.
- **AI through Gemini** (`gemini-flash-lite-latest`, free tier) with JSON output, a 60-second timeout and a clear error instead of a hang.
- **Model output is escaped** before it is shown, so a company name from the model cannot inject markup into the page.
- **Duplicates are checked** by normalised name, accents and case ignored, against both clients and prospects.

## What I would add next

- A shared backend with a login, so reps cannot edit each other's pipelines.
- Converting a won prospect into a client in one click.
- Activity history per prospect: who changed the status, and when.
- A weekly summary per rep: new prospects, meetings booked, clients without contact for 90 days.
