# Writing and Explaining Code Prompts

This section provides prompts for writing clear, readable code and explaining complex code concepts using GitHub Copilot.

## Code Documentation

### Comprehensive Function Documentation

**Use Case:** Creating detailed documentation for a complex function.

**The Prompt:**
```javascript
/**
 * Write comprehensive JSDoc documentation for this function:
 */
function parseQueryParams(url, options = {}) {
  const defaultOptions = {
    parseNumbers: true,
    parseBooleans: true,
    arrayFormat: 'comma',
    undefinedForMissing: false
  };
  
  const mergedOptions = { ...defaultOptions, ...options };
  const queryStartIndex = url.indexOf('?');
  
  if (queryStartIndex === -1) {
    return {};
  }
  
  const query = url.slice(queryStartIndex + 1);
  const pairs = query.split('&');
  const result = {};
  
  for (const pair of pairs) {
    const [key, value] = pair.split('=').map(decodeURIComponent);
    
    // Skip if key is empty
    if (!key) continue;
    
    // Handle missing values
    if (value === undefined || value === '') {
      if (mergedOptions.undefinedForMissing) {
        result[key] = undefined;
      } else {
        result[key] = null;
      }
      continue;
    }
    
    // Parse arrays
    if (mergedOptions.arrayFormat === 'comma' && value.includes(',')) {
      const arrayValues = value.split(',').map(item => parseValue(item, mergedOptions));
      result[key] = arrayValues;
      continue;
    }
    
    // Add bracket notation support for arrays
    if (key.endsWith('[]')) {
      const cleanKey = key.slice(0, -2);
      if (!result[cleanKey]) {
        result[cleanKey] = [];
      }
      result[cleanKey].push(parseValue(value, mergedOptions));
      continue;
    }
    
    result[key] = parseValue(value, mergedOptions);
  }
  
  return result;
}

function parseValue(value, options) {
  // Parse booleans
  if (options.parseBooleans) {
    if (value.toLowerCase() === 'true') return true;
    if (value.toLowerCase() === 'false') return false;
  }
  
  // Parse numbers
  if (options.parseNumbers && !isNaN(Number(value)) && value.trim() !== '') {
    return Number(value);
  }
  
  return value;
}
```

**Example Output:**
```javascript
/**
 * Parses URL query parameters into an object with various type conversion options.
 * 
 * @param {string} url - The URL containing query parameters to parse
 * @param {Object} [options] - Configuration options for query parameter parsing
 * @param {boolean} [options.parseNumbers=true] - Whether to convert numeric strings to numbers
 * @param {boolean} [options.parseBooleans=true] - Whether to convert 'true'/'false' strings to booleans
 * @param {string} [options.arrayFormat='comma'] - The format for parsing arrays ('comma' for comma-separated values)
 * @param {boolean} [options.undefinedForMissing=false] - Whether to use undefined (true) or null (false) for parameters without values
 * @returns {Object} An object containing the parsed query parameters
 * 
 * @example
 * // Returns { page: 5, limit: 10, sort: 'desc', filters: ['active', 'featured'] }
 * parseQueryParams('https://example.com?page=5&limit=10&sort=desc&filters=active,featured');
 * 
 * @example
 * // With array bracket notation
 * // Returns { items: [1, 2, 3] }
 * parseQueryParams('https://example.com?items[]=1&items[]=2&items[]=3');
 * 
 * @example
 * // With custom options
 * // Returns { count: '10', active: 'true' } (no type conversion)
 * parseQueryParams('https://example.com?count=10&active=true', { 
 *   parseNumbers: false, 
 *   parseBooleans: false 
 * });
 */
function parseQueryParams(url, options = {}) {
  // Function implementation remains the same...
}

/**
 * Helper function for parsing individual query parameter values based on options.
 * 
 * @private
 * @param {string} value - The string value to parse
 * @param {Object} options - Parsing options
 * @param {boolean} options.parseNumbers - Whether to parse numeric strings to numbers
 * @param {boolean} options.parseBooleans - Whether to parse 'true'/'false' to booleans
 * @returns {string|number|boolean} The parsed value
 */
function parseValue(value, options) {
  // Function implementation remains the same...
}
```

