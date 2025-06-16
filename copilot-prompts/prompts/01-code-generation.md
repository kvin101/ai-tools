# Code Generation Prompts

This section provides prompts for generating common code patterns, functions, and snippets using GitHub Copilot.

## Function Generation

### Python JSON API Client

**Use Case:** Creating a Python function to fetch and parse JSON from an API.

**The Prompt:**
```python
# Python function to fetch and parse JSON from a URL
# - takes a url as an argument
# - uses the requests library to make a GET request
# - handles potential request errors
# - returns the JSON data as a Python dictionary
```

**Example Output:**
```python
import requests

def get_json_from_url(url):
    """
    Fetches and parses JSON from a URL.

    Args:
        url: The URL to fetch the JSON from.

    Returns:
        The JSON data as a Python dictionary, or None if an error occurs.
    """
    try:
        response = requests.get(url)
        response.raise_for_status()  # Raise an exception for bad status codes
        return response.json()
    except requests.exceptions.RequestException as e:
        print(f"Error fetching data from {url}: {e}")
        return None

# Example usage:
# data = get_json_from_url("https://api.github.com/users/octocat")
# if data:
#     print(data)
```

**Explanation:** This prompt is effective because it clearly outlines the function's purpose, inputs, behavior, and error handling requirements. The comment format gives Copilot enough context to generate a well-structured function with appropriate error handling and documentation.

### JavaScript Data Processor

**Use Case:** Creating a function to transform an array of objects based on specific criteria.

**The Prompt:**
```javascript
/**
 * Function to filter and transform an array of user objects
 * - Filter users who are active (status === 'active')
 * - Transform each user to include their full name and formatted join date
 * - Sort users by their join date (newest first)
 * 
 * @param {Array<{id: number, firstName: string, lastName: string, status: string, joinDate: string}>} users
 * @return {Array<{id: number, fullName: string, formattedJoinDate: string, status: string}>}
 */
```

**Example Output:**
```javascript
/**
 * Function to filter and transform an array of user objects
 * - Filter users who are active (status === 'active')
 * - Transform each user to include their full name and formatted join date
 * - Sort users by their join date (newest first)
 * 
 * @param {Array<{id: number, firstName: string, lastName: string, status: string, joinDate: string}>} users
 * @return {Array<{id: number, fullName: string, formattedJoinDate: string, status: string}>}
 */
function processUsers(users) {
  return users
    .filter(user => user.status === 'active')
    .map(user => ({
      id: user.id,
      fullName: `${user.firstName} ${user.lastName}`,
      formattedJoinDate: new Date(user.joinDate).toLocaleDateString(),
      status: user.status
    }))
    .sort((a, b) => new Date(b.joinDate) - new Date(a.joinDate));
}
```

**Explanation:** This prompt uses JSDoc comments to clearly specify input and output types, making it easier for Copilot to generate accurate code. The bullet points outline the exact transformations needed, providing a clear step-by-step guide for the function logic.

## Class Generation

### Python Data Class

**Use Case:** Creating a Python data class for representing a product in an e-commerce system.

**The Prompt:**
```python
# Create a Product data class with the following attributes:
# - id (int): unique product identifier
# - name (str): product name
# - description (str): product description
# - price (float): product price
# - category (str): product category
# - in_stock (bool): whether the product is in stock
# - created_at (datetime): when the product was created
#
# Include:
# - proper type hints
# - default values where appropriate
# - string representation method
# - method to calculate discounted price (takes discount percentage)
```

**Example Output:**
```python
from dataclasses import dataclass
from datetime import datetime
from typing import Optional

@dataclass
class Product:
    id: int
    name: str
    description: str
    price: float
    category: str
    in_stock: bool = True
    created_at: datetime = datetime.now()
    
    def __str__(self) -> str:
        status = "In Stock" if self.in_stock else "Out of Stock"
        return f"{self.name} (${self.price:.2f}) - {status}"
    
    def calculate_discounted_price(self, discount_percentage: float) -> float:
        """
        Calculate the discounted price of the product.
        
        Args:
            discount_percentage: The discount percentage (0-100)
            
        Returns:
            The discounted price
        """
        if not 0 <= discount_percentage <= 100:
            raise ValueError("Discount percentage must be between 0 and 100")
        
        discount_factor = 1 - (discount_percentage / 100)
        return round(self.price * discount_factor, 2)
```

**Explanation:** This prompt provides a clear structure for the data class, including attribute names, types, and descriptions. By specifying additional methods and behaviors, Copilot can generate a more complete and useful class implementation.

## Algorithm Implementation

### Sorting Algorithm

**Use Case:** Implementing a merge sort algorithm in Java.

**The Prompt:**
```java
/**
 * Implement a merge sort algorithm for an array of integers
 * - Include the main mergeSort method
 * - Include the merge helper method
 * - Add appropriate comments explaining the algorithm
 * - Handle edge cases (null or empty array)
 */
```

