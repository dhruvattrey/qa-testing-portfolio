# 🔵 Xoobill Billing Platform — QA Report

![Bugs](https://img.shields.io/badge/Bugs%20Found-13%2B-red?style=for-the-badge)
![Type](https://img.shields.io/badge/Type-Manual%20%2B%20Automation-0052CC?style=for-the-badge)
![Rejections](https://img.shields.io/badge/Defect%20Rejections-Zero-43B02A?style=for-the-badge)

> **Application:** Xoobill — Fintech Billing & Invoicing SaaS  
> **Company:** Sparrowbyte Fintech Solutions  
> **Tester:** Dhruv Attrey  
> **Tools:** Python · Selenium · Jira · SQL · Chrome DevTools

---

## 📋 Summary

Performed end-to-end QA on the Xoobill billing platform covering authentication, customer/vendor/item forms, billing workflows, quotation, GST calculations, and session handling.

| Metric | Result |
|---|---|
| Functional Defects Found | 13+ |
| Defect Rejection Rate | **0%** |
| Testing Type | Manual + Selenium Automation |
| Bug Tracking | Jira with severity, priority & reproduction steps |

---

## 🐛 Key Defects Found

| Area | Issue | Severity |
|---|---|---|
| Forms | Invalid input accepted in customer, vendor, and item forms | High |
| Billing | Incorrect GST and subtotal calculations on invoices | High |
| Navigation | Broken redirects after form submission | Medium |
| Session | Session handling errors on timeout | Medium |
| Logic | Paid status shown without a payment method selected | High |
| Validation | Boundary condition failures on numeric input fields | Medium |

---

## 🔍 Testing Performed

- **UI Validation** — layout consistency, element alignment, typography, colour rendering across browsers
- **Functional Testing** — all major user workflows: login, create customer, create invoice, generate quote
- **Boundary & Edge Case Testing** — min/max values, empty fields, special characters
- **Regression Testing** — verified fixes after developer patches without introducing new regressions
- **SQL Validation** — queried backend database to verify data integrity against UI outputs
- **Automation** — built Selenium scripts in Python (AI-assisted with Claude & ChatGPT) for repetitive test flows

---

## 📂 Documentation Maintained

- Structured test case suites reusable across release cycles
- Jira tickets with annotated screenshots, steps to reproduce, expected vs actual
- Living QA documentation library — sole quality reference for the team
- Full traceability from test execution through sign-off

---

## 🛠️ Tools Used

`Python` `Selenium WebDriver` `Jira` `SQL` `Chrome DevTools` `Claude AI` `ChatGPT`

---

*Part of [QA Testing Portfolio](../README.md) · Dhruv Attrey · 2026*
