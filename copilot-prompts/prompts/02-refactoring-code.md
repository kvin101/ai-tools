# Code Refactoring Prompts

This section provides prompts for refactoring existing code to improve readability, performance, and maintainability using GitHub Copilot.

## Simplifying Complex Logic

### Refactor Nested Conditionals

**Use Case:** Simplifying deeply nested if-else statements into more readable code.

**The Prompt:**
```javascript
// Refactor this complex nested conditional structure
// to be more readable and maintainable
// Consider using early returns, guard clauses, or the strategy pattern

function processOrder(order) {
  if (order) {
    if (order.isValid) {
      if (order.items && order.items.length > 0) {
        if (order.paymentMethod) {
          if (order.paymentMethod === 'credit' || order.paymentMethod === 'debit') {
            if (order.paymentInfo && order.paymentInfo.cardNumber && order.paymentInfo.expiryDate) {
              // Process the payment
              const paymentResult = processPayment(order.paymentInfo);
              if (paymentResult.success) {
                // Update inventory
                const inventoryResult = updateInventory(order.items);
                if (inventoryResult.success) {
                  // Generate shipping label
                  const shippingResult = generateShippingLabel(order.shippingAddress);
                  if (shippingResult.success) {
                    return {
                      success: true,
                      message: 'Order processed successfully'
                    };
                  } else {
                    return {
                      success: false,
                      message: 'Failed to generate shipping label'
                    };
                  }
                } else {
                  return {
                    success: false,
                    message: 'Failed to update inventory'
                  };
                }
              } else {
                return {
                  success: false,
                  message: 'Payment processing failed'
                };
              }
            } else {
              return {
                success: false,
                message: 'Incomplete payment information'
              };
            }
          } else {
            return {
              success: false,
              message: 'Unsupported payment method'
            };
          }
        } else {
          return {
            success: false,
            message: 'Payment method not specified'
          };
        }
      } else {
        return {
          success: false,
          message: 'Order has no items'
        };
      }
    } else {
      return {
        success: false,
        message: 'Order is invalid'
      };
    }
  } else {
    return {
      success: false,
      message: 'Order not provided'
    };
  }
}
```

**Example Output:**
```javascript
/**
 * Process an order through payment, inventory update, and shipping
 * @param {Order} order - The order to process
 * @return {Object} Result with success status and message
 */
function processOrder(order) {
  // Guard clauses for validation
  if (!order) {
    return { success: false, message: 'Order not provided' };
  }
  
  if (!order.isValid) {
    return { success: false, message: 'Order is invalid' };
  }
  
  if (!order.items || order.items.length === 0) {
    return { success: false, message: 'Order has no items' };
  }
  
  if (!order.paymentMethod) {
    return { success: false, message: 'Payment method not specified' };
  }
  
  const validPaymentMethods = ['credit', 'debit'];
  if (!validPaymentMethods.includes(order.paymentMethod)) {
    return { success: false, message: 'Unsupported payment method' };
  }
  
  const { paymentInfo } = order;
  if (!paymentInfo || !paymentInfo.cardNumber || !paymentInfo.expiryDate) {
    return { success: false, message: 'Incomplete payment information' };
  }
  
  // Process the payment
  const paymentResult = processPayment(paymentInfo);
  if (!paymentResult.success) {
    return { success: false, message: 'Payment processing failed' };
  }
  
  // Update inventory
  const inventoryResult = updateInventory(order.items);
  if (!inventoryResult.success) {
    return { success: false, message: 'Failed to update inventory' };
  }
  
  // Generate shipping label
  const shippingResult = generateShippingLabel(order.shippingAddress);
  if (!shippingResult.success) {
    return { success: false, message: 'Failed to generate shipping label' };
  }
  
  // All processes completed successfully
  return { success: true, message: 'Order processed successfully' };
}
```

**Explanation:** This prompt asks Copilot to refactor nested conditionals using specific strategies like early returns and guard clauses. By showing the complex code structure and asking for a simplified version, Copilot can apply good programming practices to transform spaghetti code into clean, readable code. The suggested techniques in the comment guide Copilot toward preferred solutions.

## Performance Optimization

### Refactor Inefficient Loop

**Use Case:** Optimizing a function that inefficiently processes an array of data.

