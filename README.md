# Today I Learned by [Diego Aaron Figueroa Campos]

Ruby and Rails official documentation reading personal journal

## Week 1

### Thu 22, July 2020 [Ruby On Rails Installation]
Rails is a Framework focused on creating websites according to the Model-View-Controller (MVC) pattern. It combines Ruby with HTML, CSS and JavaScript to create web applications that run on a web server. It is considered server-side or Back-end.

In my case, I am using GNU/Linux, so first, you must have the Ruby language and the Rubygems library manager in the system, and after that, you can do the following:

**Install Rails at the command prompt:**
```console
diego@diego:~$ gem install rails 
```

**Create a new Rails application:**
```console
diego@diego:~$ rails new firstapp
```

### Fri 23, July 2020 [RoR Directory Structure]
A new RoR project created has a directory with several auto generated files and folders that make up the structure of a Rails application. Here is a basic rundown on the function of each of the files and folders that Rails created by default:

|Folder      |Purpose                                                                                                   |
|------------|----------------------------------------------------------------------------------------------------------|
|app         |Contains the controllers, models, views, helpers, mailers, channels, jobs, and assets for your application|
|bin         |It basically contains Rails script that start your app. It can also contain other scripts use to setup, upgrade or run the app
|config      |Configure your application's routes, database, and more                                                   |
|db          |It contains your current database schema, as well as the database migrations                              |
|lib         |It contains extended module for your application                                                          |        
|log         |It contains application log files                                                                         |
|public      |It contains static files and compiled assets. This is the only folder seen by the world                   |
|storage     |Active Storage files for Disk Service                                                                     |
|test        |It contains unit tests, other test apparatus and fixtures                                                 |
|tmp         |It contains temporary files like cache and pid files                                                      |
|vendor      |A place for all third-party code. In a typical Rails application this includes vendored gems              |

## Week 2

### Mon 27, July 2020 [RoR Models]
In the MVC pattern, a model is a Ruby class that represents a table in the database. Models are located in the app / models folder. By convention, the name of the table is the same name as the model but not capitalized and in the plural. In the model, the columns of the table are not defined explicitly, ActiveRecord takes them from the table directly.

Although it is possible to create the table and model manually, it is easier to use the model generator of the command line application that includes Rails.
For example, I want to create a table named BrightCoder with the name, github_username, bootcamp and entry_date fields. I should run the following command in the console:

```console
diego@diego:~$ rails generate model BrightCoder name:text github_username:text bootcamp:text entry_date:date
```

The above command will create multiple files, among those:
* The model (BrightCoder class) in app / models / brightcoder.rb.
* A file in db / migrate with the instructions to create the table. This is known as a migration.

### Tue 28, July 2020 [RoR Controllers]
The Rails controller is the logical center of your application. It coordinates the interaction between the user, the views, and the model. The controller is also a home to a number of important ancillary services.

* It is responsible for routing external requests to internal actions.

* It manages caching, which can give applications orders of magnitude performance boosts.

* It manages helper modules, which extend the capabilities of the view templates without bulking up their code.

* It manages sessions, giving users the impression of an ongoing interaction with our applications.

### Wed 29, July 2020 [RoR Views]
Writing all the HTML code directly to the actions (the controller methods) would be quite cumbersome. The solution is to use views. They are the visual representation of the data, everything that has to do with the graphical interface here. Neither the model nor the controller is concerned with how the data will look, that responsibility is the controller of the view.

Views are files located in the app / views folder. The interesting thing about views is that we can mix HTML code with Ruby code.

### Thu 30, July 2020 [RoR Architecture Part 1]
#### Rails Components
Ruby on Rails uses a concept called a configuration convention so that the structure of all projects is similar and we write less code.

The most important components of Ruby on Rails are the following:

* The **router**, which is configured in the `config/routes.rb` file and allows us to associate the **routes** with the **actions**.
* The **controllers**, which are located in the `app/controllers` folder and store the **actions**.
* The **views**, found in `app/views`, allow us to define the HTML code that is rendered from the **controllers**.
* A component that you don't know yet is **ActiveRecord**, which will allow us to interact with the database.
* The **console application**, which will allow us to save development time.

### Fri 31, July 2020 [RoR Architecture Part 2]
#### Router
The router is the component that decides which controller and which method will process an HTTP request. It is configured in the `config/routes.rb` file.

There are several ways to define the routes. I test the following:

`get '/home', to: 'pages#home'`

In this example, we are saying that when someone makes a request to `GET/home`, the index method of the PagesController controller (located in `app/controllers/pages_controller.rb`) is the one in charge of processing the request.

