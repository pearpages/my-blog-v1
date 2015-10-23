#### Angular Editors

+ Sublime
+ Brackets
+ Visual Studio
+ Atom

#### Platorm

+ nodejs

#### Repository

https://github.com/johnpapa/ng-demos

+ modular (application)
+ cc-bmean (application, larger app with mongo)

#### Packages to install

Remember to use *sudo* when installing globally *-g*

+ bower (package manager)
+ gulp (task automazion system)
+ karma-cli (unit-testing launcher)
+ nodemon (restart node anytime there are changes)


## Playing with Modular Folder from Repository

$ npm install

### Structure

gulpfile.js

### Webstorm

Edit Configurations...

**Command Shift E (Configuring Mongo)**
/usr/local/bin/mongod
--config mongodb.config
/Users/mattmax/_git/ng-demos/cc-bmean/src/server/data

**Command 1**
hide the left bar

## Separation of Concerns (SoC)

Helps manage complexity

+ Easier to maintain
+ Easier to extend
+ Reuse more code
+ Easier to test
+ Easier to isolate bugs

### The Rule of One (Ravioli state)

Doing one thing and doing one thing well.

For example, a controller should only handle logic for a view.

A component has one Role!

Summary:

+ One Role
+ One component per file
+ One singular purpose

The opposite of this is **spaghetti code**.

### How to Separate

Does our component have 1 job?

**AngularJS has familars terms**

+ Modules
+ Factories / Services
+ Directives
+ Models
+ Views
+ Controllers

**Vertical SoC with Modularity (Example)**

+ Customer Module
  + Customer Controller
  + Customer Data Factory
  + Customer Address Widget
+ Sales Module
+ Admin Module

**Other Examples**

+ Cross Cutting and Specific to the app
  + Managing XHR calls (i.e. a data service)
+ Cross cutting and generic
  + Logging service
  + Exception Handling consolidation
+ Feature and Role
  + Customer Controller
  + Customer address widget (vida directive) 

#### Tips for Seperating in AngularJS

+ Small, readable, and Singularly Focused
+ Controllers defer to Factories
+ Module Startup Logic is Difficult to Test
    * Inject and Invoke Module Startup Code
+ Group Features into Modules

#### Summary

1 Component, 1 Role, 1 File
Use Dependencies
Modularize
Decreases risk, cost, time to deliver
Increases testability, code reuse, maintainability

## Organizing your App

### Benefits

+ Faster and easier to develop
+ Align with SoC
+ Easier to find and locate code
+ Transitions to modularity when its time to extend your app

### Sorting Boxes

/app
/content or /assets
/scripts or /components or /bower_components or /vendor
/test

**app**

+ folders by type
+ folders by feature <--

**feature example**

app/
    dashboard/
    layout/
    people/
    services/

#### The LIFT Principle

Following the order of importance

**L**ocating our code is easy
**I**dentify code at a glance
**F**lat structure as long as we can (no depths in folders)
**T**ry to stay DRY

#### Above the Fold

**Controller**
angular
    .module('app.my_module')
    .controller('my_controller',['common','dataservice',my_controller]);

function my_controller(common,dataservice){
    var vm = this;
    vm.avengers = [];
    vm.title = 'Avengers';

    ////////// Implementation
}
**Factory**

angular
    .module('app.core')
    .factory('dataservice',['$http','commont',dataservice]);

function dataservice($http,common){
    var logger = common.logger;

    var service = {
        getAvengersCast: getAvengersCast,
        getAvengersCount: getAvengersCount,
        getAvengers: getAvengers,
        ready: ready
    };

    return service;

    ///////// Implementation
}

### Naming Conventions

#### Modules
//Main app Module
//app.js
angular.module('app',['my_module']);

//my_module Module
//my_module.module.js
angular.module('my_module',['ngRoute']);

#### Controllers
//my_controller.js
angular
  .module('my_module')
  .controller('My_Controller',['common','dataservice', My_Controller]);

function My_Controller(common,dataservice)

#### Factories
//logger.js
angular
  .module('app.whatever')
  .factory('logger',['$log', factory]);

  function factory($log){
    var logger = {
      error: error,
      info: info,
      success: success,
      warning_ warning
    };

    return logger;

    ///////////// code
  }

  #### Directives
//myappWidgetHeader.js
angular
  .module('app.widgets')
  .directive(',myappWidgetHeader',['$window', widgetHeader]);

  function myappWidgetHeader()

  /////////code

### App Structure

#### Super Small

everything is in one folder

app/
  app.js
  config.js
  dataservice.js
  sessions.html
  sessions.js

#### Small by Feature

app/
  app.js
  config.routes.js
  directives.js
  layout/
  people/
    attendees.html
    attendees.js
    speakers.html
    speakers.js
    speaker-detail.html
    speaker-detail.js
  sessions/
  services/

### Summary

+ LIFT principle
+ Start with the smallerst that makes sense
+ When in doubt, organize by feature
+ Be consistent with your team

## Modules

+ each module can be an app, services or widgets
+ or all of these
+ modules can depend on other modules
+ promotes continous development

**Modules can have**

+ config, routes
+ filters
+ directives
+ factories, services, providers, values, constants
+ controllers

### Defining a Module

//setter
var app = angular.module('app',[]);

//getter
var app = angular.module('app');

**defining a module with dependencies**
angular.module('app',[
  'ngRoute',
  'app.avengers',
  'app.dashboard',
  'app.layout'
]);

### Categories of Modules

+ AngularJS Modules
+ 3rd Party Modules
+ Custom Modules

**example**

