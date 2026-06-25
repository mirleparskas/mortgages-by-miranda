# Deploy Guide

The site is committed locally on the `main` branch.

## GitHub Pages

GitHub CLI is installed on this machine, but it still needs login.

From PowerShell:

```powershell
$env:Path += ';C:\Program Files\GitHub CLI'
cd C:\Users\m1gun\mortgages-by-miranda
gh auth login
gh repo create mortgages-by-miranda --public --source=. --remote=origin --push
```

Then enable Pages:

```powershell
gh api `
  --method PUT `
  -H "Accept: application/vnd.github+json" `
  /repos/OWNER/mortgages-by-miranda/pages `
  -f source='{"branch":"main","path":"/"}'
```

If the API command says Pages is already configured, the included GitHub Actions workflow will deploy after the push.

Expected test URL:

```text
https://OWNER.github.io/mortgages-by-miranda/
```

Replace `OWNER` with the GitHub username or organization.

## Railway

This repo already includes:

- `Dockerfile`
- `railway.json`
- `.dockerignore`

The easiest Railway path is to connect the GitHub repo in Railway:

1. Push to GitHub.
2. Open Railway.
3. Create a new project from the GitHub repo.
4. Select `mortgages-by-miranda`.
5. Railway will use the Dockerfile and serve the static site with nginx.

CLI path after Node and Railway CLI are installed:

```powershell
cd C:\Users\m1gun\mortgages-by-miranda
npm i -g @railway/cli
railway login
railway init
railway up
```
