## How to build a DevSecOps Pipeline in GitHub
This repository shows you how to build up an enterprise-ready DevSecOps Pipeline with GitHub. 

Note: For GitHub Actions to work (OWASP) --> repo "Settings" -> Actions -> General -> Workflow permissions : V Read and write permissions.

Ref: https://docs.github.com/en/actions/using-jobs/assigning-permissions-to-jobs && https://arinco.com.au/blog/changes-to-the-default-github_token-permissions/

## GitHub Actions Used 

| Security Type         | Tool Example           | Phase of SDLC    | Why Used Here                         |
| --------------------- | ---------------------- | ---------------- | ------------------------------------- |
| **SAST**              | CodeQL                 | Development (CI) | Catch code issues early               |
| **SCA**               | Dependabot             | Post-merge / CI  | Update unsafe dependencies            |
| **Secrets Detection** | GitHub Secret Scanning | Pre-commit / CI  | Prevent leaking credentials           |
| **Policy/Advisories** | GitHub UI              | Anytime          | For secure communication & disclosure |


### SCA Scan with CRDA:
SCA (Software Composition Analysis): check external dependencies/libraries used by the project have no known vulnerabilities. Third-party dependency scanning with CRDA.

Ref: https://github.com/redhat-actions/crda

### Container Image Scanning with Trivy:
Identify vulnerabilities in built images -> Trivy Image Scanner

Ref: https://github.com/aquasecurity/trivy-action

### DAST Scan with OWASP ZAP Scan 
DAST: Dynamic Application Security Testing

OWASP (Open Web Application Security Project) ZAP (Zed Attack Proxy)

Ref: https://github.com/zaproxy/action-baseline

Ref: https://github.com/zaproxy/action-full-scan

### License Compliance Scan

Ref: https://github.com/jmservera/license-finder-action && https://github.com/pivotal/LicenseFinder

### How to analyze scan reports (json & serif report files)

Ref: 
https://docs.github.com/en/code-security/code-scanning/integrating-with-code-scanning/sarif-support-for-code-scanning

https://www.defectdojo.org

Note: https://github.com/alexgracianoarj/gitlab-pipeline-demo/blob/main/.gitlab-ci.yml -> example python script to upload scan results to defectdojo to analyze scan reports (json & serif report files)

### GH Actions References: 

https://github.com/actions

https://github.com/marketplace?type=actions

Syntax: 

https://docs.github.com/en/actions/using-workflows/workflow-syntax-for-github-actions

### GitHub Advanced Security (GHAS) Implementation - Assignment

** Objective**

Enable GitHub Advanced Security (GHAS) features for a repository to integrate security early into the SDLC.

** Repository Setup**

Create a Repository on GitHub.

Push Application Code:

Create a Personal Access Token (PAT) with required scopes (repo, workflow, security_events).

Use git to push the code:

git remote add origin https://github.com/<username>/<repo>.git
git push -u origin main

**GHAS Features Enabled**

Navigate to your GitHub repository ➝ Go to Security tab ➝ Enable the following:

1. Security Policy

Navigate to Settings ➝ Security ➝ Security Policy

Add a SECURITY.md file describing how to report vulnerabilities.

2. Security Advisory

Enable private advisories to disclose and patch vulnerabilities responsibly.

3. Dependabot Alerts

Enable from Settings ➝ Code Security and Analysis ➝ Dependabot Alerts

Detect known vulnerable dependencies.

4. Code Scanning Alerts

Configure GitHub Actions workflow for static code scanning.

Modify .github/workflows/codeql.yml to include:

name: CodeQL

on:
  push:
    branches: [ "main" ]
  pull_request:
    branches: [ "main" ]
  schedule:
    - cron: '0 0 * * 0'

jobs:
  analyze:
    name: Analyze
    runs-on: ubuntu-latest

    permissions:
      security-events: write
      actions: read
      contents: read

    strategy:
      fail-fast: false
      matrix:
        language: [ 'javascript' ]

    steps:
      - name: Checkout repository
        uses: actions/checkout@v3

      - name: Initialize CodeQL
        uses: github/codeql-action/init@v2
        with:
          languages: ${{ matrix.language }}

      - name: Autobuild
        uses: github/codeql-action/autobuild@v2

      - name: Perform CodeQL Analysis
        uses: github/codeql-action/analyze@v2

5. Secret Scanning Alerts

Enable from Settings ➝ Code Security and Analysis ➝ Secret Scanning

Detect leaked tokens and credentials.

**Running the Scan**

After enabling GHAS features and merging the workflow, GitHub will:

Trigger a CodeQL scan on every push/PR.

Scan for secrets and dependency issues automatically.


