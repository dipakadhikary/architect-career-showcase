# ADR-0023: BCrypt Password Hashing with Timing-Safe Login Compare

Interview summary of [`ADR-0023`](../architecture/adr/ADR-0023-bcrypt-password-hashing.md).

## Decision

Hash passwords with BCrypt and always run password matching on login, using a dummy hash when the user is absent.

## Benefits

- Industry-standard password hashing.
- Reduced user-enumeration timing signal on login.

## Limitations

- BCrypt CPU cost must be sized for login throughput.
- Password policy is separate and must stay aligned with validator rules.

## Code References

- `PasswordEncoderConfiguration`
- `AuthServiceImpl` (`DUMMY_PASSWORD_HASH`)
