# ✅ HF Space Sync

> A lightweight GitHub Action that verifies your Hugging Face Space exists and force-syncs your GitHub **main** branch to the Space’s **main** branch.

---

## 🚀 Overview

Whenever you push to **GitHub’s `main`**, this action will:

1. **Check out** your repository (full history + LFS).  
2. **Compute** the full Space repository path (`hf_user`/`hf_space`).  
3. **Verify** that `https://huggingface.co/spaces/<hf_user>/<hf_space>.git` exists.  
4. **Force-push** your local `HEAD` (GitHub’s `main`) to the Space’s `main` branch.  

No extra branch configuration—just trigger on `main` and your Space stays in lock-step.

---

## 📥 Inputs

| Name       | Description                                                                                 | Required |  
|------------|---------------------------------------------------------------------------------------------|:--------:|  
| `hf_user`  | Your Hugging Face username or organization (e.g. `ealizadeh`).                              |   ✅ Yes  |  
| `hf_space` | The name of your Hugging Face Space (e.g. `GAIA-Agent`). **Do not** include the `user/` prefix. |   ✅ Yes  |  
| `hf_token` | Your Hugging Face API token with **write** permissions on the Space. Store this as a GitHub secret. |   ✅ Yes  |  

---

## 🔧 Usage

Add a workflow file in your repo, for example at `.github/workflows/sync-hf-space.yml`:

```yaml
name: 🚀 Sync HF Space

on:
  push:
    branches: [ main ]      # ← only runs on pushes to `main`
  workflow_dispatch:        # ← also allows manual triggers

jobs:
  sync:
    runs-on: ubuntu-latest

    steps:
      - name: ✅ HF Space Sync
        uses: e-alizadeh/gh-actions/hf-space-sync@v1.0.0
        with:
          hf_user:  "ealizadeh"     # e.g. "ealizadeh"
          hf_space: "GAIA-Agent"                # just the Space’s name
          hf_token: ${{ secrets.HF_TOKEN }}     # write-enabled HF token
```