# Assignment 6 — Building an AI-Assisted Git Safety Net (PR Ready Check)

Part of the DevOps Micro Internship (DMI) with Agentic AI

---

## Purpose

In Week 2 you built Claude Code hooks that block a dangerous action *before* it happens (`PreToolUse`), and a restricted skill that could look but not touch (`allowed-tools` without `Write`). In this assignment you will discover that Git has the exact same idea, decades older: a **pre-commit hook** that blocks a commit before it's created.

You will build both halves of a real "PR Ready" workflow:

1. A **Git hook that follows fixed rules** — scans staged changes for hardcoded secrets and oversized files and refuses the commit. No AI involved, no guessing, just a rule that gives the same answer every time.
2. A **restricted Claude Code skill** (`/pr-ready`) that reads your staged diff and drafts a Pull Request title, description, and a short list of things worth a second look — the kind of judgment a fixed rule can't make (mixed changes, missing context, unclear intent). The skill never commits, pushes, or opens the PR. You do that yourself, using its draft as a starting point.

This mirrors the Agentic Loop from Week 3's Linux triage assignment: **Gather → Analyze → Human Act → Verify**. The hook and the skill both gather and analyze; only you act.

---

# Task 0 — Confirm Your Fork and Create a Feature Branch

## Goal

Confirm you are working in your own fork, then create a dedicated branch for this assignment.

### Evidence

#### Screenshot 1 — Output of git remote -v and git branch showing the new branch

<img width="953" height="215" alt="image" src="https://github.com/user-attachments/assets/d705005a-4588-4a06-9942-7327a4b73ec9" />

---

### Notes

**1. Why create a dedicated branch instead of doing this work on main?**

A separate branch keeps my assignment changes away from the main branch. It also makes the work easier to review and safer to test.
---

# Task 1 — Stage a Change With Realistic Risk

## Goal

