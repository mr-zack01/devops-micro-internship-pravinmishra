# Assignment 1 — CodeTrack: Initial Git Setup (Local Only)

Part of the DevOps Micro Internship (DMI) with Agentic AI

---

## Purpose

In this assignment, you will set up Git correctly on your local machine before starting the CodeTrack project. You will create a local repository and configure your Git identity at both the repository level (local) and the machine level (global). This assignment is local only — you will not push anything to GitHub yet.

---

# Task 1 — Create the CodeTrack Project and Initialize Git

## Goal

Create a `CodeTrack` project folder and initialize it as a Git repository.

### Evidence

#### Screenshot 1 — Output of `git init` inside `CodeTrack` showing "Initialized empty Git repository"

<img width="915" height="483" alt="image" src="https://github.com/user-attachments/assets/17e5dc86-a513-44e6-9276-d92a934ab853" />

---

#### Screenshot 2 — Output of `ls -a` showing the `.git` folder

<img width="772" height="108" alt="image" src="https://github.com/user-attachments/assets/1a431280-d8b9-439b-9117-fea5b8e159b0" />

---

### Notes

**1. What is the `.git` folder, and why does it matter?**

The .git folder is a hidden directory created when we initialize a Git repository. It stores important information such as commit history, repository configuration, branches, and Git's internal tracking data. It allows Git to track changes in the project over time and helps us manage different versions of our code. If this folder is removed, the project generally loses its existing local Git history and repository metadata.
---

# Task 2 — Configure Git Identity Locally (Repository-Only)

## Goal

Set your Git username and email for the `CodeTrack` repository only, using `git config --local`.

### Evidence

#### Screenshot 3 — Output of `git config --local --list` showing your `user.name` and `user.email`

<img width="731" height="245" alt="image" src="https://github.com/user-attachments/assets/1edd668b-9165-450f-9cac-713ba48607de" />

---

# Task 3 — Configure Git Identity Globally

## Goal

Set a global Git username and email for this machine using `git config --global`. Note that CodeTrack's local settings still take priority over these.

### Evidence

#### Screenshot 4 — Output of `git config --global --list` showing your `user.name` and `user.email`

<img width="766" height="101" alt="image" src="https://github.com/user-attachments/assets/b6488d5c-cdb4-473c-90c0-3497fe00c6ab" />

---

# Submission Instructions

- Add all required screenshots in your submission
- Full Name must be visible in required screenshots
- Do not expose passwords, access tokens, or private keys

---

# Completion Checklist

- [✅] `CodeTrack` folder created and initialized as a Git repository (Screenshots 1–2)
- [✅] Explanation of the `.git` folder written in your own words
- [✅] Local `user.name` and `user.email` configured and verified (Screenshot 3)
- [✅] Global `user.name` and `user.email` configured and verified (Screenshot 4)
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
