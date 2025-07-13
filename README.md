# NodeJs-SAST-Pipeline
# 🔐 Static Application Security Testing (SAST) Report

## 📌 What is SAST?

**SAST (Static Application Security Testing)** is a method of analyzing source code for security vulnerabilities **without executing the application**. It helps developers catch common issues such as:

- Code injection
- Use of unsafe functions (`eval`, `exec`, etc.)
- Insecure data handling
- Credential exposure in code

---

## 🛠️ Tool Used

This project uses **GitLab's built-in SAST scanner** through the GitLab CI/CD pipeline.

- Template included: `Security/SAST.gitlab-ci.yml`
- SAST is automatically triggered during the pipeline's `test` stage.
- The tool outputs a `gl-sast-report.json` file containing structured results.

---

## 🚀 How It Works

### Pipeline Configuration

```yaml
include:
  - template: Security/SAST.gitlab-ci.yml

stages:
  - install-stage
  - test
  - run-stage
```
GitLab automatically detects your language (Node.js in this case).

It runs static analyzers like:

Semgrep
ESLint security rules
Vulnerability results are stored in the pipeline job artifacts as gl-sast-report.json.
