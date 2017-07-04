# Guild Wars 2 Web App
A javascript web app utilising the Guild Wars 2 API.

<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->


- [User Guide](#user-guide)
  - [How to obtain a personal API key](#how-to-obtain-a-personal-api-key)
  - [How to obtain a guild API key if you are a guild leader](#how-to-obtain-a-guild-api-key-if-you-are-a-guild-leader)
- [Developer Setup](#developer-setup)
  - [Git Installation and Configuration](#git-installation-and-configuration)
  - [Clone the Repository](#clone-the-repository)
  - [NodeJS Installation and Configuration](#nodejs-installation-and-configuration)
  - [Yarn Installation and Configuration](#yarn-installation-and-configuration)
  - [Webpack Installation and Configuration](#webpack-installation-and-configuration)
  - [Test the Installation was Successful](#test-the-installation-was-successful)
- [Repository Structure](#repository-structure)
  - [`app`](#app)
  - [`node_modules`](#node_modules)
  - [`test`](#test)
- [Style Guide](#style-guide)
  - [Naming Conventions](#naming-conventions)
    - [File Names](#file-names)
    - [Component Names](#component-names)
  - [Angular Style Guide](#angular-style-guide)
    - [Controllers](#controllers)
    - [Directives](#directives)
- [Common Development Tasks](#common-development-tasks)
  - [Adding a New View](#adding-a-new-view)
  - [Adding a New Component](#adding-a-new-component)
  - [Adding a Common Injectable](#adding-a-common-injectable)
  - [Mocking a HTTP Endpoint in `gulp serve`](#mocking-a-http-endpoint-in-gulp-serve)
- [Unit Testing](#unit-testing)
  - [Folder Structure and Naming Conventions](#folder-structure-and-naming-conventions)
  - [Using `ngMock`](#using-ngmock)
    - [Loading Modules](#loading-modules)
    - [Injecting Services](#injecting-services)
    - [Using `$httpBackend`](#using-httpbackend)
    - [Testing `$interval` and `$timeout`](#testing-interval-and-timeout)
  - [Common Angular Testing Patterns](#common-angular-testing-patterns)
    - [Testing a Service](#testing-a-service)
    - [Testing a Filter](#testing-a-filter)
    - [Testing a Controller](#testing-a-controller)
    - [Testing a Directive](#testing-a-directive)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

## User Guide
### How to obtain a personal API key
Open your favourite browser and navigate to your arena net account page (https://account.arena.net/), then navigate to the Applications page.

Create a <em>New Key</em> with the following options enabled:

* `account` (mandatory)
* `inventories`
* `characters`
* `tradingpost`
* `wallet`
* `unlocks`
* `pvp`
* `builds`
* `progression`

Do not set the `guilds` permission, as this will be covered by a second API key that must be linked to your guild leader's account.

This key is entered under the `Personal Key` field in the app.

### How to obtain a guild API key if you are a guild leader
Open your favourite browser and navigate to your arena net account page (https://account.arena.net/), then navigate to the Applications page.

Create a <em>New Key</em> with the following options enabled:

* `account` (mandatory)
* `guilds`

This key can be freely passed out to your guild members or anyone else you wish to share your guild information with. Note that while this key will enable someone to potentially view your account `name`, `ID`, `home world`, `joined guilds` and `date of creation`, the app will not display this information - the app pulls those values from the `personal key`.

This key is entered under the `Guild Key` field in the app.

## Developer Setup
### Git Installation and Configuration
First of all, <a href="https://git-scm.com/downloads">download</a> and install git for your operating system. In Windows, if prompted for how to handle line endings, select the "Checkout Windows-style, commit Unix-style" option. If using Windows, open a git bash (which should have a shortcut in the start menu, but is located at `<git-install-dir>/bin/sh.exe`). If using linux of OS-X, open up a console/terminal window.

To ensure git is on your path, run:

    > git version   
    git version x.x.x.xxxxxxxx.x

Configure your name and email address globally:

    > git config --global user.name "My Name"   
    > git config --global user.email "myemail@example.com"

If using Windows, you will want to ensure that git is handling line endings correctly (we would like to commit with LF line endings, as opposed to the Windows CRLF line endings). To check your line ending handling run:

    > git config --global --list | grep autocrlf  
    core.autocrlf=true

If the returned value of `core.autocrlf` is set to anything other than `true`, of if `grep` does not return anything, then you will want to configure autocrlf by running:
 
    > git config --global core.autocrlf true

You may additionally want to configure other options in git (for example, your editor tool). You are encouraged to refer to the freely available <a href="https://git-scm.com/book/en/v2">Pro Git</a> book for a comprehensive guide on how to configure and use git.

### Clone the Repository
Open a git bash shell (or equivalent in your OS) and navigate to a suitable directory to clone the repository.

Clone the repository and cd into it:

    git clone https://github.com/AerosAtar/GW2WebApp.git && cd GW2WebApp

### NodeJS Installation and Configuration
<a href="https://nodejs.org/en/download/">Download</a> and install Node.js for your operating system. If using Windows, open a git bash shell. If using linux of OS-X, open up a console/terminal window.

To ensure node is on your path, run:

    > node --version
    vx.xx.x

### Yarn Installation and Configuration
<a href="https://yarnpkg.com/en/docs/install">Download</a> and install Yarn for your operating system. If using Windows, open a git bash shell. If using linux of OS-X, open up a console/terminal window.

To ensure yarn is on your path, run:

    > yarn --version
    x.xx.x

Install yarn dependencies:

    > yarn install

### Webpack Installation and Configuration
If using Windows, open a git bash shell. If using linux of OS-X, open up a console/terminal window.

Install Webpack:

    > yarn add webpack --dev
    
Install webpack dependencies:

    > webpack install

### Test the Installation was Successful
Serve the web app locally to ensure everything is working:

    > yarn start

## Repository Structure
The following directories exist at the root of the web app repository. The following sections will briefly describe the contents of these directories, and what should go in them.

### `app`
This is the folder that houses the main code base for the web app. Any code that will be used by the web app should be placed here (in the respective subdirectory). Each subdirectory of this directory contains its own README.md file, which has guidance on what belongs in that subdirectory.

### `node_modules`
This directory is listed in the `.gitignore` file, but will be present once a npm install has been run. This directory houses all of the yarn modules that are listed in the `package.json` file.

### `test`
This directory contains any data produced by the unit testing framework.

## Style Guide
This section will briefly outline the naming conventions and general style guidelines that should be used in the web app.

### Naming Conventions
#### File Names 
Javascript and Typescript files for angular components should use the component name in `spinal-case` suffixed with the type of component they represent, using a `.` to separate name parts. For example:

* `my-component-name.directive.js`
* `my-component-name.controller.js`
* `my-component-name.service.js`
* `my-component-name.filter.js`
* `my-component-name.factory.js`

Files that define the routes for a view should be suffixed with `routes`:

* `my-view.html`
* `my-view.controller.js`
* `my-view.routes.js`

Javascript and Typescript files containing unit tests for a component should be suffixed with the word `test`, and should be located in the same directory as the component. For example:

    - my-component
      |- my-component.html
      |- my-component-directive.js
      |- my-component-directive.test.js

#### Component Names
These are the names that are used to register the components with Angular (e.g. `myModule.directive('myDirective')` or `myModule.filter('myFilter')`). Directives, services, factories and filters should register names in `camelCase`, whereas controllers should use `UpperCamelCase`, as these should be constructors. Controller names, and the name of the function that defines the controller, should be suffixed with `Ctrl` for easy recognition:

    var MyComponentCtrl = function() {
        var vm = this;
        this.foo = 'bar';
    };
    
    myModule.controller('MyCompopnentCtrl', MyComponentCtrl);

Directive names should be prefixed with `wn` to make them easily identifiable in the HTML and to avoid potential naming collisions with directives from libraries (i.e. `myModule.directive('wnMyDirective', function() {...})` which would display in the HTML as `<wn-my-directive></wn-my-directive>`). It is not necessary to prefix the corresponding file names.

Services, factories and filters _should not_ be prefixed with a `$`, so as to avoid naming collisions with Angular internal services.

### Angular Style Guide
#### Controllers
Controllers should be focused on the view that they are associated with. Generally, it does not make sense to reuse controller logic. In such cases where this might be desirable, extract the logic into a reusable service instead, as this can then be injected into multiple controllers.

Use the "controller as" pattern when defining controllers, and define a view model object inside the controller to hold any properties that need to be exposed to the view, rather than exposing properties via an injected `$scope`:

    var MyCtrl = function() {
        var vm = this;
        vm.foo = 'bar';
    };
    
    myModule.controller('MyCtrl', MyCtrl);

This can help to prevent potential confusion with property shadowing within the scope hierarchy. Compare this:

    <!-- Not recommended -->
    <div ng-controller="MyCtrl">
      {{foo}}
      <div ng-controller="MyOtherCtrl">
        {{foo}}
        {{$parent.foo}}
      </div>
    </div>
    
With this:

    <!-- Preferred -->
    <div ng-controller="MyCtrl as parent">
      {{parent.foo}}
      <div ng-controller="MyOtherCtrol as child">
        {{child.foo}}
        {{parent.foo}}
      </div>
    </div>
    
Only use the injected `$scope` as a service - for things like setting up watches and event handling (`$emit`, `$broadcast` and `$on`).

Any startup logic for a controller (logic that needs to be run the first time the controller is instantiated) should be placed inside an initialisation function for easier readability and maintainability. In particular, this should include any asynchronous call to retrieve data for the controller:

    var MyCtrl = function() {
      var vm = this;
      vm.foo = 'bar';
      var init = function() {
        $http.get('http//www.example.com/some/service')
          .then(function(response) {
            vm.data = response.data;
          });
      };
      
      init();
    };
    
    myModule.controller('MyCtrl', MyCtrl);
    
You should avoid DOM manipulation in controller code. If DOM manipulation is required, you should probably be using a directive.

#### Directives
Each directive should be defined in its own file to maintain modularity and avoid confusion. If DOM manipulation is required inside a directive, this should be carried out inside the directive's `link` function, and not in its `controller`.

Directives should clean up after themselves. Any cleanup code can be executed by listening to the `$destroy` event on the `$scope`:

    $scope.$on('$destroy', function() {
      // Cleanup code
    });
    
Restrict directives to elements if they make sense as standalone elements. Otherwise restrict to elements and attributes:

    myModule.directive('wnMyDirective', function() {
      return {
        ...
        restrice: 'EA',
        ...
      }
    });
    
Allowing class directives is strongly discouraged, unless there is a _very_ compelling reason to do so.

If the directive defines a controller, this should follow the guidance for controllers as defined in the previous section. In particular, the "controller as" pattern should be followed:

**my-directive.directive.js:**
    var MyDirectiveCtrl = function() {
      var vm = this;
      vm.foo = 'bar';
    }
    
    myModule.directive('wn-MyDirective', function() {
      return {
        restrict      : 'E',
        scope         : {},
        templateUrl   : 'path/to/my-directive',
        controller    : 'MyDirectiveCtrl'
        controllerAs  : 'vm'
      };
    });
    
**my-directive.html**
    <div>
      {{vm.foo}}
    </div>
    
If the directive uses an isolate scope, then the `bindToController` option should be used, to allow easy access to external variables that are bound onto the directive's isolate scope.

Instead of:

    // Not recommended
    var MyDirectiveCtrl = function() {
      var vm = this;
      vm.bar = $scope.bar;
    }
    
    myModule.directive('wnMyDirective', function() {
      return {
        restrict      : 'E',
        scope         : { bar: '=' },
        templateUrl   : 'path/to/my-directive.html',
        controller    : MyDirectiveCtrl,
        controllerAs  : 'vm'
      };
    });
    
This would be preferred:

    // Preferred
    var MyDirectiveCtrl = function() {
      var vm = this;
      // vm.bar is already bound to $scope.bar here
    }
    
    myModule.directive('wnMyDirective', function() {
      return {
        restrict          : 'E',
        scope             : { bar: '=' },
        templateUrl       : 'path/to/my-directive.html',
        controller        : MyDirectiveCtrl,
        controllerAs      : 'vm',
        bindToController : true
      };
    });

It is preferable to use an isolated scope in directives. This makes for more reusable directives and can help to avoid accidental inheritance from parent scopes. Directives should, wherever possible, be self-encapsulated components that can be re-used in any number of views with bindings passed into the isolated scope by the parent view, rather than relying on accessing a variable directly on the parent scope. For example, consider the following directive:

    var MyDirectiveCtrl = function() {
      var vm = this;
      //We're relying on the property 'foo' existing on the parent scope
      var capsFoo = $filter('uppercase') (vm.foo);
    };
    
    myModule.directive('wnMyDirective', function() {
      restrict    : 'E',
      templateUrl : 'path/to/my-directive.html',
      controller  : MyDirectiveCtrl,
      controllerAs: 'vm'
    });
    
This works fine if we place our directive inside the scope of a controller that has a `foo` property on its scope. However, in order to re-use the directive, we need to make sure that the parent controller has a `foo` property on its scope, which may cause issues if `foo` is already being used as a property name. Additionally, if we decide to change the name of the `foo` property in the parent controller, we need to make sure that this is propagated to the child, making refactoring more difficult. A preferred approach would be to place the `foo` property inside an isolate scope:

    var MyDirectiveCtrl = function () {
      var vm = this;
      // We've declared foo on the isolate scope, and bound the isolate scope to the controller, so this is ok.
      var capsFoo = $filter('uppercase') (vm.foo);
    };
    
    myModule.directive('wnMyDirective', function() {
      restrict        : 'E',
      scope           : { foo: '=' },
      templateUrl     : 'path/to/my-directive.html',
      controller      : MyDirectiveCtrl,
      controllerAs    : 'vm',
      bindToController: true
    });
    
Now, we can re-use the directive whenever we like, and it won't accidentally change values on the parent scope, unless the binding has been explicitly declared:

    <div>
      {{foo}} <¬-- This 'foo' is a property on the parent scope -->
      <my-directive foo="bar"></my-directive>
    </div>
    
Now, if `my-directive` makes changes to its `foo` scope property, this will not alter the `foo` property in the parent scope, but will change the parent scope's `bar` property instead. Similarly, we can re-use the directive multiple times in the same scope, binding to different variables each time:

    <my-directive foo="bar"></mydirective>
    <my-directive foo="baz"></mydirective>
    <my-directive foo="qux"></mydirective>

## Common Development Tasks
### Adding a New View
1. Create a new subdirectory for your view under the app/views directory.
2. Any javascript/typescript or HTML code for your view should live in this directory, including the unit tests for your view (if any). It is most likely that you view will consist of a `my-view.html` file and possible a `my-view.controller.ts` file. However, any services, filters, factories or constants files that are specific to your view should also live in this directory.
3. Add a `my-view.routes.ts` file to declare the routes for your view.
4. If your view requires any specific styles, add a `_my-view.scss` file containing your view-specific styles to the `app/assets/scss/partials` directory. Any `.scss` files in this directory will be added to the `app/assets/scss/main.scss` imports list automatically when running `gulp serve` or `gulp build`.
5. Run `gulp serve` to test your view - the javascript for the view will be added to `app/index.html` automatically as part of the `serve` task (they will also be added as part of the build tast if you would rather run `gulp serve:dist` or `gulp build`).

### Adding a New Component
1. Create a new subdirectory for your component under the `app/components` directory.
2. Any javascript/typescript or HTML code for your component should live in this directory, including the unit tests for your component (if any). It is most likely that you component will consist of a `my-component.html` file and possible a `my-component.controller.ts` file. However, any services, filters, factories or constants files that are specific to your component should also live in this directory.
3. If your component requires any specific styles, add a `_my-component.scss` file containing your view-specific styles to the `app/assets/scss/partials` directory. Any `.scss` files in this directory will be added to the `app/assets/scss/main.scss` imports list automatically when running `gulp serve` or `gulp build`.
4. When you have added the component to any view that you would like it to be in, run `gulp serve` to test your component - the javascript for the view will be added to `app/index.html` automatically as part of the `serve` task (they will also be added as part of the `build` task if you would rather run `gulp serve:dist` or `gulp build`).

### Adding a Common Injectable
1. Create a javascript/typescript file for your injectable inside the relevant subdirectory of `app/common`. If creating an Angular service, you should creae a `my.service.js` file inside the `app/common/servies` directory, whereas filters belong in the `app/common/filters` directory, etc.
2. Run `gulp serve` to test your injectable - any javascript files inside the `app/common` directory will be added to `app/index.html` automatically as part of the `serve` task (they will also be added as part of the `build` task if you would rather run `gulp serve:dist` or `gulp build`).

### Mocking a HTTP Endpoint in `gulp serve`
1. Create a javascript file defining your HTTP endpoint inside the `server/services` directory. This should be a Node.js module, and should expose a function that takes a single arguement: `server`. This is an <a href="http://expressjs.com">Express</a> server, which you can use to configure the HTTP endpoint (see <a href://expressjs.com/4x/api.html#app>here</a> for how to do this, or use an existing endpoint as a template).
2. If you are currently running the `gulp serve` task,you will need to kill the task and restart it for the change to take effect.
3. Your endpoint should now be available on `http://localhost:3000`.

## Unit Testing
Any piece of javascript code that provides any piece of non-trivial functionality should be unit tested wherever possible. The web app project's unit testing framework uses <a href="http://jasmine.github.io">Jasmine</a> as its unit testing language, and <a href="http://karma-runner.github.io">Karma</a> as a test runner. Angular's `ngMock` module is used to assist in mocking Angular components and services. Code coverage information is also gathered using the `karma-coverage` module, which uses the <a href="https://github.com/gotwarlost//istanbul">Istanbul</a> coverage framework internally. The following provides a guide to how to write unit tests, and several of the Angular-specific quirks that you may come across whilst writing unit tests for an Angular application.

### Folder Structure and Naming Conventions
The unit tests for a component should all be placed in a single file, and any unit test file should only contain unit tests for a single component. This unit test file should be placed in the same directory as the component that it is testing, and the file should be suffixed with `test`, using a `.` as a separator. For example, if we have written a component that contains a directive and a service specific to that component, the directory should look something like this:

    - my-component
      |- my-component.directive.js
      |- my-component.directive.test.js
      |- my-component.html
      |- my-component.service.js
      |- my-component.service.test.js
      
The Jasmine test suites should use the same name as the name of your component, and specs should provide a descriptive summary of the expected behaviour for that spec:

    describe('my-component', function () {
      it('should turn red when the user enters a non-numberic character', function() {
        // Test code goes here.
      });
    });
    
Note that each test file should contain exactly one test suite( `describe` invocation), which may contain one or many test specs (`it` invocations). For a thorough guide to writing unit tests with Jasmine, see the <a href="http://jasmine.github.io/pages/docs_home.html">Jasmine documentation pages</a>.

### Using `ngMock`
The `ngMock` module provides a range of functions and mock services to assist in unit testing Angular apps. The following provides a guide to may of the useful features of the `ngMock` module. For additional information, see the <a href="https://docs.angularjs.org/guide/unit-testing">Angular unit testing documentation</a>.

#### Loading Modules
When unit testing any component of an Angular module, the first thing that you will need to do is to inject that module using the `module` global function provided by `ngMock`:

    describe('my-component', function() {
      
      //If only one module is needed
      beforeEach(module('my-module'));
      
      //Alternatively, if multiple modules are required
      beforeEach(function() {
        module('my-module');
        module('my-other-module');
        module('some-other-module');
      });
    });
    
#### Injecting Services
In order to test certain features, you will frequently need to access injectable services inside your unit tests, either from core Angular, or from your own module. This can be achieved by using `ngMock`'s global `inject` function:

    describe('my-service', function() {
     
      beforeEach(module('my-module'));
      
      var myService,
          $http;
          
      beforeEach(inject(function(_$http_, _myService_) {
        $http = _$http_;
        myService = _myService_;
      }));
      
      it('should return "bar" when we call foo()', function() {
        expect(myService.foo().toBe('bar');
      });
    });
    
Here, we inject Angular's `$http` service as well as our own `myService` service into our unit test, and will have access to the services in any spec through the `myService` and `$http` variables. The use of underscores when injecting services is a convention used by the Angular community to keep variable names clean. The injector will ignore the underscores when locating the service, <em>but only if there is exactly one leading and one trailing underscore</em>:

    inject(function($http) {});     // valid
    inject(function(_$http_) {});   // invalid
    inject(function(_$http) {});    // invalid
    inject(function($http_) {});    // invalid
    inject(function(__$http__) {}); // invalid
    
#### Using `$httpBackend`
In several cases, you may be testing a component which needs to make HTTP calls via the `$http` service. `ngMock` provides a fake HTTP backend implementation, `$httpBackend`, that will catch calls from the `$http` service. If a component needs to make HTTP requests through the `$http` service, then we need to tell `$httpBackend` to expect these HTTP requests and dictate its behaviour upon receiving the requests.

In order to preserve the asynchronous API for the real HTTP backend, the `$httpBackend` provided by `ngMock` exposes a `flush` function, which will flush any pending `$http` requests, and respond with the pre-prepared responses.

For example, suppose we have a service which exposes a `foo` method, which makes a HTTP request when called, and stores the response data in an array, which can be retrieved via the `getResults` method:

    myModule.service('myHttpService', function($http) {
    
      var results = [];
      
      this.foo = function() {
        $http.get('http://localhost:3000/service/example').then(function(response) {
          results.push(response.data);
        });
      });
      
      this.getResults() {
        return results;
      });
    });
    
We might unit test this service as follows:

    describe('my-http-service', function() {
    
      var $httpBackend,
          myHttpService;
          
      beforeEach(module('my-module'));
      
      beforeEach(inject(function(_$httpBackend_, _myHttpService_) {
        $httpBackend = _$httpBackend_;
        myHttpService = _myHttpService_;
      }));
      
      it('should get some data via HTTP', function() {
        $httpBackend.whenGET('example').respond(JSON.stringify('bar'));
        
        // Let's make 3 HTTP calls
        myHttpService.foo();
        myHttpService.foo();
        myHttpService.foo();

        // We haven't flushed the $httpBackend yet
        expect(myHttpService.getResults().length).toBe(0);
        
        // Flush one request
        $httpBackend.flush(1);
        expect(myHttpService.getResults().length).toBe(1);
        expect(myHttpService.getResults()[0]).toBe('bar');
        
        // Flush all pending requests
        $httpBackend.flush();
        expect(myHttpService.getResults().length).toBe(3);
      });
    });
    
For further information on using the `$httpBackend` provided by `ngMock`, see the <a href="http://docs.angularjs.org/api/ngMock/service/$httpBackend">`$httpBackend` documentation</a>.

#### Testing `$interval` and `$timeout`
In order to test components that make use of the `$interval` and `$timeout` services provided by Angular, the `ngMock` module provides mocks for these services that provide additional `flush` methods, and in the case of the mock `$timeout` service, a `verifyNoPendingTasks` method to check that there are no tasks which haven't been flushed.

Let's look at testing a service that uses `$timeout`:

    myModule.service('myTimeoutService', function($timeout) {
      
      this.delayCallback - function(callback) {
        $timeout(callback, 500);
      });
    });

We might test this as follows:

    describe('my-timeout-service', function() {
    
      var $timeout,
          myTimeoutService;
          
      beforeEach(module('my-module'));
      
      beforeEach(inject(function(_$timeout_, _myTimeoutService_) {
        $timeout = _$timeout_;
        myTimeoutService = _myTimeoutService_;
      }));
      
      var callback;
      
      beforeEach(function() {
        callbacks = {
          foo:function() {}
        };
        spyOn(callbacks, 'foo');
      });
      
      it('should delay a callback function by 500ms', function() {
        myTimeoutService.delayCallback(callbacks.foo);
        
        // We haven't flushed yet
        expect(callbacks.foo).not.toHaveBeenCalled();
        
        // Flush 501ms
        $timeout.flush(501);
        expect(callbacks.foo).toHaveBeenCalled();
        
        // Check that there are no outstanding tasks to flush
        $timeout.verifyNoPendingTasks();
      });
    });

Now let's take a look at a service that uses `$interval`:

    myModule.service('myIntervalService', function($timeout) {
    
      var callCount = 0;
      
      this.go = function() {
        $interval(function() {
          callCount++;
        }, 1000);
      });
      
      this.count = function() {
        return callCount
      });
    });

And a test for the service:

    describe('my-interval-service', function() {
    
      var $interval,
          myIntervalService;
          
      beforeEach(module('my-module'));
      
      beforeEach(inject(function(_$interval_, _myIntervalService_) {
        $interval = _$interval_;
        myIntervalService = _myIntervalService_;
      }));
      
      it('should increment its count once a second', function() {
        myIntervalService.go();
        
        // We haven't flushed yet
        expect(myIntervalService.count()).toBe(0);
        
        // Flush 500ms - count should still be 0
        $timeout.flush(500);
        expect(myIntervalService.count()).toBe(0);
        
        // Flush 501ms - we've not flushed 1001ms, so count should be 1
        $timeout.flush(501);
        expect(myIntervalService.count()).toBe(1);
        
        // Flush another 9 seconds - count should now be 10
        $timout.flush(9000);
        expect(myIntervalService.count()).toBe(10);
      });
    });

### Common Angular Testing Patterns
#### Testing a Service
Testing services should be fairly straighforward. All we need to do is load the module containing the service, and then inject the service into our test suite:

    describe('my-service', function() {
      
      var myService;
      
      beforeEach(module('my-module'));
      
      beforeEach(inject(function(_myService_) {
        myService = _myService_;
      }));
      
      it('should do useful service things', function() {
          //Test code for myService
      });
    });

#### Testing a Filter
This is similar to testing a service. We can access the desired filter by injecting the Angular `$filter` service:

    describe('my-filter', function() {
    
      var myFilter;
      
      beforeEach(module('my-module'));
      
      beforeEach(inject(_$filter_) {
        muFilter = _$filter_;
      }));
      
      it('should filter things properly', function() {
        // Test code for myFilter
      });
    });
    
#### Testing a Controller
To test a standalone controller, we just need to instantiate the controller using Angular's `$controller` service, which we can inject in the usual way:

    describe('MyCtrl', function() {
    
      var $controller;
      
      beforeEach(module('my-module'));
      
      beforeEach(inject(function(_$controller_) {
        $controller = _$controller_;
      }));
      
      var instantiateCtrl = function() {
        return $controller('MyCtrl', ($scope: {}});
      });
      
      it('should have a "foo" property with the value "bar"', function() {
        var ctrl = instantiateCtrl();
        expect(ctrl.foo).toBe('bar');
      });
      
      it('should return "qux" when the bax method is called', function() {
        var ctrl = instantiateCtrl();
        expect(ctrl.baz()).toBe('qux');
      });
    });

#### Testing a Directive
Testing a directive is slightly more complicated than testing other Angular components. In order to test a directive, we need to first compile the directive from HTML in order to get access to both the directive's HTML element and its controller, if necessary:

    describe('my-directive', function() {
    
      var $compile,
          $rootScope;
          
      beforeEach(module('my-module'));
      
      beforeEach(inject(function(_$compile_, _$rootScope_) {
        $compile = _$compile_;
        $rootScope = _$rootScope_;
      }));
      
      var element,
          controller;
          
      var compileDirective = function() {
        element = $compile('<wn-my-directive></wn-my-directive>')($rootscope);
        //Run a digest to allow ontroller properties to initialise
        $rootScope.$digest();
        controller = element.controller('myDirective');
      };
      
      it('should compile its template correctly', function() {
        compileDirective();
        expect(element.html()).toBe('<span>This is my directive!</span>');
      });
      
      it('should have a property "foo" with the value "bar" on its controller', function() {
        compileDirective();
        expect(controller.foo).toBe('bar');
      });    
    });
    
Note that the test process uses a Karma pre-processor to read all of the template files in the project and store them in the Angular `$templateCache`. This means that if our directive uses a `templateUrl` (which it should, if it needs to use a template), then a HTTP request <em>will not</em> be made to load the directive's template, so there is no need to use `$httpBackend` to handle this.

If our directive has an isolate scope, then we can simulate the scope bindings by adding the relevant properties to the `$rootScope` and adjusting the template accordingly. For example, if our directive definition looks like this:

    var MyDirectiveCtrl = function($filter) {
      var vm = this;
      vm.capsFoo = $filter('uppercase')(vm.foo);
    });
    
    myModule.directive('myDirective', function() {
      return {
        restrict         : 'E',
        scope            : { foo: '@' },
        templateUrl      : 'path/to/my-directive.html',
        controller       : MyDirectiveCtrl,
        controllerAs     : 'vm',
        bindToController : true
      };
    });
    
Then we might go about testing it as follows:

    describe('my-directive', function() {
    
      var $compile,
          $rootScope,
          $filter;
          
      beforeEach(module('my-module'));
      
      beforeEach(inject(function(_$compile_, _$rootScope_, _$filter_) {
        $compile = _$compile_;
        $rootScope = _$rootScope_;
        $filter = _$filter_;
      }));
      
      var element,
          controller;
          
      var compileDirective = function(foo) {
        $rootScope.parentFoo = foo;
        element = $compile('<wn-my-directive foo = "parentFoo"></wn-my-directive>')($rootScope);
        // Run a digest to allow controller properties to initialise
        $rootScope.$digest();
        controller = element.controller('myDirective');
      };
      
      it('should havea property "foo" with the value "bar" on its controller'), function() {
        compileDirective();
        expect(controller.foo).toBe('bar');
        expect(controller.capsFoo).toBe('BAR');
      });
    });