Another equivalent way is to use the operator => (hashrocket) in the following way:

`get '/home' => 'pages#home'`

### Mon 03, August 2020 [RoR Architecture Part 3]
#### Controllers
Controllers are Ruby classes with methods that are going to process HTTP requests. 

```
class PagesController < ApplicationController
  def home
    render html: "<h1>Hello BrightCoders</h1>".html_safe
  end
end
```
En este ejemplo estamos renderizando el HTML `<h1>Hello BrightCoders</h1>`.
El método `html_safe` es necesario para decirle a Rails que no escape el código HTML.

### Tue 04, August 2020 [RoR Architecture Part 4]
#### Views
By convention Rails renders a default view that must be found in a specific location and must be called in a specific way:

* The file name must be the same as the method followed by `.html.erb`.
* It must be located in the `app/views` folder inside a folder that is called the same as the controller.

For example, the home method of the following **controller** will try to render the view `app/views/pages/home.html.erb`:

```
class PagesController < ApplicationController
  def home
  end
end
```

### Wed 05, August 2020 [RoR Architecture Part 5]
#### Passing controller information into view

When you define an **instance variable** (the ones that start with @) in the action, this variable will be available in the view. For example:

```
class PagesController < ApplicationController
  def home
    @name = "Diego"
  end
end
```

The `@name` variable will be available in the view (`app/views/pages/home.html.erb`) and we can display it as follows:

```
<h1>Hello <%= @name %></h1>
```
The `<%=` tag tells **Rails** that we want to display the variable on the screen. One of the most common mistakes is forgetting to add the equal `=` and not understanding why the variable does not appear on the screen.

### Thu 06, August 2020 [RoR Architecture Part 6]
#### Query String

The **query string** is the set of properties that come after the question mark (`?`) Of a URL. **Rails** automatically converts properties into the `params` hash that you can access from the **controller** or the **view**.

For example, if we want to obtain the value of a property called `name` we would use` params [: name] `. Modify `app/views/pages/home.html.erb` to read as follows:

```
<h1> Hello <% = params [: name]%> </h1>
```

Now go to http: // localhost: 3000 /? Name = Diego. You should see "Hello Diego" on the screen. Try changing the **query string** with other names.

The **query string** values always arrive as text strings. If you want another type, you must convert it manually. For example:

```
<h1> In five years you will have <% = params [: age] .to_i + 5%> years </h1>
```

In this case we are converting the `age` property to an integer so we can add it to` 5`.

### Fri 07, August 2020 [RoR Architecture Part 7]
#### ActiveRecord

**ActiveRecord** is the layer that allows us to access and manipulate the information in the database without having to write [SQL (Structured Query Language)] (SQL (Structured Query Language)).

#### The console application

**Ruby on Rails** comes with a powerful console application that allows us, among other things, to generate code through commands called **generators**.

For example:

* `rails new` allows us to create a new application.
* `rails server` allows us to start the server.
* `rails generate controller` allows us to create a controller.

### Mon 10, August 2020 [RoR Routes]
#### Routes
The routes are defined in the file `config/routes.rb`.

Each route is made up of the following elements:

* The **HTTP verb**.
* The **path**.
* The **controller** and **method (action)** that will process the matching request.

For example, the following path:

```
get '/pages/home', to: 'pages # home'
```

* Use the verb `GET`.
* Use the path `/pages/home`
* The `home` method of the` pages_controller.rb` controller will handle the action.

The following are two other ways you can define the same route:

```
get '/ pages / home' => 'pages # home'
get '/ pages / home' # Rails infers controller and path method
```

### Tue 11, August 2020 [RoR Routes Part 2]
#### Path variables

It is possible to define variables in the path of the route to create "dynamic routes". For example, the following path uses a variable named `:name` to match any path that has the structure `/hello/<any_string>`:

```
get '/ hello /: name', to: "pages # hello"
```

In the controller we use the hash `params` to obtain the value of the variable `:name`:

```
class PagesController <ApplicationController
  def hello
    @name = params [: name]
  end
end
```

Although in the view we can also access the hash `params`, in general it is recommended to pass the information through **instance variables**.

### Wed 12, August 2020 [RoR Routes Part 3]
#### Naming the routes

You can give each path a name so you don't have to use the path (e.g. `/pages/home`) in links and redirects.

The name is given with the option `as` as shown in the following example:

```
get '/ pages / home', to: 'pages # home', as: "home"
```

That way, we can now use the name followed by `_path` or` _url` (e.g. `home_path` or` home_url`).