On your own fork of this repository (the one you've been submitting your DMI work in since onboarding), create a new branch and stage a change that a real reviewer should catch: a hardcoded-looking secret and a leftover debug statement.

### Evidence

#### Screenshot 1 — Output of  `git status` showing the staged file on feature/ai-pr-ready

<img width="642" height="175" alt="image" src="https://github.com/user-attachments/assets/2da58807-86bb-4498-9898-328b1538a4e5" />

---

### Notes

**1. Why does this assignment use an obviously fake key instead of a real one?**

A fake key lets me test the security checks without exposing real credentials. Using a real key could put an account or system at risk.
---

# Task 2 — Write a Real Git Pre-Commit Hook

## Goal

Create a tracked, shareable pre-commit hook that blocks a commit containing secret-like patterns or files over 1MB.

### Evidence

#### Screenshot 2 — `hooks/pre-commit` open in VS Code showing the full script

<img width="1695" height="1078" alt="image" src="https://github.com/user-attachments/assets/b46f024f-09c1-42fe-872e-d6f3a0b44eb6" />


---

#### Screenshot 3 — Output of `git config core.hooksPath` confirming it points to `hooks`

<img width="822" height="85" alt="image" src="https://github.com/user-attachments/assets/1b4200bb-b0a5-453a-b9dd-784687a3b43e" />


---

### Notes

**1. Why is `hooks/pre-commit` tracked in the repo instead of living only in `.git/hooks/`?**

Tracking the hook makes it part of the repository, so it can be shared with other developers. A hook stored only in .git/hooks/ is local and is not committed with the project.
---

**2. Compare this to `PreToolUse` from Week 2 Assignment 6. What does each one intercept, and what do they have in common?**

The Git pre-commit hook checks staged files before a commit is created. PreToolUse intercepts a tool action before it runs. Both act as safety gates that can stop a risky action before it happens.
---

# Task 3 — Prove the Hook Blocks the Risky Commit

## Goal

Attempt to commit the staged file from Task 1 and show the hook rejecting it.

### Evidence

#### Screenshot 4 — Terminal showing `git commit` rejected with the hook's "BLOCKED" message naming the exact file

<img width="1062" height="145" alt="Screenshot 2026-10-17 182152" src="https://github.com/user-attachments/assets/c43110dc-fc6b-4ce3-b4b2-ffd34ffd4ffc" />

---

### Notes

**1. Which line in `hooks/pre-commit` matched your fake key, and why did it match?**

The line using grep -Eni 'AKIA[0-9A-Z]{12,}|API_KEY[[:space:]]*=' matched the fake key because it contained an AWS-style AKIA prefix and an API_KEY assignment.
---

**2. Could this hook have caught a poorly-named variable that stores a secret without the `AKIA` prefix? What does that tell you about the limits of a fixed rule like this?**

Not necessarily. The hook only checks for patterns it knows about, so a secret written in a different format could slip through. Fixed rules are useful, but they cannot detect every possible secret.
---

# Task 4 — Build the `/pr-ready` Skill

## Goal

Create a manually invoked Claude Code skill that reads your staged changes and produces a PR-readiness report and a draft PR description — without writing, committing, or pushing anything itself.

### Evidence

#### Screenshot 5 — `SKILL.md` frontmatter showing `allowed-tools: Bash, Read, Grep` (no `Write`) and `disable-model-invocation: true`

<img width="1121" height="526" alt="image" src="https://github.com/user-attachments/assets/7218ddd4-1124-4b2a-bcfa-759c6be3d4ff" />

---

#### Screenshot 6 — `/pr-ready` output while the risky file is still staged, showing it flagged the secret and/or debug statement

<img width="1203" height="277" alt="image" src="https://github.com/user-attachments/assets/9117d906-10af-48f4-b11b-dfb4aef699b3" />

---

### Notes

**1. Why does `/pr-ready` have `Bash` and `Read` but not `Write`?**

Bash and Read let the skill inspect the staged changes and relevant files. Without Write, it is restricted from editing files, helping keep the review separate from the actual changes.
---

**2. The pre-commit hook and `/pr-ready` both looked at the same staged diff. Did they flag the same things? What did one catch that the other didn't?**

The hook blocks known secret-like patterns and files larger than 1 MB. The AI review can also identify issues such as leftover debug statements or code that doesn't provide meaningful tests. In my work, the hook blocked the fake secret, while GitHub Copilot flagged both the secret-like value and debug statement. I used Copilot for review rather than running the /pr-ready skill itself.
---

# Task 5 — Fix the Issues and Re-Verify

## Goal

Remove the secret and debug statement, then prove both gates now pass clean.

### Evidence

#### Screenshot 7 — `git commit` succeeding after the fix (no BLOCKED message)

<img width="1067" height="170" alt="image" src="https://github.com/user-attachments/assets/ebdf9c8e-b180-4811-a5bc-de8a069605de" />

---

#### Screenshot 8 — Second `/pr-ready` run showing a clean risk report and a drafted PR title + description

<img width="1213" height="462" alt="image" src="https://github.com/user-attachments/assets/3de405d0-edb8-48a7-a9fb-fbe6fc8c2d58" />

---

### Notes

**1. What exactly did you change to satisfy the pre-commit hook?**

I removed the fake API key and debug statement from test/app.py and replaced them with a harmless print statement. The pre-commit hook then passed, and the commit succeeded.
---

# Task 6 — Push and Open a Pull Request Using the AI Draft

## Goal

Push your branch and open a real Pull Request, using `/pr-ready`'s drafted title and description as your starting point — read it critically and edit before you use it.

**Important:** Open this Pull Request with base repository set to **your own fork** — not the shared upstream `pravinmishraaws/devops-micro-internship-pravinmishra` repository. This assignment's hook and skill files are your own practice work, not a change meant for the shared class repo.

### Evidence

#### Screenshot 9 — Your Pull Request showing the base repository is your own fork, plus the title and description, with the `/pr-ready` draft visible for comparison (paste it in the PR conversation or your notes below)

<img width="1915" height="1027" alt="image" src="https://github.com/user-attachments/assets/e758e29b-eaae-443b-86a1-bd4fce4d0003" />

---

#### PR Link

https://github.com/mr-zack01/devops-micro-internship-interviews/pull/1
---

### Notes

**1. What, if anything, did you edit in the AI's drafted PR description before using it? Why?**

I used the review findings to write a description that explains the hook, the skill instructions, and the validation results. I also mentioned that the placeholder script is not a functional test, so the PR description stays accurate.
---

**2. If you had blindly copy-pasted the AI's draft without reading it, what could go wrong?**

The draft might contain incorrect claims, miss important details, or describe a placeholder as a real test. Reviewing it helps me catch mistakes before submitting the PR.
---

**3. Why does this PR need to target your own fork instead of the shared upstream repository?**

This assignment is practice work in my own fork. Targeting my fork avoids sending these experimental changes to the shared class repository.
---

# Task 7 — Map the Workflow to the Agentic Loop

## Goal

Explain this assignment's workflow using the same Gather → Analyze → Human Act → Verify structure from Week 3.

### Notes

**1. Which step(s) represent Gather?**

Gather means collecting the staged Git diff, filenames, and relevant file contents for review.
---

**2. Which step(s) represent Analyze?**

Analyze is when the hook checks fixed patterns and the AI reviews the changes for possible risks and missing context.
---

**3. Which step is Human Act, and why must a human — not Claude — run `git commit`, `git push`, and open the PR?**

Human Act is when I decide what to change, commit the approved changes, push the branch, and open the PR. Keeping these actions under human control prevents the AI from making important repository changes without my approval.
---

**4. Which step is Verify?**

Verify means checking the hook's rejection and successful run, reviewing the commit, and confirming that the PR targets the correct repository and branch.
---

**5. In one or two sentences: why do you need *both* the fixed-rule pre-commit hook and the AI skill? Isn't one enough?**

The hook reliably catches specific patterns, while AI can identify contextual issues that fixed rules may miss. Using both provides stronger protection than relying on either one alone.
---

# Task 8 — LinkedIn Post

## Goal

Publish a LinkedIn post summarizing what you built and what you learned about combining fixed-rule safety checks with AI-assisted review.

### Evidence

#### LinkedIn Post URL

https://www.linkedin.com/posts/mr-zack01_devops-git-github-share-7517218637661790209-9Oq4/?utm_source=share&utm_medium=member_desktop&rcm=ACoAAGxq6h8BmFdxEjgZsRCQ-jggJncjMKLdHOk
---

## Key Learnings

Add 3-5 bullet points on what you learned this week.

-Git hooks can block risky commits before they are created.
-Tracking hooks in a repository makes them easier to share.
-AI-assisted reviews can identify contextual risks and unclear code.AI-assisted reviews can identify contextual risks and unclear code.
-Humans should verify AI suggestions before committing or opening a PR.

---

# Submission Instructions

- Ensure `hooks/pre-commit` and `.claude/skills/pr-ready/SKILL.md` are committed to your GitHub repository
- Add all required screenshots to your submission
- All written answers must be in your own words
- Do not use a real secret or credential anywhere in your submission — the fake key in Task 1 is intentional and must stay clearly fake
- Open your Pull Request against your own fork, not the shared upstream repository
- Push your final changes to your forked repository
- Include your PR link and LinkedIn post URL

---

## GitHub Repository URL

Paste your forked repository URL here:

https://github.com/mr-zack01/devops-micro-internship-interviews
---

# Completion Checklist

- [✅] Branch `feature/ai-pr-ready` created with a staged file containing a fake secret and a debug statement
- [✅] `hooks/pre-commit` created and tracked in the repo (not only in `.git/hooks/`)
- [✅] `core.hooksPath` configured to point at `hooks/`
- [✅] Pre-commit hook shown blocking the risky commit
- [✅] `.claude/skills/pr-ready/SKILL.md` created with correct `allowed-tools` (no `Write`) and `disable-model-invocation: true`
- [✅] `/pr-ready` run against the risky diff and shown flagging issues
- [✅] Risky file fixed; `git commit` succeeds cleanly
- [✅] `/pr-ready` re-run showing a clean report and drafted PR title/description
- [✅] Pull Request opened using the AI draft as a starting point, with your own fork as the base repository (not upstream), PR link included
- [✅] Agentic Loop mapping (Task 7) completed in your own words
- [✅] LinkedIn post published and URL submitted
- [✅] All required screenshots added
- [✅] GitHub repository URL provided

---

## 📌 About DMI & CloudAdvisory

DevOps Micro Internship (DMI) is a project-based DevOps program run by Pravin Mishra (The CloudAdvisory) focused on real-world execution, systems thinking, and career readiness.

It helps learners build strong DevOps foundations with hands-on experience.

---

## 📌 Resources

- 🌐 DMI Official Website: https://dmi.pravinmishra.com?utm_source=github&utm_medium=readme  
- 🎓 University: https://university.pravinmishra.com?utm_source=github&utm_medium=readme  
- 💬 Discord Community: https://discord.pravinmishra.com?utm_source=github&utm_medium=readme  
- 📝 Blog: https://dmi.pravinmishra.com/blog?utm_source=github&utm_medium=readme  
- ▶️ YouTube Playlist: https://www.youtube.com/playlist?list=PLFeSNDtI4Cho  
- 🔗 Pravin Mishra (LinkedIn): https://www.linkedin.com/in/pravin-mishra-aws-trainer/  
- 🏢 CloudAdvisory (LinkedIn): https://www.linkedin.com/company/thecloudadvisory/

---

*This submission is part of DevOps Micro Internship (DMI) — Agentic AI Track.*
