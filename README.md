# Municipal Intel

An independent research and engineering project that reads what municipalities publish, budgets, council minutes, meeting recordings, grant awards and announcements, and shows what a municipality is planning, what it is funding and what it is not, with the source and the date on every line.

Built by [Mo Helmy](https://www.mohamedhelmy.com) on his own time from public records. It is not a commercial product. This repository describes the project; the application code is private.

## The problem

What a municipality is planning is public, but it is scattered across thousands of agency websites, scanned PDFs, meeting recordings and dozens of funding programs. Reading all of it for one municipality is a research project on its own, and most people never do it.

## The rule

Every claim points to a public source and a date. What you see is the raw evidence, dated: name, role, department, source. There are no confidence scores and no fit scores, because a score hides the reasoning you need to check.

## What it covers

- Public funding records from federal, state and local programs: 1.9M+ records from 100+ sources
- 2,000+ municipalities, seeded across seven states: the six New England states plus Pennsylvania

## How it works

1. **Sources:** public sources in every format: web pages, scanned PDFs, meeting minutes and meeting recordings.
2. **Ingest:** no model is involved, on purpose; this part has to be deterministic, auditable and cheap to run again. 500+ workers launch every county at once.
3. **Extract:** scanned pages are read with OCR; recordings are transcribed, each speaker identified, on a local GPU, so there are no per-minute fees.
4. **Unify:** records that share no identifier are stitched into one picture: what the agency needs, the money, and the people who decide.
5. **Retrieve:** search by meaning and by keyword at once, on full-precision embeddings in PostgreSQL with pgvector, and every hit carries where it came from.
6. **What you see:** the raw, dated evidence, with no scores attached.

## Stack

Python and FastAPI, PostgreSQL with pgvector (managed in production), Next.js. Row-level security keeps workspaces apart; operators get a read-only MCP server.

AI coding agents built most of it, under written architecture decisions and verification gates. The simplest of those gates: every database write is read back before the job counts as done.

More: [mohamedhelmy.com/municipal-intel](https://www.mohamedhelmy.com/municipal-intel)
