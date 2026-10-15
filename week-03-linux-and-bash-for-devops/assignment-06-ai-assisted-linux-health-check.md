# Assignment 6 — Build an AI-Assisted Linux Health Check (AI-Assisted Linux Incident Triage)

Part of the DevOps Micro Internship (DMI) with Agentic AI

---

## Purpose

In this assignment, you will build a read-only Bash triage script that checks the health of your Ubuntu server and Nginx application, connect it to Claude Code as a reusable `/linux-triage` skill, simulate a controlled Nginx incident, use the skill to gather and analyze evidence, recover the service manually, and verify recovery. The workflow follows the Agentic Loop: Gather → Analyze → Human Act → Verify.

---

# Task 1 — Confirm the Healthy Baseline and Create the Workspace

## Goal

Confirm that Nginx and the React application are healthy before building the automation.

### Evidence

#### Screenshot 1 — Output of `systemctl is-active nginx`, `ss -ltn | grep ':80'`, and `curl -I http://localhost`

<img width="617" height="325" alt="image" src="https://github.com/user-attachments/assets/7d116f07-436f-45f3-8e25-daee3b6b0ce5" />

---

#### Screenshot 2 — Output of `pwd` and `find . -maxdepth 4 -type d | sort` showing the workspace folder structure

<img width="742" height="221" alt="image" src="https://github.com/user-attachments/assets/3b9a3b1f-2b35-4d5c-8164-9ce60ddf100e" />

---

### Notes

Answer the following in your own words:

**1. What proves that Nginx is running?**

The command systemctl is-active nginx returns active.
---

**2. What proves that the server is listening for HTTP traffic?**

The ss -ltn output shows a listening socket on port 80, and curl -I http://localhost checks whether the server responds to an HTTP request.
---

**3. Why must you capture a healthy baseline before simulating an incident?**

It gives us evidence of the server's normal state so we can compare it with the state during the simulated incident and verify recovery afterward.
---

# Task 2 — Create Project Context and Safety Rules in CLAUDE.md

## Goal

Tell Claude exactly what this project does and what it is not allowed to do.

### Evidence

#### Screenshot 3 — CLAUDE.md open in VS Code showing all four sections (Project Overview, Incident Workflow, Safety Rules, Output Rules)

<img width="1907" height="713" alt="image" src="https://github.com/user-attachments/assets/79780dd1-8631-4d20-8c55-8e2fe6322ae4" />

---

### Notes

Answer the following in your own words:

**1. Why should Claude receive project-specific operational rules?**

They define the project's purpose, permitted actions, and safety boundaries so Claude can assist consistently without making unauthorized changes.
---

**2. Why is the human required to execute the recovery command?**

A human must review the evidence and approve the action to prevent unintended service disruption or unsafe changes.
---

**3. Which rule prevents Claude from making an unsupported diagnosis?**

The rule requiring Claude to state observed evidence before making a diagnosis and clearly distinguish facts from assumptions.
---

# Task 3 — Use Agentic AI to Plan Before Writing the Script

## Goal

Use Claude Code to inspect the environment and produce a read-only plan before creating any Bash code.

### Evidence

#### Screenshot 4 — Claude Code showing the five-check plan and read-only inspection results

<img width="1517" height="497" alt="image" src="https://github.com/user-attachments/assets/b79267ff-01b3-4131-90ba-84198d38908b" />

---

### Notes

Answer the following in your own words:

**1. Which part of this task represents the Gather phase?**

The Gather phase consists of collecting evidence about Nginx status, the localhost HTTP response, port 80, root filesystem usage, and system load using read-only commands.
---

**2. Did Claude follow the instruction not to create files? How did you verify this?**

Claude Code stopped because the account's credit balance was too low, so it did not complete the requested inspection. I checked the project using pwd and ls -la and confirmed that the existing project files were present. This does not prove what Claude would have done if it had run successfully.
---

**3. Why is planning before coding useful in DevOps automation?**

Planning identifies the required checks, expected evidence, and safety restrictions before implementation. This helps prevent unnecessary commands and reduces the risk of accidental changes to a running server.
---

# Task 4 — Build the Linux Triage Bash Script

## Goal

Create one Bash script that gathers consistent Linux and Nginx health evidence.