**Explanation:** This prompt asks Copilot to document an existing function that has complex behavior. By showing the full implementation, Copilot can analyze the code's functionality, options, and edge cases. Copilot then generates comprehensive JSDoc documentation that explains parameters, return values, default options, and provides examples demonstrating different use cases. This approach is effective for obtaining quality documentation for complex functions without having to write it manually.

### Code Explanation

**Use Case:** Explaining a complex algorithm or code snippet in plain language.

**The Prompt:**
```python
# Explain this algorithm in clear, simple language:
# What is it doing and how does it work?
# Provide an example of when it would be used.

def find_largest_subarray_sum(arr):
    """
    Kadane's algorithm implementation for maximum subarray sum.
    """
    if not arr:
        return 0
        
    max_so_far = arr[0]
    max_ending_here = arr[0]
    
    for i in range(1, len(arr)):
        max_ending_here = max(arr[i], max_ending_here + arr[i])
        max_so_far = max(max_so_far, max_ending_here)
    
    return max_so_far
```

**Example Output:**
```markdown
# Explanation of Kadane's Algorithm

This code implements **Kadane's algorithm**, which efficiently finds the contiguous subarray with the largest sum within a one-dimensional array of numbers.

## What it's doing, step by step:

1. It starts by assuming the first element of the array is both the current best subarray ending at position 0 and the overall best subarray.

2. Then, for each subsequent element in the array, it makes a choice:
   - Either start a new subarray at the current position
   - OR extend the previous subarray by including the current element

3. At each step, it keeps track of two values:
   - `max_ending_here`: The maximum sum of a subarray that **must end** at the current position
   - `max_so_far`: The maximum sum found in any subarray examined so far

4. For each array element, it updates `max_ending_here` by choosing the better option between:
   - Taking just the current element (starting a new subarray)
   - Adding the current element to the previous subarray (extending the subarray)

5. It then updates `max_so_far` if the current subarray sum (`max_ending_here`) is better than any found so far.

6. After examining all array elements, `max_so_far` contains the maximum subarray sum.

## Example:

For the array `[-2, 1, -3, 4, -1, 2, 1, -5, 4]`:

| Position | Array Value | max_ending_here | max_so_far | Decision |
|----------|-------------|-----------------|------------|----------|
| 0        | -2          | -2              | -2         | Initial value |
| 1        | 1           | 1               | 1          | Start new subarray (1 > -2+1) |
| 2        | -3          | -2              | 1          | Extend subarray (1+(-3) > -3) |
| 3        | 4           | 4               | 4          | Start new subarray (4 > -2+4) |
| 4        | -1          | 3               | 4          | Extend subarray (4+(-1) > -1) |
| 5        | 2           | 5               | 5          | Extend subarray (3+2 > 2) |
| 6        | 1           | 6               | 6          | Extend subarray (5+1 > 1) |
| 7        | -5          | 1               | 6          | Extend subarray (6+(-5) > -5) |
| 8        | 4           | 5               | 6          | Extend subarray (1+4 > 4) |

The maximum subarray is `[4, -1, 2, 1]` with a sum of 6.

## When it's used:

Kadane's algorithm is commonly used in:

1. **Stock market analysis**: Finding the maximum profit possible from a single buy-sell transaction given historical prices.

2. **Image processing**: Identifying the brightest or most contrasting region in an image.

3. **Data analysis**: Finding periods of highest activity in time-series data.

4. **Game development**: Analyzing patterns in player performance over time.

The algorithm is highly efficient with O(n) time complexity, meaning it only needs to scan the array once, making it much faster than the naive approach of checking all possible subarrays, which would be O(n²).
```

**Explanation:** This prompt asks Copilot to provide a human-readable explanation of a complex algorithm. By including the algorithm's name in a comment and showing the code implementation, Copilot can identify the algorithm and explain its purpose, functionality, and applications. This approach is useful for understanding unfamiliar code or learning new algorithms by getting a clear, step-by-step explanation with examples and use cases.

## Writing Self-Documenting Code

### Self-Explanatory Variable Names

**Use Case:** Improving code readability by using descriptive variable names.

