<div align="center">

# React TypeScript i18next Localization Skill

### A production-ready AI agent skill for adding clean English/Turkish localization to React + TypeScript apps.

Turn hardcoded English UI text into a scalable, maintainable, type-friendly `i18next` localization setup — faster, cleaner, and with better AI agent results.

<br />

![React](https://img.shields.io/badge/React-20232A?style=for-the-badge&logo=react&logoColor=61DAFB)
![TypeScript](https://img.shields.io/badge/TypeScript-3178C6?style=for-the-badge&logo=typescript&logoColor=white)
![i18next](https://img.shields.io/badge/i18next-26A69A?style=for-the-badge&logo=i18next&logoColor=white)
![AI Agents](https://img.shields.io/badge/AI_Agents-111827?style=for-the-badge&logo=openai&logoColor=white)
![License](https://img.shields.io/badge/License-MIT-green?style=for-the-badge)

<br />

· [🚀 Quick Start](#-quick-start) · [📁 Structure](#-recommended-project-structure) · [🧠 Agent Prompt](#-recommended-agent-prompt)

</div>

---

## ✨ What is this?

**React TypeScript i18next Localization Skill** is a ready-to-use Markdown skill designed for AI coding agents.

It helps your agent convert a React + TypeScript application from hardcoded English UI text into a clean bilingual localization system using:

- `i18next`
- `react-i18next`
- English locale files
- Turkish locale files
- semantic translation keys
- clean `t("key.path")` usage
- optional language switcher
- scalable folder structure

Instead of giving your AI agent a vague instruction like:

> “Make this app Turkish.”

You give it a clear, reusable skill that explains exactly how localization should be done.

---

## 🎯 Why use this skill?

AI agents can translate text, but they often make messy changes:

- hardcoded Turkish strings inside components
- inconsistent translation keys
- broken layouts
- missing English fallback text
- mixed Turkish/English UI
- duplicated translations
- unnecessary refactors
- changed business logic

This skill gives the agent strict rules so it can localize your app more safely and professionally.

---

## 🚀 Features

- ✅ Converts hardcoded English UI text into `t()` keys
- ✅ Adds English and Turkish translation files
- ✅ Uses clean semantic translation keys
- ✅ Supports React + TypeScript projects
- ✅ Recommends `i18n.ts` for TypeScript apps
- ✅ Includes language switcher guidance
- ✅ Handles interpolation and pluralization rules
- ✅ Explains when to use `<Trans />`
- ✅ Keeps existing UI and business logic unchanged
- ✅ Works with most Markdown-based AI agent skill systems

---

## 🧠 Best for

This skill is useful for:

- React TypeScript apps
- SaaS dashboards
- admin panels
- portfolio projects
- startup MVPs
- student projects
- AI coding workflows
- English-to-Turkish localization
- apps that need future multi-language support

---

## 📦 Quick Start

### 1. Download or copy the skill file

Use the skill file in this repository:

```txt
react-i18next-localization-skill.md
```

You can rename it depending on your agent/tool convention:

```txt
SKILL.md
```

or:

```txt
react-i18next-localization.md
```

---

### 2. Add it to your AI agent skills folder

Example structure:

```txt
skills/
  react-i18next-localization/
    SKILL.md
```

If your agent uses a different convention, place the Markdown content wherever your agent reads custom instructions, skills, rules, or project knowledge.

---

### 3. Ask your AI agent to apply it

Use this prompt:

```txt
Use the React TypeScript i18next Localization Skill.
Convert this React TypeScript app from hardcoded English UI text to i18next-based English/Turkish localization.
Preserve all existing design and functionality.
Create clean translation keys, add en/tr locale files, add a language switcher, and make sure there are no remaining hardcoded visible English UI strings.
Prefer i18n.ts instead of i18n.js if the project is fully TypeScript.
```

---

## 📁 Recommended Project Structure

The skill encourages a clean structure like this:

```txt
src/
  i18n/
    i18n.ts
    locales/
      en/
        common.json
        auth.json
        dashboard.json
        settings.json
      tr/
        common.json
        auth.json
        dashboard.json
        settings.json
```

This keeps translations organized and easy to scale as your application grows.

---

## 🛠 Recommended Packages

For a standard React + TypeScript app:

```bash
npm install i18next react-i18next i18next-browser-languagedetector
```

With pnpm:

```bash
pnpm add i18next react-i18next i18next-browser-languagedetector
```

With yarn:

```bash
yarn add i18next react-i18next i18next-browser-languagedetector
```

---

## 🔥 Example Transformation

### Before

```tsx
export function SaveButton() {
  return <button>Save Changes</button>;
}
```

### After

```tsx
import { useTranslation } from "react-i18next";

export function SaveButton() {
  const { t } = useTranslation("common");

  return <button>{t("buttons.saveChanges")}</button>;
}
```

### English locale

```json
{
  "buttons": {
    "saveChanges": "Save Changes"
  }
}
```

### Turkish locale

```json
{
  "buttons": {
    "saveChanges": "Değişiklikleri Kaydet"
  }
}
```

---

## 🌐 Language Switcher Example

```tsx
import { useTranslation } from "react-i18next";

export function LanguageSwitcher() {
  const { i18n } = useTranslation();

  return (
    <select
      value={i18n.language}
      onChange={(event) => i18n.changeLanguage(event.target.value)}
    >
      <option value="en">English</option>
      <option value="tr">Türkçe</option>
    </select>
  );
}
```

---

## 🧩 What the skill teaches the agent

The skill tells the agent to:

- search for hardcoded visible English UI text
- move text into locale JSON files
- create matching English and Turkish keys
- avoid translating variables, routes, API fields, and CSS classes
- use natural Turkish UI wording
- avoid literal machine translation
- preserve the existing design
- avoid unrelated refactors
- check for missing translation keys

---

## 🇹🇷 Turkish UI Translation Style

The skill prefers natural Turkish UI language:

| English | Turkish |
| --- | --- |
| Save | Kaydet |
| Cancel | İptal |
| Settings | Ayarlar |
| Profile | Profil |
| Dashboard | Panel |
| Sign in | Giriş yap |
| Sign up | Kayıt ol |
| Log out | Çıkış yap |
| Loading... | Yükleniyor... |
| Something went wrong | Bir şeyler ters gitti |
| Try again | Tekrar dene |
| Apply | Uygula |
| Confirm | Onayla |

---

## ✅ Agent Checklist

After localization, the agent should verify:

- [ ] No hardcoded visible English UI text remains
- [ ] English and Turkish locale files have matching keys
- [ ] `useTranslation()` is used correctly
- [ ] dynamic values use interpolation
- [ ] plural text uses `count`
- [ ] rich text uses `<Trans />` when needed
- [ ] language switcher works
- [ ] existing UI design is preserved
- [ ] business logic is unchanged
- [ ] TypeScript errors are fixed

---

## 🧪 Example Agent Request

```txt
Apply the React TypeScript i18next Localization Skill to this project.
Start by scanning the UI for hardcoded English text.
Create a clean i18n setup with English and Turkish JSON files.
Refactor components to use react-i18next.
Do not change the existing UI design or business logic.
```

---

## 💡 Tips for better results

For best AI agent performance:

1. Run the agent on one feature/page at a time.
2. Review generated translation keys before merging.
3. Keep namespaces small and meaningful.
4. Use `common.json` only for shared UI text.
5. Keep page-specific text inside page-specific locale files.
6. Run TypeScript checks after localization.
7. Search manually for remaining English strings before deployment.

---

## 🗺 Roadmap

Possible future improvements:

- [ ] Add ready-to-use Cursor rules
- [ ] Add Claude Code skill format
- [ ] Add Codex-compatible instructions
- [ ] Add Next.js example
- [ ] Add Vite example project
- [ ] Add automated key extraction guide
- [ ] Add type-safe i18next setup
- [ ] Add ESLint checks for hardcoded strings

---

## 🤝 Contributing

Contributions are welcome.

You can help by:

- improving Turkish translation examples
- adding support for more languages
- adding framework-specific examples
- improving AI agent prompts
- adding real-world migration examples
- reporting issues or edge cases

To contribute:

1. Fork the repository
2. Create a new branch
3. Make your changes
4. Open a pull request

---

## ⭐ Support the Project

If this skill helps you localize your React app faster, please consider giving the repository a star.

It helps more developers discover the project and improves the visibility of open-source AI agent workflows.

<div align="center">

### ⭐ Star this repo if you find it useful!

</div>

---

## 📄 License

This project is released under the MIT License.

You are free to use, modify, and share it in personal, academic, and commercial projects.

---

## 🇹🇷 Türkçe Not

Bu repo, React + TypeScript projelerine `i18next` kullanarak Türkçe dil desteği eklemek isteyen geliştiriciler için hazırlanmış bir AI agent skill dosyasıdır.

Amaç, agent’ın projeyi bozmadan İngilizce arayüz metinlerini düzenli `en/tr` çeviri dosyalarına taşımasını sağlamaktır.

Eğer işine yararsa repoya yıldız vermeyi unutma. ⭐