**The Prompt:**
```python
# Refactor this function to improve performance:
# - Avoid multiple iterations over the same data
# - Reduce time complexity
# - Use more efficient data structures if appropriate
# - Maintain the same functionality

def process_user_data(users):
    """
    Process user data to:
    1. Find users with premium accounts
    2. Calculate the average age of users
    3. Identify the most common country
    4. Return summary statistics
    """
    premium_users = []
    for user in users:
        if user.get('account_type') == 'premium':
            premium_users.append(user)
    
    total_age = 0
    for user in users:
        if 'age' in user:
            total_age += user['age']
    avg_age = total_age / len(users) if users else 0
    
    countries = {}
    for user in users:
        country = user.get('country')
        if country:
            if country in countries:
                countries[country] += 1
            else:
                countries[country] = 1
    
    most_common_country = None
    max_count = 0
    for country, count in countries.items():
        if count > max_count:
            most_common_country = country
            max_count = count
    
    return {
        'premium_user_count': len(premium_users),
        'average_age': avg_age,
        'most_common_country': most_common_country,
        'total_users': len(users)
    }
```

**Example Output:**
```python
from collections import Counter

def process_user_data(users):
    """
    Process user data to:
    1. Find users with premium accounts
    2. Calculate the average age of users
    3. Identify the most common country
    4. Return summary statistics
    
    Args:
        users (list): List of user dictionaries
        
    Returns:
        dict: Summary statistics about the users
    """
    if not users:
        return {
            'premium_user_count': 0,
            'average_age': 0,
            'most_common_country': None,
            'total_users': 0
        }
    
    # Process everything in a single pass
    premium_count = 0
    total_age = 0
    valid_age_count = 0
    countries = Counter()
    
    for user in users:
        # Count premium users
        if user.get('account_type') == 'premium':
            premium_count += 1
        
        # Sum ages
        if 'age' in user:
            total_age += user['age']
            valid_age_count += 1
        
        # Count countries
        country = user.get('country')
        if country:
            countries[country] += 1
    
    # Calculate average age
    avg_age = total_age / valid_age_count if valid_age_count > 0 else 0
    
    # Find most common country
    most_common_country = countries.most_common(1)[0][0] if countries else None
    
    return {
        'premium_user_count': premium_count,
        'average_age': avg_age,
        'most_common_country': most_common_country,
        'total_users': len(users)
    }
```

**Explanation:** This prompt works well because it specifies clear optimization goals while emphasizing that the functionality must remain the same. By pointing out specific issues like multiple iterations and suggesting more efficient data structures, Copilot can focus on applying appropriate optimizations like using Counter and processing everything in a single pass.

## Modernizing Legacy Code

### Convert to Modern JavaScript

**Use Case:** Updating legacy JavaScript code to use modern ES6+ features.

**The Prompt:**
```javascript
// Convert this legacy JavaScript code to modern ES6+:
// - Use let/const instead of var
// - Use arrow functions where appropriate
// - Use template literals for string concatenation
// - Use destructuring assignment
// - Use spread/rest operators
// - Use default parameters
// - Use async/await instead of Promises
// - Add proper JSDoc comments

var API_URL = "https://api.example.com/v1/";

function fetchUserData(userId, callback) {
  var url = API_URL + "users/" + userId;
  
  $.ajax({
    url: url,
    type: "GET",
    success: function(data) {
      var user = {
        name: data.firstName + " " + data.lastName,
        email: data.email,
        roles: data.roles || []
      };
      
      callback(null, user);
    },
    error: function(xhr, status, error) {
      callback(error, null);
    }
  });
}

function displayUserInfo(error, user) {
  if (error) {
    console.log("Error fetching user: " + error);
    return;
  }
  
  var rolesText = "";
  for (var i = 0; i < user.roles.length; i++) {
    rolesText += "<li>" + user.roles[i] + "</li>";
  }
  
  var userInfoDiv = document.getElementById("user-info");
  userInfoDiv.innerHTML = "<h2>" + user.name + "</h2>" +
                          "<p>Email: " + user.email + "</p>" +
                          "<ul>" + rolesText + "</ul>";
}

function init(userId) {
  userId = userId || "default";
  fetchUserData(userId, displayUserInfo);
}

$(document).ready(function() {
  init();
});
```

