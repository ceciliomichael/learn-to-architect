# Exercise: Security Hardening

## Steps

1. Use a 16-byte command buffer.
2. Accept only complete start and stop commands.
3. Reject empty, overlong, and unknown commands.
4. Drain leftover bytes after excess input.
5. Add supported hardening flags without removing validation.

## Success check

Only complete bounded commands are accepted, excess input is drained, and hardening never replaces validation.

