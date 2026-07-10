# company-research-skill

A packaged Claude Agent Skill that researches a B2B company from its URL and
generates a professionally styled PDF "Account Research Report."

The repository contains a single distributable artifact, `research-company.skill`,
which is a ZIP archive bundling the skill definition, a data schema reference, and
a PDF-generation script.

## Contents

The `research-company.skill` archive contains:

- `research-company/SKILL.md` — the skill manifest and workflow instructions.
- `references/data-schema.md` — the full JSON schema used as input to the PDF generator.
- `scripts/generate_report.py` — a Python script that renders a JSON research file
  into a styled PDF using [reportlab](https://pypi.org/project/reportlab/).

## Features

- Defines a research workflow that gathers company information via web fetches and
  searches, then structures it as JSON (per `references/data-schema.md`).
- Generates a multi-section PDF report covering executive summary, company profile,
  products/offerings, target market, use cases, competitors, industry trends,
  recent developments, lead-generation notes, and information gaps.
- Uses a fixed slate-based color palette and reportlab's built-in fonts for
  consistent typography (no external font files are registered).

## Installation

The PDF generator requires Python 3 and reportlab. Per the instructions in
`SKILL.md`:

```bash
pip install reportlab
```

> Note: the repository does not include a dependency manifest
> (`requirements.txt` / `pyproject.toml`); `reportlab` is the only third-party
> import in `generate_report.py`.

To use the skill with Claude, the `research-company.skill` archive is uploaded as
an Agent Skill. (This usage is inferred from the `.skill` package format; it is not
documented in the repository.)

## Usage

The report generator takes a JSON input file and an output PDF path:

```bash
python3 scripts/generate_report.py input.json output.pdf
```

Running it without both arguments prints usage and exits:

```
Usage: python generate_report.py input.json output.pdf
```

The input JSON must follow the schema in `references/data-schema.md`. Required
top-level fields include `company_name` and `source_url`; optional sections include
`executive_summary`, `profile`, `products`, `target_market`, `use_cases`,
`competitors`, `industry`, `developments`, `lead_gen`, and `info_gaps`.

## Configuration

There are no environment variables or configuration files. Behavior is controlled
entirely by the input JSON and the two command-line arguments.

## License

No license file is included in this repository.