**The Prompt:**
```javascript
// Refactor this code to use self-explanatory variable and function names
// Add appropriate comments where needed
// Don't change the logic, just make it more readable

function p(a, t) {
  let r = 0;
  let d = [];
  
  for (let i = 0; i < a.length; i++) {
    let c = a[i];
    if (c.s === "a") {
      r += c.v;
    }
    
    if (c.t > t) {
      d.push(c.id);
    }
  }
  
  return {
    r: r,
    d: d
  };
}

// Example usage:
// const items = [
//   { id: 1, v: 10, s: "a", t: 5 },
//   { id: 2, v: 20, s: "i", t: 8 },
//   { id: 3, v: 30, s: "a", t: 3 },
//   { id: 4, v: 40, s: "a", t: 7 }
// ];
// const threshold = 6;
// const result = p(items, threshold);
```

**Example Output:**
```javascript
/**
 * Process a collection of items to calculate total active value and find delayed items
 * 
 * @param {Array<Object>} items - Array of items to process
 * @param {number} items[].id - Item identifier
 * @param {number} items[].v - Item value
 * @param {string} items[].s - Item status ('a' for active, 'i' for inactive)
 * @param {number} items[].t - Item time/duration
 * @param {number} timeThreshold - Threshold for identifying delayed items
 * @returns {Object} Object containing total active value and array of delayed item IDs
 */
function processItems(items, timeThreshold) {
  let totalActiveValue = 0;
  let delayedItemIds = [];
  
  for (let i = 0; i < items.length; i++) {
    const currentItem = items[i];
    
    // Sum values of active items
    if (currentItem.status === "a") {
      totalActiveValue += currentItem.value;
    }
    
    // Identify items that exceed the time threshold
    if (currentItem.time > timeThreshold) {
      delayedItemIds.push(currentItem.id);
    }
  }
  
  return {
    totalActiveValue: totalActiveValue,
    delayedItemIds: delayedItemIds
  };
}

// Example usage:
// const items = [
//   { id: 1, value: 10, status: "a", time: 5 },
//   { id: 2, value: 20, status: "i", time: 8 },
//   { id: 3, value: 30, status: "a", time: 3 },
//   { id: 4, value: 40, status: "a", time: 7 }
// ];
// const threshold = 6;
// const result = processItems(items, threshold);
```

**Explanation:** This prompt asks Copilot to improve code readability without changing its functionality. By showing the original code with unclear variable names and minimal comments, Copilot can identify the function's purpose and transform it with descriptive names and proper documentation. The prompt works well because it focuses on a specific aspect of code improvement (naming) while preserving the underlying logic.

## Writing Modular Code

### Function Decomposition

**Use Case:** Breaking down a large function into smaller, more focused functions for better readability and maintenance.

