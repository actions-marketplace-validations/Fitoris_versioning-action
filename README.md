# 🏷 Service Versioning GitHub Action

A reusable GitHub Action that enables **independent semantic versioning for each service in a monorepo**.  
Useful for managing deployments, CI/CD pipelines, or Docker image tagging per service.

---

## 💡 What Problem Does It Solve?

In monorepos with multiple services or microservices, using a single version for the whole repository leads to:

- Unnecessary rebuilds or deployments
- Difficult release tracking
- Entangled version histories

This action solves that by:
- Managing **version state separately per service**
- Bumping versions automatically or via tags
- Storing versions in dedicated `VERSION` files

---

## ✨ Features

- ✅ Tag-based versioning via Git tags like `ServiceName@1.2.3`
- ✅ Patch auto-bump on branch pushes
- ✅ Git commit and push of updated version file
- ✅ Customizable version folder root
- ✅ Easily used across any CI/CD or Docker pipeline

---

## 📥 Inputs

| Name             | Required | Description                                                                 |
|------------------|----------|-----------------------------------------------------------------------------|
| `service-name`   | ✅ Yes   | Name of the service (e.g., `AuditLog`, `UserService`).                      |
| `version-folder` | ✅ Yes   | Root folder to store version files. Actual path becomes `<root>/<service>/VERSION`. |

---

## 📤 Outputs

| Name     | Description                             |
|----------|-----------------------------------------|
| `version`| Computed version string (e.g., `1.0.4`) |

---

## 🚀 Usage

```yaml
permissions:
  contents: write

jobs:
  version:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4

      - name: Determine service version
        id: version
        uses: your-org/service-versioning-action@v1
        with:
          service-name: YourService
          version-folder: versions

      - name: Use version
        run: echo "VERSION=${{ steps.version.outputs.version }}"
