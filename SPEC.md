# Lesson 01 specification

## STUDIO-001 · Launch a tested calculator on an existing server

**Status:** Hosted calculator verified; documentation and GitHub review pending.

**Instructor implementation:** [Issue #9](https://github.com/kaw393939/373_hosting/issues/9).

**My issue:** [STUDIO-001 #3](https://github.com/BryanF23/my-server-studio/issues/3).

## Agreed result

Deploy the supplied published calculator image through the existing
Docker/Traefik network and a nonconflicting HTTPS hostname. Preserve unrelated
services. Do not add another proxy, database, updater, or substitute image.

- **Public hostname:** https://calculator.bryanfselfhosted.xyz
- **Server:** Existing DigitalOcean server, accessed through SSH.
- **Docker network:** self-hosted-site_default
- **Image:** docker.io/kaw393939/is373_ci_cd
- **Image commit:** 4600202bad42da0c5ffb11d83ce8364671293d3d
- **Deployment project:** is373-studio-calculator
- **Deployment provenance:** Already-managed deployment found during
  verification; report records new_launch=false.
- **Feature branch:** feature/studio-001-calculator
- **Existing services:** Six containers checked; container identity, state,
  and published ports were unchanged.

## HTTPS configuration

The initial calculator route returned an untrusted self-signed certificate.
Inspection showed that the existing Traefik websecure entrypoint did not
specify its default Let's Encrypt resolver.

A backup of the original Traefik configuration was created. The websecure
entrypoint was updated to use the existing letsencrypt resolver, and only
the Traefik container was restarted.

After the change, the public HTTPS connection succeeded with trusted
certificate verification.

## Evidence to keep

| Evidence | Actual result |
|---|---|
| Black formatting | Passed; 8 files unchanged |
| Pylint | Failed; three Windows-related no-member warnings |
| Pytest unit/integration | Collection failed because Windows lacks signal.SIGHUP |
| Local real-image/browser E2E | Not completed |
| Hosted image and commit identity | Passed |
| Calculator health | Passed |
| Positive multiplication API case | HTTP 200; result 42 |
| Division by zero | HTTP 400 |
| Invalid numeric string | HTTP 422 |
| Trusted public HTTPS | Passed |
| Existing container preservation | Passed; six containers checked |
| Manual public browser test | Confirmed page loaded and 6 × 7 returned 42 |
| Sanitized runtime evidence | studio/evidence.json |

The local test limitations are documented rather than represented as
passing. Full CI results remain pending.

## Scope and limitations

This lesson deployed a supplied published image. It does not demonstrate
building my own application image or creating an independent CI/CD pipeline.

The runtime checks establish the selected image identity, API behavior,
trusted HTTPS, and preservation checks. They do not certify the entire
server or prove that every possible application behavior is correct.

The calculator was reported as already managed during verification, so
this specification does not claim a fresh launch based solely on that
verification result.

## GitHub review

- **Issue:** https://github.com/BryanF23/my-server-studio/issues/3
- **Feature branch:** feature/studio-001-calculator
- **Pull request:** Pending
- **Latest CI:** Pending
- **Merge and issue closure:** Pending

Review the evidence and documentation before committing or publishing.