# **Developer Handoff & Architecture Guide**

**Lead Developer:** Brenn

**Project:** Kdock HubSpot CMS Theme

Welcome to the command center, Brenn. Kevin has successfully established the foundational architecture, resolved the CLI environment configuration, and merged the base global CSS into the repository.

You are now in the driver's seat. This document is your single source of truth for the project workflow, CLI commands, and HubSpot references.

## **1\. System Architecture**

We are using an enterprise-grade, multi-sandbox architecture to ensure no code is overwritten and the live site remains completely safe.

* **The Source of Truth:** The main branch on our GitHub repository.  
* **The Workbenches:** Individual HubSpot Sandboxes (you are targeting kdock-dev-brenn).  
* **The Golden Rule:** We never write code directly in the live production account. We write locally, sync to our personal sandboxes for testing, merge to GitHub, and deploy to live only when finished.

## **2\. The Daily Developer Loop**

Whenever you sit down to build a new module or template, follow this exact sequence:

### **Step 1: Sync & Branch**

Always start with the latest blueprint and create an isolated workspace.

git checkout main  
git pull origin main  
git checkout \-b feature/name-of-your-feature

### **Step 2: Start the Engine**

**Crucial Note:** We are building a standard CMS Theme. Do not use hs project commands. Only use hs cms commands.

Run this to sync your local files to your personal sandbox in real-time:

npx hs cms watch src/theme/kdock kdock-theme

*(Leave this terminal tab running while you work\!)*

### **Step 3: Code & Preview**

1. Write your HTML/CSS/JS in Antigravity and hit save.  
2. The terminal will instantly beam the file to your sandbox.  
3. Open a "Test Page" in your HubSpot Sandbox browser (kdock-dev-brenn), set it to use the Kdock Theme, and hit refresh to see your live changes.

### **Step 4: Commit & Merge**

When the feature is done:

git add .  
git commit \-m "feat: description of what you built"  
git push origin feature/name-of-your-feature

Open a Pull Request on GitHub to merge it into main.

## **3\. Your Current Mission: Base Layout**

You are currently building the base Canvas (the master HTML layout).

1. Ensure your watcher is running (npx hs cms watch src/theme/kdock kdock-theme).  
2. Create or open the file: src/theme/kdock/templates/base.html  
3. Paste in this standard HubL skeleton:

\<\!doctype html\>  
\<html lang="en"\>  
  \<head\>  
    \<meta charset="utf-8"\>  
    \<meta name="viewport" content="width=device-width, initial-scale=1"\>  
    \<title\>{{ page\_meta.name }}\</title\>  
    \<meta name="description" content="{{ page\_meta.meta\_description }}"\>  
      
    {\# Required by HubSpot \#}  
    {{ standard\_header\_includes }}  
      
    {\# Links Kevin's global CSS \#}  
    {{ require\_css(get\_asset\_url("../styles/styles.css")) }}  
  \</head\>  
  \<body\>  
      
    \<header\>  
      \<\!-- Global header goes here \--\>  
      \<h2\>Header Placeholder\</h2\>  
    \</header\>

    \<main class="body-wrapper"\>  
      {\# The injection zone for individual page content \#}  
      {% block body %}  
      {% endblock body %}  
    \</main\>

    \<footer\>  
      \<\!-- Global footer goes here \--\>  
      \<p\>Footer Placeholder\</p\>  
    \</footer\>

    {\# Required by HubSpot \#}  
    {{ standard\_footer\_includes }}  
  \</body\>  
\</html\>

4. Save the file.  
5. Create a test page in your HubSpot sandbox using this template to verify the CSS and layout are rendering.

## **4\. Emergency CLI Commands**

If the CLI ever gets stuck or stops watching, run this "Nuclear Reset" to clear the NPM cache and grab the newest tools:

rm \-rf node\_modules package-lock.json  
npm cache clean \--force  
npm install @hubspot/cli@latest

To manually force an upload of the entire theme to your sandbox:

npx hs cms upload src/theme/kdock kdock-theme

## **5\. HubL & CMS Documentation Hub**

Keep these bookmarked. As of 2026, HubSpot uses modern HubL and component-based theme architecture. These are your cheat sheets:

* **HubL Supported Variables & Macros:** [HubSpot HubL Reference](https://developers.hubspot.com/docs/cms/hubl/variables)  
* **Building Custom Modules:** [Modules Documentation](https://developers.hubspot.com/docs/cms/building-blocks/modules)  
* **Theme theme.json Configuration:** [Theme Settings & Config](https://www.google.com/search?q=https://developers.hubspot.com/docs/cms/building-blocks/themes/theme-json)  
* **CLI CMS Commands (hs cms):** [HubSpot CLI Reference](https://www.google.com/search?q=https://developers.hubspot.com/docs/cms/developer-tooling/local-development-cli)