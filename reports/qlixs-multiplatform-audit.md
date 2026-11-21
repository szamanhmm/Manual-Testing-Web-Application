# QLIXS — Multi-Platform Quality Audit Report

**Product Under Test:** [Qlixs (AI Productivity & Scheduling Platform)](https://dashboard.qlixs.ai)  
**Lead QA Engineer:** [Saifuz Zaman](https://szamanqa.me) (C4U Tech)  
**Full PDF Report:** [`reports/Qlixs_Comprehensive_Quality_Report.pdf`](./Qlixs_Comprehensive_Quality_Report.pdf)  
**Assessment Date:** February 2026  
**Overall Quality Rating:** **Average** *(Blockers present in auth & third-party integrations)*

---

## 1. Executive Summary

During full-cycle manual acceptance testing across **4 platforms** (Web, Android, iOS, Chrome Extension), **71 defects** were identified, isolated, and documented in Jira.

The **Web platform exhibited the highest defect density** (48 defects, ~68%), primarily concentrated around authentication loops, payment/upgrade state synchronisation, profile management, and broken external integrations (Zoom/Teams). Mobile platforms (Android: 9, iOS: 7) showed edge-case crashes and inconsistent validation messages. The Chrome Extension (7 bugs) contained critical authentication state barriers preventing onboarding.

```
Total Defects Detected: 71
├── Web Platform:       48 (67.6%)
├── Android App:         9 (12.7%)
├── iOS App:             7  (9.9%)
└── Chrome Extension:    7  (9.9%)
```

---

## 2. Defect Breakdown & Classification

### A. Severity Distribution
| Severity Level | Count | Definition |
| :--- | :---: | :--- |
| **Critical** | **1** | System unusable, onboarding blocked, infinite loading screen with no recovery. |
| **Major** | **34** | Core business logic broken, authentication loopholes, data submission failure, 404 links. |
| **Average (Medium)** | **25** | Secondary functional flaws, field validation lapses, edge-case state mismatch. |
| **Minor (Low)** | **11** | Cosmetic GUI inconsistencies, alignment, typography, minor styling bugs. |

### B. Defect Classification by Type
- **Functional Defects:** **61 (85.9%)**
- **GUI / Visual Defects:** **10 (14.1%)**

---

## 3. High-Priority Defects by Platform

| Platform | Bug ID | Severity | Issue Summary | Impact |
| :--- | :---: | :---: | :--- | :--- |
| **Web** | `B_01` | **Major** | Page loops and reloads infinitely when signing in using legacy credentials. | User locked out of existing accounts. |
| **Web** | `B_05` | **Major** | Password input field lacks validation for uppercase, numbers, and special characters. | Security compliance vulnerability. |
| **Web** | `B_06` | **Major** | Full platform access and feature navigation permitted prior to email verification. | Unverified accounts able to consume cloud resources. |
| **Web** | `B_18` | **Major** | In-person meeting module fails to upload and parse new audio/video recordings. | Core feature non-functional. |
| **Web** | `B_41` | **Major** | Clicking *"Connect Zoom"* redirects user to broken external `404 Not Found` page. | OAuth integration failure. |
| **Extension** | `B_04` | **Critical** | Persistent infinite spinner appears immediately upon submitting credentials in Chrome Extension. | 100% blocker for extension users. |
| **Extension** | `B_03` | **Major** | *"Please Upgrade your account"* modal interrupts user while actively on valid Freemium trial. | Artificial paywall blocking trial users. |
| **iOS** | `B_02` | **Major** | Generic *"Something went wrong"* alert displayed instead of explicit *"Account not found"* feedback. | Degraded user onboarding experience. |

---

## 4. Test Environments & Devices

| Platform | Target Software Version | Hardware / OS Environment |
| :--- | :--- | :--- |
| **Web** | Production Web Application | Windows 11 (23H2), Chrome v145.0.7632.117 |
| **Chrome Extension** | Manifest V3 Extension Build | Chrome Browser v145 on Windows 11 & macOS |
| **Android** | Native Android APK | Samsung Galaxy S23+ (Android 14), Poco M2 (Android 11) |
| **iOS** | TestFlight iOS Build | iPhone XS Max (iOS 18) |

---

## 5. Strategic QA Recommendations

1. **R1 — UX Architecture for Empty States:** Redesign the *"Interview Section"* empty state with clear calls to action (CTAs) rather than displaying blank containers.
2. **R2 — Streamline Call Flow:** Remove redundant intermediate confirmation modals in the meeting creation workflow to reduce drop-off rates.
3. **R3 — Visual State Iconography:** Standardize active vs. inactive toggle states in the *"Ready to Call"* interface to prevent user confusion.
4. **R4 — Auth & Session Hardening:** Enforce strict server-side validation on email verification before issuing JWT session tokens.
