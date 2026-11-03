# Lesson 01 · Conversation evidence

AI-drafted task summary, not a transcript or grade. This document records actual work, observations, and assistance. Review and correct before publishing.

**Lesson:** STUDIO-001

**Repository:** [my-server-studio](https://github.com/BryanF23/my-server-studio)

**Issue:** [STUDIO-001 #3](https://github.com/BryanF23/my-server-studio/issues/3)

**Specification:** [SPEC.md](SPEC.md)

**Runtime evidence:** [studio/evidence.json](studio/evidence.json)

## Prediction / routing explanation

**Reconstructed explanation — not an original pre-deployment prediction:**

A request to `calculator.bryanfselfhosted.xyz` reaches the server through DNS. Traefik receives the HTTPS request, matches the hostname to the calculator router, and forwards the request through the existing Docker network to the calculator container on port 8000.

## Check interpretation

The hosted verification passed. The calculator image and commit matched the expected release. The multiplication API test returned HTTP 200 with result 42. Division by zero returned HTTP 400, and invalid numeric input returned HTTP 422.

The first HTTPS verification failed because the server presented an untrusted self-signed certificate. I inspected the existing Traefik configuration, backed it up, added the existing Let's Encrypt resolver as the websecure entrypoint default, and restarted Traefik. Trusted HTTPS verification then passed.

The local checks were not all successful. Black passed, but Pylint reported three Windows-related warnings. Pytest collection failed because `signal.SIGHUP` is unavailable on Windows. Full local browser E2E was not completed. These results must remain documented as limitations.

## Browser observation

I opened `https://calculator.bryanfselfhosted.xyz` in my browser and tested 6 × 7. The calculator loaded and returned 42. This matched the expected result and the automated API verification.

## Keep decision

**Keep the deployment.** The calculator is accessible through trusted HTTPS, the expected image is running, the API checks passed, and the six-container preservation check reported unchanged container identity, state, and published ports.

The existing Traefik configuration was updated to enable its existing Let's Encrypt resolver as the default for the secure entrypoint. The original configuration backup was retained.

## Review

Pending learner review and correction before publication. This summary is AI-assisted and should not be treated as proof of independent authorship or understanding.

## AI work and contributions

AI assistance included guiding repository setup, interpreting the deployment plan, helping inspect Docker and Traefik configuration, troubleshooting HTTPS certificate verification, and drafting documentation.

My work included creating the repository from the instructor template, configuring the existing server target and hostname, creating issue #3 and the feature branch, running the deployment and verification commands, inspecting the server configuration, applying the approved Traefik change, testing the public calculator, and exporting sanitized runtime evidence.

**Remaining work:** Review this document, complete the GitHub pull request, record actual CI results, merge when the scope is satisfied, and close the issue.