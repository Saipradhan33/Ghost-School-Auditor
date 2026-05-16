Manual test checklist

1) Positive case
- Open `RPA Workflow/Main.xaml` in UiPath Studio.
- Open Variables panel and set `extractedText` default value to the contents of `mocks/extracted_positive.txt` (copy-paste).
- Run the workflow — it should detect known names and not flag excessive fraud.

2) Negative case
- Set `extractedText` default value to the contents of `mocks/extracted_negative.txt`.
- Run the workflow — it should NOT flag fraud for lack of names.

3) Integration with Google Drive
- Place a PDF in Google Drive and ensure `Get File or Folder` points to it.
- Run end-to-end and confirm the file downloads (or implement download step) before `Extract PDF Text`.

Notes
- For automated CI, UiPath licensed runners or orchestrator integration are required; Tests here are for manual verification in Studio.
