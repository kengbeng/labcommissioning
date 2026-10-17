# Lab Commissioning

A browser-based laboratory commissioning notification and verification form built as a single HTML application. The form supports structured checklists, conditional comments, follow-up actions, draft save/load, and printable PDF export for safety and compliance workflows.

## Purpose

This project helps academic supervisors, laboratory teams, and safety personnel complete and review a lab commissioning checklist in a consistent format. It captures key laboratory information, tracks compliance responses, allows comments for items marked as "No", records follow-up actions, and produces a PDF-ready report.

## Key Features

- Multi-stage form flow for details, checklist, and review
- Response tracking for Yes / No / NA across a structured set of requirements
- Conditional comment fields triggered for non-compliant items
- Follow-up action tracking with owners and target dates
- Save/load draft support as JSON
- Local browser recovery for unsaved changes
- Printable report generation suitable for PDF export
- Section-level applicability toggles for areas not relevant to a site or activity

## Repository Contents

- `index.html` — complete single-file web app
- `README.md` — project overview and usage notes
- `NOTES.md` — implementation and operational notes

## Quick Start

1. Open `index.html` in a modern browser.
2. Complete the laboratory details section.
3. Progress through the checklist stages.
4. Use the review screen to confirm missing responses and unresolved issues.
5. Export the final form as a PDF using the print flow.

A local browser save draft or recovery option is available for convenience, but the app does not require any package installation or backend service.

## How It Works

The application is a self-contained HTML page with embedded CSS and JavaScript.

- The form definition is stored in a structured `SECTIONS` array in the page script.
- Each checklist item is rendered dynamically and bound to a response value.
- The app validates required fields and shows review warnings before export.
- The printable report is constructed from the form state and formatted for A4 portrait printing.
- Drafts are stored in JSON format and can be re-imported later.

## Typical Use

The workflow is intended for:

- Academic supervisors completing laboratory setup review
- Safety and health reviewers checking compliance
- Record retention and sign-off documentation
- Follow-up tracking and action closure

## Notes for Maintenance

- The checklist content is centralized in the script section of `index.html` and can be adjusted by editing the `SECTIONS` data.
- Styling is embedded in the same file; any visual adjustments should be made carefully to preserve print layout.
- PDF generation depends on the browser print dialog and should be tested in supported browsers such as Chrome and Safari.
- For substantial form changes, keep the JSON draft schema compatible with the validation logic.

## License

This repository does not currently include a formal license file. If this project is intended for broader sharing or reuse, add an appropriate open-source license before publication.

## Suggested Future Improvements

- Separate form data and script logic into external files
- Add validation rules per department or facility type
- Support import/export of completed forms as CSV or structured JSON
- Add a server-backed persistence layer for shared team use
- Add automated UI tests for form validation and PDF output
