# Claude Code Security Guardrails (MANDATORY)

Follow these rules for all code, tests, configs, docs, and examples in this repository.

## BLOCKING: Do not generate or introduce any of the following
1) **Hardcoded secrets** (API keys, passwords, tokens, private keys, connection strings, creds).
   - Use environment variables + managed secret stores.
2) **Arbitrary code execution** patterns:
   - Python: `eval`, `exec`
   - JavaScript/TypeScript: `eval`, `new Function(...)`
   - Any equivalent dynamic execution mechanism
3) **Weak/broken crypto**:
   - MD5, SHA-1, DES, RC4, ECB mode, custom crypto
   - For passwords: never use plain hash; use Argon2/bcrypt/scrypt
4) **SQL injection risk**:
   - Never build SQL via string concatenation or interpolation.
   - Always use parameterized queries / prepared statements / ORM bindings.
5) **Unsafe deserialization of untrusted input**:
   - Python: `pickle.loads` on untrusted data
   - Java: `ObjectInputStream.readObject` on untrusted data
6) **Insecure transport for sensitive data**:
   - Do not transmit secrets/PII over plaintext HTTP.
   - Enforce HTTPS and certificate validation.

## REQUIRED: Authorization, validation, and secure defaults
- For any privileged or sensitive operation, implement explicit authorization checks before business logic.
- Validate and sanitize external inputs (request params, headers, files, webhook payloads).
- Use least privilege and deny-by-default patterns.

## REQUIRED: Dependency hygiene
- Pin dependency versions (lockfiles / exact versions).
- Avoid introducing untrusted or unmaintained libraries.

## REQUIRED: Audit logging (without sensitive leakage)
- Add structured audit logs for authn/authz decisions, admin actions, sensitive data access.
- Never log secrets/tokens/passwords or full PII.

## GOVERNANCE: Architecture decisions require approval
- Do not introduce new services/datastores/queues/auth systems/crypto/key mgmt/observability components without explicit approval.
- If needed, propose options and request approval.

## Behavior when ambiguous
- Ask clarifying questions rather than guessing.
- If repo docs conflict with instructions, pause and ask for resolution.
