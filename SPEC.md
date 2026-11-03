# Lesson 01 specification

## STUDIO-001 · Launch a tested calculator on an existing server

**Status:** Hosted calculator verified; documentation reviewed; GitHub PR merged; issue closed.

**My repository:** https://github.com/BryanF23/my-server-studio

**My issue:** [STUDIO-001 #3](https://github.com/BryanF23/my-server-studio/issues/3)

**Merged pull request:** [PR #4](https://github.com/BryanF23/my-server-studio/pull/4)

## Agreed result

Use the supplied published calculator image with the existing Docker/Traefik hosting environment and a public HTTPS hostname. Preserve unrelated services.

- **Public calculator:** https://calculator.bryanfselfhosted.xyz
- **Server:** Existing DigitalOcean server accessed through SSH.
- **Docker network:** `self-hosted-site_default`
- **Image:** `docker.io/kaw393939/is373_ci_cd`
- **Pinned image commit:** `4600202bad42da0c5ffb11d83ce8364671293d3d`
- **Deployment project:** `is373-studio-calculator`
- **Verification provenance:** `already-managed`; runtime evidence reports `new_launch=false`. The final verification does not claim a fresh launch.
- **Feature branch:** `feature/studio-001-calculator`

## HTTPS configuration

The initial calculator route did not pass trusted certificate verification.

I inspected the existing Traefik configuration, created a backup, configured the existing Let's Encrypt resolver as the default for the `websecure` entrypoint, and restarted only Traefik.

After the configuration change, trusted public HTTPS verification passed.

## Actual verification evidence

| Check | Actual result |
|---|---|
| Black formatting | Passed; 8 files unchanged |
| Pylint | Three Windows-related warnings |
| Local pytest | Collection failed because Windows lacks `signal.SIGHUP` |
| Local real-image/browser E2E | Not completed |
| Hosted image identity | Passed |
| Calculator health | Passed |
| Multiplication API | HTTP 200; result 42 |
| Division by zero | HTTP 400 |
| Invalid numeric string | HTTP 422 |
| Trusted public HTTPS | Passed |
| Existing services | Six containers checked; identity, state and published ports unchanged |
| Manual browser test | 6 × 7 returned 42 |

**Sanitized runtime evidence:** [studio/evidence.json](studio/evidence.json)

## GitHub review and CI

- **Issue:** [STUDIO-001 #3 – Closed](https://github.com/BryanF23/my-server-studio/issues/3)
- **Pull request:** [#4 – Merged](https://github.com/BryanF23/my-server-studio/pull/4)
- **PR checks:** [Three successful checks](https://github.com/BryanF23/my-server-studio/pull/4/checks)
- **Main-branch CI after the learning update:** [Successful workflow run](https://github.com/BryanF23/my-server-studio/actions/runs/41698718759)
- **Merged commit:** `52ebc09`
- **Latest learning-document commit:** `e4cb1ea`

## Scope and limitations

This lesson uses a supplied published image. It does not demonstrate building my own application image or creating an independent application CI/CD pipeline.

The hosted checks establish the selected image identity, health, API behavior, trusted HTTPS and the specified preservation checks. They do not certify the entire server or every possible application behavior.

Local Pylint and pytest limitations are recorded honestly. The local real-image/browser E2E check was not completed. GitHub CI passed its three PR checks.

The original pre-deployment prediction was not recorded. The retrospective routing explanation is identified as retrospective in `LEARNING.md`; it is not presented as an original prediction.

## Submission

**Repository URL:** https://github.com/BryanF23/my-server-studio