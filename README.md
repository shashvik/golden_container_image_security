# 🔐 Secure Image Pipeline with Cosign

This repository demonstrates a secure DevSecOps workflow using [Sigstore Cosign](https://github.com/sigstore/cosign) to:

- ✅ Verify that only **signed, golden base images** are used in Dockerfiles
- 🛠️ Build microservice images using GitHub Actions
- 🔏 Sign the final image with your organization's **Cosign private key**

---

## 🚀 Workflow Overview

1. Parse the `Dockerfile` to extract `FROM` image(s)
2. Use `cosign verify` to check that base images are signed with a trusted **public key**
3. Build the final image via `docker build`
4. Sign the final image using your **private key**
5. (Optional) Push to your image registry

---

## 📂 Repository Layout

.
├── Dockerfile # Microservice Dockerfile using a signed base image
├── .github
│ └── workflows
│ └── cosign-pipeline.yml # GitHub Actions pipeline
└── README.md

yaml
Copy
Edit

---

## 🔧 Secrets Required

To run this pipeline securely, configure the following repository secrets:

| Secret Name               | Purpose                            |
|--------------------------|-------------------------------------|
| `DOCKER_USER`            | Docker registry username            |
| `DOCKER_PASSWORD`        | Docker registry password/token      |
| `COSIGN_PUBLIC_KEY_NEW`  | Base64-encoded Cosign public key    |
| `COSIGN_PRIVATE_KEY_NEW` | Base64-encoded Cosign private key   |
| `COSIGN_PRIVATE_PHRASE`  | Passphrase for your private key     |

---

## ✅ Enforcing Golden Base Images

This approach helps ensure:
- Developers can only build from **organization-approved base images**
- Final images are **signed at build-time**
- You can enforce signature validation using **Kyverno** in Kubernetes

![Supply Chain Flow](supply-chain-diagram.png)

---

## 📚 References

- [Cosign Documentation](https://docs.sigstore.dev/cosign/overview)
- [Kyverno verifyImages](https://kyverno.io/policies/)
- [Software Supply Chain Security](https://slsa.dev)

---

## 👮‍♂️ Who Signed This?

> You did. With Cosign.
