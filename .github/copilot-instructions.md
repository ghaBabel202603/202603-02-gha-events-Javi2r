# Copilot Instructions for ghababel202603-classroom-202603-02-gha-events-github-action-starter-template

This repository is a simple educational **GitHub Actions** starter template used in a classroom exercise. The goal is to make learners comfortable with workflow triggers and validation.

## 🧠 Big Picture

- There is **no application code**; the only artifacts are a `README.md` describing the task and a `test/run.sh` script that verifies the workflow file.
- The main work happens in a YAML workflow under `.github/workflows/02-workflow-events.yaml`.
- Learners must add triggers and a job that prints the event name using `${{ github.event_name }}`.
- The build/test step is the bash script; think of it as the "unit tests" for this repository.

## 📁 Key Files and Directories

- `README.md` – Spanish instructions for the exercise. Contains the required workflow configuration in prose.
- `test/run.sh` – validation script executed by the classroom infrastructure. It errors out if the workflow file is missing or malformed.
- `.github/workflows/` – the directory where the workflow lives. Only `02-workflow-events.yaml` is relevant here.

## 🔧 Developer Workflow

1. **Create or edit** `.github/workflows/02-workflow-events.yaml`.
2. Ensure the file defines a workflow named `02 - Eventos`.
3. Add the following event triggers (all of them are required by the tests):
   - `push`
   - `pull_request`
   - `schedule` (with any valid cron expression)
   - `workflow_dispatch`
4. Add a job called `echo` that runs on `ubuntu-latest` and has one step, `ShowTrigger`:
   ```yaml
   jobs:
     echo:
       runs-on: ubuntu-latest
       steps:
         - name: ShowTrigger
           run: |
             echo "Event name: ${{ github.event_name }}"
   ```
5. Commit and push changes. The workflow should run automatically on push and on PRs.
6. Run `bash test/run.sh` locally to verify the file satisfies all checks.

> ⚠️ The CI used by the classroom will execute `test/run.sh`; don't rely on other tools.

## 🧩 Project-Specific Conventions

- Workflow names and job identifiers are exact strings and must match the tests (`02 - Eventos`, job `echo`).
- The script uses `grep` to confirm triggers; formatting (indentation) isn’t validated, but the keywords must appear literally.
- All instructions in the `README.md` guide the expected outcome—follow them closely.

## 🧾 Examples

The following snippet is a minimal passing workflow that the script accepts:

```yaml
name: 02 - Eventos
on:
  push:
  pull_request:
  schedule:
    - cron: "0 0 * * *"
  workflow_dispatch:

jobs:
  echo:
    runs-on: ubuntu-latest
    steps:
      - name: ShowTrigger
        run: |
          echo "Event name: ${{ github.event_name }}"
```

## ❓ Tips for AI Agents

- Do not propose features outside the scope of the exercise (no extra jobs or steps).
- Keep responses oriented around editing or creating the single workflow file.
- Refer to the `test/run.sh` output when diagnosing failures.
- Remember the repository uses Spanish in the README; adapt suggestions accordingly if you reference user-facing text.

---

Please review the instructions above and let me know if any section needs clarification or if there are missing details you'd like added.