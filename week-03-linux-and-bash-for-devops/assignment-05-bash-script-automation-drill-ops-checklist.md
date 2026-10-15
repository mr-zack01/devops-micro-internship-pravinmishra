# Assignment 5 — Bash Script Automation Drill (OPS Checklist)

Part of the DevOps Micro Internship (DMI) with Agentic AI

---

## Purpose

In this assignment, you will practice Bash scripting by building a series of small automation scripts covering environment setup, variables, arrays, loops, file conditionals, if-else logic, and functions. These scripts form the foundation of real-world Linux automation used in DevOps, cloud, and production support environments.

---

# Task 1 — Bash Environment & Workspace Setup

## Goal

Verify that Bash is available on your system and create a clean workspace for this assignment.

### Evidence

#### Screenshot 1 — Output of `echo $SHELL` and `bash --version`

<img width="1652" height="285" alt="image" src="https://github.com/user-attachments/assets/7f63457e-4275-445f-ba6a-d3ec3423191a" />

---

#### Screenshot 2 — Output of `pwd` and `ls -lah` showing the scripts directory

<img width="1128" height="145" alt="image" src="https://github.com/user-attachments/assets/939e307d-2bf8-4b30-9f20-df8a52aac20a" />

---

### Notes

Answer the following in your own words:

**1. What is Bash?**

Bash stands for Bourne Again Shell. It is a command-line interpreter used to execute Linux commands and automate repetitive tasks through scripts.
---

**2. What is the difference between shell and Bash?**

A shell is a program that interprets commands and allows users to interact with an operating system. Bash is one specific type of shell.
---

**3. Why is it important to confirm the Bash version before writing scripts?**

Checking the Bash version helps confirm that the system supports the features and syntax used in a script. It can help prevent compatibility problems during execution.
---

# Task 2 — Your First Bash Script

## Goal

Create your first Bash script, make it executable, and run it from the terminal.

### Evidence

#### Screenshot 1 — Content of `first-script.sh`

<img width="1657" height="178" alt="image" src="https://github.com/user-attachments/assets/0823ebf9-60f9-4d30-958c-b99ce30091ef" />

---

#### Screenshot 2 — Output of `./first-script.sh`

<img width="1412" height="95" alt="image" src="https://github.com/user-attachments/assets/ec806732-c3f9-4515-b328-e063ceb1b0a2" />

---

#### Screenshot 3 — Output of `ls -l first-script.sh` showing executable permission

<img width="1652" height="147" alt="image" src="https://github.com/user-attachments/assets/a58332dc-1053-449b-af6f-ad0b4762bf02" />

---

### Notes

Answer the following in your own words:

**1. What is the purpose of `#!/bin/bash`?**

It is the shebang line. It tells the operating system to use /bin/bash to execute the script when run directly.
---

**2. Why do we use `chmod +x` before running a script?**

It adds executable permission so you can run the script directly using ./first-script.sh.
---

**3. What is the difference between running a script using `./script.sh` and `bash script.sh`?**

./script.sh runs the script directly and requires executable permission.
bash script.sh explicitly runs it with Bash and does not require executable permission.
---

# Task 3 — Variables: User Information Script

## Goal

Use variables to store and display user-related information.

### Evidence

#### Screenshot 1 — Content of `user-info.sh`

<img width="1652" height="321" alt="image" src="https://github.com/user-attachments/assets/9940509e-10a9-4cbc-b1ec-14516457e407" />

---

#### Screenshot 2 — Output of `./user-info.sh`

<img width="1656" height="178" alt="image" src="https://github.com/user-attachments/assets/009487df-f26b-451a-8977-c9c274ab6874" />

---

### Notes

Answer the following in your own words:

**1. What is a variable in Bash?**

A variable stores a value that can be reused in a script, such as a name or course.
---

**2. Why should we avoid spaces around the `=` sign when creating variables?**

Bash requires assignments like name="ZAKARIYA AHMED" without spaces. Adding spaces causes Bash to interpret the statement differently.
---

**3. How do you access the value stored inside a Bash variable?**

Use $variable_name, such as echo "$name".
---

# Task 4 — Arrays & Loops: Tools Checklist Script

## Goal

Use arrays and loops to print a checklist of tools used in Bash scripting.

### Evidence

