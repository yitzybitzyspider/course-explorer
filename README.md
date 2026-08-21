# Haas Elective Explorer

A course-planning tool for Berkeley Haas MBA electives, built from the AAI/TIES evaluation
portal. Two tabs: a filterable course finder, and a set of charts on what five years of
evaluations actually show.

**Private repository.** It embeds 52,381 student-to-student comments written behind CalNet.
Do not make this repo public.

## Layout

```
index.html          the whole app - markup, styles, logic. Hand-editable (~63 KB).
data/explorer.json  course + comment payload. Generated, do not hand-edit (~2 MB).
data/insights.json  aggregates behind the six charts. Generated (~11 KB).
_headers            noindex / no-referrer headers, read by Cloudflare Pages.
robots.txt          keeps the site out of search engines.
```

Edit `index.html` freely — copy, styling, caveats, layout. Regenerating the data
replaces only the files under `data/`, so your edits survive.

## Running it locally

The page fetches its data, so `file://` will not work — you need a local server:

```bash
python3 -m http.server 8000
# then open http://localhost:8000
```

Opening `index.html` directly shows a "could not load the data files" message. That is expected.

## Deploying

Connected to Cloudflare Pages. Push to `main` and it redeploys automatically —
no build command, output directory is the repo root.

## Data provenance

- 4,867 section evaluations, 16 terms (Spring 2021 – Spring 2026), all Haas programs
- 2,492 student-to-student comment PDFs, 52,381 individual comments
- Fall 2026 elective schedule from the FTMBA Academics Team
- Instructor priors computed across every program, not just MBA electives

Scores are shrunk toward the population mean in proportion to sample size
(empirical Bayes). Confidence intervals are 90%. Bid-point history is absent because
Haas does not retain it.

## Known gaps

- Detailed score reports retrieved for a subset of sections; the rest use comment
  counts as a sample-size proxy, which correlates only 0.47 with true respondent counts.
- Four comments appear as summaries rather than verbatim (personal disclosures and
  unverified allegations), each labelled with the reason.
