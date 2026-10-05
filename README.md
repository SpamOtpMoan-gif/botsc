# SC GitHub Workers

Ini **repo worker**, bukan source bot Telegram.

Upload seluruh isi folder ini ke root repository GitHub.

## Actions yang muncul

- `Build Flutter`
- `Build Android`
- `Validate Worker`

Ketiganya memakai `workflow_dispatch`, sehingga tersedia tombol **Run workflow**.

## Kontrak yang cocok dengan SC

Bot memanggil:

```text
workflow: build-flutter.yml
inputs:
  jobId
  userId
  payload
```

Payload ZIP:

```json
{
  "mode": "zip",
  "url": "https://github.com/OWNER/REPO/releases/download/TAG/project.zip",
  "buildType": "release",
  "tag": "build-123"
}
```

Payload Web2APK:

```json
{
  "mode": "url",
  "url": "https://example.com",
  "appName": "My App",
  "iconUrl": ""
}
```

Artifact output:

```text
apk-JOB_ID
```

## Upload

Struktur root repo WAJIB:

```text
.github/
└── workflows/
    ├── build-flutter.yml
    ├── build-android.yml
    └── validate.yml
README.md
```

Jangan taruh `.github` satu tingkat terlalu dalam.

Setelah commit/push:
**GitHub → Actions** → workflow akan muncul.

## Token

Token GitHub **tidak disimpan di worker**. Token yang dipakai bot untuk
memanggil Actions tetap disimpan di server bot/environment variable.

Untuk private repository, token bot harus punya izin Actions/workflow dan akses
ke repository worker.
