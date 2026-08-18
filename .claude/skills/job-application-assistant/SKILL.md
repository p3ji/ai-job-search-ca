---
name: job-application-assistant
description: >
  Assists with job applications: evaluating job postings, tailoring CVs, writing cover letters,
  and preparing for interviews. Triggers on keywords like: job posting, job application, CV,
  cover letter, resume, interview prep, job fit, career, application, apply, ansøgning, stilling
allowed-tools: Read, Glob, Grep, WebFetch, WebSearch, Bash, Edit, Write, AskUserQuestion
framework_version: 1.3.4
---

# Job Application Assistant

> **Canadian fork.** For any application to a Canadian employer, read
> `09-canada-conventions.md` before drafting. It overrides the generic CV and
> cover-letter guidance where the two differ — most importantly on what must be left
> off a Canadian résumé (photo, age, marital status, SIN) and on stating work
> authorization explicitly.
>
> ### Route by sector before drafting anything
>
> | Posting type | Read first |
> |---|---|
> | **Federal government** | `CLAUDE.md` internal-candidate box + `09-canada-conventions.md` §5, §8 |
> | **Private sector, consulting, non-profit** | `10-private-sector-playbook.md`, if present |
>
> A candidate whose record is entirely public-sector needs deliberate translation work for
> every private-sector draft: government vocabulary (classification levels, committee
> acronyms, internal programme names) is opaque outside government, and federal writing
> convention understates personal contribution. Never reuse a federal bullet verbatim in a
> private-sector application — strip the acronyms and lead with the outcome.
>
> `10-private-sector-playbook.md` is personal and git-ignored; `/setup` generates it when
> the profile warrants one.

---

## Workflow

When the user provides a job posting (URL or text), follow this workflow:

### Step 1: Research & Evaluate Fit
- Fetch the job posting content (use WebFetch for URLs). **A 403 is not a dead end** - follow the escalation order in `09-web-research.md` before concluding a page is unavailable, and prefer the employer's own careers posting over an aggregator listing
- Keep the **full posting text verbatim** for Step 3b to archive - never a summary
- Analyze the posting for required competencies, keywords, and priorities
- Research the company (website, LinkedIn, mission, recent news), per `09-web-research.md`
- Score the posting against the candidate's profile using the framework in `04-job-evaluation.md`
- Present the evaluation table and verdict
- Suggest whether the candidate should call the employer before applying (see `04-job-evaluation.md` for guidance)
- Ask the user if they want to proceed with an application

### Step 2: Tailor CV
- Before writing either document, derive `<company>_<role>` once by the **Subfolder naming** rule in `documents/README.md`; reuse that exact value for the CV, cover letter, and Step 3b archive path. If the rule says to stop because the derived name is empty, stop before creating any file.
- Read the most relevant existing CV variant from `cv/` as a starting point
- Follow the guidelines in `05-cv-templates.md`
- For Canadian employers, apply `09-canada-conventions.md`: no photo/age/marital status/SIN,
  city + province only, Canadian spelling, work authorization stated, ≤2 pages
- **Private sector: apply `10-private-sector-playbook.md` §1–§3.** Strip every federal
  acronym, restate achievements outcome-first, drop classification levels, compress
  pre-2017 roles to one line, hard-cap at 2 pages
- Create `cv/main_<company>_<role>.tex` with tailored content
- Adjust: profile statement, skills section, experience bullet emphasis, section order

### Step 3: Write Cover Letter
- Follow the writing style rules in `03-writing-style.md` (critical: no em-dashes, no cliches)
- Follow the template structure in `06-cover-letter-templates.md`
- For Canadian employers, apply `09-canada-conventions.md`; match the language of the
  posting (a French posting means a fully French application)
- For federal (GC Jobs) postings, screening questions replace the letter — answer each
  essential qualification separately with a dated, concrete example
- **Private sector: apply `10-private-sector-playbook.md`.** Lead with a funded, quantified
  outcome; pre-empt the "why are you leaving your sector" question (§4); and check whether a
  referral path exists before recommending a cold application (§8)
- Create `cover_letters/cover_<company>_<role>.tex`
- Ensure the letter connects specific experience to the role requirements

### Step 3b: Record the Application
- Run this once both documents exist. A CV or cover letter drafted alone is not yet an application.
- Follow **`/apply` Step 6b** (`.claude/commands/apply.md`) exactly: same header, same match-then-update rule, same `drafted` row, same posting archive, same prohibition on touching `job_scraper/seen_jobs.json`. It is stated there once so the two paths cannot drift. Four of its values are named in `/apply`'s own terms: `cv_file`/`cover_letter_file` are the paths written in Steps 2 and 3 here, `source` is the posting URL from Step 1, `deadline` is the application deadline from the posting text Step 1 keeps verbatim (empty when the posting states none - never guess one), and the posting text item 7 archives is the one Step 1 read.
- This step exists here because `/scrape` Step 5 routes straight into this skill. Without it, that path writes two documents and records nothing.

### Step 4: Interview Preparation
- Follow the framework in `07-interview-prep.md`
- STAR entries generated by `/setup` are a **stub library**, not finished answers: complete
  the S/T/A/R lines against the actual questions asked in a given process
- **Private sector: apply `10-private-sector-playbook.md` §9.** No competency essays;
  expect conversational and case formats, and strip federal vocabulary from every answer
- Prepare STAR-format answers for likely questions
- Identify role-specific talking points
- Draft questions the candidate should ask the interviewer

---

## Reference Files

| File | Purpose |
|------|---------|
| `01-candidate-profile.md` | Education, experience, skills, publications, awards |
| `02-behavioral-profile.md` | Behavioral assessment, strengths, ideal environments |
| `03-writing-style.md` | Tone, structure, do's and don'ts |
| `04-job-evaluation.md` | Scoring framework for job fit |
| `05-cv-templates.md` | LaTeX CV structure and tailoring rules |
| `06-cover-letter-templates.md` | LaTeX cover letter structure and tailoring rules |
| `07-interview-prep.md` | STAR examples, tough questions, roleplay guidelines |
| `08-application-forms.md` | Portal free-text fields: self-introduction, project entries, character-limited pitches |
| `09-web-research.md` | Fetching postings and company pages: trust boundary, the WebFetch 403 fallback, escalation order, claim verification |
| `09-canada-conventions.md` | **Canadian market rules** — what must never appear on a résumé, work-authorization phrasing, Canadian spelling, NOC codes, provincial licensing, Quebec/French, federal screening questions |
| `10-private-sector-playbook.md` | *(personal, git-ignored)* Private-sector applications — public-sector-to-business translation, achievement restatements, objection handling, compensation, referral strategy, interview-format differences |

---

## Quick Commands

The user may also ask for individual steps without the full workflow:
- "Evaluate this job posting" - Step 1 only
- "Write a CV for [company]" - Step 2 only
- "Write a cover letter for [role] at [company]" - Step 3 only
- "Help me prepare for an interview at [company]" - Step 4 only
- "What jobs should I look for?" - Career strategy discussion using profile + evaluation framework
