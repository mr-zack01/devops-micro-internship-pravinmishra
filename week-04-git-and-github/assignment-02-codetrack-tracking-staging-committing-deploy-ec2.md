# Assignment 2 — CodeTrack: Tracking, Staging, Committing + Deploy to EC2

Part of the DevOps Micro Internship (DMI) with Agentic AI

---

## Purpose

In this assignment, you will track and stage project files, create two meaningful Git commits in `CodeTrack`, verify your commit history, and deploy the CodeTrack static website to an EC2 instance using Nginx. This connects local version-control practice with a basic manual deployment workflow used in real DevOps environments.

---

# Task 1 — Verify Git Setup and Enter the Repository

## Goal

Confirm that Git works and that you are inside the correct `CodeTrack` repository.

### Evidence

#### Screenshot 1 — Output of `pwd` showing you're inside `CodeTrack`

<img width="522" height="86" alt="image" src="https://github.com/user-attachments/assets/5f3dd70d-a167-45eb-9c8e-4e7b94624a3b" />

---

#### Screenshot 2 — Output of `git status` showing no "not a git repository" error

<img width="645" height="170" alt="image" src="https://github.com/user-attachments/assets/b9ad2822-bd28-4350-a0a4-0ad3f244c803" />

---

# Task 2 — Create index.html and style.css

## Goal

Create the two starter UI files inside `CodeTrack`.

### Evidence

#### Screenshot 3 — Output of `ls` showing `index.html` and `style.css`

<img width="612" height="98" alt="image" src="https://github.com/user-attachments/assets/a4832405-9d84-4e0e-a06b-b5fa98837e7c" />

---

# Task 3 — Add Starter Content

## Goal

Copy the provided starter HTML and CSS content into your local `index.html` and `style.css` files.

### Evidence

#### Screenshot 4 — Your editor showing the contents of `index.html` and `style.css`

<img width="807" height="601" alt="image" src="https://github.com/user-attachments/assets/88b22c6b-e45f-43a9-9637-119fc21da6fd" />
<img width="837" height="880" alt="image" src="https://github.com/user-attachments/assets/139671dd-5793-46dc-a04b-cb75c88ad253" />

---

# Task 4 — Track and Stage Files Correctly

## Goal

Confirm both files show as untracked, then stage them individually with `git add`.

### Evidence

#### Screenshot 5 — Output of `git status` showing both files as untracked

<img width="793" height="275" alt="image" src="https://github.com/user-attachments/assets/d057c0b9-469c-4281-b92a-f518e0227599" />

---

#### Screenshot 6 — Output of `git status` showing both files staged under "Changes to be committed"

<img width="571" height="255" alt="image" src="https://github.com/user-attachments/assets/a05e55ef-f1ed-4987-aa7f-d4946c8536a3" />

---

# Task 5 — Create the First Commit (Clean Initial Commit)

## Goal

Commit the staged starter files using the message `Initial UI scaffold: add index.html and style.css`, then check the log.

### Evidence

#### Screenshot 7 — Output of `git commit`

<img width="1002" height="112" alt="image" src="https://github.com/user-attachments/assets/a71c7484-77cd-4221-8003-9e393b729445" />

---

#### Screenshot 8 — Output of `git log --oneline` showing the first commit

<img width="792" height="47" alt="image" src="https://github.com/user-attachments/assets/9aa66e01-ce43-40fd-90e4-900cc38a3ab2" />

---

# Task 6 — Modify index.html and Create a Second Commit

## Goal

Follow the instruction comment inside `index.html` to update the Student Name and Group Name, then commit that change separately using the message `Update homepage content: heading, tagline, CTA button`.

### Evidence

#### Screenshot 9 — Browser showing the updated page with your Student Name and Group Name visible

<img width="1232" height="865" alt="Screenshot 2026-10-15 195526" src="https://github.com/user-attachments/assets/1785c1cd-9bba-4569-a707-603fbc0b4a36" />

---

#### Screenshot 10 — Output of `git status` showing `index.html` as modified

<img width="715" height="225" alt="image" src="https://github.com/user-attachments/assets/4ddacbb3-de9b-4e49-8f10-3540ceab1606" />

---

#### Screenshot 11 — Output of `git commit`

<img width="808" height="162" alt="image" src="https://github.com/user-attachments/assets/c39866f6-8d3a-433d-a5bb-4ac444e82d93" />

---

#### Screenshot 12 — Output of `git log --oneline` showing two commits

<img width="807" height="121" alt="image" src="https://github.com/user-attachments/assets/bc65818f-9903-451b-8f7a-2c894e0aac11" />

---

# Task 7 — Deploy to EC2 with Nginx (Static Website)

## Goal

Install and start Nginx on your EC2 instance, then copy `index.html` and `style.css` into the Nginx web root.

### Evidence

#### Screenshot 13 — Output of `systemctl status nginx --no-pager` showing Nginx `active (running)`

<img width="1183" height="452" alt="image" src="https://github.com/user-attachments/assets/d3419779-d2a8-4739-b6b8-d65c160edeab" />

---

#### Screenshot 14 — Output of `curl -I http://localhost` showing `HTTP/1.1 200 OK`

<img width="647" height="285" alt="image" src="https://github.com/user-attachments/assets/1ecaa022-82f3-44b3-a2e8-588e736ed884" />

---

#### Screenshot 15 — Browser showing the CodeTrack site loaded at `http://<EC2_PUBLIC_IP>`, with your Full Name and Group Name visible

<img width="1232" height="865" alt="image" src="https://github.com/user-attachments/assets/08d57509-2e91-4410-aec0-d1faef2ea060" />

---

# LinkedIn Post (Required)

## Evidence

#### LinkedIn Post URL

Paste your LinkedIn post URL here:

https://www.linkedin.com/posts/mr-zack01_devops-aws-ec2-share-7516504861954359296-uIdU/?utm_source=share&utm_medium=member_desktop&rcm=ACoAAGxq6h8BmFdxEjgZsRCQ-jggJncjMKLdHOk
---

#### Screenshot — LinkedIn post showing the deployed CodeTrack application

<img width="1018" height="597" alt="image" src="https://github.com/user-attachments/assets/d6e06e8d-cddf-4c0a-805e-ced1e477a622" />

---

# Submission Instructions

- Add all required screenshots in your submission
- Full Name and Group Name must be visible in the deployed application evidence
- `git log --oneline` output must show at least two meaningful commits
- Do not expose AWS access keys, passwords, private key contents, or other sensitive information

---

# Completion Checklist

- [ ] `CodeTrack` repository verified with `git status` (Screenshots 1–2)
- [ ] `index.html` and `style.css` created and populated (Screenshots 3–4)
- [ ] Starter files staged and committed in the first commit (Screenshots 5–8)
- [ ] Student Name and Group Name updated in `index.html` (Screenshot 9)
- [ ] Second controlled commit created (Screenshots 10–12)
- [ ] Nginx active on the EC2 instance and CodeTrack reachable via its public IP (Screenshots 13–15)
- [ ] LinkedIn post published and URL submitted
- [ ] No sensitive data exposed

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
