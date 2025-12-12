## Security Checklist (required)
- [ ] No hardcoded secrets/tokens/credentials introduced
- [ ] No eval/exec/dynamic code execution introduced
- [ ] No weak/deprecated cryptography introduced
- [ ] SQL is parameterized / prepared (no concatenation)
- [ ] AuthZ checks exist for protected actions/endpoints
- [ ] Dependencies pinned (lockfile updated)
- [ ] Security/audit logs added for sensitive operations (no secrets logged)
- [ ] No new architecture components without approval
