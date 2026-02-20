# API Key Rotation Checklist

## 1) Rotate key immediately
- Create a new Web API key in Firebase/Google Cloud.
- Disable or delete the exposed key.

## 2) Restrict key usage
- Set **Application restrictions** to `HTTP referrers (web sites)`.
- Allow only your actual domains, for example:
  - `https://hoitddu.github.io/*`
  - `https://<your-custom-domain>/*`
- Set **API restrictions** to only APIs your app needs.

## 3) Lock Firebase access
- In Firebase Realtime Database Rules, apply `FIREBASE_SECURITY_RULES.json`.
- Keep anonymous auth enabled only if required for this app.
- Enable Firebase App Check for stronger abuse protection.

## 4) Remove leaked key from this repository history
- If the key was pushed, rewrite git history and force push.
- After rewriting, all collaborators should re-clone.

### Example commands
```powershell
python -m pip install git-filter-repo
'EXPOSED_API_KEY_VALUE==>REMOVED' | Set-Content -Encoding ASCII replacements.txt
git filter-repo --force --replace-text replacements.txt
git push origin --force --all
git push origin --force --tags
```

## 5) Verify
- Confirm old key no longer works.
- Confirm app works with the new key.
- Confirm GitHub Actions `Secret Scan` workflow passes.
