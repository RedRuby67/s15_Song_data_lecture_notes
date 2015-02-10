# Lecture Notes for Data Engineering Spring 2014

## Lecture 1

This is where we take notes for this class...

Applications of data engineering and big data: social networks, 

data analytics (sampling to machine learning, 

storage (NoSQL - No sequel)
  
    Issues with queries and performance
    
    Graph
    Key values
    Colorner
    
Data Collection and Cleaning

Data modeling is wicked hard!

Infoviz

    ex. D3
    
Data Lifecycle:

Question (Curation:longevity of data, triach:prioritization) -> Collection, Generation -> Clean up -> Storage -> Processing/Analysis -> Query + Visualize + Act -> New Questions

Software engineers play large role in the stages of the data lifecycle

Request Response Cycle:

Start -> Get/Post/Put/Delete -> HTTP Server

## Lecture 2

Go to https://github.com/cu-data-engineering-s15/syllabus -> wiki

__Markdown presentation:__

Markdown is a plain text formatting that converts easily to HTML

Types of Markdown: Standard Markdown (SM) and Github Flavored Markdown (GFM)

What can you do with it? Styling, word formatting, add images, create lists, links, code blocks

Headers - created with the '#' symbol

Bold/Italics - use "-" symbol

Links - created with square brackets and parenthesis

Code blocks - create with " ``` code ``` "

Tables - create with pipes ie. |, dashes ie. -

Horizontal lines - create with triple hyphens, astericks, underscores

__Services:__

REST - Representation State Transfer

    Resources - URI
    CRUD (Create, Read, Update, Destroy
    

__Given /users :__

Get - Read

Post - creates {data}

Put - update

Delete - destroy

__Simple Example:__

```
require 'sinatra'
require 'sinatra/reloader' if development?

require 'json'

configure do
  set :port, 3000
end

get '/api/1.0/whattimeisit' do
  {status: true, message: Time.now}.tojson + "\n"
end
```

__More Complicated Example:__

```
require 'json'
require 'time'

class Contact

  attr_reader :id, :name, :birthdate, :email, :phone, :twitter 

```

## Lecture 3

Restful Web Services

__Rest__

REST- architectural web service style (inventor: Roy Fielding)

Approach to developing web services tha mimic design of Web itself

Service provides access to linked set of resources

Operations: CRUD (Create, Read, Update, Delete)

```
Example:
GET /api/1.0/users     Retrieves list of users
GET /api/1.0/users/0   Retrieves details of user0
POST /api/1.0/users    Creates new user

PUT /api/1.0/users/0   Update user0
DELETE /api/1.0/users/0 Delete user0
GET /api/1.0/search?q=tattersall   Performs a search with the query tattersail
```

Each operation may produce a result (JSON format is KING)

POST and PUT methods typically send data

__Dealing with accessing shared resources__
```
One approach:
GET /api/1.0/posts/0/comments/1  Gets first coment on post0
POST /api/1.0/posts/0/comments   Creates a new comment n ost0
```

Alternative approach: While performing an operation on one resource, you reference other resources in the data that is sent with the request.

__Issues__

Security, Identity, Failure, Persistence

__Example__

Contacts Web Servce

Implemented in Ruby and Javascript

Technologies used: Sinatra, Rspec, Typhoeus, Node, Express

Goto: https://github.com/cu-data-engineering-s15/contacts

## Lecture 4

__Git Presentations__

Initialization: git init - starts a git repo in current directory whith no files currently tracked

Clone: git clone remote_repository_address - creates a new git repo in current directory that is copy of current

Branching: git branch, git branch new_branch_name (create), git branch -d new_branch_name (delete), git checkout branch_name (change to branch), git checkout commit 

Add: git add file

Commit: git commit -m "Commit Message" - "-m" flag is optional

Merge: git merge branch_name - merges named branch

Pull: git pull [remote_repository] [branch_name]

Push: git push [remote_repository]

Other cool things: log (commit history), remote (setup remote knowledge of remote repos), stash (shelving), rebase (change how branches are related), diff (show differences between commits), fetch (get changes but does not integrate), reset (move to current head), tag (mark git objects), mv (moves files), rm (stops tracking changes to file)

__Github Presentation__

Fork - exact copy of repo, use to run experiments without risk  of messing things up

Github workflow: Branch your commit, Submit a pull request, Re-merge with feedback

Demo: https://github.com/Zandrr/pull_requests_demo

>git checkout -b "new-branch-bug-fix"

make changes >git

>git add README.md

>git commit -m "updated readme"

## Lecture 5

__Node.js__

Node.js - service site for executing javascript

Hello World:

```
var http = require('http');
http.createServer(function (req, res) {
  res.writeHead(200, {'Content-Type': 'text/plain'});
  res.end('Hello World\n');
}).listen(1337, '127.0.0.1');
console.log('Server running at http://127.0.0.1:1337/');
```

Basic Structure:

```
while (there are events to handle) {
  event
  }
```

Callback hell - situation where callbacks are indented, this makes code hard to read, Delays in callbacks

Problems with synchronicity

Two ways to solve problem:

1. Use synchronous functions
2. Use named callback functions

__Node Execution Model__

Node is single-threaded!

Any written code is guaranteed to be synchronous

No need to worry about race conditions

IO is handled in parallel

If you issue an asynchronous call for IO:

    Callback is registered
    IO call is executed in separate thread
        immediately blocks because it is an IO call
  
Makes it easy to implement services that run server-side

## Lecture 6

__Express__

Web app framework written in Javascript for use in Node.js

Design influenced by Sinatra

Makes it easy to define endpoints of web-based service

Includes feautures to create website

Minimum framework - designed to be augmented by node packs

Create Directory - cd into directory and run 'npm init'

Install express: npm install --save express

Install middleware: npm install --save body-parser
                    nmp install --save morgan
                    
See what nmp installed: npm list

Creating Test.json: start with Get request

Creating a module: install moment --save, mkdir lib, cd lib, vi time.js

## Lecture 7

### AngularJS
* client side web application framework
* written in Javascript
* compatibility with JSON RESTful services.

### Core Concepts
* Data bindings
	* Html tag is associated with model object and automatically updates
* Controllers
	* Define all states/methods, Modulize and decompose data
* Services
  * Services remember things that controllers may leave behind when they return multiple times
		* i.e. login controller
* Directives
	* Allow angular to integrate into HTML in a natural way
	* They can also be used to create reusable components that combine controllers, data, and HTML
* Embeddable
	* Anuglar can control as much or as littel of a web page as you specify
	* Provides control over web page, easy to add new functinality

```javascript
Public class Employee
Public Employee(Database d) 
// employee needs  a database to exist, 
// injectable -> finds a database for you without you needing to set up database connections, etc.
// Spring framework is an example of this that gives you dependency injections
```

#### Modules
* Module is the primary way to package upa  set of controllers into an Angular application
* To Create a module: give name and list dependencies
``` javascript
angular.module('contactsApp', [])
```
* Creates a module called contactsApp; with no dependencies
```javascript
angular.module('contactsApp')
```
* When you created a module, you can gain a handle to it by calling angular.module
* When you have defined a module yo ucan tell angular where it lives in the html like this:
```javascript
<html ng-app="contactsApp">
</html>
```

#### Controllers
* To do something in angular, you need a controller.
* Declared using controller function:
```javascript
angular.module('contactsApp').controller('MainController', [<dependencies and code>])
```
* second param is an array that allows controller to declare its dependencies
```javascript
angular.module('contactsApp').controller('MainController', [function() {
  var self    = this;
  self.name   = "Ken Anderson";
  self.update = function() {
    self.name = "Kenneth M. Anderson";
  };
}]);
```
* Anything defined on <i>this</i> is available to the HTML that makes use of the controller.
</br>
* here is an example of using dependencies
```javascript
<MODULE>.controller('MainController', ['$http', function($http) {
  var self    = this;
  self.name   = "Ken Anderson";
  self.update = function() {
    return $http.get('/api/1.0/update_name').then(function(response) { 
      self.name = response.data.new_name;
      return response;
    });
  };
}]);
```
* Create a controller that requires use of ANgulars build-in http module.
* Event lifecycle
	* http get -> returns a promise
	* pass a function, gives a response.
	* inside function do what you want with the response
	* can chain these things... i.e. .then().then()....
```javascript
var age = 22 // private var
this.age = 22 // public var
```
#### AngularJS Hello World

```javascript
<!DOCTYPE html>
<html>
  <head>
    <title>Hello World</title>
  </head>
  <body ng-app>
    <h1>Hello {{name}}</h1>
    <input type="text" ng-model="name" placeholder="First Name">
    <script src="http://ajax.googleapis.com/ajax/libs/angularjs/1.3.11/angular.min.js"></script>
  </body>
</html>
```


## Lecture 8

### More Angular JS

Demonstration with html files.


## Lecture 9

### Getting Data from Twitter

Go to contacts_web_app for example code
