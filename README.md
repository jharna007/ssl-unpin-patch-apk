# 🤖 Auto SSL-Unpin APK Action

> **GitHub Actions workflow** that automatically downloads an APK, patches it to **disable SSL-pinning** with [apk-mitm](https://github.com/shroudedcode/apk-mitm), and uploads the patched file as a workflow artifact.

---

## 📁 Repository layout
```bash
.
├── .github
│   └── workflows
│       └── patch-apk.yml   ← the workflow file
└── README.md               ← this file
```

---

## ⚙️ Workflow (`patch-apk.yml`)

| Step | Description |
|------|-------------|
| **1** | `workflow_dispatch` – triggered **manually** from the *Actions* tab |
| **2** | Installs **Node.js 20** |
| **3** | Installs **apk-mitm** globally |
| **4** | Downloads the APK from the **Catbox** mirror (fallback URL) |
| **5** | Runs `apk-mitm` → `base.apk` → `base-patched.apk` |
| **6** | Uploads the patched APK as an artifact named `base-patched-apk` |

The **latest patched APK** can be downloaded from the workflow run summary page.

---

## 🚀 How to use

1. **Fork** this repo.
2. Go to **Actions** → **Edit the `.github/workflows/patch-apk.yml` file** → Paste your apk download link inside the placeholder → **Run workflow**.  
3. Wait ~1-2 minutes.  
4. Download the artifact from the run summary page.

---

## 🔄 Changing the target APK

Edit the `Download APK from external download link` step inside `.github/workflows/patch-apk.yml`:

```yaml
- name: Download APK
  run: |
    curl -L -o base.apk 'DOWNLOAD_LINK'
```

> ⚠️ Make sure the new URL is a **direct download** link (no HTML pages).

---

## 🐛 Troubleshooting

| Issue | Fix |
|-------|-----|
| **Artifact empty / 0 B** | Check the download URL – must be a **raw file** (`curl -I` should return `Content-Type: application/vnd.android.package-archive`). |
| **apk-mitm fails** | Verify the APK is **not corrupted**; try locally first. |
| **Action permissions error** | Ensure repo has **Read & Write** Actions permissions (`Settings → Actions → General`). |

---

## 📄 License

The workflow script is released under [MIT](./LICENSE).  
[apk-mitm](https://github.com/shroudedcode/apk-mitm) is © Niklas Higi under MIT.
```
