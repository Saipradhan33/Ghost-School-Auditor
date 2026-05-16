Project: RPA Workflow

Overview
- UiPath process that extracts names from a PDF and flags potential fraud by comparing to a whitelist.

Prerequisites (local run)
- Install UiPath Studio (Community or Enterprise) matching project Studio version 26.x.
- Place your Google connection JSON files under `resources/solution_folder/connection/`.
- Restore packages via UiPath Studio (Open Project → Manage Packages).

Quick run (local)
1. Open UiPath Studio and open the folder `RPA Workflow`.
2. Confirm `Main.xaml` is the project `Main` and `project.json` lists required packages.
3. If using Google Drive/Gmail connections, ensure `resources/solution_folder/connection/*.json` contains your credentials.
4. Run `Main.xaml` from Studio or publish to Orchestrator and run via Robot.

Testing guidance
- Positive test: the workspace already contains sample names in `RPA Workflow/data/census_names.csv`.
- Negative test: use the mock sample `RPA Workflow/mocks/extracted_negative.txt` and set the `extractedText` variable in `Main.xaml` to the file contents via the Variables panel for manual testing.

Adding to GitHub
- Initialize repo at workspace root and push:

```bash
# Clone and navigate
git clone <repo-url>
cd "Solution 1.uis"

# Open in UiPath Studio
# File → Open Project → select "RPA Workflow" folder
```

### 2. Configure Credentials
1. Open Google Cloud Console and generate OAuth2 credentials
2. Save JSON files to:
   - `resources/solution_folder/connection/uipath-google-gmail/revasahu2006@gmail.com.json`
   - `resources/solution_folder/connection/uipath-google-drive/revasahu2006@gmail.com_1.json`

### 3. Restore Packages
In UiPath Studio:
- Project → Manage Packages → Restore

### 4. Run
- Open `RPA Workflow/Main.xaml`
- Click **Run** (F5) or publish to Orchestrator

---

## Testing

### Manual Testing (Local)
See [RPA Workflow/tests/TESTS.md](RPA%20Workflow/tests/TESTS.md) for step-by-step test cases:
- **Positive:** Report with all valid names → no fraud flag
- **Negative:** Report with >30% unknown names → fraud flag raised

### Mock Data
Test cases include:
- `mocks/extracted_positive.txt` – All names match census
- `mocks/extracted_negative.txt` – No names in census (fraud scenario)

---

## Fraud Detection Logic

### Threshold: 30% Unknown Names
```
Fraud Score = (Unknown Names + Duplicates) / Total Names × 100

If Fraud Score > 30%
  → Flag Report
  → Move to FraudReports folder
  → Send Alert Email
  → Log to Audit Trail
```

### Example
```
Total Names Extracted: 100
Names in Census: 70
Unknown Names: 30
Duplicate Count: 0

Fraud Score = (30 + 0) / 100 × 100 = 30%
Status: ⚠️ BORDERLINE (at threshold)
```

---

## Configuration

### Adjust Fraud Threshold
Edit `Main.xaml`, find the condition:
```
If Condition="[fraudCount > (cleanNames.Count * 30 / 100)]"
```
Change `30` to your desired percentage (e.g., `25` for stricter detection).

### Update Census Data
Replace `RPA Workflow/data/census_names.csv` with your official district student list (one name per line, lowercase).

### Modify Alert Recipients
In `Main.xaml`, find `SendEmailConnections` and update:
```
To="[New String(){"auditor.general@education.gov.xx"}]"
```

---

## Deployment

### To UiPath Orchestrator
1. In Studio: Publish Project
2. Select Orchestrator URL and credentials
3. Deploy to a Robot with Google API access
4. Configure schedule (e.g., daily email check)

### To UiPath Cloud (Automation Cloud)
1. Log into Automation Cloud
2. Upload project via Studio (Publish)
3. Create process and set trigger (e.g., email arrival)
4. Assign to available robot

---

## Security & Compliance

⚠️ **Do NOT commit credentials** – `.gitignore` excludes connection JSONs  
✅ Use UiPath Orchestrator Vault or Azure Key Vault for secrets  
✅ Audit logs stored locally (recommend archival to secure storage)  
✅ Email alerts contain only summary metrics, not raw data  

---

## Troubleshooting

| Issue | Solution |
|-------|----------|
| "Connection Failed" | Verify Google API credentials in `resources/solution_folder/connection/` |
| "PDF not extracting text" | Ensure PDF is NOT scanned-image; OCR may be needed |
| "No emails detected" | Check Gmail inbox filter settings; ensure bot has inbox access |
| "False positives in fraud detection" | Verify `census_names.csv` is up-to-date and matches report name format |

---

## Future Enhancements

- [ ] Machine-learning model to detect fabricated attendance patterns
- [ ] Real-time dashboard for fraud metrics & trends
- [ ] Integration with education ministry database (direct census sync)
- [ ] Multi-language OCR support
- [ ] SMS alerts to Auditor General for critical flags

---

## Support & Contact

For issues, feature requests, or integration help, open an issue on GitHub or contact: **education-audit-support@example.gov**

---

## License

This project is the property of the Education Ministry Audit Division. Use, modification, and distribution are governed by ministry policy and applicable anti-corruption regulations.