**Example Output:**
```javascript
/**
 * Base API URL for all requests
 * @constant {string}
 */
const API_URL = "https://api.example.com/v1/";

/**
 * Fetches user data from the API
 * @param {string} userId - The ID of the user to fetch
 * @returns {Promise<Object>} - The user data
 */
const fetchUserData = async (userId) => {
  const url = `${API_URL}users/${userId}`;
  
  try {
    const response = await fetch(url);
    
    if (!response.ok) {
      throw new Error(`HTTP error! Status: ${response.status}`);
    }
    
    const data = await response.json();
    
    const { firstName, lastName, email, roles = [] } = data;
    
    return {
      name: `${firstName} ${lastName}`,
      email,
      roles
    };
  } catch (error) {
    throw error;
  }
};

/**
 * Displays user information in the DOM
 * @param {Object} user - The user object
 * @param {string} user.name - User's full name
 * @param {string} user.email - User's email address
 * @param {Array<string>} user.roles - User's roles
 */
const displayUserInfo = (user) => {
  const rolesText = user.roles
    .map(role => `<li>${role}</li>`)
    .join('');
  
  const userInfoDiv = document.getElementById("user-info");
  userInfoDiv.innerHTML = `
    <h2>${user.name}</h2>
    <p>Email: ${user.email}</p>
    <ul>${rolesText}</ul>
  `;
};

/**
 * Initializes the application with the specified user
 * @param {string} [userId="default"] - The ID of the user to load
 */
const init = async (userId = "default") => {
  try {
    const user = await fetchUserData(userId);
    displayUserInfo(user);
  } catch (error) {
    console.error(`Error fetching user: ${error}`);
  }
};

// Use DOMContentLoaded event listener instead of jQuery
document.addEventListener("DOMContentLoaded", () => {
  init();
});
```

**Explanation:** This prompt lists specific ES6+ features to incorporate, guiding Copilot to apply common modernization patterns to legacy JavaScript. By requesting proper JSDoc comments, the refactored code will also include improved documentation. The prompt is effective because it provides clear transformation targets while leaving room for Copilot to apply best practices.

## Code Structure Improvement

### Refactor to Use Design Pattern

**Use Case:** Refactoring code to implement the Observer design pattern.

**The Prompt:**
```java
// Refactor this code to use the Observer pattern
// - Create a proper Subject interface and implementation
// - Create an Observer interface
// - Allow multiple observers to subscribe to and unsubscribe from notifications
// - Use proper encapsulation and access modifiers

public class WeatherStation {
    private float temperature;
    private float humidity;
    private float pressure;
    
    private Display currentConditionsDisplay;
    private Display forecastDisplay;
    private Display statisticsDisplay;
    
    public WeatherStation() {
        currentConditionsDisplay = new CurrentConditionsDisplay();
        forecastDisplay = new ForecastDisplay();
        statisticsDisplay = new StatisticsDisplay();
    }
    
    public void setMeasurements(float temperature, float humidity, float pressure) {
        this.temperature = temperature;
        this.humidity = humidity;
        this.pressure = pressure;
        notifyDisplays();
    }
    
    private void notifyDisplays() {
        currentConditionsDisplay.update(temperature, humidity, pressure);
        forecastDisplay.update(temperature, humidity, pressure);
        statisticsDisplay.update(temperature, humidity, pressure);
    }
}

interface Display {
    void update(float temperature, float humidity, float pressure);
}

class CurrentConditionsDisplay implements Display {
    public void update(float temperature, float humidity, float pressure) {
        System.out.println("Current conditions: " + temperature + "F degrees, " 
            + humidity + "% humidity, and " + pressure + " pressure");
    }
}

class ForecastDisplay implements Display {
    public void update(float temperature, float humidity, float pressure) {
        System.out.println("Forecast: More of the same");
        // Imagine more complex forecasting logic here
    }
}

class StatisticsDisplay implements Display {
    public void update(float temperature, float humidity, float pressure) {
        System.out.println("Statistics: Avg/Max/Min temperature = " + temperature);
        // Imagine more complex statistics logic here
    }
}
```

