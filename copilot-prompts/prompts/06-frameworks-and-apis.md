# Frameworks and APIs Prompts

This section provides prompts for generating code that interacts with popular frameworks and APIs using GitHub Copilot.

## Web Frameworks

### Express.js REST API Endpoint

**Use Case:** Creating a REST API endpoint in Express.js.

**The Prompt:**
```javascript
// Create an Express.js route handler for GET /users
// - Fetch users from a database
// - Return users as JSON
// - Handle errors
```

**Example Output:**
```javascript
const express = require('express');
const router = express.Router();

// Mock database function
const getUsers = async () => [
  { id: 1, name: 'Alice' },
  { id: 2, name: 'Bob' }
];

router.get('/users', async (req, res) => {
  try {
    const users = await getUsers();
    res.json(users);
  } catch (error) {
    res.status(500).json({ error: 'Failed to fetch users' });
  }
});

module.exports = router;
```

**Explanation:** This prompt is effective because it specifies the framework (Express.js), the endpoint, and the requirements for error handling and data fetching, guiding Copilot to generate a complete and robust route handler.

## API Integration

### Python API Client

**Use Case:** Creating a Python client to interact with a REST API.

**The Prompt:**
```python
# Write a Python class to interact with a REST API
# - Use requests library
# - Implement GET and POST methods
# - Handle errors and timeouts
```

**Example Output:**
```python
import requests

class APIClient:
    def __init__(self, base_url):
        self.base_url = base_url

    def get(self, endpoint, params=None):
        try:
            response = requests.get(f"{self.base_url}{endpoint}", params=params, timeout=5)
            response.raise_for_status()
            return response.json()
        except requests.RequestException as e:
            print(f"GET request failed: {e}")
            return None

    def post(self, endpoint, data=None):
        try:
            response = requests.post(f"{self.base_url}{endpoint}", json=data, timeout=5)
            response.raise_for_status()
            return response.json()
        except requests.RequestException as e:
            print(f"POST request failed: {e}")
            return None
```

**Explanation:** This prompt is effective because it asks Copilot to generate a reusable API client class with error handling and support for both GET and POST requests, making it easy to interact with REST APIs.

## Framework-Specific Patterns

### Django Model Example

**Use Case:** Creating a Django model for a blog post.

**The Prompt:**
```python
# Create a Django model for a blog post
# - Fields: title, content, author, created_at, updated_at
# - Use appropriate field types
# - Add __str__ method
```

**Example Output:**
```python
from django.db import models

class BlogPost(models.Model):
    title = models.CharField(max_length=200)
    content = models.TextField()
    author = models.CharField(max_length=100)
    created_at = models.DateTimeField(auto_now_add=True)
    updated_at = models.DateTimeField(auto_now=True)

    def __str__(self):
        return self.title
```

**Explanation:** This prompt is effective because it specifies the fields and requirements for the Django model, guiding Copilot to generate a complete and idiomatic Django model class.
