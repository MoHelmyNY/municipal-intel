# Municipal Intel

Public-sector demand and funding research, built from public records. It joins agency need, funding and decision-makers into one cited record, before the RFP.

It is for companies that sell to government in any industry: telecom, automotive and fleet, industrial and manufacturing, construction and engineering, energy and utilities, IT and software, healthcare equipment, and more.

A personal side project by [Mo Helmy](https://www.mohamedhelmy.com), built on my own time from public records. It is not a commercial product and has no customers. This repository describes the project; the application code is private.

## The problem

Government demand is scattered across thousands of agency websites, scanned PDFs, meeting recordings and dozens of funding programs. Sellers usually find it when the RFP drops.

## The rule

Every claim is cited to a public source and a date. Seller screens show raw, dated evidence (name, role, department, source, date). There are no confidence or fit scores.

## What it covers

- Public funding records from federal, state and local programs
- 2,000+ municipalities, seeded across seven states: the six New England states plus Pennsylvania
- 45,000+ NY/NJ nonprofits

## How it works

1. **Sources:** public sources in every format: web pages, scanned PDFs, meeting minutes and meeting recordings.
2. **Ingest:** no LLM, so it's deterministic, auditable and cheap to re-run. 500+ concurrent workers; every county shard launches at once.
3. **Extract:** OCR for scanned documents; transcription and speaker diarization on a local GPU, with no per-minute API fees.
4. **Unify:** joins records that don't share identifiers into agency need, funding and decision-makers.
5. **Retrieve:** hybrid semantic and lexical search with provenance, on full-precision embeddings in PostgreSQL + pgvector.
6. **Industry lenses:** the evidence core is industry-neutral. A lens reframes the same evidence for what a given seller offers, without changing the evidence underneath.

## Stack

Python/FastAPI, PostgreSQL + pgvector (managed in production), Next.js. Row-level security. A read-only MCP server for operators.

Built with AI coding agents governed by written architecture decisions and verification gates: every database write is queried back before a job counts as done.

More: [mohamedhelmy.com/municipal-intel](https://www.mohamedhelmy.com/municipal-intel)
