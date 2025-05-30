# MITRE-Cyber-Security-CVE-Database

The **MITRE-Cyber-Security-CVE-Database** is a cybersecurity initiative by Enterprises, dedicated to providing a comprehensive, open-source platform for managing and tracking Common Vulnerabilities and Exposures (CVEs). This repository, `mitre-cve-database`, aggregates CVE data from multiple authoritative sources to support cybersecurity professionals, researchers, and organizations.

*An Enterprises Initiative • Established 2025*

---

## Overview

The `mitre-cve-database` repository consolidates CVE data from various trusted sources, including MITRE, the National Vulnerability Database (NVD), CISA’s Known Exploited Vulnerabilities (KEV) catalog, CVEDetails, and Tenable. Our goal is to provide a centralized, accessible platform for vulnerability management and foster community collaboration.

### Key Features

- **Multi-Source CVE Data**: Aggregates CVE records from MITRE, NVD, CISA, CVEDetails, and Tenable.
- **Community-Driven**: Open for contributions of tools, scripts, and documentation to enhance usability.
- **Automated Updates**: Includes a script to keep CVE data in sync with the latest from all sources.

### Data Sources

- **MITRE CVE Database**:

  - Source: https://cve.mitre.org (mirrored via https://github.com/CVEProject/cvelistV5)
  - Total Records: Over 275,000 CVE entries (as of June 2024)
  - Directory: `cve-data/mitre/`

- **National Vulnerability Database (NVD)**:

  - Source: https://nvd.nist.gov
  - Description: Enriched CVE data with CVSS scores and CPE applicability
  - Directory: `cve-data/nvd/`

- **CISA Known Exploited Vulnerabilities (KEV) Catalog**:

  - Source: https://www.cisa.gov/known-exploited-vulnerabilities-catalog
  - Description: A subset of CVEs known to be exploited in the wild
  - Directory: `cve-data/cisa-kev/`

- **CVEDetails**:

  - Source: https://www.cvedetails.com
  - Description: Recent CVEs with additional details like exploits and trends
  - Directory: `cve-data/cvedetails/`

- **Tenable CVE List**:

  - Source: https://www.tenable.com/cve
  - Description: A sample of recent CVEs (full list requires API access)
  - Directory: `cve-data/tenable/`

---

## Governance

The MITRE-Cyber-Security-CVE-Database initiative is governed by Enterprises, with a commitment to transparency, collaboration, and adherence to industry standards. We operate under the following principles:

- **Data Integrity**: CVE data is mirrored without modification, in compliance with each source’s terms of use.
- **Open Access**: All data and tools in this repository are publicly accessible under open-source licenses.
- **Community Engagement**: We encourage contributions and discussions to improve the platform.

For more details, see our Governance Policy (coming soon).

---

## Getting Started

Follow these steps to set up and use the CVE data in this repository:

### 1. Clone the Repository

Clone this repository to your local machine to access the CVE data:

```bash
git clone https://github.com/MITRE-Cyber-Security-CVE-Database/mitre-cve-database.git
cd mitre-cve-database
```

### 2. Fetch CVE Data

Use the provided script to fetch or update CVE data from all sources:

```bash
chmod +x fetch-cve-data.sh
./fetch-cve-data.sh
```

### 3. Explore the Data

The CVE data is stored in the `cve-data` directory, organized by source. For example:

- `cve-data/mitre/2024/CVE-2024-12345.json` (MITRE CVE data)
- `cve-data/nvd/nvdcve-2025.json` (NVD CVE data for 2025)

---

## Usage Examples

Here are some practical ways to use the CVE data in this repository:

### Search for a Specific CVE in MITRE Data

Use `grep` to find a specific CVE by ID in the MITRE data:

```bash
grep -r "CVE-2024-12345" cve-data/mitre/
```

### Parse NVD CVE Data with Python

Use Python to parse and analyze NVD CVE JSON files:

```python
import json

# Load NVD CVE data for 2025
with open("cve-data/nvd/nvdcve-2025.json", "r") as f:
    nvd_data = json.load(f)

# Example: Print CVE IDs and CVSS scores
for item in nvd_data["CVE_Items"][:5]:  # Limit to first 5 for demonstration
    cve_id = item["cve"]["CVE_data_meta"]["ID"]
    cvss_score = item.get("impact", {}).get("baseMetricV3", {}).get("cvssV3", {}).get("baseScore", "N/A")
    print(f"CVE ID: {cve_id}, CVSS Score: {cvss_score}")
```

### Automate Updates with GitHub Actions

Set up a GitHub Action to run the `fetch-cve-data.sh` script daily:

```yaml
name: Fetch CVE Data
on:
  schedule:
    - cron: '0 0 * * *'  # Runs daily at midnight UTC
  workflow_dispatch:     # Allows you to run this workflow manually from the Actions tab
jobs:
  fetch-cve-data:
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@v3
    - name: Install Dependencies
      run: sudo apt-get update && sudo apt-get install -y jq
    - name: Run Fetch Script
      run: |
        git config --local user.email "action@github.com"
        git config --local user.name "GitHub Action"
        chmod +x fetch-cve-data.sh
        ./fetch-cve-data.sh
    - name: Commit Changes
      run: |
        git commit -a -m "Automated CVE data fetch" || echo "No changes to commit"
        git push
```

---

## Repository Structure

- **cve-data/**: Contains CVE data from multiple sources, organized by provider.
  - `mitre/`: MITRE CVE data from `CVEProject/cvelistV5`.
  - `nvd/`: NVD CVE data in JSON format.
  - `cisa-kev/`: CISA KEV catalog in JSON format.
  - `cvedetails/`: Recent CVEs from CVEDetails in JSON format.
  - `tenable/`: Sample of recent CVEs from Tenable in text format.
- **/*.sh**: Utility scripts, including `fetch-cve-data.sh` for syncing CVE data.
- **docs/**: Documentation for using and contributing to this repository (coming soon).

### Related Repositories

- **mitre-cve-database** (Current Repository)\
  Core repository for CVE data.\
  Explore the database
- **cve-services**\
  APIs and tools for interacting with the CVE database.\
  *Coming soon!*
- **cve-discussions**\
  A space for community discussions on vulnerabilities.\
  *Coming soon!*

---

## Enterprise Features

- **SAML Single Sign-On**\
  Secure access for enterprise teams (coming soon).
- **Automated Dependency Updates**\
  Keep your codebase secure with automatic updates (coming soon).

---

## Contributing

We welcome contributions to enhance this repository! While the CVE data itself must remain unchanged (per the sources’ terms), you can contribute by:

- Developing tools or scripts to analyze CVE data.
- Improving documentation or adding usage tutorials.
- Submitting pull requests with your enhancements.

Please review our Contributing Guidelines (coming soon) before submitting contributions.

---

## License and Attribution

The CVE data in this repository is provided under the terms of use of each respective source:

- MITRE CVE data: https://cve.mitre.org/about/termsofuse.html
- NVD data: Public domain (U.S. government data)
- CISA KEV data: Public domain (U.S. government data)
- CVEDetails and Tenable data: Used under fair use for non-commercial purposes; refer to their respective terms.

Any additional scripts, documentation, or tools added to this repository are licensed under the MIT License. See the LICENSE file for details.

---

*© 2025 MITRE-Cyber-Security-CVE-Database, Enterprises. All rights reserved.*