```
home_path # / pages / home
home_url # http: // localhost: 3000 / pages / home
```

In general use `_path` unless you are sharing a link in emails or want to show the full URL.

You can use the path name in links like this:

```
<a href="<%= home_path %> "> Go Home </a>
```

In fact Rails comes with a helper method that we will see later called `link_to` that allows you to create links in the following way:

```
<% = link_to "Go home", home_path%>
```

The latter is the recommended way to make internal links in the application.

### Thu 13, August 2020 [RoR Routes Part 4]
#### Listing the routes

If you want to see a list of all the routes in the application you can use the command `rails routes` from the console (or `rake routes` if you are using a Rails version lower than 5):

```
$ rails routes
    Prefix Verb URI Pattern Controller # Action
pages_home GET /pages/home(.:format) pages # home
```

The `Prefix` is the name of the path. By default Rails gives the path a name even if we haven't used `as`.

### Fri 14, August 2020 [RoR Layouts and Rendering]
#### Listing the routes
By default all views use the layout located in `app/views/layouts/application.html.erb`. The changes you make to that file will affect all views.

In general, within this file there are elements that apply to all views of the application such as the main menu, the footer of the page, etc.

Inside the file you will find the word `yield` which is the line that is replaced by the content of each view.

### Mon 17, August 2020 [RoR Layouts and Rendering Part 2]
#### Changing the layout

There are several ways to change the layout to use when rendering a view:

##### 1. Creating a layout that has the same name as the controller

By default Rails looks for a file in `app/views/layouts` that has the same name as the controller.

For example, if the controller is `pages_controller.rb`, Rails looks for the file `app/views/layouts/pages.html.erb` and uses that file as the layout for all actions in that controller.

Otherwise use `application.html.erb`.

##### 2. Changing the layout in the controller

You can define the layout that all the actions of a controller will use in the following way:

```
class PagesController <ApplicationController
  layout "mi_layout"

  ...
end
```

The line `layout" my_layout "` is telling Rails to use the file `app/views/layouts/my_layout.html.erb` as the layout of all actions in that controller.

You can add conditions so that the layout only applies to some actions or excludes others. For example, with the following line the layout `my_layout.html.erb` will only apply to the actions` index` and `new` of the controller.

```
layout "my_layout", only: [: index,: new]
```

You can also exclude actions. The following line will use the `my_layout.html.erb` layout for all actions except` index`:

```
layout "my_layout", except: [: index]
```

You can prevent controller actions from using a layout with the following line:

```
layout false
```

### Tue 18, August 2020 [RoR Layouts and Rendering Part 4]
#### Rendering and redirecting

By default, when the **action** of a **controller** is executed, Rails renders a view **that is called the same as the action (the method) and is located in a folder that is called the same as the controller** inside `app / views`.

For example, when the `index` action of the` pages_controller.rb` controller is executed by default it will try to render the view `app / views / pages / index.html.erb`.

You can change this behavior in several ways, for now we are going to see the two most common:

##### Using `render`

We used the `render` method before to change the layout. However, you can also use it to render HTML or a different view.

To render HTML:

```
class PagesController <ApplicationController
  def index
    render html: "<h1> Hello World </h1>"
  end
end
```

To render a different view:

```
class PagesController <ApplicationController
  def index
    render "my_view" # also works: render: my_view
  end
end
```

In this case, instead of trying to render `app / views / pages / index.html.erb`, it will render` app / views / pages / my_view.html.erb`.

If the view is in another folder you can use:

```
render "products / index" # render app / views / products / index.html.erb
```

By default Rails uses the response code `200 OK` but you can change it with the` status` option:

```
render status: 200
# render status:: ok
```

### Wed 19, August 2020 [RoR Layouts and Rendering Part 5]
#### Using redirect_to to redirect
To redirect to another path in your application or to an external site use the `redirect_to` method. For example, the following line would redirect the user to `/ authors`:

```
redirect_to authors_path
```

To redirect to an external site simply use the site's URL as follows:

```
redirect_to "http://www.google.com/"
```

### Thu 20, August 2020 [RoR Models]
#### Models
**ActiveRecord** is the layer that allows us to access and manipulate the information in the database without the need to write [SQL (Structured Query Language)] (SQL (Structured Query Language)).

The most important **ActiveRecord** concept is the **model**. A **model** is a Ruby class that represents a table in the database:

```
class Book <ActiveRecord :: Base
end
```

Models are located in the `app / models` folder.

By convention, the table name is the same name as the **model** but not capitalized and in plural (`books` in this case).