**The Prompt:**
```java
// Refactor this monolithic method into smaller, focused methods
// Each method should have a single responsibility
// Use meaningful method names
// Don't change the overall functionality

public class OrderProcessor {
    public OrderResult processOrder(Order order, User user) {
        // Validate order and user
        if (order == null || user == null) {
            return new OrderResult(false, "Order or user is null", null);
        }
        
        if (order.getItems() == null || order.getItems().isEmpty()) {
            return new OrderResult(false, "Order has no items", null);
        }
        
        if (!user.isActive()) {
            return new OrderResult(false, "User account is not active", null);
        }
        
        // Check inventory
        List<String> outOfStockItems = new ArrayList<>();
        double totalOrderPrice = 0.0;
        
        for (OrderItem item : order.getItems()) {
            Product product = inventory.getProduct(item.getProductId());
            if (product == null) {
                return new OrderResult(false, "Product not found: " + item.getProductId(), null);
            }
            
            if (product.getStock() < item.getQuantity()) {
                outOfStockItems.add(product.getName());
            }
            
            double itemPrice = product.getPrice() * item.getQuantity();
            totalOrderPrice += itemPrice;
        }
        
        if (!outOfStockItems.isEmpty()) {
            String errorMsg = "Items out of stock: " + String.join(", ", outOfStockItems);
            return new OrderResult(false, errorMsg, null);
        }
        
        // Apply discounts
        double discountedPrice = totalOrderPrice;
        
        if (user.isVip()) {
            discountedPrice = totalOrderPrice * 0.9; // 10% discount for VIP
        } else if (totalOrderPrice > 500) {
            discountedPrice = totalOrderPrice * 0.95; // 5% discount for large orders
        }
        
        if (user.hasPromoCode()) {
            PromoCode promoCode = promoCodeService.getPromoCode(user.getPromoCode());
            if (promoCode != null && promoCode.isValid()) {
                discountedPrice = discountedPrice * (1 - promoCode.getDiscountPercent() / 100.0);
            }
        }
        
        // Process payment
        PaymentResult paymentResult = paymentService.processPayment(user.getPaymentMethod(), discountedPrice);
        
        if (!paymentResult.isSuccess()) {
            return new OrderResult(false, "Payment failed: " + paymentResult.getErrorMessage(), null);
        }
        
        // Update inventory
        for (OrderItem item : order.getItems()) {
            Product product = inventory.getProduct(item.getProductId());
            product.setStock(product.getStock() - item.getQuantity());
            inventory.updateProduct(product);
        }
        
        // Create shipment
        Shipment shipment = new Shipment();
        shipment.setOrderId(order.getId());
        shipment.setAddress(user.getShippingAddress());
        shipment.setItems(order.getItems());
        shipment.setShippingMethod(order.getShippingMethod());
        
        ShipmentResult shipmentResult = shipmentService.createShipment(shipment);
        
        if (!shipmentResult.isSuccess()) {
            // Revert payment
            paymentService.refund(paymentResult.getTransactionId());
            return new OrderResult(false, "Shipment creation failed: " + shipmentResult.getErrorMessage(), null);
        }
        
        // Generate order confirmation
        OrderConfirmation confirmation = new OrderConfirmation();
        confirmation.setOrderId(order.getId());
        confirmation.setUserId(user.getId());
        confirmation.setOrderDate(new Date());
        confirmation.setTotalAmount(discountedPrice);
        confirmation.setEstimatedDelivery(shipmentResult.getEstimatedDeliveryDate());
        
        emailService.sendOrderConfirmation(user.getEmail(), confirmation);
        
        return new OrderResult(true, "Order processed successfully", confirmation);
    }
}
```

