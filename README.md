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