In the **model** the table columns are not defined explicitly, **ActiveRecord** takes them from the table directly.

### Fri 21, August 2020 [RoR Models Part 2]
#### My first model

I'm going to test models with the application of books. If you followed the steps you can continue with that same application. Otherwise, you can clone the project and start in the branch of this chapter by executing the following commands:

```
$ git clone https://github.com/makeitrealcamp/books-app.git
$ cd books-app
$ git checkout step-2
```

Although it is possible to create the table and the model manually, it is easier to use the model builder in the command line application that Rails includes.

Let's create our first `Book` model with the fields` title`, `author`,` description`, `publication_date` and` price`. Run the following command in the console:

```
$ rails generate model Book title author description: text publication_date: date price: decimal
```

Several things to keep in mind:

* You can write `generate` or, shorter,` g`.

* The model name can be lowercase or capitalized. If it has multiple words like ** BookComment ** you can write `book_comment` or` BookComment`.

* The fields are separated by ** space **.

* You can define the type of the field using `:` followed by the data type (no spaces!).

* The most common types are: `string`,` text`, `integer`,` decimal`, `date`,` time`, `datetime`,` boolean` and `references`.

* If the type is `string` you can define the maximum length with braces at the end:` string {10} `

* If you omit the type of the field, it is assumed to be `string {255}`.

* The fields `id` (primary key),` created_at` and `updated_at` are created automatically, there is no need to specify them in the command.

The **above command** is going to create multiple files, among those:

* The model (The `Book` class) in` app / models / book.rb`.

* A file in `db / migrate` with the instructions to create the table. This is known as a **migration**.

To create the table you must execute:

```
$ rails db: migrate
```

### Mon 24, August 2020 [RoR Models Part 3]
#### Using the model

With a model we can list, create, modify and delete records from the table it represents. This is known as the **CRUD** by the acronym (**C** reate, **R** ead, **U** pdate, **D** elete).

Later we will use our model from the controllers, but first we will do it from the Rails console.

To open the Rails console run the following command in the console:

```
$ rails console
```

The Rails console is an environment similar to IRB but in which we can access the classes of our application.

### Tue 25, August 2020 [RoR Models Part 4]
#### Creating a record

To create a new record in the database we must instantiate the `Book` model and use the` save` method:

```
> book1 = Book.new (title: "The Pragmatic Programmer", author: "Andrew Hunt, David Thomas", publication_date: "1999-10-20", price: 31.19)
> book1.save
```

There is an equivalent but shorter way:

```
book1 = Book.create (title: "The Pragmatic Programmer", author: "Andrew Hunt, David Thomas", publication_date: "1999-10-20", price: 31.19)
```

### Wed 26, August 2020 [RoR Models Part 5]
#### Finding specific records

When you create a record, the database automatically assigns it a unique `id` that you can use to find that record through the` find` method.

```
book = Book.find (1)
book.title # => The Pragmatic Programmer
book.author # => Andrew Hunt and David Thomas
book.price # => 31.19
```

### Thu 27, August 2020 [RoR Models Part 6]
#### Updating records

To update the information of a record you can use the `save` method again:

```
book = Book.find (1)
book.title = "The Pragmatic Programmer: From Journeyman to Master"
book.save
```

An equivalent but shorter way is with the `update` method:

```
book = Book.find (1)
book.update (title: "The Pragmatic Programmer: From Journeyman to Master")
```

It is also possible to update multiple records at once using `update_all`:

```
# updates the price of all books to 1000
Book.update_all (price: 1000)
```

### Fri 28, August 2020 [RoR Models Part 7]
#### Deleting records

To delete records use the `destroy` method:

```
book = Book.find (1)
book.destroy
```

### Mon 31, August 2020 [RoR Models Part 8]
#### Listing records

```
# returns a collection with all the books
books = Book.all
```

```
# returns the first user, there is also the .last method
book = Book.first
```

```
# returns the book with id 1
book = Book.find (1)
```

```
# returns the first book named Team Geek
book = Book.find_by (title: "Team Geek")
```

Another equivalent way to do the above is:

```
# returns the first book named Team Geek
book = Book.where (title: "Team Geek"). take
```

The `where` method is used to make complex queries and returns a collection of records. (That's why we have to do the `take` in the previous example,` take` gets the first element of the collection.

`where` can also receive a string to create more complex queries:

```
expensive_books = Book.where ("price> 20")
```

For security reasons (especially when the conditions come from users) and for performance it is recommended to change the previous example for the following:

```
expensive_books = Book.where ("price>?", 20)
```

The question marks will be replaced by the following `where` arguments in the order they appear.
