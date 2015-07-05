---
layout: post
title: "Rails"
---

$ rails new hello
$ bundle install
$ rails server

$ rails generate controller salutation

create app/controllers/salutation_controller.rb
create app/views/salutation
create test/functional/salutation_controller_test.rb
create app/helpers/salutation_helper.rb
create test/unit/helpers/salutation_helper_test.rb

creates:
* controller
* helper
* view
* javascript 
* stylesheet

## Create a view

app/views/salutation/hello.html.erb

## Route

config.routes.rb

Hello::Application.routes.draw do
	get ':controller(/:action(/:id(.:format)))'
end

## About the Folder Structure

* **app** All the components of your application.
* **bin** Executables to support Rails.
* **config** Configuration files for all of the components of your application.
* **config.ru** A file used by rack servers to start the application.
* **db Files** related to the database you’re using, and a folder for migrations.
* **Gemfile** Used by the bundler gem to keep a list of gems used in your application.
* **Gemfile.lock** Canonical resource of what gems should be installed.
* **lib** Libraries that may be used in your application.
* **log** Log files that your application may require.
* **public** Static assets served by your application, such as images, JavaScript, and CSS files.
* **Rakefile** Lists available for tasks used by Rake.
* **README.rdoc** Human readable file generated to describe an application.
* **test** Directory containing test unit tests for your application.
* **tmp** Contains temporary files supporting your application.
* **vendor** External libraries, such as gems and plug-ins, that your application bundles.

## Config Database

config/database.yml

## Creating Proejct Databases **Rake**

$ rake db:create

* database migrations
* tests
* updating Rails support files

For a list of all available Rake tasks.
$ rake -T 

### Create all the db for all the environments

$ rake db:create:all

### dbconsole

$ rails dbconsole

$ .exit

$ rake db:migrate

## Creating a Model 

Model names are camel-cased singular and correspond to lower-cased plural table names e.g. Article expected a table named articles.

$ rails generate model Article

* article model
* article test
* articles fixture
* migration

class CreateArticles < ActiveRecord::Migration
  def change
    create_table :articles do |t|
    	t.string :tible
    	t.text :body
    	t.datetime :published_at
      t.timestamps null: false
    end
  end
end

$ rake db:migrate

## Scaffolding

The scaffold provides methods and pages that allow you to insert, update, and delete records in your databse.

$ rails generate scaffold Article title:string body:text published_at:datetime --skip-migration


## Adding fields
$ rails generate migration add_excerpt_and_location_to_articles excerpt:string location:string

$ rails generate scaffold Article title:string location:string excerpt:string body:text published_at:datetime --skip-migration

## Interatctive Interpreter

$ irb

$ rails console

## Ruby Data Types

### Strings
	
#### String interpolation 
"Now is #{Time.now}"

#### Methods
"Toronto - Canada".downcase
"New York, USA".upcase
"a " + "b"
"HELLO".capitalize
"whatever".methods

### Numbers

* Fixnum
* Bignum
* Float

### Symbols

:my_symbol

### Arrays and Hashes

#### Arrays
city_array = ['Toronto,'Miami','Paris]
city_array[0]
city_array[1] = 'New York'
city_array << 'London'
city_array + ["Los Angeles"]

#### Hashes

my_hash = {:canada => "Toronto", :france => "Paris", :uk => "London"}
my_hash[:uk]
my_hash[:canada] = 'Calgary'
my_hash.first
my_hask.keys

## Language Basics

### Variables

* @@count class variables
* @name instance variable
* SERVER_IP constant
* my_string local variables

### Operators

* assignment [] []=
* arithmetic * / % + ** 
* comparision
* range .. ...
* bitwise & ^ |
* logical || && not or and

### Blocks Iterators

5.times {puts "Hello"}

[1,2,3,4,5].each { |item| puts item }

["a","b","c"].each_with_index do |item, index|
	puts "Item: #{item}"
	puts "Index: #{index}"
	puts "---"
end

### Control Structure

now = Time.now

if now == Time.now
	puts "now is the past"
else
	puts "time has passed"
end



a = 5
b = 10
puts "b is greater than a" if a < b
puts "a is greater than b" unless a < b


a = 5
b = 10

while a < b
	puts "a is #{a}"
	a += 1
end

## Methods

def time_as_string
    Time.now.to_s
end

def say_hello_to(name)
    "Hello, #{name}!"
end

## Classes and Objects

{% highlight ruby %}
class Student
    # Setter method for @first_name
    def first_name=(value)
        @first_name=(value)
    end

    # getter method for @first_name
    def first_name
        @first_name
    end

    # setter method for @last_name
    def last_name=(value)
        @last_name = value
    end

    # Getter method for @last_name
    def last_name
        @last_name
    end

    # returns full name
    def full_name
        last_name + ", " + first_name
    end
end
{% endhighlight %}

### Getting to know accessors

{% higlight ruby %}
class Student
    attr_accessor :first_name, :last_name, :id_number

    def full_name
        last_name + ", " + first_name
    end
end
{% endhiglight %}

{% higlight ruby %}
class Team
    attr_accessor :name, :students

    def initialize(name)
        @name = name
        @students = []
    end

    def add_student(id_number, first_name, last_name)
        student = Student.new
        student.id_number = id_number
        student.first_name = first_name
        student.last_name = last_name
        @students << student
    end

    def print_students
        @students.each do |student|
            puts student.full_name
        end
    end
end
{% endhilight %}

## Ruby Style

* INdentation size is two spaces
* Spaces are preferred to tabs
* variables should be lowercase and underscored: some_variable
* method definitons should include parenteses and no unnecessary spaces

**Ruby Documentation**
* Core Library
* Standard Library
* Online resources


