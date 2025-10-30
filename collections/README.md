# Collections Directory

This directory contains backed-up Postman collections. Each collection should be stored in its own subdirectory.

## Structure

```
collections/
├── my-api-collection/
│   ├── collection.json          # The exported Postman collection
│   └── README.md               # (Optional) Documentation for the collection
├── another-api/
│   └── collection.json
└── README.md                    # This file
```

## Adding a New Collection

1. **Export from Postman**:
   - Open Postman
   - Right-click on your collection
   - Select "Export"
   - Choose "Collection v2.1"
   - Save the file

2. **Create a folder** for your collection:
   ```bash
   mkdir -p collections/my-collection-name
   ```

3. **Move the exported file**:
   ```bash
   mv ~/Downloads/MyCollection.postman_collection.json collections/my-collection-name/collection.json
   ```

4. **(Optional) Add documentation**:
   Create a `README.md` in your collection folder describing:
   - What the API does
   - Required variables
   - Setup instructions

5. **Commit and push**:
   ```bash
   git add collections/my-collection-name/
   git commit -m "Add my-collection-name backup"
   git push
   ```

## Security Checklist

Before committing a collection, ensure:

- [ ] All API keys are replaced with variables (e.g., `{{api_key}}`)
- [ ] No Bearer tokens are hardcoded
- [ ] No passwords or credentials are included
- [ ] Authorization headers use variables
- [ ] Environment-specific values use variables

## Example Collection

Check out the `example-api` folder for a sample collection that follows best practices.

## Automation

When you push changes to this directory, an automated workflow will:
- Scan for hardcoded secrets
- Alert if any sensitive data is detected
- Provide guidance on securing your collections
- Block merges if secrets are found

## Tips

- **Use descriptive folder names**: `stripe-api` instead of `collection1`
- **Include version info**: `my-api-v2` if you have multiple versions
- **Document variables**: List required variables in the collection's README
- **Keep it organized**: One collection per folder
