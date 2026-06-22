# React TypeScript i18next Localization Skill

## Purpose
This skill helps migrate a React + TypeScript application from hardcoded English UI text to a scalable bilingual i18next setup with English and Turkish language support.

## Project Context
The project is a React TypeScript frontend application. The app currently has English hardcoded UI strings. The goal is to add Turkish language support using i18next / react-i18next while keeping the code clean, scalable, and type-safe.

## Main Rules

1. Do not directly translate UI text inside components.
2. Replace hardcoded user-facing strings with `t("key.path")`.
3. Keep translation files organized by namespace or feature.
4. Use semantic translation keys, not full sentences as keys.
5. Add both English and Turkish translations.
6. Preserve all existing UI layout, styling, routing, and business logic.
7. Do not change unrelated code.
8. Prefer `i18n.ts` in TypeScript projects instead of `i18n.js` when possible.
9. Use `useTranslation()` inside React components.
10. Use `<Trans />` only when translation text contains React elements, links, bold text, line breaks, or nested markup.
11. Use interpolation for dynamic values.
12. Use pluralization with the `count` variable when needed.
13. Keep Turkish translations natural, professional, and suitable for a modern web app.
14. Do not translate code identifiers, API fields, route paths, CSS class names, or database values unless explicitly required.
15. After editing, ensure no visible English hardcoded UI text remains unless it is a brand name, technical term, or intentionally English.

## Recommended File Structure

Use this structure unless the project already has a better convention:

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

## Recommended Packages

Use these packages unless the project already has them installed:

```bash
npm install i18next react-i18next i18next-browser-languagedetector
```

or with pnpm:

```bash
pnpm add i18next react-i18next i18next-browser-languagedetector
```

## i18n Setup Rules

Create or update the i18n setup using:

- `i18next`
- `react-i18next`
- optional browser language detection if useful

The i18n config should:

- use English as fallback language
- support `en` and `tr`
- load namespaces cleanly
- default to `common`
- export the configured i18n instance

Example `src/i18n/i18n.ts`:

```ts
import i18n from "i18next";
import { initReactI18next } from "react-i18next";
import LanguageDetector from "i18next-browser-languagedetector";

import enCommon from "./locales/en/common.json";
import trCommon from "./locales/tr/common.json";

const resources = {
  en: {
    common: enCommon,
  },
  tr: {
    common: trCommon,
  },
};

i18n
  .use(LanguageDetector)
  .use(initReactI18next)
  .init({
    resources,
    fallbackLng: "en",
    supportedLngs: ["en", "tr"],
    defaultNS: "common",
    ns: ["common"],
    interpolation: {
      escapeValue: false,
    },
    detection: {
      order: ["localStorage", "navigator"],
      caches: ["localStorage"],
    },
  });

export default i18n;
```

Import the config once near the app root, usually in `main.tsx` or `App.tsx`:

```ts
import "./i18n/i18n";
```

## Translation Key Style

Use clean nested keys.

Good:

```json
{
  "navbar": {
    "home": "Home",
    "settings": "Settings"
  },
  "buttons": {
    "save": "Save",
    "cancel": "Cancel"
  }
}
```

Bad:

```json
{
  "Home": "Home",
  "Click here to save changes": "Click here to save changes"
}
```

## Component Refactor Example

Before:

```tsx
<button>Save Changes</button>
```

After:

```tsx
import { useTranslation } from "react-i18next";

export function SaveButton() {
  const { t } = useTranslation("common");

  return <button>{t("buttons.saveChanges")}</button>;
}
```

English translation:

```json
{
  "buttons": {
    "saveChanges": "Save Changes"
  }
}
```

Turkish translation:

```json
{
  "buttons": {
    "saveChanges": "Değişiklikleri Kaydet"
  }
}
```

## Dynamic Text Example

Before:

```tsx
<p>Welcome, {user.name}</p>
```

After:

```tsx
<p>{t("user.welcome", { name: user.name })}</p>
```

English:

```json
{
  "user": {
    "welcome": "Welcome, {{name}}"
  }
}
```

Turkish:

```json
{
  "user": {
    "welcome": "Hoş geldin, {{name}}"
  }
}
```

## Pluralization Rule

Use `count` for plural forms.

Example:

```tsx
t("notifications.count", { count: unreadCount })
```

English:

```json
{
  "notifications": {
    "count_one": "{{count}} notification",
    "count_other": "{{count}} notifications"
  }
}
```

Turkish:

```json
{
  "notifications": {
    "count_one": "{{count}} bildirim",
    "count_other": "{{count}} bildirim"
  }
}
```

## Rich Text Rule

Use `<Trans />` when text contains React elements.

Example:

```tsx
import { Trans } from "react-i18next";

<Trans
  i18nKey="auth.termsText"
  components={{
    terms: <a href="/terms" />,
    privacy: <a href="/privacy" />,
  }}
/>
```

English:

