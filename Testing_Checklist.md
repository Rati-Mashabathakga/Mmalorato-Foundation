# Testing Checklist (Mobile – React Native & Web – React + Vite)

> Use this as your working checklist for **Phase 4 – Testing**. Tick items as you go and paste results/screenshots into your Word doc.

---

## 0) Test Data & Environments

- [ ] Create **staging** Firebase project (separate from prod).  
- [ ] Seed data: 3–5 `projects` with varied categories; 2 test users (normal + admin).  
- [ ] Prepare `.env.local` / RN config with **redacted** keys in docs.  
- [ ] Accessibility baseline: ensure fonts ≥ 14px and sufficient contrast.

---

## 1) Unit Tests (where feasible)

- [ ] `southAfricanValidation` – mobile numbers, ID formats, currency ranges.  
- [ ] `formatting` – ZAR display, date/time formatting.  
- [ ] `popiaCompliance` – consent flag, deletion routine.  
- [ ] `storage/offlineStorage` – set/get/remove paths.  
- [ ] Pure React helpers/components (props defaults, edge cases).

_Outcome: brief notes or screenshots of passing results._

---

## 2) Integration Tests

**Mobile (RN):**
- [ ] Register → consent captured → email verification flagged.  
- [ ] Login (online) → session established; Profile loads.  
- [ ] Login (offline) → friendly message or supported fallback.  
- [ ] Donate flow → validation blocks < R10 or > R50,000 → valid amount proceeds.  
- [ ] Volunteer flow → local enqueue when offline; sync once online.  
- [ ] Admin PIN → good PIN grants access; bad PIN limited attempts.

**Web (React):**
- [x] Signup/Login with AuthContext; redirect to protected pages.  
- [x] Projects grid filter → correct items shown.  
- [x] Project page → volunteer form writes to Firestore with `serverTimestamp()`.  
- [x] Get Involved CTAs navigate; forms validate and submit.  
- [x] Responsive: navbar collapse, cards stack at small widths.

_Evidence: screenshots + short notes per case._

---

## 3) System / E2E Flows

- [ ] **Mobile E2E:** Onboarding → Register → Dashboard → Project Details → Volunteer → Donate → Profile.  
- [ ] **Web E2E:** Home → Projects → Project Detail → Get Involved → Volunteer → Logout.

_Tools (optional): Detox (RN), Playwright/Cypress (web). Manual walkthrough acceptable for submission._

---

## 4) UAT (User Acceptance Testing)

- [ ] Prepare checklist for client walkthrough (10–20 items).  
- [ ] Capture feedback (issues, suggestions, acceptance).  
- [ ] Prioritise, fix, retest critical items.  
- [ ] Obtain sign-off note/email.

_Paste bullet points or screenshots into the Word doc’s UAT section._

---

## 5) Accessibility & Performance

- [ ] **Web:** Lighthouse (Chrome) – record Accessibility ≥ 90, Performance ≥ 80 baseline.  
- [ ] **Mobile:** Check TalkBack/VoiceOver basic labels; ensure hit targets ≥ 44×44.  
- [ ] Keyboard focus order (web) is logical; visible focus rings.  
- [ ] Images have `alt`; decorative images are hidden from AT.

_Add snapshots of reports to the Word doc._

---

## 6) Security & Privacy (POPIA)

- [ ] Consent displayed pre-registration; stored with timestamp.  
- [ ] “Delete my data” clears local keys and creates a deletion request path.  
- [ ] Firestore rules (draft) documented; confirm reads/writes are restricted appropriately.  
- [ ] Sensitive data not stored in plain text locally.

---

## 7) Defect Log & Regression

- [ ] Log issues with ID, Platform, Severity, Steps, Expected/Actual, Status, Owner.  
- [ ] Retest after each fix; mark status updated.  
- [ ] Run a small regression pass on high-risk areas (auth, donations, volunteers).

---

## 8) Release Readiness

- [ ] **Mobile:** Build release (or EAS build) smoke test on physical device.  
- [x] **Web:** `npm run build` → `npm run preview`; confirm routes and assets load.  
- [ ] Update docs with final screenshots & dates.  
- [ ] Tag release and archive test evidence.

---

**Tip:** Keep all screenshots in `/docs/testing-evidence/2025-09-09/` and reference them in the Word doc.
