# Biotech Intelligence

A single-page tool that searches any biotech topic against live PubMed literature and generates a synthesized intelligence brief — state of the field, trending sub-topics, and a founder-oriented commercial insight — directly from the retrieved papers.

**Live demo:** https://aryab19.github.io/biotech-intelligence

## What it does

1. You enter a topic (e.g. "liquid biopsy", "CRISPR delivery", "GLP-1 obesity").
2. It queries the [PubMed E-utilities API](https://www.ncbi.nlm.nih.gov/books/NBK25501/) for the most recent matching papers from the last 12 months.
3. It synthesizes a short brief from the retrieved abstracts — extracting recurring themes, estimating research momentum from publication recency, and framing a commercial-whitespace takeaway.
4. If PubMed is unreachable, it falls back to curated example data for a set of biotech topics so the demo still works.

## Why the brief is generated client-side, not by an LLM API call

An earlier version of this tool called the Anthropic API directly from the browser to generate the brief. That doesn't actually work on a static, key-less site: the Anthropic API requires an API key, and there's no secure way to hold a secret key in client-side JavaScript on GitHub Pages — anyone viewing the page source would see it, and the call would fail without one anyway. That version silently fell back to two hardcoded example briefs on every real search, so the "AI brief" a visitor saw almost never matched the actual papers being shown.

This version replaces that with a lightweight synthesis function that runs entirely in the browser: it extracts recurring keywords and phrases across the retrieved abstracts, checks publication recency to estimate momentum, and composes the three sections of the brief from that. No API key, no backend, and the brief is always about the papers actually on screen.

## Tech stack

- Vanilla HTML/CSS/JS — no build step, no dependencies
- [PubMed E-utilities](https://www.ncbi.nlm.nih.gov/books/NBK25501/) (`esearch` + `efetch`) for live literature data
- Deployed via GitHub Pages

## Running locally

No build step needed — it's a single static file.

```bash
git clone https://github.com/aryab19/biotech-intelligence.git
cd biotech-intelligence
python3 -m http.server 8000
# then open http://localhost:8000
```

## Known limitations

- PubMed E-utilities allows a modest unauthenticated rate limit (3 requests/sec). For heavier use, register a free NCBI API key and pass it as an environment-injected value at build time rather than hardcoding it in source.
- The mock fallback library covers the 8 topics shown as quick-search chips; other queries fall back to a generic template if PubMed can't be reached.
- Brief synthesis is extractive/heuristic, not generative — it summarizes patterns in the retrieved abstracts rather than reasoning about the field the way an LLM would.

## Author

Arya Bhure — Biomedical Engineering, UT Dallas.
[LinkedIn](https://linkedin.com/in/arya-bhure-601404269)
EOF
echo "README written"
Output

README written
