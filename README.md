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


## Lecture 10

### Getting Data from Twitter

Prerequisites: Need ruby, gem

### Consumer keys and Access tokens

consumer key: identifies app

accesss tokens: identifies user

Goto: https://github.com/cu-data-engineering-s15/get_tweets


## Lecture 11

### Twitter Data Collection Framework

#### Contracts

__Sample Call__

ruby get_tweets.rb --props=/home/user/oauth.properties badastronomer

Statically-typed language - (like java) uses interfaces

Dynamically-typed language - (like ruby) improvise with method

```
def url
  raise NotImplementedError, "No URL Specified for the Request"
end
```

Subclasses provide implementations of: url, request_name, twitter_endpoint, success

Subclasses may provide implementations for error, authorization, options, make_request, collect

#### Logging

Consists of custom class def and method to create default logger

Created in TwitterRequest's constructor:

```
@log = args[:log] || default_logger
```

Accessed via log attribute:

```
log.info("REQUESTING: #{request.base_url}?#{display_params}")
```

#### Rates

Automatically keeps track of rate imits for Twitter endpoint

Blocks call and sleeps until current Twitter window is done

make_request: ensures rates are checked on each request

```
def make_request
  check_rates
  request = Typhoeus::Request.new(url, options)
  log.info("REQUESTING: #{request.base_url}?#{display_params}")
  response = request.run
  @rate_count = @rate_count - 1
  response
end
```

### Types of Requests

MaxIdRequest, CursorRequest, StreamingRequest

__MaxIdRequest__: subclass for endpooints to traverse timelines with max_id parameter

Defines new contract with: init_condition, condition, update_condition

__CursorRequest__: does not need to define contract for subclasses, but can implement functinality directly

__StreamingRequest__: collect designed to run forever

handlers - on_headers, on_body, on_complete


## Lecture 12

### Intro to NoSQL

NoSQL databases aer AWARE of their distributed nature

They manage sharding and replication for you and are horizontally scalable

NoSQL databases tend to avoid mutable data

NoSQL databases are fault tolerant

### Types of NoSQL Databases

Key-Value, Graphs, Columnar, Documents

__Key-Value Stores__

Just like a hash table, values are untyped

Benefits: Simple

__Graph Stores__

Optimized to store and traverse graph structures

Provide structural query language to locate info based on data structure

__Columnar Stores__

Able to store enormous amounts of data and achieve very fast writes while also reading efficiently

Distributed hash table that is easy to partition across nodes of cluster


__Document Stores__

Similar to key-value but with more structure

Each document gets indexed in various ways and can be grouped into collections, which are grouped into databases


## Lecture 13

### CouchDB

__Document Database__

Document NoSQL Database

Implemented in Erlang

Embraces the web

__Document Model__

self-contained data

stores documents, which contain everything that might be needed by an app that uses it

No schema is enforced

__CAP Theorem__

When designing a distributed data store, there are issues you must confront as soon as your system has more than one running server

Issues: Consistency, Availability, Partial Tolerances

CAP theorem: PICK ANY TWO

## Lecture 14

### MongoDB

__Consistency and Transactions__

CAP theorem: Consistency and availability compete with one another

__Terminology__

document - basic unit of data

collection - table with dynamic schema

__Documents__

Case sensitive and type sensitive

Cannot contain duplicate keys

__Collections__

group of documents

names can be of any UTF- string, but cannot be empty string, have null character, statrt with System, or have '$' character

__Databases__

Reserved database names: Admin, Local, Config

__When to use MongoDB?__

Medicat records, other large document systems

read heavy environments like analytics and mining

partnered with relational databases

__Install MongoDB on Windows__

Go to: https://www.mongodb.org/downloads


## Student Lectures

### Solr

__Lucene__

Powerful search engine written in Java

Used in Solr

__Solr__

search server built on top of Apache Lucene that provides array of features

Searches indexed documents

Each document has ID and term list

Has list of documents for each term

Identifies each document by ID and returns

__Sunspot__

Gem for Ruby on Rails

Bundled version of Solr

__Pitfalls__

Issues with Solr and Rake

Starting server with Solr - different ports

__Conclusion__

Solr is a good way to get search functionality for DB

Fash, reliable, fantastic features like pagination and indexing


### Redis

key value store

__Basics__

not a database replacement

all keys and final values are strings

__Users__

Github, stackoverflow, twitter, etc.

__Optional Features__

Persistence, replication, clustering, server-side scripting

__Special Commands__

Incr, Decr, etc.

__Cloud Providers__

AWS, Morpheous, etc.

__Lists__

Blocking operations provided

__Sorted Set__

Don't have to sort each time set is presented

__Bitmaps__

constant time set/get methods


### Kafka

work with streaming data (ie. gathering tweets about Kanye on Twitter)

Bottleneck created

keeps all messages for u to N days 

written in Scala

named after Franz Kafka

__Alternatives__

RabbitMQ, A Database, Redis, etc.

__Example Architecture__

detecting civil unrest

Interaction of Kafka with Spark, Express,js, MongoDB, AngularJS

Zookeeper - allows for greater coordination in machines



















