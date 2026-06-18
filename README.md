# ☁️ Cloud-Based Blogging Platform with Automated CI/CD Deployment

> A mini-project for the Cloud Computing course — Third Year IT Engineering  
> **Author:** Aayush Abhyankar | **Deployed on:** Azure Static Web Apps

🌐 **Live Site:** [https://kind-desert-0fa242a00.7.azurestaticapps.net](https://kind-desert-0fa242a00.7.azurestaticapps.net)

![Deploy to Azure](https://github.com/4yu-san/cloud-blog/actions/workflows/deploy.yml/badge.svg)
![Azure Static Web Apps](https://img.shields.io/badge/Azure-Static%20Web%20Apps-0078D4?logo=microsoftazure)
![License](https://img.shields.io/badge/license-MIT-green)

---

## 📋 Table of Contents

- [Project Overview](#-project-overview)
- [Objectives](#-objectives)
- [Technologies Used](#-technologies-used)
- [Features](#-features)
- [Project Structure](#-project-structure)
- [Architecture](#-architecture)
- [CI/CD Workflow](#-cicd-workflow)
- [Deployment Steps](#-deployment-steps)
- [Future Scope](#-future-scope)
- [Viva Reference](#-viva-reference)

---

## 📖 Project Overview

This project is a **cloud-hosted static blogging platform** built with plain HTML and CSS,
version-controlled on GitHub, and automatically deployed to **Microsoft Azure Static Web Apps**
via a **GitHub Actions** CI/CD pipeline.

The blog contains three technical posts on Linux, Docker, and Cloud Computing — topics covered
in the IT engineering curriculum. Every push to the `main` branch triggers an automatic
deployment, demonstrating a real-world DevOps workflow at minimal cost (Azure free tier).

---

## 🎯 Objectives

| # | Objective |
|---|-----------|
| 1 | Demonstrate cloud computing concepts through a working deployment |
| 2 | Implement a CI/CD pipeline using GitHub Actions |
| 3 | Host a static website on Azure Static Web Apps |
| 4 | Apply version control best practices using Git and GitHub |
| 5 | Understand the flow from developer commit to live production website |

---

## 🛠️ Technologies Used

| Technology | Role | Category |
|---|---|---|
| **HTML5** | Website structure and content | Frontend |
| **CSS3** | Dark theme styling, responsive layout | Frontend |
| **Git** | Version control | DevOps |
| **GitHub** | Remote repository hosting | DevOps |
| **GitHub Actions** | CI/CD pipeline automation | DevOps |
| **Azure Static Web Apps** | Cloud hosting + global CDN | Cloud |
| **Azure CDN** | Content delivery to users worldwide | Cloud |

---

## ✨ Features

- **Dark theme** responsive UI — mobile, tablet, and desktop friendly
- **3 blog posts** covering Linux, Docker, and Cloud Computing
- **Automated CI/CD** — push to `main` → site goes live automatically
- **PR Preview Environments** — every pull request gets its own preview URL
- **Global CDN delivery** via Azure — fast load times worldwide
- **Zero cost** hosting on Azure Static Web Apps free tier
- **No backend or database** required — fully static architecture

---

## 📁 Project Structure

```
cloud-blog/
│
├── .github/
│   └── workflows/
│       └── deploy.yml          ← GitHub Actions CI/CD pipeline
│
├── blog/
│   ├── linux-journey.html      ← Blog Post 1: My Journey Learning Linux
│   ├── docker-getting-started.html  ← Blog Post 2: Getting Started with Docker
│   └── cloud-computing-intro.html   ← Blog Post 3: Introduction to Cloud Computing
│
├── css/
│   └── style.css               ← Complete stylesheet (dark theme, responsive)
│
├── images/                     ← Static image assets
│
├── index.html                  ← Homepage (hero, posts, footer)
├── about.html                  ← About page (Aayush Abhyankar)
└── README.md                   ← This file
```

---

## 🏗️ Architecture

### System Architecture Diagram

```
┌─────────────────────────────────────────────────────────────┐
│                        DEVELOPER SIDE                        │
│                                                              │
│   ┌──────────────┐    git push     ┌──────────────────────┐ │
│   │  Local Code  │ ─────────────→  │   GitHub Repository  │ │
│   │  (VS Code)   │                 │   (Source of Truth)  │ │
│   └──────────────┘                 └──────────┬───────────┘ │
│                                               │             │
│                                    Triggers workflow        │
│                                               │             │
│                                    ┌──────────▼───────────┐ │
│                                    │   GitHub Actions      │ │
│                                    │   CI/CD Pipeline      │ │
│                                    │                       │ │
│                                    │  1. Checkout code     │ │
│                                    │  2. Validate files    │ │
│                                    │  3. Deploy to Azure   │ │
│                                    │  4. Print summary     │ │
│                                    └──────────┬───────────┘ │
└───────────────────────────────────────────────┼─────────────┘
                                                │
                                    Deploys to cloud
                                                │
┌───────────────────────────────────────────────┼─────────────┐
│                      AZURE CLOUD              │              │
│                                    ┌──────────▼───────────┐ │
│                                    │  Azure Static Web    │ │
│                                    │  Apps (Origin)       │ │
│                                    └──────────┬───────────┘ │
│                                               │             │
│                                    Distributed via CDN      │
│                                               │             │
│              ┌────────────────────────────────┼──────────┐  │
│              │         Azure CDN Edge Network            │  │
│              │  (Mumbai) (London) (New York) (Singapore) │  │
│              └────────────────────────────────┬──────────┘  │
└───────────────────────────────────────────────┼─────────────┘
                                                │
                                    Served to user
                                                │
┌───────────────────────────────────────────────┼─────────────┐
│                       USER SIDE               │              │
│                                    ┌──────────▼───────────┐ │
│                                    │    User's Browser    │ │
│                                    │  (Loads CloudBlog)   │ │
│                                    └──────────────────────┘ │
└─────────────────────────────────────────────────────────────┘
```

### Component Responsibilities

| Component | Responsibility |
|---|---|
| **GitHub Repository** | Stores all source code; single source of truth |
| **GitHub Actions** | Detects push events; runs the deployment pipeline |
| **Azure Static Web Apps** | Hosts the site files; provides HTTPS and custom domain |
| **Azure CDN** | Caches and serves files from edge servers close to users |
| **User Browser** | Requests and renders the HTML/CSS from the nearest CDN node |

---

## 🔄 CI/CD Workflow

```
Developer writes code
        │
        ▼
git add . && git commit -m "update"
        │
        ▼
git push origin main
        │
        ▼
GitHub detects push event
        │
        ▼
GitHub Actions runner (ubuntu-latest) starts
        │
        ├── Step 1: Checkout repository code
        │
        ├── Step 2: Validate all HTML/CSS files exist
        │
        ├── Step 3: Azure/static-web-apps-deploy@v1
        │           └── Zips files → Uploads to Azure → CDN propagates
        │
        └── Step 4: Print deployment summary to logs
                │
                ▼
        Site is LIVE at your Azure URL
        (typically within 1–2 minutes)
```

### Workflow Triggers

| Trigger | Action |
|---|---|
| Push to `main` | Full production deployment |
| Pull request opened | Preview environment created at temporary URL |
| Pull request closed | Preview environment automatically removed |

---

## 🚀 Deployment Steps

### Prerequisites
- GitHub account
- Microsoft Azure account (free tier is sufficient)
- Git installed on your machine

---

### Step 1 — Create GitHub Repository

```bash
# Initialise git in your project folder
git init

# Add all files
git add .

# First commit
git commit -m "Initial commit: Cloud Blog project"

# Add your GitHub remote (replace with your URL)
git remote add origin https://github.com/<YOUR_USERNAME>/cloud-blog.git

# Push to GitHub
git push -u origin main
```

---

### Step 2 — Create Azure Static Web App

1. Go to [portal.azure.com](https://portal.azure.com) and sign in
2. Click **"Create a resource"** → search **"Static Web App"**
3. Click **Create** and fill in:
   - **Subscription:** Free Trial (or your subscription)
   - **Resource Group:** Create new → `cloud-blog-rg`
   - **Name:** `cloud-blog-aayush`
   - **Plan type:** Free
   - **Region:** East Asia (or closest to you)
4. Under **Deployment details:**
   - **Source:** GitHub
   - Click **"Sign in with GitHub"** and authorise Azure
   - **Organisation:** your GitHub username
   - **Repository:** `cloud-blog`
   - **Branch:** `main`
5. Under **Build details:**
   - **Build Presets:** Custom
   - **App location:** `/`
   - **Output location:** *(leave blank)*
6. Click **Review + Create** → **Create**

---

### Step 3 — Azure Connects to GitHub Automatically

After creation, Azure will:
- Add `AZURE_STATIC_WEB_APPS_API_TOKEN` as a secret to your GitHub repo automatically
- Commit a `deploy.yml` workflow file to your repo (you can replace it with ours)
- Trigger the first deployment immediately

---

### Step 4 — Verify Deployment

1. Go to your GitHub repository → **Actions** tab
2. You should see a workflow run in progress (yellow dot) or completed (green tick)
3. Click the run to see the logs for each step
4. Once complete, go back to Azure Portal → your Static Web App
5. Click the **URL** shown on the overview page — your blog is live!

---

### Step 5 — Test CI/CD

Make a small change to verify the pipeline works end-to-end:

```bash
# Make a visible change (e.g. edit the hero text in index.html)
# Then push it
git add .
git commit -m "test: verify CI/CD pipeline"
git push origin main
```

Watch the **Actions** tab in GitHub — a new workflow run starts automatically.
Within 1–2 minutes, the change will be live on your Azure URL.

---

## 🔮 Future Scope

| Enhancement | Description |
|---|---|
| **Search functionality** | Add client-side search using a JSON index |
| **Dark/Light toggle** | Allow users to switch themes via CSS variables |
| **Comments system** | Integrate Giscus (GitHub Discussions-based comments) |
| **More blog posts** | Expand to cover Kubernetes, Azure Functions, Terraform |
| **Custom domain** | Connect a custom domain name via Azure DNS |
| **Analytics** | Add privacy-friendly analytics (e.g. Umami) |
| **RSS Feed** | Generate an RSS feed for subscribers |
| **PWA Support** | Add a service worker for offline reading |

---

## 📚 Viva Reference

**Key terms to know:**

- **CI/CD** — Continuous Integration / Continuous Deployment. Automates building, testing, and deploying code.
- **Static Web App** — A website with no server-side processing; files are served directly from a CDN.
- **CDN** — Content Delivery Network. Serves files from servers geographically close to the user.
- **GitHub Actions** — A CI/CD platform built into GitHub, triggered by repository events.
- **IaaS / PaaS / SaaS** — Infrastructure / Platform / Software as a Service (cloud service models).
- **Azure** — Microsoft's public cloud platform offering 200+ services.
- **YAML** — Human-readable data format used to write GitHub Actions workflows.

---

## 📄 License

This project is submitted as an academic mini-project for the Cloud Computing course,
Third Year IT Engineering.

**© 2025 Aayush Abhyankar**
