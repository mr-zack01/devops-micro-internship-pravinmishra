# Assignment 2 — Deploy a React App on Ubuntu VM Using Nginx

Part of the DevOps Micro Internship (DMI) with Agentic AI

---

## Purpose

In this assignment, you will deploy a React application on an Ubuntu EC2 instance and serve it using Nginx. You will provision a Linux server, install the required tools, personalize the application with your details, and verify that it is publicly accessible via a browser.

---

# Task 1 — Setup Environment (Node.js & npm)

## Goal

Install Node.js and npm on the Ubuntu VM and verify the installation.

### Evidence

#### Screenshot 1 — Output of `node -v && npm -v` showing installed versions

<img width="1493" height="462" alt="image" src="https://github.com/user-attachments/assets/dcf80b7e-37de-4d4b-89ad-72e7cf3b60fe" />

---

# Task 2 — Setup Environment (Nginx)

## Goal

Install Nginx, start the service, and confirm it is running.

### Evidence

#### Screenshot 2 — Output of `systemctl status nginx --no-pager` showing Active (running)

<img width="1501" height="565" alt="image" src="https://github.com/user-attachments/assets/9f28855a-dfb8-4d61-aaab-ef0fc25a09c7" />

---

# Task 3 — Clone React Application

## Goal

Clone the project repository and verify the project files are present.

### Evidence

#### Screenshot 3 — Output of `ls` inside the `my-react-app` directory showing project files

<img width="1493" height="405" alt="image" src="https://github.com/user-attachments/assets/20dd72b5-6d96-4fc5-bf06-0f8245b29329" />

---

# Task 4 — Modify Application (Personalization)

## Goal

Update `App.js` with your full name and the current date.

### Evidence

#### Screenshot 4 — `nano App.js` open showing your full name and date filled in

<img width="1492" height="995" alt="image" src="https://github.com/user-attachments/assets/e314e772-5948-408a-8512-8db7f15eba00" />

---

# Task 5 — Build React Application

## Goal

Install dependencies and generate the production build.

### Evidence

#### Screenshot 5 — Output of `ls` inside `my-react-app` showing the `build/` folder generated

<img width="1235" height="372" alt="image" src="https://github.com/user-attachments/assets/6166eadd-4429-4ac5-b3ef-a1c1203911de" />

---

# Task 6 — Deploy React Build to Nginx Web Root

## Goal

Copy the production build files to the Nginx web root directory.

### Evidence

#### Screenshot 6 — Output of `ls /var/www/html/` showing the deployed build contents

<img width="1503" height="382" alt="image" src="https://github.com/user-attachments/assets/91b368b1-8635-4c8b-aff5-f473b266c8f2" />

---

# Task 7 — Configure Nginx for React Application

## Goal

Apply Nginx configuration for React routing and confirm the service is active.

### Evidence

#### Screenshot 7 — Output of `systemctl is-active nginx` showing `active`

<img width="1502" height="405" alt="image" src="https://github.com/user-attachments/assets/a4dc083c-6c57-44be-b3d3-592aacef5f0b" />

---

#### Screenshot 8 — Output of `cat /etc/nginx/sites-available/default` showing the Nginx config

<img width="1507" height="526" alt="image" src="https://github.com/user-attachments/assets/9e3fc9f1-5ab1-4332-8a5d-a3e5e936279e" />

---

# Task 8 — Test Deployment

## Goal

Verify the React application is publicly accessible via the server's public IP.

### Evidence

#### Screenshot 9 — Output of `curl ifconfig.me` showing the server's public IP address

<img width="1107" height="160" alt="image" src="https://github.com/user-attachments/assets/2dceaa19-c76c-4ade-89d1-12a3657db2aa" />

---

#### Screenshot 10 — Browser showing the deployed React app at `http://<public-ip>` with your name and date visible

<img width="1616" height="886" alt="image" src="https://github.com/user-attachments/assets/3fa2c3b8-2f59-4f71-96ba-ca240d47d03a" />

---

# LinkedIn Post (Required)

## Evidence

#### LinkedIn Post URL

Paste your LinkedIn post URL here:

`Add your URL here`

---

#### Screenshot — LinkedIn post showing the deployed application

Add your screenshot here.

---

# Submission Instructions

- Add all required screenshots in your submission
- Full name must be visible in required screenshots
- Do not expose sensitive information (keys, passwords, account IDs)

---

# Completion Checklist

- [ ] Node.js and npm installed and verified (Screenshot 1)
- [ ] Nginx installed and running (Screenshot 2)
- [ ] Repository cloned and files verified (Screenshot 3)
- [ ] App.js updated with full name and date (Screenshot 4)
- [ ] Production build generated (Screenshot 5)
- [ ] Build files deployed to Nginx web root (Screenshot 6)
- [ ] Nginx configured and active (Screenshots 7 & 8)
- [ ] Public IP retrieved (Screenshot 9)
- [ ] React app accessible in browser with personal details visible (Screenshot 10)
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
