# advanced-seo-audit

A [Claude Code](https://claude.com/claude-code) skill that audits and implements search and
AI-citation optimization across five lanes — then measures whether the numbers actually moved.

Point it at a domain or a local project. It sweeps the site with the crawler's eye, produces
a scorecard, proposes priorities, implements the fixes it has access to make, and sets a
re-measurement date.

## The five lanes

| Lane | Target | The question it answers |
|---|---|---|
| **SEO** | Google & Bing crawlers | Can crawlers read and index my content at all? |
| **AEO** (Answer Engine) | Google AI Overviews, Bing Copilot | Does the AI answer box above the results cite me? |
| **GEO** (Generative Engine) | ChatGPT, Perplexity, Claude | When generative AI browses, am I the primary source? |
| **LLMO** (LLM Optimization) | The model's own knowledge | Does the model know my brand — and know it correctly? |
| **NEO** (Naver Engine) | Naver search & AI Briefing | For the Korean market — does Naver cite me? |

## Install

```bash
git clone https://github.com/<your-username>/advanced-seo-audit.git ~/.claude/skills/advanced-seo-audit
```

Restart Claude Code. The skill loads automatically when a request matches its description,
or you can invoke it directly with `/advanced-seo-audit`.

## Usage

Just describe what you want:

```
audit my site's SEO — https://example.com
get my site cited by ChatGPT and Perplexity
create an llms.txt for this project
```

The procedure is always audit → implement → measure. Every report ends with what changed,
curl evidence that a crawler can actually see it, the next measurement date, and anything
that was declined and why.

## Keyword map input

Phase 2 designs one landing page per search question. It can interview you for those
questions, but it works better from a file. Drop a `keyword-map.csv` in your project root
and it will read that instead:

```bash
cp ~/.claude/skills/advanced-seo-audit/keyword-map-template.csv ./keyword-map.csv
```

Four columns are required — `primary_keyword`, `question`, `target_url`, `status` — and the
rest are optional. `status` is one of `keep`, `rewrite`, or `new`. Full column reference is
in [SKILL.md](./SKILL.md) under Phase 2.

Export as CSV rather than XLSX, keep one header row at the top, and put the file inside the
folder you open Claude Code in.

## What it will not do

Buy backlinks, join link-exchange schemes, cloak, hide text, or ship structured data that
disagrees with the visible page. Guideline violations risk the whole domain, not just a
ranking. Ask it for those and it will refuse and tell you why.

## Structure

```
advanced-seo-audit/
├── SKILL.md                    # operating procedure — the five phases
├── keyword-map-template.csv    # copy into your project as keyword-map.csv
└── references/
    ├── seo.md            # technical foundation checklist
    ├── aeo.md            # answer engine optimization
    ├── geo.md            # generative engine optimization
    ├── llmo.md           # LLM knowledge optimization
    ├── neo-naver.md      # Naver search & AI Briefing
    └── measure.md        # the measurement loop
```

`SKILL.md` is loaded whenever the skill triggers; the reference files are read on demand,
only for the lane being worked on.

## Credits

English translation and adaptation of
[fire-your-seo-agency](https://github.com/leopard627/fire-your-seo-agency) by
[@leopard627](https://github.com/leopard627). Original work is MIT licensed; this
adaptation keeps that license and copyright notice.

## License

MIT — see [LICENSE](./LICENSE).
