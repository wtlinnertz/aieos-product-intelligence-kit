# ANONYMIZATION

This document defines the **mandatory anonymization rules** for all content in the **Product Intelligence Kit** repository.

The goal is to ensure this repository remains:
- Publicly shareable
- Employer-neutral
- Tool-agnostic
- Safe for reuse and contribution
- Suitable for AI-assisted generation and validation

These rules apply to **all files**, including examples, templates, validators, prompts, and documentation.

---

## Core Rule

> **No content may reference a real employer, internal system, proprietary product, or real customer.**

If there is any doubt, **anonymize**.

---

## Prohibited Content (Must NOT Appear)

### Employer & Organization Identifiers
- Company names (current or former)
- Business unit names
- Internal team names
- Employer-specific acronyms
- Internal program or initiative names

### Real Products and Systems
- Proprietary product names
- Internal platform names
- Internal service or dashboard names
- Real customer or partner names
- Internal initiative names

### Identifiers & Metadata
- Internal URLs or domains
- Email addresses
- Usernames or personal names
- Internal ticket IDs or prefixes
- Project codes or initiative identifiers tied to a real organization

### Market & Customer Data
- Real revenue figures tied to a specific company
- Real customer counts or churn figures attributed to a real company
- Proprietary research data or competitive intelligence tied to a real organization

---

## Required Anonymization Patterns

When examples require realism, use **explicit fictional placeholders**.

### Approved Placeholder Conventions

The built-in examples use fictional companies and products:

| Element | Example Used in This Kit |
|---------|--------------------------|
| Product | TaskFlow (fictional project management SaaS) |
| Feature initiative | TaskFlow Intelligent Notification System |
| User groups | Project Managers, Team Contributors, Executive Stakeholders |
| Data references | Anonymized percentages and survey data (not tied to a real company) |

When contributing new examples, use similarly fictional but realistic contexts. Do not use real company names, even as inspiration for naming patterns.

### Domains & URLs
Use:
- `example.com`
- `app.example.com`
- `api.example.com`

Never use:
- Real company domains
- Personal domains

### Environments
Use generic names only:
- `dev`
- `staging`
- `prod`

Avoid:
- Internally meaningful environment names
- Region-specific or datacenter labels tied to a real organization

---

## What Is Allowed

- Fictional company names (e.g., TaskFlow, Acme Corp) that do not correspond to real organizations
- Generic industry references (e.g., "mid-market SaaS," "enterprise accounts") without naming real companies
- Open-source tool and framework names (e.g., PostgreSQL, React, Kubernetes)
- Generic cloud service references (e.g., "a managed Kubernetes cluster," "object storage")

---

## Pre-Submission Checklist

Before opening a PR, verify:

- [ ] No real company names appear anywhere in the contribution
- [ ] No real product names appear (unless open-source tools with public names)
- [ ] No internal URLs, domains, or identifiers appear
- [ ] No real customer data, revenue figures, or research attributed to a real organization
- [ ] All user names are fictional or replaced with role labels
- [ ] All examples use fictional scenarios or approved placeholder conventions

---

## Reporting Violations

If you find an anonymization violation in this repository, open an issue with:
- The file path
- The specific content that violates the rules
- A suggested anonymized replacement if possible

Violations found in PRs will be flagged before merge. Violations found post-merge will be corrected immediately.
