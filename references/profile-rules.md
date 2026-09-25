# Candidate profile — content rules

Read this before writing `profile.json`. The document is a resume and nothing else.

## 1. What goes in, in this order

1. Header — three lines, nothing more:
   - `ROLE TITLE` in capitals (the normalised title from the MPC line)
   - three specialisms separated by ` / ` (the specialties in the MPC line, padded from the JD)
   - `<Metro> metro area | N years' experience | YYYY – Present` (the script builds this line from `metro`, `years` and the earliest role start)
2. Professional summary — 4 sentences, ~70–110 words
3. Core skills — 8 items
4. Experience — 2–4 roles (see §4)
5. Education — degree level and field, one line
6. Certifications / licenses — only if typical for the role; omit the section otherwise
7. Systems — tools and software, 4–7 items

Nothing else: no name, no contact line, no photo, no label, no note, no footer, no "about this
document" sentence, no bracketed placeholder. The build script rejects the file if any of that
is present.

## 2. Consistency with the MPC line

The MPC line is the contract. Everything the email claimed must be visible on the page:

- **Title** — the header title and the first words of the summary use the normalised title from
  the MPC line ("staff software engineer" → `STAFF SOFTWARE ENGINEER`), not the raw ad title.
- **Years** — `N` is the single integer from the MPC line. It appears in the header and in the
  first sentence of the summary, exactly. Role dates sum to `N` (§4).
