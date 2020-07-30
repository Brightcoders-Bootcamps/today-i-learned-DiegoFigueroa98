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

### Fri 29, July 2020 [RoR Views]
Writing all the HTML code directly to the actions (the controller methods) would be quite cumbersome. The solution is to use views. They are the visual representation of the data, everything that has to do with the graphical interface here. Neither the model nor the controller is concerned with how the data will look, that responsibility is the controller of the view.

Views are files located in the app / views folder. The interesting thing about views is that we can mix HTML code with Ruby code.

