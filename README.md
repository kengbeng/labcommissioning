# Lab Commissioning

A browser-based laboratory commissioning notification and verification form built as a single HTML application. The form supports structured checklists, conditional comments, follow-up actions, draft save/load, and printable PDF export for safety and compliance workflows.

## Purpose

This project helps academic supervisors, laboratory teams, and safety personnel complete and review a lab commissioning checklist in a consistent format. It captures key laboratory information, tracks compliance responses, allows comments for items marked as "No", records follow-up actions, and produces a PDF-ready report.

## Key Features

- Multi-stage form flow for details, checklist, and review
- Response tracking for Yes / No / NA across a structured set of requirements
- Conditional comment fields triggered for non-compliant items
- Follow-up action tracking with owners and target dates
- Calendar (.ics) export for individual or all open follow-up actions, with configurable Singapore-time reminders
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

## Calendar Reminders

In **Follow-up actions**, enter an action description, owner and target date. Download one action using its calendar button, or use **Download all open actions (.ics)**. Completed actions are excluded; incomplete open actions must be corrected before export.

The default calendar entry is 09:00 Singapore time on the target date, with a reminder one day before. Both settings can be changed, including choosing no reminder. Events are marked as free and include the form reference, laboratory location, question reference, owner and action description.

Follow-up actions open on the Open filter. Use All, Overdue or Completed to review other actions. Required details and linked question wording appear beside the fields. The calendar panel allows selection of individual open actions; completed actions are excluded. Past reminder times are flagged before download and require an explicit acknowledgement if the user keeps those settings. Calendar selections and the acknowledgement are temporary controls, not saved form data.

Open or import the downloaded file in Outlook or another calendar application, then confirm the event times and reminders. No invitations or emails are sent. Imported events are copies: changing or completing an action here does not update or remove its calendar event. Re-importing may create duplicates, so update or remove older calendar entries when needed.

Calendar references are retained in downloaded form drafts and device recovery copies. Download an updated draft after calendar export when retaining those references for future exports.

## Notes for Maintenance

- Print output keeps short question groups and both signing blocks together where space permits. Follow-up actions precede supervisor confirmation and verification.
- All checklist questions remain in print. Scope-excluded responses show NA; retained earlier responses and comments are labelled separately. Long comments use a full-width continuation row.
- Printed records include the export time in Singapore time. Pagination is measured at the A4 print width; recheck representative draft and completed records after changing print styles.

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

## Optional Drawn Signatures

The Academic Supervisor and verifier can draw signatures using a mouse, finger or stylus, with Clear drawing, Cancel, Use signature and Draw again controls. A name and signing date are required when capturing a signature. Signing the exported PDF or printed copy remains available.

Signatures are generated locally within the single HTML file, retained in downloaded JSON drafts and device recovery, and included in printed PDFs with capture timestamps. Older unsigned drafts remain compatible. A drawn signature does not verify identity or provide certificate-based digital signing or tamper protection. Signed drafts and PDFs contain signature data and should be kept secure.

Changes to record details, scope, answers, evidence or actions clear both signatures and display a warning. Changing verifier signing details clears only the verifier signature. Adding a verifier signature preserves the supervisor signature; replacing or removing the supervisor signature clears the verifier signature. Calendar reminder settings, calendar export references and navigation do not invalidate signatures. Imported signing data that does not match the restored record is cleared for review and re-signing; this prevents accidental reuse, not deliberate modification.
