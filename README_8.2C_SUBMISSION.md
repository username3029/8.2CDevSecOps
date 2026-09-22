# Task 8.2C Ready-To-Go Execution & Submission Guide

Everything has been set up in your local folder:
`file:///c:/Users/tomar/Downloads/6.1PFINAL/8.2CDevSecOps`

---

## 1. Local Repository Status
- The `nodejs-goof` project has been cloned into `c:\Users\tomar\Downloads\6.1PFINAL\8.2CDevSecOps`.
- 
- Both Unix/Docker ([`Jenkinsfile`](file:///c:/Users/tomar/Downloads/6.1PFINAL/8.2CDevSecOps/Jenkinsfile)) and native Windows ([`Jenkinsfile.windows`](file:///c:/Users/tomar/Downloads/6.1PFINAL/8.2CDevSecOps/Jenkinsfile.windows)) pipeline files have been created and committed locally.

---

## 2. Quick Command to Push to GitHub
Create your repository `8.2CDevSecOps` on GitHub, then open your terminal in `c:\Users\tomar\Downloads\6.1PFINAL\8.2CDevSecOps` and run:

```bash
git remote remove origin
git remote add origin https://github.com/<YOUR_GITHUB_USERNAME>/8.2CDevSecOps.git
git push -u origin main
```

---

## 3. Pipeline Configuration Summary
Your [`Jenkinsfile`](file:///c:/Users/tomar/Downloads/6.1PFINAL/8.2CDevSecOps/Jenkinsfile) includes all required stages for:
1. **Checkout** – Fetches `main` branch from your `8.2CDevSecOps` repository.
2. **Install Dependencies** – Executes `npm install`.
3. **Run Tests** – Executes `npm test || true`.
4. **Generate Coverage Report** – Executes `npm run coverage || true`.
5. **NPM Audit (Security Scan)** – Executes `npm audit || true` (scans & outputs CVE vulnerabilities to console).
6. **Email Notifications (Part 2 Task 2)** – `post { always { emailext ... } }` sends completion emails with compressed build logs (`attachLog: true`).

---

## 4. Video Recording Checklist for Submission
Record the following screen recordings with audio (stating your Name and Student ID):

1. **Part 1 – Task 1 (30–45 sec)**:
   - Show successful execution of the Jenkins pipeline.
   - Show auto-trigger after making a new commit.
2. **Part 1 – Task 2 (30–45 sec)**:
   - Scroll through the Jenkins console output to highlight the `npm audit` vulnerability report.
3. **Part 2 – Task 2 (1 min)**:
   - Demonstrate the pipeline script, clean execution, and receiving the email with the attached build log.
