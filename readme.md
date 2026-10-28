# Docker & Container Security Assessment

## Student Details
- **Name:** Deepanshu Moudgil
- **Registration Number:** `202401100100092`
- **Port:** `8091`
- **Docker Hub:** [deepanshu27m/fest-backend](https://hub.docker.com/r/deepanshu27m/fest-backend)

## Project Overview
This project demonstrates Docker containerization, security hardening, Docker Compose, vulnerability scanning using Trivy, and image signing using Cosign.

Application URL: `http://localhost:8091`

## Docker Hub Images
Repository: https://hub.docker.com/r/deepanshu27m/fest-backend

- `deepanshu27m/fest-backend:1.0.0`

**Version 1.0.0 digest:**

```text
sha256:c5cdf70f665b429df902b229caa13db7ce268d37719850224c786a0094591e15
```

The `1.0.0` image was built from `backend/` and pushed to Docker Hub. Tags `1.0` and `1.0.1` have not been published to this repository.

## Security Measures
- Backend runs as a non-root user.
- Dependencies are specified in `requirements.txt`.
- Docker Compose uses a dedicated network and persistent database volume.
- Trivy scans the container image for vulnerabilities.
- Cosign signing instructions are provided; the published image is not signed yet.
- `.env` and private signing keys are excluded from Git.

## Trivy Vulnerability Results

| Severity | Before | After |
|---|---:|---:|
| Critical | 0 | 0 |
| High | 6 | 5 |
| Medium | 14 | 2 |
| Low | 4 | 1 |
| **Total** | **24** | **8** |

Reported findings decreased by **66.7%**, from 24 to 8. Five High-severity findings remain and require review.

Detailed reports: `reports/trivy-before.txt` and `reports/trivy-after.txt`.

## Cosign Signing and Verification

The published `1.0.0` image has not yet been signed. To sign it, install Cosign and use the matching private key (not included in this repository):

```bash
cosign sign --key cosign.key \
  deepanshu27m/fest-backend@sha256:c5cdf70f665b429df902b229caa13db7ce268d37719850224c786a0094591e15
```

After signing with the key corresponding to `cosign.pub`, verify it with:

```bash
cosign verify --key cosign.pub \
  deepanshu27m/fest-backend@sha256:c5cdf70f665b429df902b229caa13db7ce268d37719850224c786a0094591e15
```

## Submission Checklist
- Include `cosign.pub`, `.gitignore`, Docker configuration, source files, scan reports, and required assessment screenshots.
- Ensure `.env` and `cosign.key` are not tracked by Git or present in Git history.
- Include evidence for Stages 1–5 as required by the assessment instructions.
- Verify the GitHub repository and Docker Hub links before submission.

## AI Tools Disclosure
ChatGPT was used for technical troubleshooting, Docker and Cosign guidance, interpreting Trivy results, and documentation assistance.

## Conclusion
The project demonstrates container hardening and vulnerability scanning. Trivy findings in the included reports decreased from 24 to 8. The newly published image still needs to be signed with the matching private key before signature verification can succeed.
