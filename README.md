# groupproject.

## Group Members

*
* Syazwani binti Rozali (2217642)
* Auni haziqah (2116050)

## Title

## Introduction

## Objectives of Enhancement

## Security Enhancements (with code snippets):

**Vulnerability Report (based on OWASP ZAP, risk + confidence levels)**

**Input Validation (client + server, methods used)**

**Authentication (best practices used)**
### ✅ Authorization

| Aspect            | Current Implementation Before Enhancement                                                                 | Suggested Improvement (Implemented)                                                                 | How to Implemented                                                                                     |
|-------------------|------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------|
| Access Control    | No fine-grained control; users could potentially access unauthorized resources.                           | Used Laravel `RiskPolicy` to define `update` and `delete` permissions for risks.                      | Created `RiskPolicy`, registered it in `AuthServiceProvider`, used `$this->authorize()` in controllers. |
| Blade Restriction | Buttons were visible to all roles regardless of permission.                                                | Used Blade `@can('update', $risk)` and `@can('delete', $risk)` to conditionally show buttons.         | Wrapped sensitive buttons in `@can` directives to hide them for unauthorized users.                     |
| Backend Protection| No backend enforcement; only UI-level hiding.                                                             | Enforced authorization at controller level using `authorize()` method.                                | Added `$this->authorize('update', $risk)` and similar checks in `RiskController`.                      |
| Role Enforcement  | Users have a `role` field, but role checks were done manually.                                            | Created reusable `checkRole()` helper and added role checks in routes.                                | Added helper function and wrapped role-based routes (admin, staff, superadmin) in manual logic.        |


**Authorization (methods used)**

**XSS and CSRF Prevention**

**Database Security (e.g., SQL injection protection)**

**File Security (e.g., file leakage prevention, server settings)**


## Reference

