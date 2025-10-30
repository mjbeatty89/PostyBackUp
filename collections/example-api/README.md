# Example API Collection

This is a sample Postman collection that demonstrates best practices for storing API collections in this repository.

## Variables Used

- `base_url`: The base URL for the API (e.g., https://api.example.com)
- `api_token`: Your API authentication token (store in Postman environment, not in the collection)

## Endpoints

### GET /api/v1/user/profile
Retrieves the authenticated user's profile information.

### POST /api/v1/resources
Creates a new resource.

## Setup

1. Import this collection into Postman
2. Create a new environment in Postman
3. Add the required variables (`base_url` and `api_token`) to your environment
4. Never commit actual API tokens or secrets to this repository
