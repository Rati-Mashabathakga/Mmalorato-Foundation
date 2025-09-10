# Coding Standards (Mobile – React Native & Web – React + Vite)

> **Purpose:** A concise, practical standard you can paste into your repos (`/docs/Coding_Standards.md` or `CONTRIBUTING.md`).  
> **Scope:** React Native (Expo) + Firebase (Auth/Firestore) + AsyncStorage; React + Vite + Tailwind + Firebase.

---

## 1) Source Layout & Naming

**Folders (feature-first where practical):**
```
/src
  /screens            # RN screens
  /components         # Shared UI
  /services           # Firebase, donation, offline storage, network
  /utils              # popiaCompliance, southAfricanValidation, formatting, responsive, storage
  /navigation         # RN Navigation + TabNavigator
  /context            # (Web) AuthContext, providers
  /assets             # images, icons
```
**Files:**
- Components & Screens: `PascalCase.jsx/js` (e.g., `AdminLoginScreen.js`, `ProjectCard.jsx`)
- Utils & Services: `lowerCamelCase.js` (e.g., `southAfricanValidation.js`, `donationService.js`)
- Constants: `UPPER_SNAKE_CASE`
- React hooks: `useThing.js` (lowerCamelCase file; exported function `useThing`)

**Identifiers:**
- Variables & functions: `lowerCamelCase`
- React components: `PascalCase`
- Enums/immutable constants: `UPPER_SNAKE_CASE`
- Avoid abbreviations unless well-known (`id`, `url`, `db`)

---

## 2) Required Header Block & Inline Comments

Add this **header block** on top of every file (screen/component/service/util):

```js
/**
 * Author: <<Full Name>>
 * Date: <<DD Mon YYYY>>
 * Description: <<1–2 lines describing the purpose of this file>>
 */
```

Add **inline comments** for **non-trivial logic** only (validation rules, async flows, side-effects, edge cases). Prefer short sentences. Avoid narrating obvious JSX.

---

## 3) Error Handling & Async Patterns

- **Async:** Always `try/catch` around Firebase and network calls. Return **typed** objects: `{ ok: true, data }` or `{ ok: false, error }`.
- **User messaging:** Map low-level errors to friendly messages (avoid raw error strings). Centralise common messages (e.g., “Check your connection and try again.”).
- **React Native:** Wrap top-level trees with `ErrorBoundary` so a render crash shows a safe fallback screen.
- **Web:** Use toast/snackbar for recoverable errors; show full page fallbacks only for unrecoverable states.
- **Retries:** For transient network errors, allow a single retry or provide a “Retry” button.
- **Logging:** In dev and staging, `console.warn/error` with context; in prod, prefer a telemetry layer (future backlog).

---

## 4) Firebase & Data

- **Auth:** Never trust client-only checks for protected routes; use security rules for Firestore as the source of truth.
- **Firestore reads:** Use minimal projections; unsubscribe listeners when unmounting.
- **Writes:** Validate shapes **before** writes; use `serverTimestamp()` for created/updated times.
- **Collections:** Use clear names: `users`, `projects`, `volunteers`, `donations`, `auditLogs`.
- **Security rules (high-level):**
  - Authenticated users may read published `projects`.
  - Only owners/admins may write `projects` (or set via Cloud Functions).
  - `volunteers`/`donations` may be created by authenticated users; restrict reading to owner/admin where appropriate.
- **Secrets:** Never commit `.env*` with real keys. Use `.env.example` with placeholders.

---

## 5) POPIA / Privacy (South Africa)

- **Consent:** Show consent notice prior to account creation. Store a boolean + timestamp; provide **Delete My Data** option.
- **Data minimisation:** Only collect what’s necessary (name, email, mobile). Avoid storing ID numbers unless justified.
- **Local storage:** Prefer AsyncStorage for non-sensitive flags; avoid storing raw tokens or sensitive PII at rest.
- **Data deletion:** Implement a helper to clear local keys and issue a deletion request path (manual or via backend).

---

## 6) UI / UX

- **Accessibility:** Use semantic HTML on web; ensure text contrast ≥ 4.5:1; provide alt text; keyboard focus states.
- **Responsiveness:** Web: test breakpoints (≤480, 768, 1024, ≥1280). Mobile: use your `responsive.js` helpers.
- **Loading states:** Always indicate pending async operations (spinners/skeletons). Disable primary CTAs while loading.
- **Lists:** Use stable keys. Memoize expensive renders (`React.memo`, `useMemo`) when measurable.

---

## 7) Formatting & Linting

- **ESLint & Prettier:** Use project ESLint. Add Prettier with `printWidth: 100`, `singleQuote: true`, `semi: false` (example).  
  Scripts:
  ```json
  {
    "scripts": {
      "lint": "eslint .",
      "format": "prettier --write ."
    }
  }
  ```
- **Commits:** Conventional style (e.g., `feat:`, `fix:`, `docs:`, `refactor:`). Keep < 72 chars subject lines.
- **Pull requests:** Link issue, include “Before/After” screenshots for UI changes.

---

## 8) Performance & Security

- **Web performance:** Run Lighthouse; eliminate unused images; lazy-load heavy sections.
- **Bundle hygiene:** Prefer dynamic imports for large pages (web). Avoid heavy libs for simple tasks.
- **Security:** Validate all input on client; rely on Firestore rules; never show stack traces to end-users.

---

## 9) File Templates

**React component (web):**
```jsx
/**
 * Author: <<Name>>
 * Date: <<DD Mon YYYY>>
 * Description: <<Component purpose>>
 */
export default function ComponentName({ title }) {
  return <section aria-labelledby="title">{title}</section>
}
```

**Service util:**
```js
/**
 * Author: <<Name>> | Date: <<DD Mon YYYY>>
 * Description: Firebase donation service
 */
export async function createDonation({ userId, projectId, amountZar }) {
  try {
    // validate inputs...
    // await addDoc(...)
    return { ok: true }
  } catch (error) {
    return { ok: false, error }
  }
}
```
