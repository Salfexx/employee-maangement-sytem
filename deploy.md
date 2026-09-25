# 🚀 Deployment Guide: GitHub & Vercel

This guide provides step-by-step instructions to push the **Employee Management System (EMS)** to **GitHub** and deploy it to **Vercel** for a free, high-performance, and publicly accessible HTTPS URL.

---

## 📋 Table of Contents
1. [Prerequisites](#1-prerequisites)
2. [Step 1: Push Project to GitHub](#2-step-1-push-project-to-github)
3. [Step 2: Deploy to Vercel](#3-step-2-deploy-to-vercel)
   - [Method A: Vercel Web Dashboard (Recommended)](#method-a-vercel-dashboard-import-recommended)
   - [Method B: Deploy via Vercel CLI](#method-b-deploy-via-vercel-cli)
4. [Automatic CI/CD (Continuous Deployment)](#4-automatic-cicd-continuous-deployment)
5. [Custom Domain Setup (Optional)](#5-custom-domain-setup-optional)
6. [Troubleshooting & FAQs](#6-troubleshooting--faqs)

---

## 1. Prerequisites

Before starting, ensure you have:
- A [GitHub](https://github.com/) account (e.g. `https://github.com/Salfexx`).
- A [Vercel](https://vercel.com/) account (you can sign up for free using your GitHub account).
- **Git** installed on your system (already verified on your machine).
- Project files ready:
  - `index.html` (primary web entry point)
  - `Employee Management system.html` (standalone copy)
  - `vercel.json` (routing and clean URL configuration)
  - `.gitignore` (ignores `.vercel`, system logs, and temporary files)
  - `README.md` (project documentation)

---

## 2. Step 1: Push Project to GitHub

### A. Create a New Repository on GitHub
1. Open your browser and navigate to: **[github.com/new](https://github.com/new)**.
2. Enter the **Repository name**: e.g., `employee-management-system`.
3. Choose **Public** or **Private** based on your preference.
4. **Leave unchecked**: *"Add a README file"*, *"Add .gitignore"*, and *"Choose a license"* (we already created these files locally).
5. Click **Create repository**.

### B. Initialize and Push from Your Terminal
Open PowerShell or Command Prompt in the project folder (`d:\AI\Employee Management system`) and run:

```bash
# 1. Initialize local git repository
git init -b main

# 2. Add all project files
git add .

# 3. Commit the changes
git commit -m "Initial commit: Employee Management System (EMS)"

# 4. Link to your GitHub remote repository
# (Replace 'Salfexx' and repository name if different)
git remote add origin https://github.com/Salfexx/employee-management-system.git

# 5. Push your code to GitHub
git push -u origin main
```

> [!TIP]
> If Windows prompts you to authenticate, sign in via the browser popup with your GitHub account or use a GitHub Personal Access Token (PAT).

---

## 3. Step 2: Deploy to Vercel

You can deploy using either the **Vercel Dashboard** (easiest, provides automatic updates on git push) or the **Vercel CLI**.

### Method A: Vercel Dashboard Import (Recommended)

1. Go to **[vercel.com](https://vercel.com)** and log in with your GitHub account.
2. In your Vercel Dashboard, click the **"Add New..."** button (top right) and select **"Project"**.
3. Under **"Import Git Repository"**, locate `employee-management-system` and click **"Import"**.
4. Configure Project settings:
   - **Project Name**: `employee-management-system` (or custom name).
   - **Framework Preset**: Select **"Other"**.
   - **Root Directory**: `./` (leave default).
   - **Build and Output Settings**: Leave empty / default (this is a static HTML/JS site, no build step required).
5. Click **"Deploy"**.
6. In ~15–30 seconds, your site will be live with a production URL like:
   ```text
   https://employee-management-system-xxxx.vercel.app
   ```

---

### Method B: Deploy via Vercel CLI

If you prefer deploying directly from your terminal:

1. Open PowerShell in `d:\AI\Employee Management system`.
2. Run the deployment command via `npx`:
   ```bash
   npx vercel
   ```
3. Follow the interactive prompts:
   - **Set up and deploy?** Type `y` and press Enter.
   - **Which scope?** Choose your personal account.
   - **Link to existing project?** Type `n` (first time) or `y`.
   - **What's your project's name?** Press Enter for `employee-management-system`.
   - **In which directory is your code located?** Press Enter for `./`.
   - Auto-detected settings will be applied.
4. When deployment completes, you'll receive a **Preview URL**.
5. To deploy straight to **Production**:
   ```bash
   npx vercel --prod
   ```

---

## 4. Automatic CI/CD (Continuous Deployment)

When deployed via **Method A (GitHub Integration)**:
- Every time you run `git push origin main`, Vercel **automatically rebuilds and deploys** the newest version of your site.
- If you create branches or Pull Requests, Vercel automatically generates **Preview Environments** with unique URLs for testing before merging.

---

## 5. Custom Domain Setup (Optional)

To link your own custom domain (e.g., `ems.yourdomain.com`):
1. In your Vercel Dashboard, navigate to your project.
2. Go to **Settings > Domains**.
3. Enter your domain name and click **Add**.
4. Follow the DNS instructions (CNAME or A record pointing to Vercel).
5. Vercel automatically provisions and renews a free **SSL certificate (HTTPS)**.

---

## 6. Troubleshooting & FAQs

### Q: Why is `vercel.json` included?
**A:** `vercel.json` contains:
```json
{
  "cleanUrls": true,
  "rewrites": [
    { "source": "/(.*)", "destination": "/index.html" }
  ]
}
```
This ensures:
- Clean URLs without needing `.html` extensions.
- All requests route seamlessly to `index.html` as a single-page application.

### Q: Git push asks for username/password and rejects it?
**A:** GitHub deprecated password authentication for Git over HTTPS. Use one of these:
1. **GitHub Git Credential Manager** (recommended, logs in via browser).
2. **Personal Access Token (PAT)**:
   - Go to [GitHub Settings > Developer settings > Personal access tokens > Tokens (classic)](https://github.com/settings/tokens).
   - Generate a token with `repo` scope.
   - Use the token as your password when pushing.

### Q: Can I update the website later?
**A:** Yes! Just edit your local files, then run:
```bash
git add .
git commit -m "Update website features"
git push
```
Vercel will detect the push and update your live site within seconds!
