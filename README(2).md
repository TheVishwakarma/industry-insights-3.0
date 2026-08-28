# Daily Summary Tool

A browser-based workflow for preparing **UK Social Housing** daily summaries for **Tenders, Contract Awards, News, and Minutes**, with structured WordPress-ready output.

The tool is designed for Locarla's Social Housing UK publishing workflow and combines bulletin parsing, Excel matching/enrichment, manual review, ordering controls, AI-assisted summary generation, and WordPress code formatting in a single page.

---

## Key Features

### Tenders

- Paste the full daily bulletin HTML source.
- Extract Housing-sector Tender Alerts.
- Apply the existing tender filtering rules.
- Upload the Locarla Tenders Excel workbook.
- Match and enrich bulletin tenders with available data such as value, tenure, location, client, and trade/category.
- Review and manually edit extracted data.
- Drag and reorder tenders before generating the final summary.
- Select multiple tenders and delete them in one action.
- Generate a professional tender summary.
- Produce WordPress-ready code automatically wrapped with:
  - `[contracts_header]`
  - `[contracts_footer]`

### Contract Awards

- Paste the full daily bulletin HTML source.
- Extract Housing-sector contract awards.
- Upload the Locarla CANs Excel workbook.
- Match and enrich award records with winner, value, tenure, location, and other available fields.
- Review and manually edit extracted data.
- Drag and reorder awards before final output.
- Select and delete multiple awards at once.
- Generate a structured contract awards summary.
- Produce WordPress-ready code automatically wrapped with:
  - `[contracts_header]`
  - `[contracts_footer]`

### News

- Switch directly to the News Summary workflow.
- Generate/edit the daily news summary.
- Format the final content for WordPress.
- Automatically add:
  - `[daily_news_header]`
  - `[daily_news_footer]`

### Minutes

- Prepare weekly/minutes summary content.
- Format the output for WordPress.
- Automatically add:
  - `[minutes_header]`
  - `[minutes_footer]`

---

## Recent Improvements

The current version includes several workflow improvements:

1. **Drag-to-reorder Tenders and Awards**  
   After processing a bulletin, items can be reordered by dragging them into the required publishing sequence. The selected order is retained for later matching and summary generation.

2. **Bulk selection and deletion**  
   Tenders and Awards can be selected using checkboxes and removed together using the bulk delete control.

3. **Improved mode switching**  
   Switching from News Summary back to Tenders or Contract Awards no longer destroys or incorrectly resets the bulletin workflow. Previously pasted bulletin HTML remains available instead of triggering the incorrect:

   > Please paste the full bulletin HTML source first...

4. **Automatic WordPress shortcode wrappers**  
   WordPress formatter output now inserts the appropriate header and footer shortcodes automatically for Tenders, Awards, News, and Minutes.

---

## Workflow

### 1. Select a Summary Type

Choose the required mode:

- **Tenders Summary**
- **Contract Awards**
- **News Summary**
- **Minutes Summary**

### 2. Process the Bulletin

For Tenders or Awards:

1. Open the bulletin page.
2. View the full HTML source using `Ctrl+U`.
3. Select all using `Ctrl+A`.
4. Copy using `Ctrl+C`.
5. Paste the source into the bulletin HTML field.
6. Click **Process Bulletin**.

The application extracts the relevant Housing-sector records and displays them for review.

### 3. Review, Reorder, or Remove Records

After processing:

- Drag records to change their order.
- Select one or more records using the checkboxes.
- Use **Delete Selected** to remove unwanted entries.
- Edit individual record details where required.

The displayed order becomes the publishing order used by the summary generator.

### 4. Upload the Matching Excel File

For **Tenders**, upload the Locarla Tenders workbook.

For **Contract Awards**, upload the Locarla CANs workbook.

The application attempts to match bulletin records against the spreadsheet data and enrich the extracted records.

Unmatched records can still be completed manually.

### 5. Generate the Summary

Generate the final editorial summary after reviewing the records.

The application provides:

- A readable summary preview.
- WordPress-ready HTML/code.
- The correct WordPress shortcode wrapper for the selected content type.

---

## WordPress Output

The formatter automatically applies the expected shortcode wrapper.

| Content Type | Header | Footer |
|---|---|---|
| Tenders | `[contracts_header]` | `[contracts_footer]` |
| Contract Awards | `[contracts_header]` | `[contracts_footer]` |
| News | `[daily_news_header]` | `[daily_news_footer]` |
| Minutes | `[minutes_header]` | `[minutes_footer]` |