angular.module('app',[
  //Angular modules
  'ngRoute',
  //custom modules
  'app.dashboard',
  // 3rd party modules
  'ui.bootstrap',
  'breeze.angular'
]);

### Dependency Chains

app -> avengers, dashboard, layout

avengers -> core, widgets
dashboard -> core, widgets
layout -> core, widgets

core, widgets -> ngRoute, blocks.logger, ui-bootstrap

### Organization Strategies

**options**

+ Define dependencies for each module in each module
  * Will always work
  * Fairly Common
  * May be difficult to follow
+ Define dependencies at specific levels
  * Requires some forethought
  * May be easier to maintain

#### Structuring Modules

+ Main App Module (aggregator, no much logic)
+ Cross App Modules (aggregates app generic and custom modules)
+ App Feature Modules 

### Module Structure

In this way features almost don't have or don't have dependencies at all.

angular.module('app',[
  //everybody has access to these
  'app.core',
  'app.widgets',
  //features
  'app.dashboard',
  'app.layout'
]);


angular.module('app.core',[
  //angular modules
  'ngAnimate','ngRoute','ngSanitize'
  //resuable cross app modules
  'block.exception','blocks.logger','blocks.router',
  //3rd party
  'ngplus'
]);

### Debugging modules

...

### Directives and Modules Dependencies

Directives are kind of lazy loaded. So because of that there are no errors in the console when they are not loaded properly.

### Naming Tips

+ Name modules consistently
  * app is the main module
  * app.avengers is a feature module
+ Name files consistently
  * app.js (or app.module.js)
  * avengers.module.js

### Summary

+ Modules are features areas
+ Modules help keep features encapsulated and follows SoC
+ Don't create a spider web of module dependency chains
+ Do aggregate in where it makes sense
  * app.js module and core.module.js
+ Good debugging skills can be helpful

## Readable Code and AngularJS

### Module Variables

**global variables**
var app = angular.module('app');

**no global variables, but chaining**
angular.module('app')
  .controller('AvengerDetail', function (){
    //...
  });

### Anonymous Functions vs Named Functions

Use named functions for debugging and clarity.

### How Do we Contain Global Variables? --> Immediately Invoked Function Expression (IIFE)

We use IIFE and this way we keep the global scope clean.

(function (){
  angular
    .module('app')
    .controller('AvengerDetail', AvengerDetail);

    function AvengerDetail(){
      var vm = this;
      vm.name = 'Tony Stark';
    };
})();

### Safely Minify Dependencies and Patters to Register, Inject, and Define Components

+ Register and Inject, then Function (array with Strings) aka *Hoisting* @jesseliberty
+ Function, Inject, Register @toddmotto
+ REgister, Inject, Function @john_papa


angular
  .module('app.dashboard')
  .controller('Dashboard',['common','dataservice', Dashboard]);

function Dashboard(common, dataservice){
  //code
}

vs 

function Dashboard(common, dataservice){
  //congtroller code goes here
}

Dashboard.$inject = ['common','dataservice'];

angular
  .module('app.dashboard')
  .controller('Dashboard',Dashboard)

vs

angular
  .module('app.dashboard')
  .controller('Dashboard', Dashboard);

  Dashboard.$inject = ['common','dataservice'];

  function Dashboard(common,dataservice){
    //controller code...
  }

#### Using ngAnnotate (Automation through Grunt or Gulp)

We use a notation to skip the *$inject* step and Grunt or Gulp do it for us.

angular
  .module('app.dashboard')
  .controller('Dashboard', Dashboard);

  /* @ngInject */
  function Dashboard(common, dataservice){
    //controller code...
  }

### Enhancing Readibility

+ IIFE's help reduce global variables and functions
+ Chaining and indentation
+ Named fucntions help readability
+ Keep important code up top including interfaces (above the fold)
+ Inject consistently
  * Consider **ngAnnotate** using Grunt or Gulp

## Controller Patterns

+ Role of a controller
+ Classic vs New
+ Why Dots Matter
+ Nesting
+ Linking
+ $scope
+ Resolvers
+ Testing

### The Role of a Controller

AngularJS Module -> Config -> Routes

View <- $scope -> Controller

View -> Directives

Controller -> Factories

**Creating a Controller creates a new Instance**. **Controllers are effectively Constructors!!!**.

### Nesting, Naming, and Dots

**Dots Provide Context**
  
+ Provide Clarity
+ Easier to reach the parent scope with $parent.$parent chaining
+ Remove unexpected behavior

<div ng-controller="Shell as shell">
  {{shell.name}}
  <div ng-controller="Customer as customer">
  {{customer.name}}
    <div ng-controller="Order as order">
    {{order.name}}
    </div>
  </div>
</div>

### Instantiation Controllers

+ Through the view
+ Through the route

**Through the route**

resolve runs functions before the controller.

function getRoutes(){
  return [
    {
      url: '/',
      config: {
        templateUrl: '/app/dashboard/dashboard.html',
        title: 'dashboard',
        controller: 'Dashboard',
        controllerAs: 'vm',
        resolve{
          message: function (){
            toastr.warning('You resolved');
            return {first: 'secret'};
          },
          mydata: function($q){
            var deferred = $q.defer();
            defferred.resolve({first: 'another secret'});
            return defferred.promise;
          }
        },
        settings: {
          //...
        }
      }
    }
  ]
}

### Unit Testing

scope = $rootScope.$new();
controller = $controller('Avengers as vm', {
  '$scope' : scope
});

it('should ahve a title of Avengers', function (){
  $tootScope.$apply();
  expect(scope.vm.title).to.equal('Avengers');
});