**Example Output:**
```java
/**
 * OrderProcessor handles the order processing workflow
 */
public class OrderProcessor {
    private InventoryService inventory;
    private PaymentService paymentService;
    private ShipmentService shipmentService;
    private EmailService emailService;
    private PromoCodeService promoCodeService;
    
    /**
     * Process an order for a user
     * 
     * @param order The order to process
     * @param user The user placing the order
     * @return Result of the order processing
     */
    public OrderResult processOrder(Order order, User user) {
        // Validate inputs
        OrderResult validationResult = validateOrderAndUser(order, user);
        if (!validationResult.isSuccess()) {
            return validationResult;
        }
        
        // Check inventory
        InventoryCheckResult inventoryResult = checkInventoryAvailability(order);
        if (!inventoryResult.isSuccess()) {
            return new OrderResult(false, inventoryResult.getErrorMessage(), null);
        }
        
        // Calculate price with discounts
        double finalPrice = calculateDiscountedPrice(
            inventoryResult.getTotalPrice(), 
            user
        );
        
        // Process payment
        PaymentResult paymentResult = processPayment(user, finalPrice);
        if (!paymentResult.isSuccess()) {
            return new OrderResult(false, "Payment failed: " + paymentResult.getErrorMessage(), null);
        }
        
        try {
            // Update inventory
            updateInventory(order);
            
            // Create shipment
            ShipmentResult shipmentResult = createShipment(order, user);
            if (!shipmentResult.isSuccess()) {
                // Revert payment on shipment failure
                paymentService.refund(paymentResult.getTransactionId());
                return new OrderResult(false, "Shipment creation failed: " + shipmentResult.getErrorMessage(), null);
            }
            
            // Generate order confirmation
            OrderConfirmation confirmation = createOrderConfirmation(order, user, finalPrice, shipmentResult);
            
            // Send confirmation email
            emailService.sendOrderConfirmation(user.getEmail(), confirmation);
            
            return new OrderResult(true, "Order processed successfully", confirmation);
            
        } catch (Exception e) {
            // Revert payment on any exception
            paymentService.refund(paymentResult.getTransactionId());
            return new OrderResult(false, "Error during order processing: " + e.getMessage(), null);
        }
    }
    
    /**
     * Validate order and user data
     */
    private OrderResult validateOrderAndUser(Order order, User user) {
        if (order == null || user == null) {
            return new OrderResult(false, "Order or user is null", null);
        }
        
        if (order.getItems() == null || order.getItems().isEmpty()) {
            return new OrderResult(false, "Order has no items", null);
        }
        
        if (!user.isActive()) {
            return new OrderResult(false, "User account is not active", null);
        }
        
        return new OrderResult(true, "", null);
    }
    
    /**
     * Check if all items in the order are available in inventory
     */
    private InventoryCheckResult checkInventoryAvailability(Order order) {
        List<String> outOfStockItems = new ArrayList<>();
        double totalOrderPrice = 0.0;
        
        for (OrderItem item : order.getItems()) {
            Product product = inventory.getProduct(item.getProductId());
            if (product == null) {
                return new InventoryCheckResult(false, "Product not found: " + item.getProductId(), 0);
            }
            
            if (product.getStock() < item.getQuantity()) {
                outOfStockItems.add(product.getName());
            }
            
            double itemPrice = product.getPrice() * item.getQuantity();
            totalOrderPrice += itemPrice;
        }
        
        if (!outOfStockItems.isEmpty()) {
            String errorMsg = "Items out of stock: " + String.join(", ", outOfStockItems);
            return new InventoryCheckResult(false, errorMsg, 0);
        }
        
        return new InventoryCheckResult(true, "", totalOrderPrice);
    }
    
    /**
     * Calculate final price after applying all applicable discounts
     */
    private double calculateDiscountedPrice(double totalOrderPrice, User user) {
        double discountedPrice = totalOrderPrice;
        
        // Apply user tier discounts
        discountedPrice = applyUserDiscounts(discountedPrice, user, totalOrderPrice);
        
        // Apply promo code if available
        discountedPrice = applyPromoCode(discountedPrice, user);
        
        return discountedPrice;
    }
    
    /**
     * Apply discounts based on user tier and order size
     */
    private double applyUserDiscounts(double currentPrice, User user, double originalPrice) {
        if (user.isVip()) {
            return currentPrice * 0.9; // 10% discount for VIP
        } else if (originalPrice > 500) {
            return currentPrice * 0.95; // 5% discount for large orders
        }
        return currentPrice;
    }
    
    /**
     * Apply promo code discount if user has a valid code
     */
    private double applyPromoCode(double currentPrice, User user) {
        if (user.hasPromoCode()) {
            PromoCode promoCode = promoCodeService.getPromoCode(user.getPromoCode());
            if (promoCode != null && promoCode.isValid()) {
                return currentPrice * (1 - promoCode.getDiscountPercent() / 100.0);
            }
        }
        return currentPrice;
    }
    
    /**
     * Process the payment for an order
     */
    private PaymentResult processPayment(User user, double amount) {
        return paymentService.processPayment(user.getPaymentMethod(), amount);
    }
    
    /**
     * Update inventory levels for all items in the order
     */
    private void updateInventory(Order order) {
        for (OrderItem item : order.getItems()) {
            Product product = inventory.getProduct(item.getProductId());
            product.setStock(product.getStock() - item.getQuantity());
            inventory.updateProduct(product);
        }
    }
    
    /**
     * Create a shipment for the order
     */
    private ShipmentResult createShipment(Order order, User user) {
        Shipment shipment = new Shipment();
        shipment.setOrderId(order.getId());
        shipment.setAddress(user.getShippingAddress());
        shipment.setItems(order.getItems());
        shipment.setShippingMethod(order.getShippingMethod());
        
        return shipmentService.createShipment(shipment);
    }
    
    /**
     * Create the order confirmation
     */
    private OrderConfirmation createOrderConfirmation(
            Order order, 
            User user, 
            double finalPrice, 
            ShipmentResult shipmentResult) {
        OrderConfirmation confirmation = new OrderConfirmation();
        confirmation.setOrderId(order.getId());
        confirmation.setUserId(user.getId());
        confirmation.setOrderDate(new Date());
        confirmation.setTotalAmount(finalPrice);
        confirmation.setEstimatedDelivery(shipmentResult.getEstimatedDeliveryDate());
        
        return confirmation;
    }
    
    /**
     * Helper class for inventory check results
     */
    private static class InventoryCheckResult {
        private boolean success;
        private String errorMessage;
        private double totalPrice;
        
        public InventoryCheckResult(boolean success, String errorMessage, double totalPrice) {
            this.success = success;
            this.errorMessage = errorMessage;
            this.totalPrice = totalPrice;
        }
        
        public boolean isSuccess() {
            return success;
        }
        
        public String getErrorMessage() {
            return errorMessage;
        }
        
        public double getTotalPrice() {
            return totalPrice;
        }
    }
}
```

