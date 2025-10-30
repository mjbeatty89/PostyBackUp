# PostyBackUp

A secure backup repository for Postman collections with automatic API key detection and protection.

## 📋 Purpose

This repository serves as a centralized backup location for Postman API collections. It helps you:
- Version control your Postman collections
- Maintain a backup of your API configurations
- Automatically detect and secure API keys and sensitive data
- Track changes to your API definitions over time

## 🚀 Quick Start

### Exporting Collections from Postman

1. Open Postman and navigate to your collection
2. Click the three dots (⋯) next to your collection name
3. Select **Export**
4. Choose **Collection v2.1** (recommended format)
5. Save the JSON file

### Adding Collections to this Repository

1. Create a new folder under `collections/` with a descriptive name (e.g., `my-api-collection`)
2. Place your exported Postman collection JSON file in that folder
3. Commit and push your changes:
   ```bash
   git add collections/
   git commit -m "Add [collection-name] backup"
   git push
   ```

## 📁 Directory Structure

```
PostyBackUp/
├── collections/          # Store your Postman collection JSON files here
│   ├── example-api/     # Example collection folder
│   │   └── collection.json
│   └── another-api/
│       └── collection.json
├── .github/
│   └── workflows/       # Automated workflows for security scanning
└── README.md
```

## 🔒 Security Features

### Automatic API Key Detection

This repository includes an automated workflow that:
- Scans incoming Postman collections for API keys, tokens, and secrets
- Identifies common patterns like API keys, auth tokens, passwords
- Alerts you when sensitive data is detected
- Helps you move secrets to GitHub Secrets instead of committing them

### Best Practices for API Keys

**⚠️ IMPORTANT**: Never commit actual API keys or secrets to this repository!

When backing up collections:
1. **Use Postman Variables**: Replace sensitive values with `{{variable_name}}`
2. **Use Environments**: Store secrets in Postman environments (don't export these)
3. **GitHub Secrets**: For CI/CD, store actual keys in GitHub repository secrets

Example of a safe collection entry:
```json
{
  "header": [
    {
      "key": "Authorization",
      "value": "Bearer {{api_token}}",
      "type": "text"
    }
  ]
}
```

### Storing Secrets Safely

If your workflow detects API keys in your collections, follow these steps:

1. **Remove the actual key** from your collection file
2. **Replace it with a variable**: Use `{{API_KEY}}` or similar
3. **Store in GitHub Secrets**:
   - Go to repository Settings → Secrets and variables → Actions
   - Click "New repository secret"
   - Add your secret with a descriptive name
4. **Update your collection** to use the variable instead

## 🔧 Workflow Details

### Secret Detection Workflow

The repository includes a GitHub Actions workflow that:
- Triggers on every push to the repository
- Scans all JSON files in the `collections/` directory
- Detects patterns matching API keys, tokens, and secrets
- Creates alerts when sensitive data is found
- Provides guidance on securing detected secrets

Detected patterns include:
- API keys (various formats)
- Bearer tokens
- AWS access keys
- Private keys
- Passwords and credentials
- OAuth tokens

## 📝 Contributing

When adding new collections:
1. Create a descriptive folder name
2. Include a README in the collection folder if needed
3. Ensure no sensitive data is included
4. Test your collection in Postman before backing up

## 🆘 Troubleshooting

### Secret Detected in My Collection

If the workflow detects a secret:
1. Don't panic - the secret hasn't been exposed if caught before merge
2. Follow the alert instructions to replace it with a variable
3. Store the actual secret in GitHub Secrets
4. Re-commit the sanitized collection

### Collection Not Working After Backup

Ensure you've:
- Exported the correct version (v2.1)
- Included all necessary variables in your Postman environment
- Documented any required environment variables

## 📚 Resources

- [Postman Documentation](https://learning.postman.com/docs/getting-started/introduction/)
- [GitHub Secrets Documentation](https://docs.github.com/en/actions/security-guides/encrypted-secrets)
- [Postman Variables Guide](https://learning.postman.com/docs/sending-requests/variables/)

## 📄 License

This is a personal backup repository. Collections may have their own licensing terms.