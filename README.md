# Automated Web Security Scanner

**Program:** IBM SkillsBuild Cyber Security 2026 — conducted by BharatCares  
**Project type:** Python-based web security configuration checker  
**Author:** JK

## 1. Project Overview

The Automated Web Security Scanner is an educational command-line tool that reviews selected web security configuration signals for a single URL. It checks whether the final URL uses HTTPS, looks for six common HTTP security headers, and makes a basic observation of Cross-Origin Resource Sharing (CORS) response behavior. Findings include a status, severity, evidence, and remediation guidance. The tool exports results as JSON and CSV files.

This is a lightweight first-pass configuration checker. It is not a comprehensive vulnerability scanner, penetration-testing tool, or proof that a website is secure.

## 2. Objectives

- Automate a small set of repeatable web security configuration checks.
- Observe HTTPS use after HTTP redirects.
- Check for common security headers.
- Make a basic, non-invasive CORS observation.
- Present findings with evidence and practical recommendations.
- Export findings for review and documentation.
- Encourage responsible testing on authorized systems only.

## 3. Features

- URL format validation; only `http://` and `https://` schemes are accepted.
- HTTP request timeout to avoid waiting indefinitely.
- HTTPS observation based on the final response URL.
- Checks for:
  - `Strict-Transport-Security`
  - `Content-Security-Policy`
  - `X-Content-Type-Options`
  - `X-Frame-Options`
  - `Referrer-Policy`
  - `Permissions-Policy`
- Basic CORS response observation using a test `Origin` header.
- Terminal output plus JSON and CSV report generation.
- Evidence and remediation guidance for each finding.

## 4. Technologies Used

- Python 3.10 or newer
- Requests library
- Python standard library: `argparse`, `dataclasses`, `datetime`, `json`, `csv`, `urllib.parse`

## 5. Files

- `JK_AutomatedWebSecurityScanner.py` — command-line implementation
- `JK_AutomatedWebSecurityScanner.ipynb` — Jupyter Notebook version
- `requirements.txt` — Python dependency list
- `JK_AutomatedWebSecurityScanner_ProjectReport.docx` — project report
- `README.md` — this file

## 6. Installation

1. Install Python 3.10 or newer.
2. Download or clone the project repository.
3. Open a terminal in the project directory.
4. (Recommended) Create a virtual environment:

   **Windows**
   ```bash
   py -m venv .venv
   .venv\\Scripts\\activate
   ```

   **macOS/Linux**
   ```bash
   python3 -m venv .venv
   source .venv/bin/activate
   ```

5. Install dependencies:

   ```bash
   python -m pip install -r requirements.txt
   ```

## 7. How to Run

Only scan websites that you own or have explicit permission to assess.

```bash
python JK_AutomatedWebSecurityScanner.py https://your-authorized-test-site.example
```

Optional arguments:

```bash
python JK_AutomatedWebSecurityScanner.py https://your-authorized-test-site.example --timeout 10 --json results.json --csv results.csv
```

The default report files are `scan_report.json` and `scan_report.csv`.

## 8. Understanding Results

- **PASS:** The scanner observed the item. A present header is not automatically proof that its value is correctly configured.
- **WARN / REVIEW:** Review the evidence and decide whether remediation is necessary.
- **INFO / NO ISSUE OBSERVED:** The limited check did not establish a specific issue.
- **ERROR:** A request or check could not be completed.

A missing header is a configuration observation, not by itself proof of exploitability. Recommendations must be reviewed against the target application's design.

## 9. Dataset

No external dataset is required. The application evaluates HTTP responses from a user-supplied, authorized target. If the course specifically requires a dataset URL, confirm with the program coordinator whether a test dataset is expected for this project type.

## 10. Testing

Before submission, run the code in the intended environment and record actual observations in the project report. Use a local test server or a staging website with written authorization. Verify:
1. A valid URL can be processed.
2. An invalid scheme is rejected.
3. Missing headers are reported.
4. JSON and CSV output files are created.
5. An unreachable target produces a clear error.

Do not claim a test passed unless you observed the result.

## 11. Limitations

- Scans one URL per run and does not crawl a website.
- Does not authenticate, test authorization/business logic, exploit vulnerabilities, or inspect source code.
- The CORS check is indicative and does not comprehensively validate CORS security.
- Redirects, proxies, WAFs, network errors, and application behavior can influence results.
- Security-header requirements differ by application; recommendations require human review.

## 12. Future Enhancements

- Add automated unit tests and a local demonstration server.
- Add HTML report generation and a simple dashboard.
- Support configurable header policies.
- Add safe, scope-limited crawling with explicit authorization safeguards.
- Add historical comparison of scan reports.

## 13. References

- OWASP Secure Headers Project: https://owasp.org/www-project-secure-headers/
- OWASP Web Security Testing Guide: https://owasp.org/www-project-web-security-testing-guide/
- MDN Web Docs — Cross-Origin Resource Sharing (CORS): https://developer.mozilla.org/docs/Web/HTTP/CORS
- Requests documentation: https://requests.readthedocs.io/

## Responsible Use

Use this tool only on systems you own or are explicitly authorized to assess. Follow applicable laws, organizational policies, and the program's rules.
