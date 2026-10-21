# Web Auditor & PDF Scorecard Generator

An automated Python tool designed to evaluate websites for architectural performance, modern web standards compliance, and legacy technical debt. It audits a batch of URLs from a text file, conducts multi-factor technical analysis on each target, and compiles the findings into an executive-ready PDF scorecard complete with performance grades and compliance scoring.

---

## Features

- **Batch Website Auditing**: Sequentially evaluates multiple domains from a plain text file list.
- **Performance Benchmarking**: Captures initial response latency (Time to First Byte / server load time) and assigns normalized letter grades (A–D).
- **Technology Stack Fingerprinting**: Inspects HTTP response headers and DOM metadata to detect web servers, backend frameworks, CMS platforms, and site generators.
- **Legacy Debt & Constraint Detection**: Flags critical architectural and modernization shortcomings, including:
  - Missing HTTPS / SSL encryption
  - Missing or misconfigured mobile viewport meta tags
  - Missing accessibility tags (`alt` attributes on images)
  - Deprecated or obsolete HTML tags (`<font>`, `<center>`, `<marquee>`, etc.)
- **Normalized Functionality Scoring**: Computes an objective 0–100% health score via weighted deductions across security, responsiveness, accessibility, and markup hygiene.
- **Executive PDF Scorecard**: Generates a clean, publication-ready PDF report containing an aggregated summary overview alongside individual site diagnostics.

---

## Prerequisites & Dependencies

### System Requirements

- **Python 3.8+**
- Standard Python package manager (`pip`)

### Required Python Packages

Deploying and running the auditor requires three core external dependencies:

1. **BeautifulSoup 4** (`beautifulsoup4`)
   - **Purpose**: Parses the HTML DOM tree, scans for missing accessibility attributes (`alt` tags on `<img>`), detects mobile viewport `<meta>` declarations, and flags obsolete/deprecated HTML markup (`<font>`, `<center>`, `<marquee>`).
2. **Requests** (`requests`)
   - **Purpose**: Handles outbound HTTP/HTTPS queries, follows redirects, measures initial response latency (TTFB / load time), and inspects response headers (e.g., `Server`, `X-Powered-By`) for technology stack detection.
3. **ReportLab** (`reportlab`)
   - **Purpose**: Generates the multi-page, publication-quality PDF scorecard, laying out the executive summary matrix, grade charts, and domain-by-domain diagnostic breakdowns.

---

## Installation & Deployment

### Option A: Direct Installation via pip

Install all required dependencies directly with:

```bash
pip install beautifulsoup4 requests reportlab
```

### Option B: Deploying with `requirements.txt`

If you are deploying this tool in a virtual environment or CI/CD container, create a `requirements.txt` file:

```text
beautifulsoup4>=4.12.0
requests>=2.28.0
reportlab>=3.6.0
```

Then install dependencies with:

```bash
pip install -r requirements.txt
```

---

## Project Structure

```text
.
├── web_auditor.py         # Main audit engine and PDF report generator
├── urls.txt               # Input list of target website URLs
├── requirements.txt       # Python package dependencies
├── web_audit_report.pdf   # Generated PDF scorecard (output)
└── README.md              # Project documentation
```

---

## Usage

### 1. Prepare Target URLs

Create a `urls.txt` file in the project root directory. List one fully qualified URL per line:

```text
https://example.com
https://google.com
http://insecure-example.org
```

### 2. Execute the Audit

Run `web_auditor.py` from your terminal, passing the input text file and desired output PDF filename as arguments:

```bash
python web_auditor.py urls.txt web_audit_report.pdf
```

Upon completion, the script will output execution logs to the terminal and generate `web_audit_report.pdf`.

---

## Scoring Methodology

### 1. Speed Grade (Latency Benchmarking)

Response speed evaluates initial server response time against standard industry thresholds:

| Grade | Response Time Range | Assessment |
| :---: | :--- | :--- |
| **A** | `< 0.50s` | Excellent: Highly responsive infrastructure |
| **B** | `0.50s – 1.00s` | Good: Acceptable latency for standard web applications |
| **C** | `1.00s – 1.50s` | Fair: Noticeable delay; optimization recommended |
| **D** | `> 1.50s` | Poor: Critical server or network latency |

### 2. Functionality Score (0–100%)

The functionality score starts at a baseline of **100%** and applies weighted deductions based on structural and standard compliance findings:

| Category | Finding / Violation | Impact |
| :--- | :--- | :---: |
| **Security** | Missing HTTPS protocol (unencrypted HTTP) | Major deduction |
| **Responsiveness** | Missing mobile `<meta name="viewport">` tag | Significant deduction |
| **Accessibility** | Images missing descriptive `alt` attributes | Moderate deduction |
| **Code Hygiene** | Deprecated HTML markup (`<center>`, `<font>`, `<marquee>`) | Minor deduction per instance |

---

## Generated PDF Report Overview

The generated PDF report contains two primary sections:

1. **Executive Summary Matrix**: A high-level overview table listing each audited domain, its speed grade, functionality percentage score, and primary detected technologies.
2. **Detailed Domain Diagnostics**: Breakdown per site highlighting specific issues detected, header security posture, response metrics, and remediation priorities.

---

## Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/new-audit-metric`)
3. Commit your changes (`git commit -m "Add new audit metric"`)
4. Push to the branch (`git push origin feature/new-audit-metric`)
5. Open a Pull Request

---

## License

This project is licensed under the MIT License — see the [LICENSE](https://www.google.com/search?q=LICENSE) file for details.
