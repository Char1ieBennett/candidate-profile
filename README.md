# candidate-profile

A Claude Code skill that turns a job description and an "I'm connected with …" candidate line
into a one- to two-page anonymised resume (`.docx` and `.pdf`).

## Install

```bash
git clone https://github.com/Char1ieBennett/candidate-profile ~/.claude/skills/candidate-profile
pip install python-docx
```

Restart Claude Code. To install for one project only, clone into `<project>/.claude/skills/candidate-profile` instead.

For the PDF, install LibreOffice (macOS: `brew install --cask libreoffice`). Without it you get the `.docx` only.

## Use

Type `/candidate-profile` and paste:

1. the job description (text, or a LinkedIn job URL)
2. the candidate line exactly as it was sent, e.g. *"I'm connected with a Brooklyn-based staff
   software engineer with 12 years of experience building platform services for a healthcare
   reimbursement product."*

You get back `Profile_<Metro>_<Role>.docx` and `.pdf`.

## Update

```bash
git -C ~/.claude/skills/candidate-profile pull
```

## Files

- `SKILL.md`: the workflow Claude follows
- `references/profile-rules.md`: content rules (sections, city-to-metro table, title ladders, year bands)
- `references/example-*.json`: worked examples
- `scripts/build_profile.py`: renders the document and rejects anything that breaks the rules
- `references/chatgpt-instructions.md`: the same workflow for a ChatGPT Project or custom GPT