**Example Output:**
```java
// Observer pattern implementation for weather monitoring

/**
 * Observer interface defines how observers will be notified of changes
 */
interface Observer {
    void update(float temperature, float humidity, float pressure);
}

/**
 * Subject interface defines methods for managing observers
 */
interface Subject {
    void registerObserver(Observer o);
    void removeObserver(Observer o);
    void notifyObservers();
}

/**
 * WeatherData class acts as the concrete Subject
 */
public class WeatherStation implements Subject {
    private float temperature;
    private float humidity;
    private float pressure;
    private List<Observer> observers;
    
    public WeatherStation() {
        observers = new ArrayList<>();
    }
    
    @Override
    public void registerObserver(Observer o) {
        observers.add(o);
    }
    
    @Override
    public void removeObserver(Observer o) {
        int i = observers.indexOf(o);
        if (i >= 0) {
            observers.remove(i);
        }
    }
    
    @Override
    public void notifyObservers() {
        for (Observer observer : observers) {
            observer.update(temperature, humidity, pressure);
        }
    }
    
    /**
     * Called when measurements are updated
     */
    public void measurementsChanged() {
        notifyObservers();
    }
    
    /**
     * Sets new measurements and notifies observers
     */
    public void setMeasurements(float temperature, float humidity, float pressure) {
        this.temperature = temperature;
        this.humidity = humidity;
        this.pressure = pressure;
        measurementsChanged();
    }
    
    // Getter methods
    public float getTemperature() {
        return temperature;
    }
    
    public float getHumidity() {
        return humidity;
    }
    
    public float getPressure() {
        return pressure;
    }
}

/**
 * Display interface represents the Observer role
 */
interface Display extends Observer {
    void display();
}

/**
 * Concrete Observer implementation for current conditions
 */
class CurrentConditionsDisplay implements Display {
    private float temperature;
    private float humidity;
    private float pressure;
    private Subject weatherStation;
    
    public CurrentConditionsDisplay(Subject weatherStation) {
        this.weatherStation = weatherStation;
        weatherStation.registerObserver(this);
    }
    
    @Override
    public void update(float temperature, float humidity, float pressure) {
        this.temperature = temperature;
        this.humidity = humidity;
        this.pressure = pressure;
        display();
    }
    
    @Override
    public void display() {
        System.out.println("Current conditions: " + temperature + "F degrees, " 
            + humidity + "% humidity, and " + pressure + " pressure");
    }
}

/**
 * Concrete Observer implementation for forecasts
 */
class ForecastDisplay implements Display {
    private float temperature;
    private float humidity;
    private float pressure;
    private Subject weatherStation;
    
    public ForecastDisplay(Subject weatherStation) {
        this.weatherStation = weatherStation;
        weatherStation.registerObserver(this);
    }
    
    @Override
    public void update(float temperature, float humidity, float pressure) {
        this.temperature = temperature;
        this.humidity = humidity;
        this.pressure = pressure;
        display();
    }
    
    @Override
    public void display() {
        System.out.println("Forecast: More of the same");
        // More complex forecasting logic would go here
    }
}

/**
 * Concrete Observer implementation for statistics
 */
class StatisticsDisplay implements Display {
    private float temperature;
    private float humidity;
    private float pressure;
    private Subject weatherStation;
    
    public StatisticsDisplay(Subject weatherStation) {
        this.weatherStation = weatherStation;
        weatherStation.registerObserver(this);
    }
    
    @Override
    public void update(float temperature, float humidity, float pressure) {
        this.temperature = temperature;
        this.humidity = humidity;
        this.pressure = pressure;
        display();
    }
    
    @Override
    public void display() {
        System.out.println("Statistics: Avg/Max/Min temperature = " + temperature);
        // More complex statistics logic would go here
    }
}

/**
 * Usage example
 */
class WeatherApp {
    public static void main(String[] args) {
        WeatherStation weatherStation = new WeatherStation();
        
        CurrentConditionsDisplay currentDisplay = new CurrentConditionsDisplay(weatherStation);
        ForecastDisplay forecastDisplay = new ForecastDisplay(weatherStation);
        StatisticsDisplay statisticsDisplay = new StatisticsDisplay(weatherStation);
        
        weatherStation.setMeasurements(80, 65, 30.4f);
        System.out.println("---");
        weatherStation.setMeasurements(82, 70, 29.2f);
        System.out.println("---");
        
        // Remove an observer
        weatherStation.removeObserver(forecastDisplay);
        weatherStation.setMeasurements(78, 90, 29.2f);
    }
}
```