#### Screenshot 1 — Content of `tools-checklist.sh`

<img width="872" height="222" alt="image" src="https://github.com/user-attachments/assets/01a98643-89f0-44f0-b80b-339f0937eb46" />

---

#### Screenshot 2 — Output of `./tools-checklist.sh`

<img width="922" height="222" alt="image" src="https://github.com/user-attachments/assets/eafaf8de-157e-4cbb-b760-5a62b85d3d4f" />

---

### Notes

Answer the following in your own words:

**1. What is an array in Bash?**

An array stores multiple values under one variable name.
---

**2. Why are arrays useful in scripts?**

They let you manage and process multiple items, such as tools or filenames, efficiently.
---

**3. What does `"${tools[@]}"` mean?**

It expands to all elements of the tools array, keeping each element as a separate item when quoted.
---

**4. What is the purpose of the `for` loop in this script?**

It repeats a set of commands for each item in a list.
---

# Task 5 — Loops: Number Counter Script

## Goal

Use loops to repeat a task multiple times.

### Evidence

#### Screenshot 1 — Content of `counter.sh`

<img width="973" height="252" alt="image" src="https://github.com/user-attachments/assets/e7593bdd-6f17-4989-8b5f-fad9ed2eedc2" />

---

#### Screenshot 2 — Output of `./counter.sh`

<img width="925" height="210" alt="image" src="https://github.com/user-attachments/assets/2d6f355c-1a85-4f48-a65d-46558cd78800" />

---

### Notes

Answer the following in your own words:

**1. What is a loop?**

A loop repeatedly executes a block of commands.

---

**2. Why do we use loops in Bash scripting?**

We use loops to automate repetitive tasks, reduce manual effort, and execute commands multiple times efficiently.
---

**3. How many times did the loop run in your script?**

The loop ran 5 times, counting from 1 to 5.
---

**4. What would you change if you wanted the loop to run 10 times?**

I would change for i in {1..5} to for i in {1..10} to make the loop count from 1 to 10.
---

# Task 6 — Files & Conditionals: File Validation Script

## Goal

Use file checks and conditionals to verify whether files and directories exist.

### Evidence

#### Screenshot 1 — Output of `ls -lah ../test-folder`

<img width="968" height="178" alt="image" src="https://github.com/user-attachments/assets/8def7fda-847d-41c3-ad76-e2336d60c178" />

---

#### Screenshot 2 — Content of `file-check.sh`

<img width="827" height="497" alt="image" src="https://github.com/user-attachments/assets/96c53c8b-1c3e-4043-98a7-9ff49ff567b6" />

---

#### Screenshot 3 — Output of `./file-check.sh`

<img width="837" height="187" alt="image" src="https://github.com/user-attachments/assets/f8537309-45df-4167-895d-dd8c7fe7a921" />

---

### Notes

Answer the following in your own words:

**1. What does `-d` check in Bash?**

The -d condition checks whether the specified path exists and is a directory.
---

**2. What does `-f` check in Bash?**

The -f condition checks whether the specified path exists and is a regular file.
---

**3. Why should file and directory paths be stored in variables?**

Variables make file paths easier to manage and reuse. If a path changes, we can update the variable instead of modifying it everywhere in the script.
---

**4. What happens if the file does not exist?**

The -f condition returns false, and the script executes the else block, displaying a message that the file was not found.
---

# Task 7 — Conditionals: Pass or Retry Script

## Goal

Use if-else conditionals to make decisions based on a variable value.

### Evidence

#### Screenshot 1 — Content of `score-check.sh` with `score=85`

<img width="743" height="350" alt="image" src="https://github.com/user-attachments/assets/4c0a1c1d-f345-4a4b-84db-50d56609f299" />

---

#### Screenshot 2 — Output showing `Result: Pass`

<img width="1015" height="152" alt="image" src="https://github.com/user-attachments/assets/aed0b071-0eec-4b0e-a187-ca3e86c84193" />

---

#### Screenshot 3 — Content of `score-check.sh` with `score=55`

<img width="832" height="362" alt="image" src="https://github.com/user-attachments/assets/575505aa-823d-40b7-9dac-98cb9a50b681" />

---

#### Screenshot 4 — Output showing `Result: Retry`

