# Search Queries for Job Scraper — Canada

<!-- SETUP: Replace the [PLACEHOLDER] values with your own roles, skills, and cities. -->

## Installed portal CLIs (primary for `/scrape`)

`/scrape` discovers every portal skill under `.agents/skills/*/SKILL.md` and runs its CLI
first. In this Canadian fork the relevant ones are:

| Skill | Covers | Notes |
|-------|--------|-------|
| `jobbank-ca-search` | Job Bank / Guichet-Emplois, all of Canada | Government-run, every province and territory, all sectors. `--lang fr` for the French listings |
| `gcjobs-search` | GC Jobs — federal public service | Jobs open to the public. Sweeps the listing and filters locally, so give it ~30 s |
| `linkedin-search` | Global, incl. Canada | Pass a Canadian place string, e.g. `-l "Toronto, Ontario, Canada"` |
| `freehire-search` | Country-agnostic REST API | Ships with upstream |

The Danish demo skills (`jobindex-search`, `jobnet-search`, `jobbank-search`,
`jobdanmark-search`) are inherited from upstream and left installed for reference.
**Set `enabled: false` in their `SKILL.md` frontmatter so `/scrape` skips them** — they
will otherwise run Danish queries on every scrape.

**Language scope:** write every query category in every language listed in your CLAUDE.md Languages table (typically 1-2, sometimes more). A posting requiring a language you have *not* declared, as a job condition, is excluded before scoring; a posting requiring a *higher level* than you declared in a language you *do* work in is flagged for your own judgment, not excluded — see `04-job-evaluation.md`'s Language Gate, the single source of truth for this rule. Translate each category's keywords rather than machine-translating word-for-word (e.g. "Frontend Developer" -> "Desarrollador Frontend", not a literal word-for-word translation) if you work in more than one language.

> `jobbank-search` (upstream, Danish `jobbank.dk`) and `jobbank-ca-search` (this fork,
> Canadian `jobbank.gc.ca`) are different boards with confusingly similar names. The
> Canadian one always carries the `-ca` suffix.

The `site:` query templates below are the **WebSearch fallback** — for boards without a
CLI, company career pages, or when a CLI fails.

## Search sites

Primary (have CLIs — no `site:` line needed):
- **jobbank.gc.ca** — Job Bank, national coverage
- **emploisfp-psjobs.cfp-psc.gc.ca** — GC Jobs, federal public service
- **linkedin.com/jobs** — filter to Canada / your city

Secondary (WebSearch fallback, no CLI in this fork):
- **indeed.ca** — largest commercial board in Canada; blocks automated access, so
  WebSearch only
- **glassdoor.ca** — postings plus salary and review context
- **talent.com** — Canadian-founded aggregator
- **jobillico.com** — strong in Quebec, bilingual
- **eluta.ca** — indexes employer career pages directly, good for jobs never posted to boards
- **workinnonprofits.ca**, **charityvillage.com** — non-profit sector
- **[YOUR_PROVINCIAL_PORTAL]** — e.g. BC Public Service, OPS Careers (Ontario),
  Alberta Government, Emplois Québec; each province runs its own
- **[YOUR_MUNICIPAL_PORTAL]** — City of Toronto, City of Vancouver, etc.
- Company career pages via `site:` search

## Query categories

Combine each query with your location terms. Canadian location strings that work well:
`Toronto`, `Greater Toronto Area`, `GTA`, `Vancouver`, `Metro Vancouver`, `Montréal`,
`Calgary`, `Ottawa-Gatineau`, `Edmonton`, `Winnipeg`, `Halifax`, `Québec City`,
`Waterloo Region`, `Remote Canada`, `Hybrid [YOUR_CITY]`.

Write **each category in every language from your Languages table** (see Language scope above).

**Organize by function, not job title.** The same underlying work carries different titles across companies and markets (a "Data Scientist" role at one employer may be posted as "Insights Analyst" or "Data Consultant" at another). Name each priority category after the function it covers, and list several plausible job titles as query variants within that category rather than betting an entire priority tier on one exact title string.

### Priority 1: [YOUR_PRIMARY_ROLE_TYPE]

Your strongest and most desired direction.

```
site:linkedin.com/jobs "[YOUR_PRIMARY_JOB_TITLE]" [YOUR_CITY] Canada
site:indeed.ca "[YOUR_PRIMARY_JOB_TITLE]" [YOUR_CITY]
site:eluta.ca "[YOUR_PRIMARY_JOB_TITLE]" [YOUR_CITY]
"[YOUR_PRIMARY_JOB_TITLE]" "[YOUR_CITY]" careers -site:linkedin.com
```

