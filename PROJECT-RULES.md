# **Project Context & Rules**

This file provides context for the Antigravity AI editor to ensure codebase consistency and accurate command generation.

## **Project Architecture**

* **Type:** HubSpot CMS Theme (Component-based architecture).  
* **Not an App:** This is NOT a React UI Extension or serverless app. Do not generate configurations for hsproject.json.  
* **Local Source Path:** src/theme/kdock  
* **Remote Destination Name:** kdock-theme  
* **Languages:** HubL (HubSpot Markup Language), standard HTML, CSS (using CSS variables), Vanilla JavaScript.

## **CLI Command Guardrails**

**CRITICAL:** The AI must only suggest modern HubSpot CMS CLI commands (v8+).

* **DO NOT USE:** hs project dev, hs project watch, hs project upload.  
* **USE INSTEAD:**  
  * Live Sync: npx hs cms watch src/theme/kdock kdock-theme  
  * Manual Upload: npx hs cms upload src/theme/kdock kdock-theme  
  * Fetch from HubSpot: npx hs cms fetch kdock-theme src/theme/kdock

## **Git Workflow**

* Feature branching model: feature/\[feature-name\]  
* main is the Source of Truth.  
* All code is tested in personal HubSpot developer sandboxes before merging.

## **Development Standards**

* **CSS:** Use root variables (var(--color-primary)) defined in styles.css.  
* **HubL:** Ensure {{ standard\_header\_includes }} and {{ standard\_footer\_includes }} are present in all master layout files. Use {{ require\_css(...) }} for stylesheet linking.  
* **Modules:** Keep module logic encapsulated within their respective .module folders (containing module.html, module.css, module.js, and fields.json).