**Explanation:** This prompt asks Copilot to refactor a large, complex method into smaller, focused methods following the Single Responsibility Principle. By showing the monolithic implementation, Copilot can identify distinct logical sections that can be extracted into separate methods. The prompt is effective because it emphasizes modular design while preserving the overall functionality, resulting in more maintainable and testable code.

## Writing Robust Code

### Error Handling Best Practices

**Use Case:** Adding robust error handling to existing code.

**The Prompt:**
```typescript
/**
 * Improve this TypeScript function with better error handling:
 * - Add proper type checking
 * - Use try/catch blocks appropriately
 * - Use custom error types
 * - Add descriptive error messages
 * - Log errors with context
 * - Return meaningful error responses
 */
 
async function updateUserProfile(userId: string, profileData: any) {
  const user = await database.findUserById(userId);
  
  user.name = profileData.name;
  user.email = profileData.email;
  user.preferences = profileData.preferences;
  
  if (profileData.avatar) {
    const avatarUrl = await uploadAvatar(profileData.avatar);
    user.avatarUrl = avatarUrl;
  }
  
  await user.save();
  
  return {
    success: true,
    user
  };
}
```

**Example Output:**
```typescript
/**
 * Custom error types for profile update operations
 */
class UserNotFoundError extends Error {
  constructor(userId: string) {
    super(`User with ID ${userId} not found`);
    this.name = 'UserNotFoundError';
  }
}

class ProfileUpdateError extends Error {
  public readonly cause?: Error;
  
  constructor(message: string, cause?: Error) {
    super(message);
    this.name = 'ProfileUpdateError';
    this.cause = cause;
  }
}

class AvatarUploadError extends Error {
  constructor(message: string, public readonly cause?: Error) {
    super(`Failed to upload avatar: ${message}`);
    this.name = 'AvatarUploadError';
  }
}

/**
 * Interface for user profile data
 */
interface ProfileData {
  name?: string;
  email?: string;
  preferences?: Record<string, unknown>;
  avatar?: Buffer | File | string;
}

/**
 * Interface for the function response
 */
interface ProfileUpdateResult {
  success: boolean;
  user?: User;
  message?: string;
  error?: {
    code: string;
    details?: unknown;
  };
}

/**
 * Updates a user's profile with the provided data
 * 
 * @param userId - The unique identifier of the user
 * @param profileData - The profile information to update
 * @returns A result object indicating success or failure with relevant data
 * @throws Will not throw exceptions but return them in the result object
 */
async function updateUserProfile(
  userId: string, 
  profileData: ProfileData
): Promise<ProfileUpdateResult> {
  // Validate input parameters
  if (!userId || typeof userId !== 'string') {
    return {
      success: false,
      message: 'Invalid user ID provided',
      error: {
        code: 'INVALID_USER_ID',
        details: userId
      }
    };
  }

  if (!profileData || typeof profileData !== 'object') {
    return {
      success: false,
      message: 'Profile data must be an object',
      error: {
        code: 'INVALID_PROFILE_DATA'
      }
    };
  }

  try {
    // Find the user
    const user = await database.findUserById(userId);
    
    if (!user) {
      throw new UserNotFoundError(userId);
    }
    
    // Update basic profile information with validation
    if (profileData.name !== undefined) {
      if (typeof profileData.name !== 'string' || profileData.name.trim() === '') {
        throw new ProfileUpdateError('Name must be a non-empty string');
      }
      user.name = profileData.name;
    }
    
    if (profileData.email !== undefined) {
      if (typeof profileData.email !== 'string' || !isValidEmail(profileData.email)) {
        throw new ProfileUpdateError('Invalid email address format');
      }
      user.email = profileData.email;
    }
    
    if (profileData.preferences !== undefined) {
      if (typeof profileData.preferences !== 'object') {
        throw new ProfileUpdateError('Preferences must be an object');
      }
      user.preferences = profileData.preferences;
    }
    
    // Handle avatar upload if provided
    if (profileData.avatar) {
      try {
        const avatarUrl = await uploadAvatar(profileData.avatar);
        user.avatarUrl = avatarUrl;
      } catch (error) {
        // Log the error but continue with the rest of the profile update
        const uploadError = new AvatarUploadError('Failed to upload avatar', error as Error);
        console.error(uploadError);
        
        // Add a message about the avatar failure
        return {
          success: true,
          user,
          message: 'Profile updated but avatar upload failed',
          error: {
            code: 'AVATAR_UPLOAD_FAILED',
            details: error instanceof Error ? error.message : undefined
          }
        };
      }
    }
    
    // Save the updated user profile
    await user.save();
    
    return {
      success: true,
      user,
      message: 'Profile updated successfully'
    };
    
  } catch (error) {
    // Determine the error type and log appropriately
    if (error instanceof UserNotFoundError) {
      console.warn(`User lookup failed: ${error.message}`);
      return {
        success: false,
        message: error.message,
        error: {
          code: 'USER_NOT_FOUND',
          details: userId
        }
      };
    } else if (error instanceof ProfileUpdateError) {
      console.error(`Profile update error: ${error.message}`, { userId, cause: error.cause });
      return {
        success: false,
        message: error.message,
        error: {
          code: 'PROFILE_UPDATE_FAILED',
          details: error.cause
        }
      };
    } else {
      // Unexpected error
      console.error('Unexpected error during profile update:', error, { userId });
      return {
        success: false,
        message: 'An unexpected error occurred while updating the profile',
        error: {
          code: 'INTERNAL_ERROR',
          details: error instanceof Error ? error.message : undefined
        }
      };
    }
  }
}

/**
 * Validate email format
 */
function isValidEmail(email: string): boolean {
  const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
  return emailRegex.test(email);
}
```