### Evidence

#### Screenshot 5 — Top section of `linux-triage.sh` showing variables, thresholds, and the checks array

<img width="1513" height="580" alt="image" src="https://github.com/user-attachments/assets/8246c1bc-960f-47c3-b767-4fc2bc3ecd53" />

---

#### Screenshot 6 — Middle section showing check functions and conditionals

<img width="1512" height="577" alt="image" src="https://github.com/user-attachments/assets/a9f6ba76-2eb8-483f-8f25-92b5ac82dcbd" />

---

#### Screenshot 7 — Bottom section showing the loop, summary function, and exit behavior

<img width="1287" height="870" alt="image" src="https://github.com/user-attachments/assets/58293a50-be44-4a9f-b6fe-bf5a77db01da" />

---

#### Screenshot 8 — Output of `bash -n scripts/linux-triage.sh` (no syntax errors) and `ls -l scripts/linux-triage.sh` showing executable permission

<img width="1088" height="127" alt="image" src="https://github.com/user-attachments/assets/56d55ea6-87e7-42bc-9e09-19ee934bc091" />

---

### Notes

Answer the following in your own words:

**1. What is stored in the checks array?**

The checks array stores the names of the five health checks: Nginx status, HTTP response, port 80 listener, root disk usage, and system load.
---

**2. How does the `for` loop use that array?**

The for loop goes through each item in the array and passes it to the run_check function, which runs the matching health-check function.
---

**3. Why are the health checks separated into functions?**

Functions keep each check separate and organized, making the script easier to read, test, maintain, and update.
---

**4. What is the purpose of `$(...)` in this script?**

Command substitution runs a command and inserts its output into the surrounding command or variable assignment. For example, the script uses it to capture Nginx status and HTTP response codes.
---

**5. Why does the script use different exit codes for HEALTHY, WARN, and FAIL?**

Different exit codes allow users and automation to distinguish the result: 0 means healthy, 1 means a warning was detected, and 2 means at least one check failed.
---

# Task 5 — Run and Understand the Healthy-State Report

## Goal

Run the Bash script against the healthy server and verify that it creates a report.

### Evidence

#### Screenshot 9 — Output of `./scripts/linux-triage.sh` showing your Full Name and all five check results

<img width="847" height="403" alt="image" src="https://github.com/user-attachments/assets/93ddb781-df81-4602-b6cd-563f8ca7f23f" />

---

#### Screenshot 10 — Output showing the captured exit code and final summary

<img width="843" height="522" alt="image" src="https://github.com/user-attachments/assets/e5247caa-9c92-40e8-ae5d-5d3a00bb8f67" />

---

### Notes

Answer the following in your own words:

**1. What is the overall status of your healthy baseline?**

The baseline was healthy: Nginx was active, the local HTTP request returned 200 OK, port 80 was listening, and disk usage and system load were within the script’s thresholds.


---

**2. Which exact Linux evidence proves the application is serving traffic?**

curl -I --max-time 5 http://localhost returned HTTP/1.1 200 OK, and ss -lnt showed a listener on 0.0.0.0:80.
---

**3. Did your script return exit code 0 or 1? Explain why.**

Use the actual exit code shown in my screenshot. Exit code 0 means all checks were healthy with no warnings or failures. Exit code 1 means there were warnings but no failures.
---

**4. What is the difference between a warning and a failure in this script?**

A warning indicates a threshold or condition needs attention but does not count as a failed check. A failure indicates a required service or connectivity check did not pass, or disk usage reached the failure threshold.
---

# Task 6 — Create and Run the /linux-triage Skill

## Goal

Turn the Bash script into a reusable, manually invoked Agentic AI workflow.

### Evidence

#### Screenshot 11 — `SKILL.md` showing the frontmatter, allowed tool restrictions, and safety rules

<img width="1060" height="872" alt="image" src="https://github.com/user-attachments/assets/25da7f4a-3da7-4193-be30-541ec7fd79ed" />

---

#### Screenshot 12 — `/linux-triage` output for the healthy server

<img width="1161" height="623" alt="image" src="https://github.com/user-attachments/assets/d843b512-17a8-4818-a6c3-45572f7b1a1e" />

---

### Notes

Answer the following in your own words:

