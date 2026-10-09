# Assignment 3 — Production Maintenance Drill (OPS Checklist)

Part of the DevOps Micro Internship (DMI) with Agentic AI

---

## Purpose

In this assignment, you will treat your already deployed React application (on Ubuntu VM with Nginx) as a live production system. You will perform structured operational checks covering network validation, service health, log analysis, resource monitoring, configuration verification, and incident simulation with recovery — mirroring real on-call DevOps responsibilities.

---

# Task 1 — Server Access & Networking Validation

## Goal

Verify that the deployed React application is reachable from the browser and confirm basic network connectivity of the Ubuntu VM.

### Evidence

#### Screenshot 1 — Browser showing the React app with your Full Name visible on the UI

<img width="1567" height="786" alt="image" src="https://github.com/user-attachments/assets/86bcb4c8-1f2f-4b2d-bbd2-8921f2507342" />

---

#### Screenshot 2 — Output of `ip a`

<img width="1506" height="506" alt="image" src="https://github.com/user-attachments/assets/ab65cc71-85cc-4963-81df-c2d6df7313d4" />

---

#### Screenshot 3 — Output of `sudo ss -tulpen`

<img width="1510" height="635" alt="image" src="https://github.com/user-attachments/assets/61a8c844-2559-4b31-bd77-43e53ccdcc02" />

---

#### Screenshot 4 — Output of `sudo ufw status`

<img width="1493" height="143" alt="image" src="https://github.com/user-attachments/assets/5c4efd9e-36e0-4008-a306-7c7dbd99056e" />

---

### Notes

Answer the following in your own words:

**1. What proves Nginx is listening on 0.0.0.0:80?**

The output of sudo ss -tulpen shows 0.0.0.0:80 in the LISTEN state, and the associated process is Nginx. This confirms that Nginx is listening for HTTP connections on all IPv4 network interfaces.
---

**2. What proves SSH is active on port 22?**

The output shows 0.0.0.0:22 and [::]:22 in the LISTEN state. The associated process is sshd, managed through the systemd SSH socket. This confirms that SSH is listening on port 22 for IPv4 and IPv6 connections.
---

**3. Did you find any unexpected open ports? Explain briefly.**

I observed several additional listening ports, including local ports used by systemd-resolved, chronyd, and development-related processes. Most of these are bound to the loopback address 127.0.0.1, so they are not directly listening on all network interfaces. I would verify the purpose of any unfamiliar service and check the AWS Security Group rules before deciding whether a port presents a security risk.
---

# Task 2 — Service Health & Systemd Validation (Nginx)

## Goal

Verify that Nginx is properly installed, running, enabled at boot, and safely configured.

### Evidence

#### Screenshot 1 — Output of `systemctl status nginx --no-pager`

<img width="1506" height="638" alt="image" src="https://github.com/user-attachments/assets/43b7b7d1-1fd4-4b12-928b-48ec46cd421c" />

---

#### Screenshot 2 — Output of `sudo nginx -t`

<img width="1502" height="182" alt="image" src="https://github.com/user-attachments/assets/db408d06-b322-4286-ac50-d2c9731d5974" />

---

#### Screenshot 3 — Output of `sudo ss -lptn '( sport = :80 )'`

<img width="1506" height="220" alt="image" src="https://github.com/user-attachments/assets/8f29c50c-975d-4e1c-9b2e-298eb780bfda" />

---

### Notes

Answer the following in your own words:

**1. What happens if Nginx fails to restart in production?**

If Nginx fails to restart, the website may become unavailable, and users may receive connection errors. This can happen because of invalid configuration, port conflicts, or other service problems. I would check the service status and error logs, identify the cause, and restore service as quickly and safely as possible.
---

**2. What's your basic rollback plan?**

Before making changes, I would back up the working Nginx configuration and deployed application files. If a new change causes a failure, I would restore the previous known-good configuration or application version, run sudo nginx -t, and restart Nginx only after the configuration test succeeds. Finally, I would verify the service status and test the website using curl and a browser.
---

# Task 3 — Logs & Request Trace

## Goal

Verify real traffic flow and analyze logs to understand system behavior and errors.

### Evidence

#### Screenshot 1 — Output of `sudo tail -n 30 /var/log/nginx/access.log`

<img width="1503" height="635" alt="image" src="https://github.com/user-attachments/assets/36f039c2-2c0a-4a71-b52a-21a757a727d1" />

---

#### Screenshot 2 — Output of `sudo tail -n 30 /var/log/nginx/error.log`

<img width="1502" height="155" alt="image" src="https://github.com/user-attachments/assets/d673f8b3-ca59-428f-9111-9ef08c0aba5c" />

---

#### Screenshot 3 — Output of `sudo journalctl -u nginx --no-pager -n 50`

<img width="1507" height="390" alt="image" src="https://github.com/user-attachments/assets/cd9a62ad-4e46-4677-9ae2-365e647aeb63" />

---

### Notes

Answer the following in your own words:

**1. Were there any errors in the logs?**

- If yes, mention 1–2 example error lines from the logs and explain what each one means in simple terms.
- If no, explain what it means if the error log is empty or shows no recent errors during your check.

The Nginx error log showed a notice about inherited sockets, which is informational. The access log showed some 404 responses for paths such as /login and /admin/login.asp, meaning those requested resources were not found. It also showed a 400 response for unexpected TLS-like data sent to the HTTP port. These entries do not indicate that the application itself is down.
---

