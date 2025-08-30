# Gemini Custom Slash Commands

This repository contains **custom slash commands** for [Gemini CLI](https://cloud.google.com/gemini/docs/codeassist/gemini-cli) aimed at **Vibe Coding** projects, including Angular, Tailwind v4, accessibility, and more. These commands are designed to **boost productivity, enforce best practices, and prevent common AI hallucinations** in evolving frameworks.  

---

## 📦 Repository Structure
gemini-custom-slash-commands/
```
├─ commands/ # TOML definitions of custom slash commands
│ ├─ audit_accessibility.toml
│ ├─ audit_tailwind_v4.toml
│ ├─ audit_angular.toml
│ └─ guard_tailwind_v4.toml
├─ examples/ # Example usage outputs
├─ README.md
```

---

## ⚡ Features

- **/audit-accessibility** – Full WCAG 2.2 audit with semantic HTML, ARIA, keyboard navigation, screen reader support, and contrast checks. Produces a detailed analysis + actionable task list.  
- **/audit-tailwind_v4** – Audit Tailwind v4 projects for best practices, deprecated v3 utilities, design consistency, and CSS layering. Uses Brave and Context7 MCPs for fact-checking. Produces a detailed analysis + actionable task list.
- **/audit-angular** – Angular code audit based on Angular CLI MCP best practices: performance, modern patterns, and maintainability. Produces a detailed analysis + actionable task list.
- **/guard-tailwind_v4** – Prevents hallucination of v3 patterns. Ensures all Tailwind v4 guidance is verified via official docs or trusted MCPs.
- **/self-reflect** - Reflect on my VibeCoding journey logs (chat history), detect repeated patterns, and propose rules to improve. Produces a detailed analysis + actionable task list.
---

## 📌 How to Use

1. Copy the `.toml` command files into your `.gemini/commands` folder (if commands folder doesn't exist, create it).  
2. Open Gemini and use command starting with `/` (for each change to these commands, you should restart Gemini).  
3. Complete usage examples:  
   ```bash
   /audit-accessibility --output ./audit-reports/accessibility-$(date +%F-%H%M).md
   /audit-tailwind_v4 --output ./audit-reports/tailwind-v4-$(date +%F-%H%M).md
   /audit-angular --output ./audit-reports/angular-$(date +%F-%H%M).md
   /guard-tailwind_v4

4. Reports are output in Markdown format, ready to save or integrate into project documentation.  

---

## 🧠 Vibe Coding Integration

These commands are designed to fit your **Vibe Coding workflow**:  

- Combine **experiments + community sharing**: audit outputs can be used to generate articles or blog posts.  
- **Prevent repetition**: guard commands reduce errors when AI misaligns with evolving libraries.  
- **Anchored in reality**: Brave MCP and Context7 are used to fetch live docs to avoid hallucinations.  

---

## 💡 Contribution

- Feel free to add new slash commands for other frameworks or tools.  
- Follow the same TOML format and clearly document **purpose, prompt, and output**.  
- Open a pull request and include example outputs in `examples/`.  

---

## 📜 License

MIT License — free to use, modify, and adapt for your Vibe Coding projects.  

