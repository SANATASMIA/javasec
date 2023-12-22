## How to build a DevSecOps Pipeline in GitHub
This repository shows you how to build up an enterprise-ready DevSecOps Pipeline with GitHub. 

Note: For GitHub Actions to work (OWASP) --> repo "Settings" -> Actions -> General -> Workflow permissions : V Read and write permissions.

Ref: https://docs.github.com/en/actions/using-jobs/assigning-permissions-to-jobs && https://arinco.com.au/blog/changes-to-the-default-github_token-permissions/

## GitHub Actions Used 

| Step                                                    | Github Action                                                                            | Comments | Open Source Alternative                             |
| ------------------------------------------------------- | ---------------------------------------------------------------------------------------- | -------- | --------------------------------------------------- |
| SCA: Software Composition Analysis (Dependency Checker) | [CDRA](https://github.com/redhat-actions/crda)                                           |          | OWASP Dependency Check                              |
| Container Scan                                          | [Trivy](https://github.com/marketplace/actions/aqua-security-trivy)                      |          |                                                     |
| DAST: Dynamic Application Security Testing              | [OWASP ZAP Basline Scan](https://github.com/marketplace/actions/owasp-zap-baseline-scan) |          |                                                     |
| License Checker                                         | [License finder](https://github.com/marketplace/actions/license-finder-scan)             |          |                                                     |


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



