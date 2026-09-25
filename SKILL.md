---
name: candidate-profile
description: "Build the candidate profile document (resume-format .docx + PDF) that backs up an MPC cold-email line, from the live job description plus the exact 'I'm connected with …' sentence that was sent. Anonymised (no name, contact, employer or school names), metro-level location, roles that progress up to the current title, and nothing on the page except the resume sections. Use whenever a lead has asked for the resume, or the user pastes a job description and an MPC/candidate line, or says: 'candidate profile', 'build the resume for this MPC', 'profile for this lead', 'they asked for the resume', 'dummy resume', 'resume for this job', 'send me the resume', 'make the profile for this JD'."
---

# Candidate profile

Turn a job description + the MPC line into a one- to two-page resume-format document
(`Profile_<Metro>_<Role>.docx` and `.pdf`). Content rules live in
`references/profile-rules.md` — read it before writing the profile.

## 1. Collect the two inputs

- **The job description.** Pasted text, or a job URL. LinkedIn `linkedin.com/jobs/view/…`
  pages fetch fine with a plain web fetch — use it. Indeed `viewjob?jk=…` pages return a login
  redirect to every fetcher; don't try, ask for the JD pasted. For any other URL, fetch once;
  if the text has no job title, responsibilities or requirements in it, ask for the paste and
  stop. Never guess a JD from a URL or a title.
- **The MPC line**, exactly as it went out: e.g. *"a Brooklyn-based staff software engineer
  with 12 years of experience building platform services for a healthcare reimbursement
  product."* If it's missing, ask for it. Never write one.

If a `metro` value comes with the lead, take it, minus any state code (`New York, NY` →
`New York metro area`); it overrides the city→metro table. A metro that is really a suburb
(`Huntington, NY`) still maps up to its major metro (`New York metro area`).

## 2. Parse

From the MPC line: normalised title · years `N` (single integer) · the 1–2 specialties ·
the city → **metro** (`Brooklyn` → `New York metro area`; table in the rules file §3; the page
never shows a city, borough, suburb or state).

From the JD: seniority · required skills · tools and technologies · responsibilities ·
industry · certifications and education asked for.

## 3. Write `profile.json`

Schema in the rules file §8. The contract:

- Title, `N` and the specialties come from the MPC line and appear verbatim in the header and
  the first sentence of the summary.
- Skills, tools, responsibilities, certifications and education come from the JD only.
- Roles: 2 (`N ≤ 4`), 3 (`5–14`) or 4 (`N ≥ 15`), each a different, ascending title from
  the ladder for that family (rules §4), ending at the MPC title; years chain with no gaps and
  sum to `N`, current role ~35–45% of `N`; employer **types** only, varied; bullets 6 / 4 / 3
  with scale normal for the level. Current role present tense, earlier roles past tense.
- Stay inside the year band for the seniority and never claim more years in a technology than
  it has existed (rules §5).

Before building, read the JSON once more and confirm: no name, phone, email, address, link or
photo; no employer, school, client, product, project, award or institution name; no licence
number; no salary; no month-level date; no bracket or placeholder; no sentence describing what
the document is (no "representative", "illustrative", "not a specific individual" or similar
anywhere). The document is only the resume sections.

## 4. Build

```bash
python scripts/build_profile.py profile.json --out Profile_<Metro>_<Role>.docx --pdf
```

`<Metro>` and `<Role>` with spaces removed, e.g. `Profile_NewYork_StaffSoftwareEngineer.docx`.
The script renders the sections in order (header · Professional summary · Core skills ·
Experience · Education · Certifications / licenses if any · Systems), blanks the file
author, then re-reads the document and exits `2` with a list of problems if anything banned
got through — fix `profile.json` and rebuild. `--pdf` uses LibreOffice when it is installed;
if it isn't, the script says so and the .docx is exported to PDF by hand.

Only dependency: `python-docx` (`pip install python-docx` if missing).

## 5. Hand back

The .docx and .pdf, one line. No summary of what was done, no notes about the profile. If the
environment cannot create files, output the resume as plain text in the same section order
and nothing else.

## Examples

`references/example-tech.json` — staff software engineer, New York metro area, 12 years,
healthcare data platform (3 roles).
`references/example-accounting.json` — property & construction accountant,
Minneapolis–St. Paul metro area, 7 years (3 roles).
