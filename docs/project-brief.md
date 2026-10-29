# IT Risk and Compliance Management System: Project Brief

For the full rules, see [requirements.md](requirements.md).

## Organisation
Mvelo Logistics (Pty) Ltd is a fictional, medium-sized South African logistics
company (about 200 employees, a head office in Johannesburg and two depots in
Gauteng).

## Problem
IT risks are tracked in spreadsheets. It is hard to see which risks matter most,
monitor controls, track corrective actions, or know who changed what.

## Solution
A web application that records IT risks, scores them, links them to controls
mapped to NIST CSF 2.0, tracks corrective actions, and keeps an audit trail.

## Roles
- **Admin:** manages users, risks, controls and actions.
- **Risk Owner:** manages their own risks and related actions only.
- **Auditor:** read-only access, including the audit trail.

## Scoring method
Risk score = Likelihood x Impact, each rated 1 to 5.

| Score | Severity |
|---|---|
| 1-5 | Low |
| 6-12 | Medium |
| 13-19 | High |
| 20-25 | Critical |

Residual ratings are entered by the assessor, cannot exceed the inherent
ratings, and need a written justification when they differ.

Example: inherent 4 x 5 = 20 (Critical). After patching and firewall rules,
residual 2 x 5 = 10 (Medium).

## Technology
C#, ASP.NET Core MVC (.NET 10 LTS), SQL Server, Entity Framework Core,
ASP.NET Core Identity, Bootstrap, Chart.js, xUnit, Git and GitHub.

## Status
Phase 1: database design in progress.

## Note
This is a portfolio demonstration using fictional data. It is not a production
compliance tool.