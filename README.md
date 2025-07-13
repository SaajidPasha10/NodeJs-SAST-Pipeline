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

<img width="749" height="347" alt="image" src="https://github.com/user-attachments/assets/b0cd6542-41e6-4522-950d-18ee8bbfdcdd" />

Summary of Key Findings

## 📊 SAST Scan Summary (GitLab Semgrep)

| File     | Line | Issue                                                                 | Severity | Rule / ID                         | CWE   | OWASP Reference         |
|----------|------|------------------------------------------------------------------------|----------|------------------------------------|--------|--------------------------|
| app.js   | 18   | Improper neutralization of directives in dynamically evaluated code (`eval` injection) | High     | eslint.detect-eval-with-expression | CWE-95 | A03:2021 – Injection     |

### 🔎 Description (Eval Injection)

The application uses the `eval()` function (or similar dynamic code execution like `Function()`, `setTimeout()`, `setInterval()`) which can execute user-controlled input.  
This is extremely dangerous and can lead to:
- Full system compromise (Node.js)
- Cross-site Scripting (Web apps)

> 📖 [Read more about why `eval()` is dangerous](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/eval#never_use_eval!)

### 💡 Recommendation

Avoid using `eval()`. Use **property accessors** or structured logic instead.  
Example fix:

```javascript
const obj = { key1: 'value1', key2: 'value2' };
const key = getUserInput();
const value = obj.hasOwnProperty(key) ? obj[key] : '';