**1. Why does this skill have Bash, Read, and Grep, but not Write?**

Bash can run the read-only health-check commands, while Read and Grep can inspect and search existing information. Omitting Write helps prevent the skill from editing files.
---

**2. Why is `disable-model-invocation: true` useful for this skill?**

It prevents the model from invoking the skill automatically. The user must explicitly request it, which gives the operator more control over when the workflow runs.
---

**3. What part is performed by Bash, and what part is performed by Claude?**

Bash collects system evidence and produces the check results. Claude interprets that evidence, explains likely causes, and suggests safe next steps.
---

**4. Why is this better than asking Claude "Is my server healthy?" without giving it evidence?**

The workflow supplies actual system output, allowing Claude to base its analysis on observable evidence instead of guessing about the server’s condition.
---

# Task 7 — Simulate an Nginx Incident and Let the Skill Diagnose It

## Goal

Create a controlled service failure, gather evidence through Bash, and let Claude analyze the evidence without taking recovery action.

### Evidence

#### Screenshot 13 — Output showing Nginx is inactive and the HTTP request fails

<img width="863" height="275" alt="image" src="https://github.com/user-attachments/assets/f361abe2-6b03-4e22-a9da-819b2f008b7b" />

---

#### Screenshot 14 — `/linux-triage` output showing failed evidence, most likely cause, and a suggested recovery command

<img width="1337" height="652" alt="image" src="https://github.com/user-attachments/assets/97661d6f-cd28-4ad1-a681-2065122a4eee" />

---

#### Screenshot 15 — `incident-failure-report.txt` showing the failed checks and your Full Name

<img width="857" height="777" alt="image" src="https://github.com/user-attachments/assets/b0c20bd0-e5e8-4901-a101-aa8f73dc1edf" />

---

### Notes

Answer the following in your own words:

**1. Which three checks failed?**

Nginx status, the HTTP request to localhost, and the port 80 listener check failed during the simulated outage.
---

**2. What evidence supports the conclusion that Nginx is unavailable?**

systemctl is-active nginx returned inactive, and curl -I --max-time 5 http://localhost failed with a connection error. These results support the conclusion that the local web service was unavailable.
---

**3. Did Claude execute the recovery command? Why is that important?**

No recovery command was executed by Claude in this workflow. Keeping recovery under human control prevents an AI from making an unapproved service change.
---

**4. Which phase of the Agentic Loop is represented by the Bash report?**

The Bash report represents the Gather phase because it collects and records the system evidence.
---

**5. Which phase is represented by Claude's explanation?**

Claude’s explanation represents the Analyze phase because it interprets the evidence, identifies a likely cause, and recommends a possible next action.
---

# Task 8 — Recover Manually, Verify Again, and Write the Incident Summary

## Goal

Recover the service as the human operator and prove that the system is healthy again.

### Evidence

#### Screenshot 16 — Output showing Nginx is active and `curl -I http://localhost` returns 200 OK

<img width="745" height="472" alt="image" src="https://github.com/user-attachments/assets/912a02bc-6612-4e3e-b994-28eb448657d2" />

---

#### Screenshot 17 — Second `/linux-triage` output showing successful recovery with no FAIL results

<img width="743" height="405" alt="image" src="https://github.com/user-attachments/assets/0d6c9818-e13b-4162-b0e1-ef63511bc5dd" />

---

#### Screenshot 18 — Output of `ls -lah reports` showing both `incident-failure-report.txt` and `recovery-report.txt`

<img width="812" height="862" alt="image" src="https://github.com/user-attachments/assets/a2293639-8184-4270-9518-72428998306a" />

---

#### Screenshot 19 — `incident-summary.md` showing all required sections and your Full Name

<img width="1421" height="867" alt="image" src="https://github.com/user-attachments/assets/6438e235-f0ac-4f3e-8288-0ad8ebfeb3ee" />

---

### Notes

Answer the following in your own words:

**1. What action did you execute manually?**

I manually started Nginx using sudo systemctl start nginx.
---

**2. What evidence proves that the service recovered?**

systemctl is-active nginx returned active, and the HTTP request to localhost returned HTTP/1.1 200 OK. The port 80 listener and second triage run provided additional verification.
---

**3. Why is the second triage run necessary?**