**Example Output:**
```java
/**
 * Implement a merge sort algorithm for an array of integers
 * - Include the main mergeSort method
 * - Include the merge helper method
 * - Add appropriate comments explaining the algorithm
 * - Handle edge cases (null or empty array)
 */
public class MergeSort {
    
    /**
     * Sorts an array of integers using the merge sort algorithm.
     * 
     * @param arr The array to be sorted
     * @return The sorted array
     */
    public static int[] mergeSort(int[] arr) {
        // Handle edge cases
        if (arr == null || arr.length <= 1) {
            return arr;
        }
        
        // Create a copy of the array to avoid modifying the original
        int[] result = new int[arr.length];
        System.arraycopy(arr, 0, result, 0, arr.length);
        
        // Perform the merge sort
        mergeSortHelper(result, 0, result.length - 1);
        return result;
    }
    
    /**
     * Helper method that recursively divides and merges the array.
     * 
     * @param arr The array being sorted
     * @param left The left index of the subarray
     * @param right The right index of the subarray
     */
    private static void mergeSortHelper(int[] arr, int left, int right) {
        if (left < right) {
            // Find the middle point
            int mid = left + (right - left) / 2;
            
            // Sort first and second halves
            mergeSortHelper(arr, left, mid);
            mergeSortHelper(arr, mid + 1, right);
            
            // Merge the sorted halves
            merge(arr, left, mid, right);
        }
    }
    
    /**
     * Merges two subarrays of arr[].
     * 
     * @param arr The array being sorted
     * @param left The left index of the first subarray
     * @param mid The ending index of the first subarray
     * @param right The right index of the second subarray
     */
    private static void merge(int[] arr, int left, int mid, int right) {
        // Calculate sizes of the two subarrays to be merged
        int n1 = mid - left + 1;
        int n2 = right - mid;
        
        // Create temporary arrays
        int[] L = new int[n1];
        int[] R = new int[n2];
        
        // Copy data to temporary arrays
        for (int i = 0; i < n1; i++) {
            L[i] = arr[left + i];
        }
        for (int j = 0; j < n2; j++) {
            R[j] = arr[mid + 1 + j];
        }
        
        // Merge the temporary arrays
        
        // Initial indexes of first and second subarrays
        int i = 0, j = 0;
        
        // Initial index of merged subarray
        int k = left;
        while (i < n1 && j < n2) {
            if (L[i] <= R[j]) {
                arr[k] = L[i];
                i++;
            } else {
                arr[k] = R[j];
                j++;
            }
            k++;
        }
        
        // Copy remaining elements of L[] if any
        while (i < n1) {
            arr[k] = L[i];
            i++;
            k++;
        }
        
        // Copy remaining elements of R[] if any
        while (j < n2) {
            arr[k] = R[j];
            j++;
            k++;
        }
    }
    
    /**
     * Example usage of the merge sort algorithm.
     */
    public static void main(String[] args) {
        int[] arr = {12, 11, 13, 5, 6, 7};
        int[] sortedArr = mergeSort(arr);
        
        System.out.println("Sorted array:");
        for (int num : sortedArr) {
            System.out.print(num + " ");
        }
    }
}
```

**Explanation:** This prompt specifically requests implementation details such as helper methods and edge case handling. The explicit requirements for comments helps ensure Copilot generates well-documented code. By asking for a complete implementation, Copilot provides a comprehensive solution rather than just fragments.

## Utility Functions

### Regular Expression Generator

**Use Case:** Creating a regular expression to validate email addresses.

**The Prompt:**
```javascript
/**
 * Function to validate email addresses
 * - Should validate format (username@domain.tld)
 * - Username can contain letters, numbers, underscores, periods, and hyphens
 * - Domain name can contain letters, numbers, and hyphens
 * - TLD should be at least 2 characters
 * - Should handle subdomains
 * - Returns true for valid emails, false for invalid ones
 * 
 * Include:
 * - Regular expression pattern with explanation comments
 * - Validation function
 * - Test cases showing valid and invalid emails
 */
```

**Example Output:**
```javascript
/**
 * Function to validate email addresses
 * - Should validate format (username@domain.tld)
 * - Username can contain letters, numbers, underscores, periods, and hyphens
 * - Domain name can contain letters, numbers, and hyphens
 * - TLD should be at least 2 characters
 * - Should handle subdomains
 * - Returns true for valid emails, false for invalid ones
 * 
 * Include:
 * - Regular expression pattern with explanation comments
 * - Validation function
 * - Test cases showing valid and invalid emails
 */
function validateEmail(email) {
  // Regular expression breakdown:
  // ^                      - Start of string
  // ([a-zA-Z0-9_\-\.]+)   - Username: one or more letters, numbers, underscores, hyphens, or periods
  // @                      - The @ symbol
  // ([a-zA-Z0-9\-]+\.)+   - Domain name parts: one or more letters, numbers, or hyphens, followed by a dot
  //                          The + after this group ensures we can have subdomains
  // ([a-zA-Z]{2,})        - TLD: at least 2 letters
  // $                      - End of string
  const emailRegex = /^([a-zA-Z0-9_\-\.]+)@(([a-zA-Z0-9\-]+\.)+)([a-zA-Z]{2,})$/;
  
  return emailRegex.test(email);
}

// Test cases
function testEmailValidation() {
  const validEmails = [
    "user@example.com",
    "john.doe@example.com",
    "john-doe@example.com",
    "user@sub.domain.example.com",
    "user_name@example.co.uk"
  ];
  
  const invalidEmails = [
    "user@.com",                 // Missing domain name
    "user@example",              // Missing TLD
    "user@example.c",            // TLD too short
    "user@-domain.com",          // Domain starts with hyphen
    "user@domain-.com",          // Domain ends with hyphen
    ".user@domain.com",          // Username starts with period
    "user..name@domain.com",     // Double periods in username
    "user@domain..com",          // Double periods in domain
    "user@domain.com.",          // Ends with period
    "user name@domain.com"       // Space in username
  ];
  
  console.log("Testing valid emails:");
  validEmails.forEach(email => {
    console.log(`${email}: ${validateEmail(email)}`);
  });
  
  console.log("\nTesting invalid emails:");
  invalidEmails.forEach(email => {
    console.log(`${email}: ${validateEmail(email)}`);
  });
}

testEmailValidation();
```

**Explanation:** This prompt is effective because it specifies both the requirements for the regular expression and the structure of the surrounding code. By asking for test cases, Copilot generates examples that demonstrate the function's behavior with both valid and invalid inputs. The detailed requirements help ensure the generated regex correctly handles all the specified cases.
