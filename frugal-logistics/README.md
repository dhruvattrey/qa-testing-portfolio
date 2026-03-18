# 🧪 Frugal Logistics — QA Test Report

![Status](https://img.shields.io/badge/Testing%20Status-Completed-43B02A?style=for-the-badge)
![Bugs](https://img.shields.io/badge/Bugs%20Found-7-red?style=for-the-badge)
![Security](https://img.shields.io/badge/Security%20Rating-A%2B-43B02A?style=for-the-badge)
![Type](https://img.shields.io/badge/Type-Manual%20Testing-0052CC?style=for-the-badge)

> **Application:** Frugal Logistics Pvt Ltd Website  
> **URL Tested:** https://frugallogistics.in  
> **Tester:** Dhruv Attrey  
> **Environment:** Chrome, Edge · Windows · Desktop + Mobile

---

## 📋 Executive Summary

A comprehensive QA evaluation of the Frugal Logistics website covering functional stability, usability, performance, accessibility, security, and technical implementation.

| Category | Result |
|---|---|
| Total Bugs Found | 7 (5 Medium, 2 Low) |
| Security Rating | **A+** |
| Lighthouse Performance | Opportunities identified |
| HTML Validation | 4 structural issues |
| Accessibility | Minor issues (WAVE scan) |
| Network Health | ✅ No failed requests |

---

## 🐛 Bug Summary

| # | Bug Title | Severity | Type |
|---|---|---|---|
| 1 | Invalid email format accepted by contact form | Medium | Input Validation |
| 2 | Phone number field accepts alphabetic characters | Medium | Input Validation |
| 3 | Success message persists after form becomes invalid | Low | UI State |
| 4 | Multiple submit clicks redirect user to homepage | Medium | Form Handling / UX |
| 5 | Console warning for unused CSS preload | Low | Performance |
| 6 | Phone validation inconsistent between desktop and mobile | Medium | Cross-platform |
| 7 | "Request Quote" button on homepage does nothing | Medium | Functional / Navigation |

---

## 🔍 Testing Scope

### Functional Testing
- Contact form and Request Quote form workflows
- Input validation for all form fields
- Button behavior and navigation flows
- Edge case and boundary condition testing

### Cross-Device Testing
- Desktop (Chrome, Edge)
- Mobile View via Chrome DevTools Device Emulator

### Technical Testing
| Tool | Purpose |
|---|---|
| Chrome DevTools | Console, Network, Performance |
| Lighthouse | Performance audit |
| W3C Nu HTML Validator | HTML structure validation |
| WAVE | Accessibility evaluation |
| SecurityHeaders.com | HTTP security header analysis |
| PageSpeed Insights | Performance scoring |

---

## 🐛 Detailed Bug Reports

### Bug 1 — Invalid Email Format Accepted
**Severity:** Medium | **Type:** Input Validation

**Steps to Reproduce:**
1. Open https://frugallogistics.in/contact
2. Enter: Name: `xtr`, Email: `abc@gmail`, Phone: any value
3. Click Submit Now

**Expected:** Validation error for invalid email format  
**Actual:** Form submits successfully with "Message sent successfully!"  
**Impact:** Invalid contact data stored, preventing customer follow-up

---

### Bug 2 — Phone Field Accepts Alphabetic Characters
**Severity:** Medium | **Type:** Input Validation

**Steps to Reproduce:**
1. Open the Contact page
2. Enter `dhrrrruvgr4fffWFF` in phone number field
3. Submit the form

**Expected:** Only numeric/valid phone formats accepted  
**Actual:** Alphabetic characters accepted, form submits successfully  
**Impact:** Invalid phone numbers stored in database

---

### Bug 3 — Success Message Persists on Invalid Form
**Severity:** Low | **Type:** UI Feedback / State

**Steps to Reproduce:**
1. Submit the form successfully
2. Modify email field to invalid value (e.g. `abc`)
3. Observe success message

**Expected:** Success message disappears when form becomes invalid  
**Actual:** "Message sent successfully!" remains visible  
**Impact:** User confusion about actual submission state

---

### Bug 4 — Multiple Clicks Redirect to Homepage
**Severity:** Medium | **Type:** Form Handling / UX

**Steps to Reproduce:**
1. Open https://frugallogistics.in
2. Fill the Request a Free Quote form
3. Click "Submit Now" multiple times rapidly

**Expected:** Button disabled after first click, or loading indicator shown  
**Actual:** Page reloads and redirects to homepage with no confirmation  
**Impact:** Risk of duplicate submissions, data loss, user confusion

---

### Bug 5 — Unused CSS Preload Console Warning
**Severity:** Low | **Type:** Performance Warning

**Observed:** Browser console logs preload warning for CSS file not used within load event  
**Impact:** Minor performance and resource loading inefficiency

---

### Bug 6 — Phone Validation Inconsistent Across Devices
**Severity:** Medium | **Type:** Cross-Platform Consistency

**Desktop:** Accepts alphabetic characters in phone field  
**Mobile:** Restricts to numeric input only  
**Impact:** Inconsistent data quality depending on user device

---

### Bug 7 — "Request Quote" Button Non-Functional
**Severity:** Medium | **Type:** Functional / Navigation

**Steps to Reproduce:**
1. Open https://frugallogistics.in
2. Scroll to "What Makes Us Special" section
3. Click "REQUEST QUOTE" button

**Expected:** Redirects to quote form or opens contact modal  
**Actual:** Button performs no action  
**Impact:** Lost customer inquiries, reduced conversion opportunities

---

## 📊 Performance Analysis (Lighthouse Desktop)

| Observation | Estimated Saving |
|---|---|
| Render-blocking resources | ~80ms |
| Image delivery optimization | 372 KiB |
| Unused JavaScript | 110 KiB |
| Inefficient cache lifetimes | 5 KiB |
| Legacy JavaScript | 14 KiB |

**Network Stats:**  
- Total Requests: 124 | Data Transferred: 71.7 KB | Resources: 5.4 MB  
- DOMContentLoaded: 723ms | Page Load: 1.36s

---

## 🔒 Security Analysis

**Rating: A+** via SecurityHeaders.com

| Header | Status |
|---|---|
| Strict-Transport-Security (HSTS) | ✅ Configured |
| Content-Security-Policy (CSP) | ✅ Configured |
| X-Content-Type-Options | ✅ Configured |
| X-Frame-Options | ✅ Configured |
| Referrer-Policy | ✅ Configured |
| Permissions-Policy | ✅ Configured |

---

## ♿ Accessibility (WAVE Tool)

| Issue | Severity |
|---|---|
| Language attribute missing/invalid | Error |
| Missing first-level heading (H1) | Alert |
| No defined page regions | Alert |

AIM Score: **9.4 / 10**

---

## 🏷️ HTML Validation (W3C)

| Issue | Severity |
|---|---|
| Duplicate `<meta name="description">` tag | Medium (SEO) |
| Heading jumps h1 → h4 (skips 2 levels) | Medium (Accessibility/SEO) |
| Heading jumps h2 → h4 in multiple sections | Medium |
| Empty JSON-LD structured data script | Low (SEO) |

---

## ✅ Positive Observations

- ✅ Sitemap.xml — properly structured, all key pages indexed
- ✅ Robots.txt — correctly configured, AI crawlers blocked
- ✅ Network health — 0 failed requests, all resources HTTP 200
- ✅ A+ security header rating

---

## 💡 Recommendations

1. Implement strict client-side + server-side email and phone validation
2. Disable submit button after first click to prevent duplicate submissions
3. Fix "Request Quote" CTA button to redirect correctly
4. Fix heading hierarchy (h1 → h2 → h3 → h4)
5. Remove duplicate meta description tag
6. Implement valid JSON-LD structured data
7. Optimize images (WebP/AVIF), defer non-critical JS, extend cache lifetimes
8. Add `lang="en"` attribute and semantic HTML regions

---

## 🛠️ Tools Used

`Chrome DevTools` `Lighthouse` `W3C Validator` `WAVE` `SecurityHeaders.com` `PageSpeed Insights`

---

*QA Report by **Dhruv Attrey** | Sparrowbyte Fintech Solutions Internship | 2026*
