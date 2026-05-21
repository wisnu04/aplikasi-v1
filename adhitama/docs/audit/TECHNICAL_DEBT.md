# Technical Debt

## 1. Current State
- The codebase has a strong blueprint, but several implementation gaps remain.
- Security and architecture comments outpace actual code in some modules.

## 2. Good Implementation
- Foundational security requirements are documented and partly implemented.
- Repository and module structure are present, even if not fully enforced.
- Global validation and exception handling are established.

## 3. Problems Found
- [S2] Service layer direct Prisma usage is technical debt that weakens the clean architecture contract.
- [S2] `SessionRepository.findByHash()` is unused, indicating unfinished auth discipline.
- [S2] `UserService.assertNotLastOwner()` is not transactionally safe, risking race conditions.
- [S2] Email verification and `mustChangePassword` gating are deferred and remain technical debt.
- [S3] No security middleware such as `Helmet`, CORS, or rate limiting is present yet.
- [S3] Role and permission validation is on-demand and has no cache layer, which may slow future scaling.
- [S4] Login email normalization is missing, causing a usability edge case.
- [S4] Audit logging is marked TODO in many service flows.

## 4. Root Cause Analysis
- The team prioritized feature scaffolding and phase milestones over strict architectural enforcement.
- Some blueprint requirements were documented as future work, leaving relevant code paths incomplete.
- Incomplete repository APIs caused services to implement custom queries, growing debt over time.

## 5. Recommended Fix
- Allocate a cleanup sprint for repository discipline and auth refresh flow completion.
- Implement missing blueprint security features in a prioritized order.
- Close gaps between documentation and actual runtime behavior by adding tests and audits.
- Track TODOs in a formal backlog so they are not forgotten.

## 6. Architectural Impact
- Reducing technical debt now will make later financial and rental workflows easier to secure.
- A cleaner service/repository contract improves maintainability and reduces the chance of security regressions.
- These changes support enterprise-grade scaling and auditability.
