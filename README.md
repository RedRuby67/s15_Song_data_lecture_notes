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
