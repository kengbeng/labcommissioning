# Lab Commissioning

A browser-based laboratory commissioning notification and verification form built as a single HTML application. The form supports structured checklists, conditional comments, follow-up actions, draft save/load, and printable PDF export for safety and compliance workflows.

## Purpose

This project helps academic supervisors, laboratory teams, and safety personnel complete and review a lab commissioning checklist in a consistent format. It captures key laboratory information, tracks compliance responses, allows comments for items marked as "No", records follow-up actions, and produces a PDF-ready report.

## Key Features

- Multi-stage form flow for details, checklist, and review
- Response tracking for Yes / No / NA across a structured set of requirements
- Conditional comment fields triggered for non-compliant items
- Follow-up action tracking with owners and target dates
- Calendar (.ics) export for individual or all open follow-up actions, with default Singapore-time reminders
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

The default calendar entry is 09:00 Singapore time on the target date, with a reminder one day before. The form uses fixed defaults: 09:00 Singapore time and a reminder one day before. Change reminders in the calendar after import if needed. Events are marked as free and include the form reference, laboratory location, question reference, owner and action description.

Follow-up actions open on the Open filter. Use All, Overdue or Completed to review other actions. Required details and linked question wording appear beside the fields. The calendar panel allows selection of individual open actions; completed actions are excluded. Past reminder times are flagged before download and require an explicit acknowledgement if the user keeps those settings. Calendar selections and the acknowledgement are temporary controls, not saved form data.

Open or import the downloaded file in Outlook or another calendar application, then confirm the event times and reminders. No invitations or emails are sent. Imported events are copies: changing or completing an action here does not update or remove its calendar event. Re-importing may create duplicates, so update or remove older calendar entries when needed.

Calendar references are retained in downloaded form drafts and device recovery copies. Download an updated draft after calendar export when retaining those references for future exports.

## Notes for Maintenance

- Print output keeps short question groups and both signing blocks together where space permits. Follow-up actions precede supervisor confirmation and verification.
- Only applicable checklist questions appear in print. Sections marked not applicable show a concise notice; excluded questions and retained entries are omitted. Long comments use a full-width continuation row.
- Printed records include the export time in Singapore time. Pagination uses the browser’s actual printable area; recheck representative draft and completed records after changing print styles.

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

Date/time controls use zero-minimum grid tracks and explicit border-box width limits. Horizontal padding is applied to the displayed value rather than the outer native control to avoid the iOS Safari sizing issue documented in WebKit bug 301648. Native date/time pickers remain in use. Verify on iPhone/iPad Safari after changing these styles.


Print layout uses A4 with 14 mm top/bottom and 12 mm side margins. The browser controls page breaks; there are no fixed-height page wrappers or calculated page-number labels. Tables may continue between rows with repeated column headings. Long comments and evidence may flow across pages, while ordinary rows and signing blocks are kept together where they fit. Browser headers/footers remain a print-dialog setting. Check iOS Safari print preview with the intended paper size and printer.


Direct PDF download: choose PDF / Print, then Download PDF. PDF-LIB 1.17.1 (MIT licence, embedded in the HTML) creates the document locally with A4 margins, repeating table headings, page numbers, scope information, long comments/actions and optional drawn signatures. No external scripts, fonts or upload service are required. Non-WinAnsi text is drawn using local canvas text so entered names are retained; such lines are images rather than searchable text. Save prepared PDF remains available if an automatic download is blocked. iOS may open a preview; use Share and Save to Files. Browser print remains separate. Validate iOS/Android and desktop browser downloads before wider rollout.


Animal Facility supplement: selecting Animal Biosafety (ABSL) reveals species selection, animal rooms, animal approval/protocol references and AF1–AF11 readiness checks. AF11 appears only for non-human primates. Existing source question references remain unchanged. The general approval question points to the animal-specific records rather than duplicating the approvals assessment. AF answers/comments and scope fields are retained when deselected, saved in drafts, included in review and both PDF paths, and linked to follow-up actions/calendar events. Excluded AF checks are omitted from applicable totals and printed as NA with retained history. Existing drafts import with blank new fields; an existing ABSL selection therefore requires review of the new supplement. Scope/record edits invalidate drawn signatures through the existing signing checks. Animal-specific wording should be reviewed by the facility team before publication.


Print/export scope policy: unselected animal-facility checks and other scope-excluded questions are omitted. Entire sections marked None/not applicable and unselected radiation groups show a concise not-applicable notice instead of questions, previous answers, comments or supporting details. Animal-facility questions appear only when ABSL is selected; the primate check appears only when non-human primates are selected. Retained entries remain in the editable form and JSON draft for restoration. Individual NA answers within an applicable section remain visible. This policy applies to browser printing and direct PDF downloads, and supersedes earlier notes about printing all excluded questions/history.


Calendar export now uses fixed defaults: 09:00 Singapore time on the action target date, with a reminder one day before. Time/reminder entry controls have been replaced by a short explanatory note. Older drafts remain importable; their previous calendar preferences do not override the fixed defaults. Past-reminder acknowledgement, action selection and completed-action exclusion are retained. Reminders can be adjusted in the calendar after import.
