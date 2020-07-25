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
A new RoR project created has a directory with several auto-generated files and folders that make up the structure of a Rails application. Here is a basic rundown on the function of each of the files and folders that Rails created by default:

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