Also run the NOC official title for the role, not just the colloquial one — Canadian
postings frequently use NOC wording verbatim. See `09-canada-conventions.md` §6.

### Priority 2: [YOUR_DOMAIN_EXPERTISE]

```
site:linkedin.com/jobs [YOUR_DOMAIN_KEYWORD_1] [YOUR_CITY] Canada
site:indeed.ca [YOUR_DOMAIN_KEYWORD_1] OR [YOUR_DOMAIN_KEYWORD_2] [YOUR_PROVINCE]
site:jobillico.com [YOUR_DOMAIN_KEYWORD_1] [YOUR_CITY]
```

### Priority 3: [YOUR_ADJACENT_ROLE_TYPE]

Roles you could pivot into.

```
site:linkedin.com/jobs "[YOUR_ADJACENT_TITLE_1]" [YOUR_KEY_SKILL] [YOUR_CITY]
site:indeed.ca "[YOUR_ADJACENT_TITLE_2]" [YOUR_KEY_SKILL] [YOUR_PROVINCE]
```

### Priority 4: Public sector

Federal is covered by the `gcjobs-search` CLI. These reach the provincial, municipal,
and broader-public-sector boards it does not:

```
site:gov.bc.ca/careers [YOUR_KEY_SKILL]
site:gojobs.gov.on.ca [YOUR_KEY_SKILL]
"[YOUR_PRIMARY_JOB_TITLE]" city of [YOUR_CITY] careers
"[YOUR_PRIMARY_JOB_TITLE]" [YOUR_PROVINCE] health authority careers
```

### Priority 5: Remote and cross-border

```
site:linkedin.com/jobs "[YOUR_PRIMARY_JOB_TITLE]" "remote" Canada
"[YOUR_PRIMARY_JOB_TITLE]" "remote - Canada" OR "Canada remote"
```

Watch for US postings that say "remote" but are not open to Canadian residents —
check for a Canadian entity or "authorized to work in Canada" before applying.

## Location filter

Verify the job location is realistically commutable, or genuinely remote. Define your
acceptable areas:
- [YOUR_CITY] and surrounding municipalities
- [ACCEPTABLE_AREA_1] — e.g. within [X] min by transit or car
- [BORDERLINE_AREA] (borderline)
- [TOO_FAR_AREA] (too far)

Canadian specifics worth encoding:
- Job Bank writes locations as `City (PR)`, e.g. `Mississauga (ON)`; GC Jobs writes
  `City (Province)`, e.g. `Ottawa (Ontario)`. Both spell Québec with the accent.
- Postings covering several sites appear as "Various locations" — open the posting to
  see whether yours is included.
- Winter commute distances are not summer commute distances; be honest about the limit.

## Language Filter

Your working languages and levels are in CLAUDE.md's Languages table. When filtering scraped results, apply `04-job-evaluation.md`'s Language Gate: a posting requiring a language you haven't declared at all is excluded; a posting requiring a higher level than you declared in a language you do work in is not excluded, flag it clearly instead (see `job-scraper/SKILL.md`'s Step 3 "Quick Fit Assessment" for how the flag surfaces in `/scrape` output). Postings simply *written* in a language you don't work in, that don't require it on the job, are fine.

## Date filter

Only include jobs posted within the last 14 days, or whose closing date has not passed.
Where a posting date cannot be determined, include it but flag as "date unknown".

GC Jobs publishes a **closing** date rather than a posting date — filter those on the
deadline instead, and treat anything closing within 48 hours as urgent.

## Work-authorization filter

Screen out postings you are not eligible for before spending effort on them:
- Federal postings: check the *Who can apply* rule (`whoCanApply` from `gcjobs-search`)
- Security-cleared roles: many require Canadian citizenship, not just residency
- Postings that state sponsorship is unavailable, if that applies to you

## Adapting queries

If the user specifies a focus area, select queries from the matching category and
generate 2-3 custom queries for that focus. For example:
- `/scrape federal` → run `gcjobs-search` with no title filter plus the public-sector queries
- `/scrape bilingual` → `gcjobs-search --lang-req Bilingual` plus `jobbank-ca-search --lang fr`
- `/scrape remote` → the remote category plus `linkedin-search --remote remote -l "Canada"`
