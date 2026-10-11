# Bizzmind

**Turns huge, messy spreadsheets into structured data, live BI dashboards and a
small working app, so you don't have to buy a separate BI tool.**

**Live app:** https://bizzmind-lac.vercel.app/

## The problem

Many small and mid-sized companies run on Excel. Over the years their workbooks
grow into huge, unstructured files: dozens of sheets, merged cells, two-row
headers, one sheet per location and a new copy every month.

- Only one or two people really understand how a given workbook works.
- Teams lose hours reading, reconciling and maintaining these files by hand,
  and the monthly report gets rebuilt from scratch every time.
- The usual fix is a BI tool. That means another subscription, and someone
  still has to model the data before the first chart appears.

## What Bizzmind does

1. **Structures the data.** You upload the files exactly as they come out of
   the ERP, the till system or the accountant. Bizzmind finds the real tables
   inside them and loads them into a normalized database with a clean business
   layer on top. When something is unclear, such as the currency or what a
   column means, the AI asks a few questions. It remembers the answers so it
   never asks twice.
2. **Shows BI analysis at no extra cost.** An AI analyst builds a live dashboard
   with real filters (month, person, product, channel and so on) and writes a
   summary of the findings. Every chart is recomputed from the database. You
   don't need a separate BI licence, and nobody has to build the data model by
   hand.
3. **Builds a mini app for maintaining the data.** On the same data, the AI
   generates a small working app with entry forms instead of typing into cells,
   editable records, live indicators and calculators. The team keeps the data
   up to date in the app and stops feeding the spreadsheet. You change the app
   by describing what you want in the chat.

Bizzmind can also turn the analysis into a branded presentation.

## Tech stack

- **Backend:** Python, FastAPI and Postgres. Supabase provides the database,
  auth and storage.
- **Frontend:** Next.js, React, Tailwind and ECharts (in `web/`).
- **AI:** Claude through the Anthropic API.
- **Billing and hosting:** Paddle for billing; Vercel for hosting
  (see [DEPLOY.md](DEPLOY.md)).

## Running locally

```bash
python3 -m venv .venv
.venv/bin/pip install -r requirements-dev.txt
(cd web && npm install)
cp .env.example .env   # fill in Supabase, Anthropic and the other keys
./start.sh             # API on :8000, background worker, web on :3000
```

Then open http://localhost:3000.

`AI_BACKEND=api` uses the Anthropic API (set `ANTHROPIC_API_KEY`). When
`AI_BACKEND` is empty, the app runs through your local Claude Code login.
That mode is for your own testing only.

To run the tests: `.venv/bin/pytest` for the backend and `cd web && npm test`
for the frontend.