- **Specialties** — the 1–2 details the MPC line named ("building platform services for a
  healthcare reimbursement product") are the first things the summary says and the first bullets
  of the current role.
- **Location** — the metro the MPC city belongs to (§3).

Skills, tools, responsibilities, industry and any certification or education come from the JD
only. Do not add technologies or credentials the JD does not mention or clearly imply.

## 3. Location = metro, never the city

Write `<Metro> metro area`. No state, no borough, no suburb, no neighbourhood.

- `Brooklyn-based` → `New York metro area`
- `Cambridge-based` → `Boston metro area`
- `Plano-based` → `Dallas–Fort Worth metro area`
- `Bellevue-based` → `Seattle metro area`
- `Denver-based` → `Denver metro area` (a city that is its own metro stays as is)

If a `metro` field is supplied with the lead (the leads CSV carries `city` and `metro`), use it.
Otherwise map with this table; a city not listed → the nearest major metro the JD's location
implies.

| Metro | Includes (common cities, boroughs, suburbs) |
|---|---|
| New York | Manhattan, Brooklyn, Queens, Bronx, Staten Island, Jersey City, Hoboken, Newark, Long Island City, White Plains, Yonkers, Stamford, Huntington, Hempstead, Garden City, Melville |
| Los Angeles | Santa Monica, Pasadena, Burbank, Glendale, Long Beach, Irvine, Anaheim, Culver City, El Segundo, Torrance |
| San Francisco Bay Area | San Francisco, Oakland, Berkeley, San Jose, Palo Alto, Mountain View, Sunnyvale, Menlo Park, Redwood City, San Mateo, Fremont, Santa Clara, Cupertino |
| Chicago | Evanston, Naperville, Schaumburg, Oak Brook, Rosemont, Skokie, Deerfield |
| Dallas–Fort Worth | Dallas, Fort Worth, Plano, Irving, Frisco, Richardson, Arlington, McKinney, Addison |
| Houston | The Woodlands, Sugar Land, Katy, Pasadena, Pearland |
| Washington, DC | Arlington, Alexandria, Bethesda, Reston, McLean, Tysons, Silver Spring, Rockville, Fairfax, Herndon |
| Boston | Cambridge, Waltham, Burlington, Somerville, Quincy, Newton, Lexington, Woburn, Framingham |
| Philadelphia | King of Prussia, Conshohocken, Cherry Hill, Wilmington, Malvern, Wayne |
| Atlanta | Alpharetta, Marietta, Sandy Springs, Roswell, Buckhead, Duluth, Norcross |
| Miami | Fort Lauderdale, Boca Raton, Coral Gables, Doral, Hollywood, Aventura, Miramar |
| Phoenix | Scottsdale, Tempe, Mesa, Chandler, Gilbert, Glendale |
| Seattle | Bellevue, Redmond, Kirkland, Tacoma, Renton, Bothell |
| Minneapolis–St. Paul | Minneapolis, St. Paul, Bloomington, Eden Prairie, Edina, Plymouth, Minnetonka |
| Denver | Boulder, Aurora, Englewood, Lakewood, Broomfield, Littleton |
| San Diego | La Jolla, Carlsbad, Sorrento Valley, Chula Vista, Escondido |
| Austin | Round Rock, Cedar Park, Pflugerville |
| San Antonio | New Braunfels, Schertz |
| Detroit | Troy, Southfield, Dearborn, Ann Arbor, Auburn Hills, Livonia |
| Tampa | St. Petersburg, Clearwater, Brandon |
| Orlando | Lake Mary, Winter Park, Kissimmee, Maitland |
| Charlotte | Huntersville, Fort Mill, Concord, Matthews |
| Raleigh–Durham | Raleigh, Durham, Cary, Chapel Hill, Morrisville |
| Nashville | Franklin, Brentwood, Murfreesboro |
| Baltimore | Columbia, Towson, Hunt Valley, Annapolis |
| St. Louis | Clayton, Chesterfield, St. Charles |
| Portland | Beaverton, Hillsboro, Lake Oswego, Vancouver WA |
| Pittsburgh | Cranberry Township, Monroeville |
| Cincinnati | Mason, Blue Ash, Covington, Newport KY |
| Cleveland | Independence, Beachwood, Mayfield, Akron |
| Columbus | Dublin, Westerville, New Albany |
| Indianapolis | Carmel, Fishers, Noblesville |
| Kansas City | Overland Park, Leawood, Olathe, Lenexa |
| Salt Lake City | Lehi, Provo, Draper, Sandy, Park City |
| Las Vegas | Henderson, Summerlin |
| Sacramento | Roseville, Folsom, Rancho Cordova |
| Milwaukee | Waukesha, Brookfield, Wauwatosa |
| Jacksonville | Ponte Vedra, Orange Park |
| Richmond | Glen Allen, Henrico, Midlothian |
| Hartford | Farmington, Glastonbury, West Hartford |
| Providence | Warwick, Cranston |
| Buffalo | Amherst, Williamsville |
| Rochester | Pittsford, Henrietta |
| Louisville | Jeffersonville, Prospect |
| Oklahoma City | Edmond, Norman |
| Memphis | Germantown, Collierville |
| Birmingham | Hoover, Homewood |
| New Orleans | Metairie, Kenner |
| Omaha | Bellevue NE, Papillion |
| Boise | Meridian, Nampa |
| Tucson | Oro Valley, Marana |
| Albuquerque | Rio Rancho |
| Honolulu | — |
| Anchorage | — |

## 4. Experience — progression, not repetition

Role count by total years `N`: `N ≤ 4` → 2 roles · `5–14` → 3 roles · `N ≥ 15` → 4 roles.

Every role has a **different title, one step up from the last**, ending at the MPC title. Never
the same title twice. Employer types differ across roles.

Years split: current role gets ~35–45% of `N`; the remainder is split across the earlier roles
with the earliest role shortest. Ranges use calendar years only and must chain with no gaps:
`start_year = current_year − N`; each role's `start` = previous role's `end`.

Worked split, `N = 12`, current year 2026:
- Staff Software Engineer — 2021 – Present (5)
- Senior Software Engineer — 2017 – 2021 (4)
- Software Engineer — 2014 – 2017 (3)

Bullets: 6 for the current role, 4 for the previous, 3 for earlier ones. Each carries scale
that is normal for the level (team size, request volume, portfolio size, docket size, project
value, revenue supported). Written from what people at that level do, in the language of the
JD — the JD's responsibilities become the current role's bullets. Present tense for the current
role, past tense for earlier ones. No employer, client, product, project or award names.

### Ladders (pick the one matching the MPC title; stop at the MPC title)

Software / product engineering
- Software Engineer → Senior Software Engineer → Staff Software Engineer → Principal Engineer
- Frontend / Backend / Full-Stack Engineer follow the same rungs with the specialty kept
- Software Engineer → Senior Software Engineer → Engineering Team Lead → Engineering Manager → Director of Engineering → VP of Engineering
- Engineering Manager → Director of Engineering → VP of Engineering → CTO

Security
- Security Analyst → Security Engineer → Senior Security Engineer → Staff Security Engineer / Security Architect
- Security Engineer → Senior Security Engineer → Security Manager → Director of Security → CISO
- Security Researcher: Vulnerability Researcher → Security Researcher → Senior Security Researcher

Data / ML / AI
- Data Analyst → Data Engineer → Senior Data Engineer → Staff Data Engineer
- Data Scientist → Senior Data Scientist → Staff Data Scientist / Lead Data Scientist
- ML Engineer → Senior ML Engineer → Staff ML Engineer; Applied Scientist → Senior Applied Scientist
- Research Engineer → Research Scientist → Senior Research Scientist

Cloud / DevOps / SRE / QA
- Systems Administrator → DevOps Engineer → Senior DevOps Engineer → Platform / SRE Lead
- Site Reliability Engineer → Senior SRE → Staff SRE
- QA Engineer → QA Automation Engineer → Senior QA Automation Engineer → QA Lead

Product / design
- Associate Product Manager → Product Manager → Senior Product Manager → Group PM / Director of Product
- Product Designer → Senior Product Designer → Lead Product Designer
- UX Researcher → Senior UX Researcher

Sales / marketing / customer
- SDR → Account Executive → Senior / Enterprise Account Executive → Sales Manager → Director of Sales → VP Sales
- Customer Success Associate → Customer Success Manager → Senior CSM → Head of Customer Success
- Marketing Coordinator → Marketing Manager → Senior Marketing Manager → Director of Marketing
- Product Marketing Associate → Product Marketing Manager → Senior PMM

Accounting / finance
- Accounting Assistant / Bookkeeper → Staff Accountant → Senior Accountant → Accounting Manager → Controller → Director of Finance → CFO
- AP Clerk → AP Specialist → AP Coordinator → AP Supervisor → AP Manager (AR mirrors this)
- Tax Associate → Tax Senior → Tax Manager; Audit Associate → Audit Senior → Audit Manager
- Financial Analyst → Senior Financial Analyst → FP&A Manager → Director of FP&A
- Payroll Clerk → Payroll Specialist → Payroll Manager

Legal
- Legal Assistant → Paralegal → Senior Paralegal → Paralegal Manager
- Litigation Assistant → Litigation Paralegal → Senior Litigation Paralegal
- Legal Secretary → Legal Administrative Assistant → Office Manager (law firm)

Construction / engineering / trades
- Project Engineer → Assistant Project Manager → Project Manager → Senior Project Manager → Director of Construction
- Estimator: Junior Estimator → Estimator → Senior Estimator → Chief Estimator
- Superintendent: Assistant Superintendent → Superintendent → General Superintendent
- Technician → Lead Technician → Field Supervisor → Service Manager

Healthcare / admin / operations
- Medical Assistant → Clinical Coordinator → Practice Manager
- Administrative Assistant → Executive Assistant → Office Manager → Operations Manager
- Operations Coordinator → Operations Manager → Director of Operations → COO
- HR Coordinator → HR Generalist → HR Manager → Director of People

Executive
- Any C-level or VP: three prior rungs from the matching functional ladder, 4 roles total.

## 5. Years — stay believable

Single integer only. Stay inside the band for the seniority the JD asks for:

- Software: mid engineer 3–6 · senior 6–10 · staff/principal 10–15 · engineering manager 8–12 · director 12–16 · VP / CTO / CISO 15–20
- Security engineer 5–9 · security researcher 6–10 · ML / AI / data engineer / data scientist 4–8 · research scientist 6–10 · DevOps / SRE / platform 5–9 · QA automation 4–8
- Product manager 5–10 · product designer 4–8 · PMM / demand gen 5–9
- Sales / AE 4–8 · CSM 3–6 · sales / marketing manager 6–10 · director 10–15 · VP 12–18 · GM / COO / CFO 15–20
- Accounting: bookkeeper / AP–AR 2–6 · staff accountant 2–5 · senior accountant 4–8 · accounting manager 7–12 · controller 8–15 · CFO 15–20
- Legal: legal assistant 2–5 · paralegal 3–8 · senior paralegal 7–12
- Construction: project engineer 2–5 · assistant PM 3–6 · PM 6–12 · senior PM 10–15 · estimator 4–10 · superintendent 8–15

Technology age — never claim more years in a technology than it has existed: Kubernetes and
Terraform 2014, Rust 2015, Swift 2014, React 2013, Go 2009, TypeScript 2012, Snowflake 2014,
dbt 2016, Databricks 2013, LLM / generative AI work 2020 onward. When the technology is younger
than `N`, attach the years to the role and the technology separately ("12 years building
backend services, the last four on Kubernetes").

Name at most two technologies in the summary and only ones in the JD. Never invent a stack.

## 6. Employer types, never names

Describe the kind of employer and its scale:

- "Venture-backed healthcare data platform, ~200 employees"
- "Publicly traded fintech, payments engineering group"
- "Regional CPA firm, transaction advisory practice"
- "Real estate and construction company, multi-entity"
- "Plaintiff-side personal injury firm, 12 attorneys"
- "Commercial general contractor, projects to $40M"
- "Mid-market SaaS company, Series C"

No company, client, product, project, building, case, patent, publication, award, school or
institution names. Licences and certifications by name and state only, no numbers.

## 7. Summary, skills, education, systems

- Summary sentence 1: `<Title> with N years of experience in <specialties from the MPC line>
  for <employer type>.` Sentence 2: scope and scale. Sentence 3: tools, standards or systems
  from the JD. Sentence 4: working style the JD asks for (independent, cross-functional,
  deadline-driven, hands-on).
- Core skills: 8 items, the JD's required skills in the JD's own words, Title Case.
- Education: one line — degree level and field the JD asks for ("Bachelor's degree in Computer
  Science"). No institution, no year.
- Certifications: only what is typical for the role and asked for or implied by the JD (CPA,
  PMP, OSHA 30, AWS Solutions Architect, Notary Public, bilingual). Omit the section for roles
  that normally carry none.
- Systems: tools named in the JD, plus the obvious baseline for the family (Microsoft Office /
  Google Workspace). 4–7 items.

## 8. profile.json schema

```json
{
  "title": "STAFF SOFTWARE ENGINEER",
  "specialisms": ["Platform Services", "Distributed Systems", "Healthcare Data"],
  "metro": "New York metro area",
  "years": 12,
  "summary": "Staff software engineer with 12 years of experience …",
  "core_skills": ["Distributed Systems", "…"],
  "roles": [
    {"title": "Staff Software Engineer", "start": 2021, "end": "Present",
     "employer_type": "Venture-backed healthcare data platform, ~200 employees",
     "bullets": ["…", "…", "…", "…", "…", "…"]},
    {"title": "Senior Software Engineer", "start": 2017, "end": 2021,
     "employer_type": "…", "bullets": ["…", "…", "…", "…"]},
    {"title": "Software Engineer", "start": 2014, "end": 2017,
     "employer_type": "…", "bullets": ["…", "…", "…"]}
  ],
  "education": ["Bachelor's degree in Computer Science"],
  "certifications": [],
  "systems": ["Go", "Kubernetes", "PostgreSQL", "AWS", "GitHub Actions", "Datadog"]
}
```

Roles are listed current-first. `end` is `"Present"` for the current role, an integer otherwise.