```json
{
  "auth": {
    "termsText": "By continuing, you agree to our <terms>Terms</terms> and <privacy>Privacy Policy</privacy>."
  }
}
```

Turkish:

```json
{
  "auth": {
    "termsText": "Devam ederek <terms>Kullanım Şartları</terms> ve <privacy>Gizlilik Politikası</privacy> koşullarını kabul etmiş olursun."
  }
}
```

## Language Switcher

If the app does not have one, create a simple language switcher component:

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

## Turkish Translation Style

Use natural Turkish UI language.

Preferred translations:

- `Save` → `Kaydet`
- `Cancel` → `İptal`
- `Settings` → `Ayarlar`
- `Profile` → `Profil`
- `Dashboard` → `Panel` or `Kontrol Paneli`
- `Sign in` → `Giriş yap`
- `Sign up` → `Kayıt ol`
- `Log out` → `Çıkış yap`
- `Loading...` → `Yükleniyor...`
- `Something went wrong` → `Bir şeyler ters gitti`
- `Try again` → `Tekrar dene`
- `Create account` → `Hesap oluştur`
- `Forgot password?` → `Şifreni mi unuttun?`
- `Search` → `Ara`
- `Filter` → `Filtrele`
- `Delete` → `Sil`
- `Edit` → `Düzenle`
- `Update` → `Güncelle`
- `Submit` → `Gönder`
- `Apply` → `Uygula`
- `Confirm` → `Onayla`
- `Continue` → `Devam et`
- `Back` → `Geri`
- `Next` → `İleri`

Avoid overly literal translations.

Bad:

- `Submit` → `Sunmak`
- `Apply` → `Başvurmak` when the UI means applying a filter or setting

Good:

- `Submit` → `Gönder`
- `Apply` → `Uygula`
- `Confirm` → `Onayla`

## Common Namespace Example

`src/i18n/locales/en/common.json`:

```json
{
  "app": {
    "name": "Application"
  },
  "navbar": {
    "home": "Home",
    "dashboard": "Dashboard",
    "settings": "Settings",
    "profile": "Profile"
  },
  "buttons": {
    "save": "Save",
    "saveChanges": "Save Changes",
    "cancel": "Cancel",
    "delete": "Delete",
    "edit": "Edit",
    "update": "Update",
    "submit": "Submit",
    "tryAgain": "Try Again"
  },
  "states": {
    "loading": "Loading...",
    "empty": "No data found.",
    "error": "Something went wrong."
  }
}
```

`src/i18n/locales/tr/common.json`:

```json
{
  "app": {
    "name": "Uygulama"
  },
  "navbar": {
    "home": "Ana Sayfa",
    "dashboard": "Panel",
    "settings": "Ayarlar",
    "profile": "Profil"
  },
  "buttons": {
    "save": "Kaydet",
    "saveChanges": "Değişiklikleri Kaydet",
    "cancel": "İptal",
    "delete": "Sil",
    "edit": "Düzenle",
    "update": "Güncelle",
    "submit": "Gönder",
    "tryAgain": "Tekrar Dene"
  },
  "states": {
    "loading": "Yükleniyor...",
    "empty": "Veri bulunamadı.",
    "error": "Bir şeyler ters gitti."
  }
}
```

## Agent Workflow

When applying this skill to a project:

1. Inspect the project structure.
2. Check whether i18next or react-i18next already exists.
3. If not installed, add required packages.
4. Create the i18n configuration.
5. Create English and Turkish locale files.
6. Refactor components gradually.
7. Replace visible hardcoded English strings with `t()`.
8. Use namespaces for large apps.
9. Add a language switcher if missing.
10. Run TypeScript checks and fix errors.
11. Search again for hardcoded English UI strings.
12. Confirm that English and Turkish translation files have matching keys.

## Do Not Translate

Do not translate:

- component names
- variable names
- function names
- route paths unless requested
- API payload keys
- enum values used by backend
- CSS class names
- image filenames
- brand names
- library names
- database values
- environment variable names

## Final Checklist

After changes:

1. Check all pages for hardcoded visible English text.
2. Check buttons, forms, modals, alerts, empty states, loading states, validation messages, navbar, sidebar, footer.
3. Ensure English and Turkish JSON files have matching keys.
4. Ensure the app does not crash when switching language.
5. Ensure TypeScript errors are fixed.
6. Keep formatting consistent.
7. Do not remove existing functionality.
8. Do not change UI design unless specifically requested.
9. Do not introduce unnecessary dependencies.
10. Keep translations natural and professional.

## Prompt To Use With This Skill

Use this prompt when asking the agent to apply localization:

```txt
Use the React TypeScript i18next Localization Skill.
Convert this React TypeScript app from hardcoded English UI text to i18next-based English/Turkish localization.
Preserve all existing design and functionality.
Create clean translation keys, add en/tr locale files, add a language switcher, and make sure there are no remaining hardcoded visible English UI strings.
Prefer i18n.ts instead of i18n.js if the project is fully TypeScript.
```
