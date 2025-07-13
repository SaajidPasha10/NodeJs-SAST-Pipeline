## ⚙️ How to Register a Custom GitLab Runner

This guide explains how to register your own **self-hosted GitLab Runner** to use in CI/CD pipelines.

### 📦 Prerequisites

- GitLab account and a project
- A machine with GitLab Runner installed (Windows/Linux/Mac)
- Admin or runner registration access to the project or group

---

### 🧩 Step 1: Install GitLab Runner

#### On Windows:

Download and install GitLab Runner from:

🔗 [https://docs.gitlab.com/runner/install/windows.html](https://docs.gitlab.com/runner/install/windows.html)

#### On Linux (Debian/Ubuntu):

```bash
sudo apt-get update
sudo apt-get install -y gitlab-runner
```

### 🔑 Step 2: Get the Registration Token
Go to your GitLab project
 
Navigate to: Settings > CI/CD > Runners > Set up a specific Runner manually
<img width="488" height="229" alt="image" src="https://github.com/user-attachments/assets/0b0f771f-0546-423a-ac75-84624742a7c9" />


Copy the Registration Token

###  🛠️ Step 3: Register the Runner
Run the following command in terminal or CMD (adjust based on OS):

gitlab-runner register

You will be asked to enter following
| Prompt              | Your Input                                                 |
| ------------------- | ---------------------------------------------------------- |
| GitLab instance URL | `https://gitlab.com` (or self-hosted instance)             |
| Registration token  | Paste your project/group token                             |
| Description         | Any name, e.g., `My Windows Runner`                        |
| Tags                | `My-HP-Windows-Runner` (use this in your `.gitlab-ci.yml`) |
| Executor            | `shell`, `docker`, or `powershell` (for Windows shell)     |

✅ Step 4: Use Runner Tags in .gitlab-ci.yml
Example:
```
install-job:
  stage: install
  tags:
    - My-HP-Windows-Runner
  script:
    - npm install

