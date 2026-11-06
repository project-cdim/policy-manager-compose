# Changelog 0.2

## 0.2.1 - 2026-11-02

The changes from oss_v0.2.0 are as follows:

- Renamed `compose.yml` to `compose.yml.template` and added configurable HTTP and HTTPS proxy build arguments. Create `compose.yml` from the template before starting the services.
- Hardened the policy-manager container by disabling privilege escalation, dropping the `NET_RAW` capability, and removing setuid and setgid permissions from image files.
- Updated Python from 3.14.2 to 3.14.6.
- Updated the policy-manager submodule, including its dependencies and development instructions.
