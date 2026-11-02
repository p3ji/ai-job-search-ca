---
framework_version: 1.0.0
---

# Canadian Application Conventions

Market rules for applying in Canada. Apply these on top of `05-cv-templates.md` and
`06-cover-letter-templates.md`, which stay country-agnostic. Where this file disagrees
with them, this file wins for Canadian applications.

> Not legal or immigration advice. Employment standards, human rights codes, and
> professional licensing are provincial — verify anything consequential against the
> relevant provincial body.

---

## 1. What must never appear on a Canadian résumé

Canadian human rights legislation bars employers from considering protected grounds,
so screeners are trained to disregard — and some ATS configurations to flag — personal
details that are routine on European CVs. Including them looks unfamiliar with the
market at best.

**Leave out:**

| Never include | Why |
|---------------|-----|
| Photo / headshot | Protected-ground exposure; many employers discard such résumés unread |
| Date of birth, age | Age is a protected ground |
| Marital or family status | Protected ground |
| Gender, nationality, ethnicity, religion | Protected grounds |
| **Social Insurance Number (SIN)** | Never on a résumé or application form. A legitimate employer asks only after a hire, for payroll |
| Full street address | City and province are enough (`Toronto, ON`) |
| Health status, disability | Protected ground; accommodation is discussed after an offer |
| References' contact details | "References available upon request" — or omit the line entirely |

**Do include:** name, city + province, phone, email, LinkedIn. A portfolio or GitHub
link where relevant.

## 2. Work authorization

This is the single most common reason a qualified candidate is screened out silently.
Employers cannot ask about immigration status directly, but they must confirm you can
legally work. Say it plainly and early — one line in the CV header area or the cover
letter's closing paragraph.

Use the phrasing that matches the actual status:

- `Canadian citizen` / `Permanent resident`
- `Authorized to work in Canada — open work permit valid to <YYYY-MM>`
- `Eligible for work in Canada under <program>` (e.g. PGWP, CUSMA, IEC)

Never write "will require sponsorship" if you already hold an open permit — the two are
routinely confused and the first phrase ends most applications.

