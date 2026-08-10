# ADR-0023: BCrypt Password Hashing with Timing-Safe Login Compare

- **Status:** Accepted
- **Date:** 2026-08-05

## Context

Credential storage and login must resist offline cracking and user-enumeration timing differences.

## Decision

Hash passwords with `BCryptPasswordEncoder`. During login, always run a password match, using a dummy BCrypt hash when the user is absent, so timing does not trivially reveal account existence.

## Consequences

- Industry-standard password hashing.
- Reduced user-enumeration signal on login.
- Password policy remains enforced by auth validators separately from hashing.

## Code References

- `src/main/java/com/acos/auth/config/PasswordEncoderConfiguration.java`
- `src/main/java/com/acos/auth/service/AuthServiceImpl.java` (`DUMMY_PASSWORD_HASH` usage)

## Related Modules

- Auth
