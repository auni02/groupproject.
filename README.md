# groupproject.

## Group Members

* Nur Atiqah Binti Mat Jusoh (2217008)
* Syazwani binti Rozali (2217642)
* Auni haziqah (2116050)

## Title

## Introduction

## Objectives of Enhancement

## Security Enhancements (with code snippets):

**Vulnerability Report (based on OWASP ZAP, risk + confidence levels)**

**Input Validation (client + server, methods used)**

**Authentication (best practices used)**

**Authorization (methods used)**
| Aspect            | Current Implementation Before Enhancement                                                                 | Suggested Improvement (Implemented)                                                                 | How to Implemented                                                                                     |
|-------------------|------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------|
| Access Control    | No fine-grained control; users could potentially access unauthorized resources.                           | Used Laravel `RiskPolicy` to define `update` and `delete` permissions for risks.                      | Created `RiskPolicy`, registered it in `AuthServiceProvider`, used `$this->authorize()` in controllers. |
| Blade Restriction | Buttons were visible to all roles regardless of permission.                                                | Used Blade `@can('update', $risk)` and `@can('delete', $risk)` to conditionally show buttons.         | Wrapped sensitive buttons in `@can` directives to hide them for unauthorized users.                     |
| Backend Protection| No backend enforcement; only UI-level hiding.                                                             | Enforced authorization at controller level using `authorize()` method.                                | Added `$this->authorize('update', $risk)` and similar checks in `RiskController`.                      |
| Role Enforcement  | Users have a `role` field, but role checks were done manually.                                            | Created reusable `checkRole()` helper and added role checks in routes.                                | Added helper function and wrapped role-based routes (admin, staff, superadmin) in manual logic.        |

**XSS and CSRF Prevention**

| Aspect             | Current Implementation Before Enhancement                                                     | Suggested Improvement (Implemented)                                                                  | How to Implemented                                                                                          |
|--------------------|------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------|
| XSS Prevention     | Input was displayed without consistent escaping, potentially exposing to script injection.     | Ensured all user input is rendered using `{{ }}` for automatic escaping in Blade.                     | Audited Blade views to remove all `{!! !!}` for user content and replaced with `{{ $data }}`.                |
| CSRF Protection    | Default Laravel CSRF protection middleware was enabled but not verified across forms.          | Verified that `@csrf` token is present in all form submissions (`POST`, `PUT`, `DELETE`).             | Manually checked and added `@csrf` where missing in Blade form templates.                                     |
| Middleware Coverage| CSRF middleware was present but not actively monitored.                                        | Maintained Laravel’s `VerifyCsrfToken` middleware for route security.                                 | Ensured `VerifyCsrfToken` is included in `'web'` middleware group in `Kernel.php`.                           |
| CSP (Partially Done) | CSP middleware was added but response headers weren’t detected due to registration issue.     | Middleware created and registered in `Kernel.php` for extra browser-level XSS protection.             | Created `ContentSecurityPolicy` middleware; added it to `'web'` group in `Kernel.php` (header not confirmed). |


**Database Security (e.g., SQL injection protection)**

**File Security (e.g., file leakage prevention, server settings)**


## Reference

