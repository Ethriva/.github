# Copilot Secure Coding Guardrails (MANDATORY)

These rules apply to all code generated or modified in this repository.

## Absolute “DO NOT” rules (BLOCKING)
1) **No hardcoded secrets**: never generate API keys, passwords, tokens, connection strings, private keys, or credentials in code, configs, tests, docs, or examples.
   - Use environment variables and managed secret stores (e.g., Azure Key Vault / AWS Secrets Manager / GCP Secret Manager).
2) **No arbitrary code execution**: do not use or suggest `eval`, `exec`, dynamic `Function(...)`, or equivalent patterns.
3) **No weak crypto**: do not use MD5, SHA-1, DES, RC4, ECB mode, or homegrown cryptography.
   - Use modern primitives (AES-GCM, SHA-256+, Argon2/bcrypt/scrypt for passwords).
4) **No insecure transport for sensitive data**: do not send credentials/PII over plaintext HTTP; enforce HTTPS and certificate validation.
5) **No SQL via string concatenation**: always use parameterized queries / prepared statements / ORM bindings.
6) **No unsafe deserialization** of untrusted input (e.g., Python `pickle.loads`, Java `ObjectInputStream.readObject`).

## Authorization & access control (REQUIRED)
- For any endpoint or action that reads/writes sensitive data or performs privileged operations:
  - Implement explicit authorization checks (roles/permissions/ownership) **before** business logic.
  - Apply least privilege.

## Dependency & supply chain (REQUIRED)
- Pin dependency versions (lockfiles / exact versions). Do not introduce floating versions.
- Prefer maintained libraries; avoid untrusted sources.

## Logging & auditing (REQUIRED)
- Add structured audit logs for: authentication, authorization decisions, admin actions, sensitive data access, security-relevant configuration changes.
- Do not log secrets, tokens, passwords, or full PII.

## Architecture governance (REQUIRED)
- Do not introduce new architectural components (new services, databases, queues, auth systems, key management, observability stacks) without explicit user approval.
- If a task requires architecture choice, present options and request approval.

## When uncertain
- Ask clarifying questions instead of guessing.
- Prefer secure defaults.
