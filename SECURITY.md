# Security Policy

## Protecting API Keys and Secrets

This repository is designed to backup Postman collections while keeping sensitive data secure.

### ✅ Do's

- **Use variables**: Always use Postman variables like `{{api_key}}` for sensitive values
- **Store in GitHub Secrets**: Keep actual API keys in GitHub repository secrets
- **Use environments**: Store secrets in Postman environments (don't export these)
- **Review before commit**: Always review your collection files before committing
- **Enable workflow**: Let the automated workflow scan for secrets before merge

### ❌ Don'ts

- **Never commit actual API keys** or tokens in collection files
- **Don't export environments** with real credentials
- **Don't disable** the secret scanning workflow
- **Don't ignore warnings** from the secret scanner

## Automated Secret Detection

This repository includes a GitHub Actions workflow that:
- Automatically scans all collection files on push
- Detects common patterns for API keys, tokens, and secrets
- Blocks merges when secrets are detected
- Provides guidance on securing your collections

## What to Do If You Accidentally Commit a Secret

If you accidentally commit an API key or secret:

1. **Revoke the exposed secret immediately** at your API provider
2. **Generate a new secret** from your API provider
3. **Remove the secret from git history**:
   ```bash
   git filter-branch --force --index-filter \
     'git rm --cached --ignore-unmatch path/to/file.json' \
     --prune-empty --tag-name-filter cat -- --all
   ```
4. **Force push the cleaned history** (⚠️ use with caution):
   ```bash
   git push origin --force --all
   ```
5. **Update your collection** to use variables instead
6. **Store the new secret** in GitHub Secrets or Postman environment

## Storing Secrets in GitHub

To use secrets in GitHub Actions:

1. Go to repository **Settings** → **Secrets and variables** → **Actions**
2. Click **New repository secret**
3. Enter a name (e.g., `POSTMAN_API_KEY`)
4. Paste the secret value
5. Click **Add secret**

## Reporting Security Issues

If you discover a security vulnerability in this repository or its workflows, please:
- Do NOT create a public issue
- Contact the repository owner directly
- Provide details about the vulnerability
- Allow time for the issue to be addressed before public disclosure

## Additional Resources

- [GitHub Secrets Documentation](https://docs.github.com/en/actions/security-guides/encrypted-secrets)
- [Postman Security Best Practices](https://learning.postman.com/docs/sending-requests/authorization/)
- [OWASP API Security](https://owasp.org/www-project-api-security/)