**Explanation:** This prompt asks Copilot to enhance a function with robust error handling, specifying several best practices. By showing a simple function with minimal error handling, Copilot can identify potential failure points and improve the code by adding type definitions, custom error classes, input validation, appropriate try/catch blocks, and error logging. The prompt is effective because it lists specific error handling techniques to implement, guiding Copilot to produce a comprehensive solution.

## Writing Dynamic Code

### Template-Based Code Generation

**Use Case:** Creating a template for generating repetitive code patterns.

**The Prompt:**
```typescript
/**
 * Generate a TypeScript React component template
 * with the following features:
 * 
 * - Functional component using React hooks
 * - TypeScript props interface
 * - State management with useState
 * - Side effects with useEffect
 * - Error handling with try/catch
 * - Loading state
 * - TypeScript generics for API response
 * - Proper JSDoc comments
 * - Export statement
 * - CSS module import
 * 
 * Component name: UserProfileCard
 * Props: userId (string), showDetails (boolean)
 * State: user object, loading state, error state
 * Effect: Fetch user data when component mounts or userId changes
 */
```

**Example Output:**
```typescript
/**
 * UserProfileCard.tsx
 * 
 * A component that displays a user's profile information in a card format.
 * Fetches user data based on the provided userId and displays it with
 * optional details when showDetails is true.
 */

import React, { useState, useEffect } from 'react';
import styles from './UserProfileCard.module.css';

/**
 * User data structure returned from the API
 */
interface UserData {
  id: string;
  name: string;
  email: string;
  avatarUrl: string;
  joinDate: string;
  bio?: string;
  location?: string;
  socialLinks?: {
    twitter?: string;
    github?: string;
    linkedin?: string;
  };
}

/**
 * Props for the UserProfileCard component
 */
interface UserProfileCardProps {
  /** The unique identifier for the user to display */
  userId: string;
  /** Whether to show additional user details */
  showDetails: boolean;
  /** Optional callback when the profile is clicked */
  onProfileClick?: (userId: string) => void;
}

/**
 * A component that displays a user's profile information in a card format
 */
export const UserProfileCard: React.FC<UserProfileCardProps> = ({
  userId,
  showDetails,
  onProfileClick,
}) => {
  // State management
  const [user, setUser] = useState<UserData | null>(null);
  const [loading, setLoading] = useState<boolean>(true);
  const [error, setError] = useState<Error | null>(null);

  /**
   * Fetches user data from the API
   */
  const fetchUserData = async (id: string): Promise<void> => {
    setLoading(true);
    setError(null);

    try {
      // Replace with your actual API endpoint
      const response = await fetch(`/api/users/${id}`);
      
      if (!response.ok) {
        throw new Error(`Failed to fetch user data: ${response.statusText}`);
      }
      
      const userData: UserData = await response.json();
      setUser(userData);
    } catch (err) {
      console.error('Error fetching user data:', err);
      setError(err instanceof Error ? err : new Error('An unknown error occurred'));
    } finally {
      setLoading(false);
    }
  };

  // Fetch user data when component mounts or userId changes
  useEffect(() => {
    if (userId) {
      fetchUserData(userId);
    }
    
    return () => {
      // Cleanup if needed (e.g., cancel pending requests)
    };
  }, [userId]);

  /**
   * Handle profile card click
   */
  const handleCardClick = () => {
    if (onProfileClick && user) {
      onProfileClick(user.id);
    }
  };

  // Loading state
  if (loading) {
    return (
      <div className={styles.profileCard}>
        <div className={styles.loadingSpinner}>Loading user data...</div>
      </div>
    );
  }

  // Error state
  if (error) {
    return (
      <div className={`${styles.profileCard} ${styles.error}`}>
        <p className={styles.errorMessage}>Error: {error.message}</p>
        <button onClick={() => fetchUserData(userId)} className={styles.retryButton}>
          Retry
        </button>
      </div>
    );
  }

  // No user data
  if (!user) {
    return (
      <div className={`${styles.profileCard} ${styles.empty}`}>
        <p>No user information available</p>
      </div>
    );
  }

  // Render user profile
  return (
    <div 
      className={styles.profileCard}
      onClick={handleCardClick}
    >
      <div className={styles.avatarContainer}>
        <img 
          src={user.avatarUrl} 
          alt={`${user.name}'s avatar`} 
          className={styles.avatar}
        />
      </div>
      
      <div className={styles.userInfo}>
        <h3 className={styles.userName}>{user.name}</h3>
        <p className={styles.userEmail}>{user.email}</p>
        
        {showDetails && (
          <div className={styles.userDetails}>
            <p className={styles.joinDate}>
              Joined {new Date(user.joinDate).toLocaleDateString()}
            </p>
            
            {user.bio && (
              <p className={styles.userBio}>{user.bio}</p>
            )}
            
            {user.location && (
              <p className={styles.userLocation}>
                <span className={styles.icon}>📍</span> {user.location}
              </p>
            )}
            
            {user.socialLinks && Object.keys(user.socialLinks).length > 0 && (
              <div className={styles.socialLinks}>
                {user.socialLinks.twitter && (
                  <a href={user.socialLinks.twitter} className={styles.socialIcon}>
                    Twitter
                  </a>
                )}
                {user.socialLinks.github && (
                  <a href={user.socialLinks.github} className={styles.socialIcon}>
                    GitHub
                  </a>
                )}
                {user.socialLinks.linkedin && (
                  <a href={user.socialLinks.linkedin} className={styles.socialIcon}>
                    LinkedIn
                  </a>
                )}
              </div>
            )}
          </div>
        )}
      </div>
    </div>
  );
};

export default UserProfileCard;
```

**Explanation:** This prompt asks Copilot to generate a template for a React component with specific features. By listing the required features in detail, Copilot can create a comprehensive component template that follows React and TypeScript best practices. The prompt is effective because it provides clear specifications about the component's name, props, state, and behaviors, allowing Copilot to generate a fully-formed, production-ready component template that can be used as a starting point for actual development.