**Explanation:** This prompt specifies both the original code structure and the desired design pattern to implement. By requesting specific interfaces and behaviors, Copilot can generate a proper implementation of the Observer pattern. The prompt works well because it outlines the key components of the pattern (Subject interface, Observer interface, subscription methods) while providing enough context about the existing code.

## Functional Transformation

### Convert Imperative to Functional Style

**Use Case:** Transforming imperative code into a more functional style using functional programming concepts.

**The Prompt:**
```typescript
// Refactor this imperative-style TypeScript code to use functional programming concepts:
// - Replace loops with map, filter, reduce
// - Avoid mutable state and side effects
// - Use pure functions
// - Apply function composition where appropriate
// - Use optional chaining and nullish coalescing when relevant

interface Product {
  id: number;
  name: string;
  price: number;
  category: string;
  stockCount: number;
}

function processProducts(products: Product[]): {
  totalValue: number;
  categoryCounts: Record<string, number>;
  affordableProductNames: string[];
} {
  let totalValue = 0;
  let categoryCounts: Record<string, number> = {};
  let affordableProductNames: string[] = [];
  
  for (let i = 0; i < products.length; i++) {
    const product = products[i];
    
    // Calculate total inventory value
    totalValue += product.price * product.stockCount;
    
    // Count products by category
    if (categoryCounts[product.category]) {
      categoryCounts[product.category]++;
    } else {
      categoryCounts[product.category] = 1;
    }
    
    // Find affordable products (less than $50)
    if (product.price < 50) {
      affordableProductNames.push(product.name);
    }
  }
  
  return {
    totalValue,
    categoryCounts,
    affordableProductNames
  };
}
```

**Example Output:**
```typescript
interface Product {
  id: number;
  name: string;
  price: number;
  category: string;
  stockCount: number;
}

/**
 * Process a list of products using functional programming techniques
 * @param products List of products to process
 * @returns Processed data including total value, category counts, and affordable product names
 */
const processProducts = (products: Product[]): {
  totalValue: number;
  categoryCounts: Record<string, number>;
  affordableProductNames: string[];
} => {
  // Calculate total inventory value
  const totalValue = products.reduce(
    (sum, product) => sum + product.price * product.stockCount,
    0
  );
  
  // Count products by category using reduce
  const categoryCounts = products.reduce<Record<string, number>>(
    (counts, product) => ({
      ...counts,
      [product.category]: (counts[product.category] ?? 0) + 1
    }),
    {}
  );
  
  // Find affordable products (less than $50)
  const affordableProductNames = products
    .filter(product => product.price < 50)
    .map(product => product.name);
  
  return {
    totalValue,
    categoryCounts,
    affordableProductNames
  };
};

// Alternative implementation using function composition
type ProductProcessor<T> = (products: Product[]) => T;

// Individual processing functions
const calculateTotalValue: ProductProcessor<number> = products =>
  products.reduce((sum, { price, stockCount }) => sum + price * stockCount, 0);

const countByCategory: ProductProcessor<Record<string, number>> = products =>
  products.reduce<Record<string, number>>(
    (counts, { category }) => ({
      ...counts,
      [category]: (counts[category] ?? 0) + 1
    }),
    {}
  );

const getAffordableNames: ProductProcessor<string[]> = products =>
  products
    .filter(({ price }) => price < 50)
    .map(({ name }) => name);

// Composed function
const processProductsComposed = (products: Product[]) => ({
  totalValue: calculateTotalValue(products),
  categoryCounts: countByCategory(products),
  affordableProductNames: getAffordableNames(products)
});
```

**Explanation:** This prompt clearly specifies which functional programming concepts to incorporate into the refactored code, providing Copilot with clear guidelines. By showing the imperative-style code first and then requesting specific transformations (map, filter, reduce, avoiding mutable state), Copilot can generate a properly functional alternative. The prompt is effective because it builds on common functional programming patterns that Copilot has been trained on.