**2. If there were no errors, what does that indicate about the system?**

The error log did not show any recent critical errors during my check. This suggests that Nginx was not recording major errors during the period examined. However, it does not guarantee that the system will never experience problems.
---

**3. Based on the access logs, were your curl requests visible in the log entries? What does that prove about traffic flow?**

The access log contains successful HTTP requests and requests for static React files. These entries confirm that Nginx is receiving HTTP traffic and serving application content. However, the displayed entries do not clearly identify a specific curl request, so I would generate a new curl request and check the latest log entries to confirm it directly.
---

# Task 4 — System Resource Health Check (Capacity Red Flags)

## Goal

Assess server capacity and detect potential performance or failure risks.

### Evidence

#### Screenshot 1 — Output of `uptime`

Add your screenshot here.

---

#### Screenshot 2 — Output of `free -h`

Add your screenshot here.

---

#### Screenshot 3 — Output of `df -h`

Add your screenshot here.

---

#### Screenshot 4 — Output of `sudo du -sh /var/* | sort -h`

Add your screenshot here.

---

### Notes

Answer the following in your own words:

**1. Which resource looks most critical right now? (CPU/load, memory, or disk) Explain why.**

Write your answer here.

---

**2. What happens if disk becomes 100% full in a production server?**

Write your answer here.

---

# Task 5 — Configuration & Deployment Verification

## Goal

Ensure the correct React build is deployed and Nginx is serving it properly.

### Evidence

#### Screenshot 1 — Output of `ls -lah /var/www/html | head -n 20`

Add your screenshot here.

---

#### Screenshot 2 — Output of `grep -R "Deployed by" -n /var/www/html 2>/dev/null | head`

Add your screenshot here.

---

#### Screenshot 3 — Output of `grep -n "try_files" /etc/nginx/sites-available/default`

Add your screenshot here.

---

### Notes

Answer the following in your own words:

**1. How do you confirm that the correct version of the application is deployed?**

Write your answer here.

---

# Task 6 — Nginx Configuration Failure Simulation

## Goal

Simulate a real-world Nginx misconfiguration and recover the service safely.

### Evidence

#### Screenshot 1 — Output of `sudo nginx -t` showing the syntax error (broken config)

Add your screenshot here.

---

#### Screenshot 2 — Output of `sudo nginx -t` showing syntax ok (fixed config)

Add your screenshot here.

---

#### Screenshot 3 — Output of `curl -I http://<public-ip>` confirming recovery (200 OK)

Add your screenshot here.

---

### Notes

Answer the following in your own words:

**1. What caused the configuration failure?**

Write your answer here.

---

**2. How did you fix the issue?**

Write your answer here.

---

**3. How can you avoid this kind of issue in real production systems?**

Write your answer here.

---

# Task 7 — Web Application Failure Simulation

## Goal

Simulate missing deployment content and recover the application safely.

### Evidence

#### Screenshot 1 — Output of `curl -I http://<public-ip>` showing failure (non-200 response)

Add your screenshot here.

---

#### Screenshot 2 — Output of `curl -I http://<public-ip>` confirming recovery (200 OK)

Add your screenshot here.

---

### Notes

Answer the following in your own words:

**1. What caused the application to break in this scenario?**

Write your answer here

---

**2. How did you fix the issue and restore the application?**

Write your answer here.

---

**3. What steps would you take to prevent this kind of issue in real production systems?**

Write your answer here.

---

# Task 8 — Security & Reliability Review

## Goal

Review and reflect on the security and reliability practices applied during this assignment.

### Security & Reliability Notes

Answer the following in your own words:

**1. Why is SSH key-based authentication more secure than sharing passwords?**

Write your answer here.

---

**2. Why should only required ports be open on a production server?**

Write your answer here.

---

**3. Why is it important for Nginx to be enabled on boot?**

Write your answer here.

---

**4. What are the risks of sharing secrets, keys, or credentials publicly?**

Write your answer here.

---

**5. Why should cloud resources be stopped or terminated when they are no longer needed?**

Write your answer here.

---

# LinkedIn Post (Required)

## Evidence

#### LinkedIn Post URL

Paste your LinkedIn post URL here:

`Add your URL here`

---

#### Screenshot — Published LinkedIn post

Add your screenshot here.

---

# Submission Instructions

- Add all required screenshots in your submission
- Full name must be visible in required screenshots
- Do not expose sensitive information (keys, passwords, account IDs)

---

# Completion Checklist

- [ ] Task 1: Screenshots (browser, ip a, ss -tulpen, ufw status) + Notes answered
- [ ] Task 2: Screenshots (nginx status, nginx -t, ss port 80) + Notes answered
- [ ] Task 3: Screenshots (access log, error log, journalctl) + Notes answered
- [ ] Task 4: Screenshots (uptime, free -h, df -h, du -sh) + Notes answered
- [ ] Task 5: Screenshots (ls html, grep deployed by, grep try_files) + Notes answered
- [ ] Task 6: Screenshots (nginx -t fail, nginx -t pass, curl recovery) + Notes answered
- [ ] Task 7: Screenshots (curl failure, curl recovery) + Notes answered
- [ ] Task 8: Security & Reliability Notes answered
- [ ] LinkedIn post published and URL submitted
- [ ] Full Name visible in all required screenshots
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