<img width="900" height="166" alt="image" src="https://github.com/user-attachments/assets/7b010372-ac6c-4d8e-b8d0-6de6d29af6ca" />

---

### Notes

Answer the following in your own words:

**1. What is the purpose of if-else in Bash?**

The if-else statement allows a script to make decisions based on whether a condition is true or false. It executes different commands depending on the result.


---

**2. What does `-ge` mean?**

The -ge operator means “greater than or equal to.” For example, [ "$score" -ge 60 ] checks whether the score is at least 60.
---

**3. Why should conditions be tested with different values?**

Testing different values helps confirm that the script behaves correctly in different situations, including when a condition is true and when it is false.
---

**4. How can conditionals help in automation scripts?**

Conditionals help automation scripts make decisions automatically, such as checking whether a file exists, validating a score, or deciding whether a task should continue or stop.
---

# Task 8 — Functions: Final Bash Automation Script

## Goal

Create a final Bash script using functions to organize reusable code.

### Evidence

#### Screenshot 1 — Content of `final-automation.sh`

<img width="1006" height="551" alt="image" src="https://github.com/user-attachments/assets/c22d7ea0-44da-439b-b15b-211cfbed9a51" />

---

#### Screenshot 2 — Output of `./final-automation.sh`

<img width="905" height="321" alt="image" src="https://github.com/user-attachments/assets/ce0954c5-7894-41d9-8194-f8499d459ba6" />

---

#### Screenshot 3 — Output of `ls -lah` showing all created scripts

<img width="781" height="320" alt="image" src="https://github.com/user-attachments/assets/e7bdf1be-c7e7-4d8e-844d-f446a5842a97" />

---

### Notes

Answer the following in your own words:

**1. What is a function in Bash?**

A function is a reusable block of commands that performs a specific task. It helps organize a script and avoid repeating the same code.
---

**2. Why are functions useful in scripts?**

Functions make scripts easier to read, maintain, reuse, and debug. They divide a large script into smaller, manageable tasks.
---

**3. Which functions did you create in this script?**

I created three functions: show_tools(), check_directory(), and check_score(). They display the DevOps tools, check whether the test directory exists, and check whether the score is passing.


---

**4. How does this final script combine variables, arrays, loops, conditionals, files, and functions?**

The final script uses variables to store personal information, an array to store DevOps tools, a loop to display each tool, conditionals to check directory existence and score, and functions to organize the tasks. Together, these concepts automate multiple operations in a single script.
---

# LinkedIn Post (Required)

## Evidence

#### LinkedIn Post URL

Paste your LinkedIn post URL here:

[`Add your URL here`
](https://www.linkedin.com/posts/mr-zack01_devops-bashscripting-linux-share-7516389101583945728-GuQ1/?utm_source=share&utm_medium=member_desktop&rcm=ACoAAGxq6h8BmFdxEjgZsRCQ-jggJncjMKLdHOk)
---

#### Screenshot — Published LinkedIn post

<img width="1031" height="892" alt="image" src="https://github.com/user-attachments/assets/d6aceaa7-d174-48c0-b321-5dcc516892d8" />

---

# Submission Instructions

- Add all required screenshots in your submission
- Full name must be visible in required screenshots
- All script files must be created and run successfully
- Required notes must be answered clearly for every task
- Do not expose sensitive information (keys, passwords, credentials)

---

# Completion Checklist

- [✅] Task 1: Environment setup verified, workspace created (Screenshots 1–2, Notes answered)
- [✅] Task 2: First script created, executed, permissions verified (Screenshots 1–3, Notes answered)
- [✅] Task 3: Variables script created and run (Screenshots 1–2, Notes answered)
- [✅] Task 4: Arrays and loops script created and run (Screenshots 1–2, Notes answered)
- [✅] Task 5: Counter loop script created and run (Screenshots 1–2, Notes answered)
- [✅] Task 6: File validation script created and run (Screenshots 1–3, Notes answered)
- [✅] Task 7: Pass/Retry conditional script tested with both values (Screenshots 1–4, Notes answered)
- [✅] Task 8: Final automation script created and run (Screenshots 1–3, Notes answered)
- [✅] All scripts run without errors
- [✅] Full Name visible in all required screenshots
- [✅] LinkedIn post published and URL submitted
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
