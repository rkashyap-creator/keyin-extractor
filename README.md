# KeyIn Extractor 2.0

Turn Excel reports, Jira exports, and pasted text into a clean list of Jira issue keys, a ready-to-use JQL query, and clickable ticket links.

## Why use this tool?

When working with large Excel sheets or exported issue reports, collecting ticket IDs manually can take time and introduce mistakes. KeyIn Extractor finds matching issue keys for you and removes duplicates, helping you prepare a Jira search in a few clicks.

- **Save time on Excel reports:** Read issue keys from cells across all worksheets without copying each ticket individually.
- **Extract keys from Excel hyperlinks:** Scan stored hyperlink targets and formula text, even when a cell displays a friendly label instead of the full ticket URL.
- **Work with Jira exports:** Download an issue report in CSV or a supported Excel format, load it into the extractor, and generate a query for the tickets found.
- **Reuse information from other sources:** Paste text copied from documents, messages, ticket lists, or console logs. You can also upload a plain text file containing the details.
- **Remove duplicate issue keys:** Repeated references appear only once in the generated query and ticket link list.
- **Build a Jira search instantly:** Copy the generated `key IN (...)` query or the combined Jira search link.
- **Open individual tickets:** Get a clickable link for every extracted key.
- **Run in your browser:** Download the HTML file and open it in a browser; no application installation or Jira API token is required.

## How to use

1. Download `KeyIn Extractor 2.0.html` and open it in your browser.
2. Export your Jira details or prepare a file in one of the supported formats: `.xlsx`, `.xls`, `.csv`, or `.txt`.
3. Click the upload area and select your file. Alternatively, paste your text directly into the input box.
4. Wait until the file contents appear in the input box, then click **Extract Keys & Build Links**.
5. Copy the generated **Key IN JQL**, copy the **Key IN Link**, or open an individual ticket link.

## Example

Input:

```text
Review GAME-102, GAME-205, and GAME-102 again.
Follow up on QA-18.
```

Generated JQL:

```jql
key IN (GAME-102, GAME-205, QA-18)
```

This is useful for regression planning, bug triage, test reports, handovers, and gathering tickets from several references into one Jira search.

## Supported files and current behavior

| Input | What the tool reads |
| --- | --- |
| Excel `.xlsx` and `.xls` | Cell values, stored hyperlink targets, and formula text across all worksheets |
| CSV `.csv` | Text containing issue keys |
| Text `.txt` | Text containing issue keys |
| Pasted content | Text copied from documents, messages, reports, or logs |

Word documents, PDFs, images, and scanned documents are not read directly. Copy their text into the input box or export it to a supported format first.

The current matching pattern finds uppercase letters followed by a hyphen and digits, such as `GAME-102`. It does not verify whether those tickets exist or whether you have permission to view them.

The supplied version generates links for `https://novaquark.atlassian.net`. To use another Jira instance, update both the `DOMAIN` constant and the displayed Target Jira Domain value in the HTML source. Jira access permissions still apply when opening links.

File contents are read and processed in the browser; the supplied code does not upload them to an application server. Excel reading uses the SheetJS library loaded from a public CDN, so internet access is needed to load that dependency. The current version uses the file picker; the upload area's drag-and-drop wording does not have a corresponding drop handler.
