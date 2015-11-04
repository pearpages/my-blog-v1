### Why Use Angular?

+ Expressive HTML (more readible)
+ Modularity
+ Rule-based Navigation
+ Powerful Data Binding (two way)
+ Testable
+ It's popular (Easy to find help)

### What Are the Key Factors in Building a Line of Business Application?

+ Data is an Asset (a critical corporate asset)
+ Amount of Data is Significant
+ Number of Data Fields is Significant (forms)
+ Data Integrity is Crititcal
+ Data Visualization (For data analysis)

### How to Build a Line of Business Application

+ Colect Busieness Requirements
    * Applications Features
    * Design Considerations
    * Architecture
+ Layout and Navigation
    * Page Layout (view)
    * Style (maybe bootstrap)
    * Navigation (Routing)
+ Data Access (DB - API?)
    * Retrieving data
    * Saving data
+ Data Entry Forms
    * Form layout
    * Validation
    * Submittal
+ Business Logic (Calculus?)
    * Services
+ Data Visualization
    * Charts

And Transversally

+ Exception Handling
+ Unit Testing
+ Security

## Basics

### Controller

+ Define the Model
+ Implement Methods (User interface actions)

#### Best Practices

+ Define each controller as a separate .js file
+ Suffic the controller with "Controller or Ctrl"
+ Use IIFE

### Organizing the Project Structure

+ Everyone knows where everything goes
+ Everyone knows where everything is
+ The result is extensible

### View

+ Template
    * HTML that defines visual elements
    * And directives
+ View
    * Load and rendered template
    * Also called the "live template"

 ### Module

+ Defines an Angular application
+ Tracks all of the application code
+ Tracks all of the dependencies for the application
+ Keeps the application modularized

```
// Setter Method
angular.module("productManagement",[]);

// Getter Method
angular.module("productManagement");
```

### The IIFE Javascript Pattern

+ Immediately-Invoked Function Expression (IIFE)
    * AKA: Self-executing anonymous function
+ Javascript "var" declarations have **global** scope
+ Javascript variables and functions defined with a function have **local** scope

## Accessing Data

### Built-In Angular Services for Calling a Web Services

+ $http
+ $resource
+ $httpBackend

#### $http

+ Facilitates communication with remote Web servers
+ Call is asynchronous
+ When the request is complete:
    * The callback funciton is executed
    * The response object is passed in

```
$http.get("/api/products")
    .then(function(response) {
            vm.products = response.date;
        });
```

#### $resource

+ Angular factory which creates a resource object
  * REST (Representational State Transfer)
+ Abstracts away complexity 

##### Methods

+ get: retrieves the specific product
+ query: retrieves all the specified products
+ save: saves modifications to the product
+ delete / remove

```
function productResource($resource) {
    return $resource("/api/prodcuts/:productId");
}
```

```
productResource.query(function (data) {
    vm.products = data;
});
```

#### $httpBackend

Angular's fake HTTP backend implementation

Mocks the calls to the Web Services

Returns static data to the application

Two implementations:

+ ngMock: for unit testing applications
+ ngMockE2E: for end-to-end testing or backend-less development

### Steps to Mocking the Web Server

1. Download the ngMockE2E module
2. Create a new module that depends on ngMockE2E
3. Set up static data
4. Define the fake responses to the Web Server calls
5. Add the new module as a dependency in the Main Module

```
(function (){
    "use strict"

    angular
        .module("productResourceMock",["ngMockE2E"])
        .run(function ($httpBackend){

            var products = [
            {
                "productId" : 1,
                "productName": "Leaf Rake",
            },
            {
                "productId" : 2,
                "productName": "Leaf Rake",
            }
            ];  

            var productUrl = '/api/products';

            $httpBackend.whenGET(productUrl).respond(products);
        });

})();
```

## Routing

+ Technique for navigating between views
+ Each route represents a specific view
+ Activating a route navigates to that view

### Frameworks

+ ngRoute (simple URL navigation)
    * based on URL fragment identifiers
    * each route has
        - URL fragment identifier
        - view template
        - optional controller
+ Ui-Router
    * based on application states
    * each states has
        - optional url fragment identifier
        - view template
        - optional controller
        - additional attached behavior


