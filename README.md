# MSDO-Netcompany
DESCRIPTION:</b>&emsp;&emsp;&emsp;&emsp;&emsp;&nbsp;This repository centrally <br>manages reusable GitHub Action workflows for secure DevOps pipelines <br>using Microsoft Security DevOps (MSDO), Gitleaks, Trufflehog,<br>
Credscan, and SARIF reporting.

It is designed for organizations with restricted environments.<br>
*******************************************************************************<br>
<br>
<b>FEATURES</b><br>
<br>
- Microsoft Security DevOps (MSDO) scanning  <br>
- Tools like `ESLint`, `Bandit`, `Binskim`, `Checkov`, `Credscan`, `Templateanalyzer`, `Terrascan`, `Trivvy`, etc<br>
- Secret scanning<br>
  - `Credscan` for code-level secrets<br>
  - `Trufflehog` for detecting API keys, passwords, and other sensitive data in source code using entropy and regex-based rules<br>
  - `Gitleaks` for Git history, tokens, config, and sensitive patterns<br>
- Custom SARIF uploader<br>
- Defender for Cloud integration supported<br>
<br>
*******************************************************************************<br>
&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;GETTING STARTED GUIDE<br>
*******************************************************************************
<li><strong>In each repo you want to scan:</strong>
    <ul>
      <li>Create a Workflow Action called <code>msdo-repo-pipeline.yml</code></li>
      <li>Copy and paste the <code>msdo-repo-pipeline.yml</code> into your newly created workflow</li>
      <li>This should trigger and run - review pipeline to confirm that it runs and completes</li>
    </ul>
---<br>
<br>
<b>INCLUDED WORKFLOWS:</b><br>
<table border="1" cellpadding="5">
  <tr><th>Workflow Name</th><th>Purpose</th></tr>
  <tr><td><code>msdo-main-pipeline.yml</code></td><td>Orchestrates all security scans + uploads</td></tr>
  <tr><td><code>msdo-dynamic-scanning.yml</code></td><td>Performs MSDO scans on infra/code/containers. Currently added to msdo-main-pipeline but commented out</td></tr>
  <tr><td><code>msdo-credscan.yml</code></td><td>Runs <code>credscan</code> with <code>.gdnsettings</code> config for secret detection</td></tr>
  <tr><td><code>msdo-trufflehog.yml</code></td><td>Runs <code>Trufflehog</code> to detect passwords and secrets using entropy and regex-based rules</td></tr>
  <tr><td><code>msdo-gitleaks.yml</code></td><td>Git-aware secret scanning using Gitleaks</td></tr>
  <tr><td><code>upload-sarif action</code></td><td>Composite action to upload SARIF locally. This is mainly for uploading to GitHub Security and is commented out, but SARIF is present where it's needed to upload to Azure </td></tr>
  <tr><td><code>gitleaks.toml</code></td><td>Custom rule config for Gitleaks</td></tr>
  <tr><td><code>msdo-repo-pipeline.yml</code></td><td>To be added into each Repo you want to scan as a Workflow Action</td></tr>
</table>
---<br>
<br>
<b>HOW TO RUN:</b><br>
<br>
- Triggers automatically on push/commit to <code>develop</code> within the Repo<br>
- Or run manually via <strong>Actions</strong> tab → Select workflow → Click <strong>Run workflow</strong><br>
<br>
---<br>
<br>
<b>SYSTEM REQUIREMENTS:</b><br>
<br>
- Runner: <code>ubuntu-latest</code><br>
- .NET 6 SDK is installed via script in workflow<br>
- <code>gh</code> CLI is available by default on GitHub-hosted runners<br>
- Gitleaks downloaded and run as part of pipeline<br>
<br>
---<br>
<br>
<b>OUTPUT:</b><br>
<br>
- Results are uploaded to <strong>GitHub Code Scanning Alerts</strong>. This has been commented out, but can be re-enabled if needed.<br>
- Results are ingested into <strong>Microsoft Defender for Cloud's DevOps Security</strong><br>
<br>