It confirms the system’s condition after recovery and checks that the expected health conditions are passing again.
---

**4. What could go wrong if an AI agent automatically restarted every failed service?**

It could restart a service during planned maintenance, hide the underlying problem, disrupt dependent applications, or make an unsafe change without understanding the operational context.
---

**5. In one sentence, explain the difference between using AI as a chatbot and using AI in this agentic workflow.**

A chatbot answers questions from the information provided, while this workflow combines scripted evidence collection with AI analysis and keeps recovery under human control.
---

# Incident Summary

Fill in all seven sections below in your own words.

**Full Name:** ZAKARIYA AHMED

**Date:** 15/10/2026

---

**1. Reported Symptom**

The local web application stopped responding to HTTP requests on port 80 during a controlled Nginx incident simulation.
---

**2. Evidence Collected**

The command systemctl is-active nginx returned inactive. The command curl -I --max-time 5 http://localhost failed to connect. The failure evidence was recorded in reports/incident-failure-report.txt.
---

**3. Most Likely Cause**

Nginx had been deliberately stopped for the controlled test, leaving no working local HTTP response on port 80. This conclusion is based on the observed service status and failed request.
---

**4. Human-Approved Recovery Action**

I manually ran sudo systemctl start nginx to restore the service.
---

**5. Verification**

After recovery, I checked Nginx service status and sent another HTTP request to localhost. The expected successful evidence was an active service status and HTTP/1.1 200 OK. The second triage run provided a further health check.
---

**6. Safety Decision**

I kept recovery under human control. The diagnosis was based on collected evidence, and the service was started manually rather than allowing the AI to make a service change.
---

**7. Agentic Loop Mapping**

Gather: Bash collected service, HTTP, port, disk, and load evidence.

Analyze: The AI interpreted the failure evidence and suggested a recovery command.

Human decision and action: I reviewed the recommendation and manually started Nginx.

Verify: I checked the service and HTTP response again and ran the triage script a second time.
---

# LinkedIn Post (Required)

## Evidence

#### LinkedIn Post URL

Paste your LinkedIn post URL here:

https://www.linkedin.com/posts/mr-zack01_devops-linux-bashscripting-share-7516473008451051520-Lh3Q/?utm_source=social_share_send&utm_medium=member_desktop_web&rcm=ACoAAGxq6h8BmFdxEjgZsRCQ-jggJncjMKLdHOk
---

#### Screenshot — Published LinkedIn post

<img width="997" height="705" alt="image" src="https://github.com/user-attachments/assets/ed6cef81-beb3-4df9-84a8-13bec7632ac0" />

---

# GitHub Repository URL

Paste the URL of your GitHub folder or repository containing the assignment files here:

`Add your URL here`

---

# Submission Instructions

- Add all required screenshots in your submission
- Full Name must be visible in required screenshots and the Bash report
- All written answers must be in your own words
- Do not expose sensitive information (keys, passwords, AWS account IDs, tokens)
- GitHub URL must be included in this document

---

# Completion Checklist

- [✅] Task 1: Healthy baseline confirmed, workspace created (Screenshots 1–2, Notes answered)
- [✅] Task 2: CLAUDE.md created with all four sections (Screenshot 3, Notes answered)
- [✅] Task 3: Five-check plan produced by Claude using read-only tools (Screenshot 4, Notes answered)
- [✅] Task 4: `linux-triage.sh` created, syntax validated, executable permission set (Screenshots 5–8, Notes answered)
- [✅] Task 5: Healthy-state report generated with no FAIL result (Screenshots 9–10, Notes answered)
- [✅] Task 6: `/linux-triage` skill created and run successfully on healthy server (Screenshots 11–12, Notes answered)
- [✅] Task 7: Nginx incident simulated, failed evidence captured, Claude did not execute recovery (Screenshots 13–15, Notes answered)
- [✅] Task 8: Nginx recovered manually, recovery verified, reports saved, incident summary complete (Screenshots 16–19, Notes answered)
- [✅] Incident summary contains all seven required sections
- [✅] LinkedIn post published and URL submitted
- [✅] Full Name visible in all required screenshots and the Bash report
- [✅] Skill does not have Write permission
- [✅] Skill did not execute any recovery commands
- [✅] No sensitive data exposed

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
