# 🧪 FleetSetu — Full QA Analysis Report

![Status](https://img.shields.io/badge/Testing%20Status-Completed-43B02A?style=for-the-badge)
![Tests](https://img.shields.io/badge/Test%20Cases-11%20Executed-red?style=for-the-badge)
![Failed](https://img.shields.io/badge/Failed-10%20of%2011-red?style=for-the-badge)
![Security](https://img.shields.io/badge/Security%20Grade-D-red?style=for-the-badge)

> **Project:** FSWS-Audit-2026  
> **Platform:** FleetSetu Web Platform  
> **QA Lead:** Dhruv Attrey  
> **Date:** March 2026

---

## 📋 Executive Summary

> *"The FleetSetu platform is visually professional but technically fragile."*

The audit identified **10 failed test cases** out of 11 in the primary test suite. The current build prioritizes high-resolution aesthetics at the cost of 9-second render delays and critical security vulnerabilities.

| Category | Result |
|---|---|
| Total Test Cases | 11 |
| Failed | 10 🔴 |
| Warnings | 1 🟡 |
| Security Grade | **D** |
| LCP (Largest Contentful Paint) | **4.4s** (target: < 2.5s) |
| Page Weight | **~8MB** (severely over-weight) |

---

## 🗂️ Test Case Execution Ledger

| TC ID | Category | Description | Status | Severity |
|---|---|---|---|---|
| TC-001 | Functional | Hero "Call" button triggers native dialer | 🔴 FAIL | Critical (P0) |
| TC-002 | Performance | Image size vs. container dimensions | 🔴 FAIL | High (P1) |
| TC-003 | Performance | Favicon optimization / file size | 🔴 FAIL | High (P1) |
| TC-004 | Performance | LCP must be under 2.5s | 🔴 FAIL (4.4s) | High (P1) |
| TC-005 | Security | HSTS header present | 🔴 FAIL | High (P1) |
| TC-006 | Security | X-Frame-Options (clickjacking) | 🔴 FAIL | High (P1) |
| TC-007 | Compliance | W3C URL encoding in asset paths | 🔴 FAIL | Medium (P2) |
| TC-008 | SEO | Heading hierarchy (H1 → H2 → H3) | 🔴 FAIL | Medium (P2) |
| TC-009 | SEO | Robots.txt syntax validation | 🔴 FAIL | Medium (P2) |
| TC-010 | Data | JSON-LD Schema — logo & social links | 🟡 WARN | Low (P3) |
| TC-011 | Technical | Preloaded assets verified as used | 🔴 FAIL | Medium (P2) |

---

## 🔍 Detailed Findings

### A. 🚨 Critical — Dead CTA Button (TC-001)
**Severity:** Critical (P0) — "Conversion Killer"

The Hero section "Call Now" button is a static element with **no `tel:` link** attached. In a B2B logistics environment, "Call Now" is the primary lead funnel.

- **Impact:** 100% of mobile users attempting to call are blocked
- **Fix:** Wrap button in `<a href="tel:+91XXXXXXXXXX">` tag

---

### B. ⚡ Performance — The "8MB Wall" (TC-002, TC-003, TC-004)
**Severity:** High (P1)

The site is technically "obese":

- **7K resolution images** served inside small web containers — fundamental asset pipeline failure
- **643KB favicon** — uncompressed, severely impacting load time
- **LCP: 4.4 seconds** (target < 2.5s) — browser downloads massive unused images before rendering the Hero section
- **Element Render Delay: 9.4s** caused by wasted preloads blocking the critical render path

**Fixes:**
- Use `<Image />` with `srcset` for mobile-first asset delivery
- Compress favicon to < 10KB
- Resize images to actual display dimensions (WebP/AVIF format)

---

### C. 🔒 Security — Grade D (TC-005, TC-006)
**Severity:** High (P1)

**Missing Headers:**

| Header | Risk |
|---|---|
| `Strict-Transport-Security` (HSTS) | Vulnerable to protocol downgrade attacks |
| `X-Frame-Options` | Vulnerable to clickjacking attacks |

For a logistics platform handling fleet data, this is a significant compliance risk.  
**Fix:** Add security header middleware to server-side configuration.

---

### D. 🧹 Code Quality — W3C Violations (TC-007)
**Severity:** Medium (P2)

Illegal characters (spaces) detected in asset filenames:
```
/FleetSetu LOGO-01.svg   ← spaces in filename = invalid URL
```

- Can cause images to break on specific browsers or high-security network filters
- **Fix:** Automate W3C validation in CI/CD pipeline

---

### E. 📈 SEO Issues (TC-008, TC-009)
**Severity:** Medium (P2)

- **Broken heading hierarchy** — H1 does not flow sequentially to H2 → H3
- **Robots.txt syntax error** — unknown directives detected that may confuse crawlers

---

### F. ⚠️ JSON-LD Schema Incomplete (TC-010)
**Severity:** Low (P3) — Warning

JSON-LD structured data script is present but missing:
- Logo URL
- Social media links
- Complete organization entity data

---

### G. 🔗 Wasted Resource Preloads (TC-011)
**Severity:** Medium (P2)

Preloaded assets are not used within the load window, causing:
- Unnecessary bandwidth consumption
- Delayed critical resource loading

---

## 🏆 Top 3 Priority Fixes

```
P0 → Fix dead "Call" button — restore lead funnel immediately
P1 → Emergency image compression — reduce 8MB payload
P1 → Implement HSTS + X-Frame-Options — upgrade security from Grade D to A
```

---

## 💡 Final Recommendations

1. **Mobile-First Asset Delivery** — Use Next.js `<Image />` with `srcset` so mobile users don't download 7K desktop images
2. **Automate Linting** — Add W3C validation to CI/CD pipeline to catch illegal file paths before deployment
3. **Security Middleware** — Add server-side header middleware for 100% compliance across all routes
4. **Fix Heading Hierarchy** — Ensure sequential H1 → H2 → H3 structure for SEO and accessibility
5. **Complete JSON-LD Schema** — Add logo, social links, and organization data for rich search results

---

## 🛠️ Tools Used

`Chrome DevTools` `Lighthouse` `W3C Nu Validator` `SecurityHeaders.com` `PageSpeed Insights`

---

*QA Report by **Dhruv Attrey** | Sparrowbyte Fintech Solutions Internship | 2026*