Example Tender/Award structure:

```html
<h6>Contract Tenders: DD/MM/YYYY</h6>
<h6><span style="font-weight: 400;">[contracts_header]</span></h6>

<!-- Generated WordPress content -->

<span style="font-weight: 400;">[contracts_footer]</span>
```

The exact generated body varies according to the selected summary type and source content.

---

## Technology

The project is implemented as a **single-page HTML/CSS/JavaScript application**.

Main browser-side dependencies include:

- PDF.js
- SheetJS / XLSX
- Anthropic API for AI-assisted summary generation

The application currently loads external browser libraries from CDN URLs.

---

## Running Locally

No compilation or build process is required.

### Option A — Open Directly

Clone or download the repository and open:

```text
index.html
```

in a modern browser.

### Option B — Run a Local HTTP Server

Using Python:

```bash
python -m http.server 8000
```

Then open:

```text
http://localhost:8000
```

Using another static hosting server is also fine.

---

## Repository Structure

A minimal repository can be structured as:

```text
.
├── index.html
├── README.md
└── reference/
    ├── WP reference code - Tenders.txt
    ├── WP reference code - Awards.txt
    ├── WP reference code - News.txt
    └── WP reference code - Minutes.txt
```

The reference files are optional at runtime but are useful for documenting the expected WordPress publishing format.

---

## API Configuration

AI-assisted summary generation requires a valid API key configured through the application's API-key interface.

Do **not** commit real API keys to the repository.

### Security Note

The current application is browser-based and makes its AI request from the client. This is suitable for controlled/internal workflows, but a public production deployment should normally move secret API credentials behind a server-side endpoint or proxy instead of exposing credentials to browser code.

---

## Data Handling

The application processes bulletin HTML and uploaded Excel files inside the browser workflow.

Users should review generated content before publishing, particularly:

- organisation names;
- contract titles;
- values;
- winners;
- contract periods;
- locations;
- descriptions; and
- unmatched spreadsheet records.

AI-generated editorial text should also receive a final human review before publication.

---

## Browser Requirements

Use a current desktop browser with JavaScript enabled.

The workflow is primarily designed for desktop use because bulletin source copying, Excel uploads, record review, and drag-and-drop ordering are easier on a larger screen.

---

## Troubleshooting

### "Please paste the full bulletin HTML source first"

Confirm that you copied the **full page source**, not only the visible webpage content:

```text
Ctrl+U → Ctrl+A → Ctrl+C → paste into the tool
```

If you previously processed content and switched between News, Tenders, or Awards, the revised version should preserve the bulletin input rather than incorrectly raising this message.

### No Tenders Found

Check that:

- the full bulletin source was pasted;
- the bulletin contains Housing Tender Alerts; and
- the records satisfy the application's tender filtering rules.

### No Contract Awards Found

Check that:

- the full bulletin HTML source was pasted;
- the bulletin contains the Contracts Awarded section; and
- Housing-sector awards are present.

### Excel Records Do Not Match

Unmatched records can occur when bulletin titles and spreadsheet titles differ.

Review the record manually and complete any missing fields before generating the summary.

### AI Summary Error

Check:

- the API key is configured;
- the browser has internet access; and
- the API request is not being blocked by the browser/network environment.

---

## Publishing Checklist

Before copying content into WordPress:

- Confirm the correct summary mode and date.
- Review all extracted records.
- Remove unwanted records.
- Arrange Tenders/Awards in the required order.
- Check spreadsheet matching.
- Verify values, winners, terms, authorities, and locations.
- Generate the summary.
- Review the editorial wording.
- Confirm the correct WordPress header/footer shortcodes are present.
- Copy the formatted WordPress code into the relevant post.

---

## Maintenance Notes

When changing the application:

- Preserve the ordering of records through parsing, Excel matching, editing, and final generation.
- Keep mode-specific state separate so switching between workflows does not destroy user input.
- Keep WordPress shortcodes mapped to the correct content type.
- Test Tenders, Awards, News, and Minutes after any change to shared UI/state logic.
- Test bulk selection and deletion after changes to review-table rendering.
- Test drag ordering before and after Excel enrichment.

---

## License

Add the repository's required licence information here if the project is distributed outside the internal team.

---

## Project

**Daily Summary Tool**  
**Locarla — Social Housing UK · Industry Insights**