**Federal public service** postings go further: the poster's *Who can apply* field is a
hard eligibility rule (often "persons residing in Canada and Canadian citizens residing
abroad", sometimes a geographic radius). Read it before drafting. `gcjobs-search`
returns it as `whoCanApply`.

## 3. Résumé vs CV

In Canada, **"résumé"** is the default document for industry roles: 1–2 pages, achievement-led,
tailored per posting. **"CV"** means the long-form academic record and is expected only in
academia, research, and some medical or senior scientific roles.

- Under ~10 years' experience → 1 page is respected, 2 is normal
- Senior / technical → 2 pages
- Academic CV → no page limit, include publications, grants, teaching, conferences

The repo's LaTeX templates produce a résumé-shaped document; keep it to two pages for
industry applications.

## 4. Spelling and register

Canadian English is its own blend and mixing systems reads as careless:

- **British-derived `-our`**: colour, behaviour, favour, labour, honour
- **American-derived `-ize`**: organize, analyze, recognize, optimize
- `centre`, `metre`, `theatre` (but `center` in proper nouns that use it)
- `defence`, `licence` (noun) / `license` (verb), `practise` (verb) / `practice` (noun)
- `cheque`, `catalogue`, `travelled`, `cancelled`, `enrolment`

Dates as `YYYY-MM-DD` or `March 2026`. Phone as `+1 416 555 0134`. Money as `CAD 85,000`
or `$85,000 CAD` when ambiguity with USD is possible.

Set `\usepackage[canadian]{babel}` in LaTeX where the template supports a language option.

## 5. Quebec and French

For any role in Quebec, or bilingual roles elsewhere:

- Quebec's language legislation makes French the normal language of business. A French
  cover letter for a Quebec-based employer is expected unless the posting is in English.
- Apply in the language of the posting. If the posting is French, the whole application
  is French — a French letter attached to an English résumé reads worse than a fully
  English application.
- State bilingual ability precisely rather than "bilingual": `French (native), English
  (fluent)` or the federal levels below.
- Both portal skills take `--lang fr` and search the French listings, which surface
  postings the English side does not.

**Federal language requirements** are a closed set and mean specific things:

| Value | Meaning |
|-------|---------|
| `English essential` | Unilingual English position |
| `French essential` | Unilingual French position |
| `English or French essential` | Either, candidate's choice |
| `Bilingual - imperative` | Must already meet the profile (e.g. BBB, CBC) **at hiring** |
| `Bilingual - non-imperative` | May be hired and trained to the profile |

A `Bilingual - imperative` posting with a CBC profile means a second-language evaluation
before appointment. Do not apply expecting to learn on the job.

## 6. NOC codes

The **National Occupational Classification (NOC 2021)** is the government's occupation
taxonomy — five-digit codes such as `21232` (software developer), `31301` (registered
nurse), `72200` (electrician). It matters because:

- Job Bank tags every posting with one, and its search infers a NOC from your keywords
- Immigration streams reference NOC codes and TEER categories directly
- The code is the reliable way to find equivalent roles under unfamiliar titles

Look up the NOC for the target role, then use its **official title wording** as a search
keyword. Canadian postings often use the NOC phrasing verbatim ("software engineer" vs
"développeur/développeuse de logiciels"), so searching the NOC title finds postings that
a colloquial title misses.

## 7. Credentials, licensing, and foreign education

Regulated professions — engineering, nursing, teaching, accounting, law, many trades —
are licensed **provincially**. A licence in one province does not automatically transfer.

- Engineering: `P.Eng.` from the provincial regulator (PEO in Ontario, APEGA in Alberta, …).
  Use `EIT` while in training. Never write `P.Eng.` unlicensed — it is a protected title.
- Accounting: `CPA`, provincial body.
- Trades: `Red Seal` endorsement travels between provinces; state it if held.

For foreign degrees, name the credential as awarded and add an equivalency if assessed:
`MSc Computer Science, TU Delft (WES-assessed: equivalent to a Canadian master's degree)`.
Do not silently translate a foreign degree into a Canadian one.

## 8. Cover letter norms

- One page, three or four paragraphs, addressed to a named person where discoverable.
- Canadian tone is warmer than German or Dutch directness and more concrete than
  British understatement: specific achievements, plainly stated, no inflation.
- Close with the work-authorization line and availability.
- Federal applications often replace the cover letter with **screening questions** that
  ask you to demonstrate each essential qualification with a dated, concrete example.
  Answer each one separately and completely — assessors score only what is written in
  the box and are instructed not to infer from the résumé.

## 9. Application channels worth knowing

| Channel | Notes |
|---------|-------|
| Job Bank (`jobbank-ca-search`) | Government-run, national, every province and territory. Strong for trades, healthcare, hospitality, rural. Employers apply by email/phone as often as by portal |
| GC Jobs (`gcjobs-search`) | Federal public service. Long processes (often 3–6 months), formal screening questions, published salary bands |
| LinkedIn (`linkedin-search`) | Dominant for corporate/tech roles in Toronto, Vancouver, Montréal, Calgary |
| Provincial / municipal portals | Each province and large city runs its own; not aggregated anywhere |
| Referrals | Canadian hiring leans heavily on referrals; a warm introduction outperforms any portal |

## 10. Checklist before submitting

- [ ] No photo, age, marital status, SIN, or full street address
- [ ] City + province in the header
- [ ] Work authorization stated in one unambiguous line
- [ ] Canadian spelling consistent throughout (`-our` + `-ize`)
- [ ] Salary expectations in CAD, if asked
- [ ] Résumé ≤ 2 pages for an industry role
- [ ] Language of application matches language of posting
- [ ] Provincial licensing named correctly, or flagged as in progress
- [ ] Federal: every screening question answered with a dated, concrete example
- [ ] Federal: eligibility against *Who can apply* actually confirmed
