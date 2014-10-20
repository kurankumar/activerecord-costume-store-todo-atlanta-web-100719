---
tags: activerecord, todo, introductory
languages: ruby
resources: 2
---

# ActiveRecord Costume Store

## Objectives

![jack o lantern emoji](http://www.emoji-cheat-sheet.com/graphics/emojis/jack_o_lantern.png) ![dog ghost emoji](http://www.emoji-cheat-sheet.com/graphics/emojis/ghost.png) ![jack o lantern emoji](http://www.emoji-cheat-sheet.com/graphics/emojis/jack_o_lantern.png)

For this morning's todo, you'll be creating a table, 'costume_stores', and a class, CostumeStore, with the help of ActiveRecord.

## Background

The table will have seven columns:
  1. name
  2. location
  3. number of costumes, or "costume inventory"
  4. number of employees
  5. whether or not it's still in business
  6. opening time
  7. closing time

Before coding out the creation of this table, take a look at just a few ActiveRecord data types below:

|Data Type                      |Examples                                |
|-------------------------------|----------------------------------------|
|boolean                        | true, false                            |
|integer                        | 2, 13, 485                             |
|string                         | "Halloween", "Boo!"                    |
|datetime                       | DateTime.now, DateTime.new(2014,10,31) |

## ActiveRecord

ActiveRecord is magic. Well, not really. But it does build out a bunch of methods for you. For instance, when it's used properly it will give you access to methods such as `create`, `save`, and `find_by`. 

ActiveRecord allows you to create a database that interacts with your class with only a few lines of code. These lines of code go to creating a model, which resides in the `app/models` folder, and a migration, which resides in the `db/migrations` folder.

The model inherits from `ActiveRecord::Base` while the migration inherits from `ActiveRecord::Migration`. Many migrations these days have a `change` method, but you might also see migrations with an `up` and a `down` method instead. To use ActiveRecord, you have to stick to some specific naming conventions: while the migrations are plural, the models are singular. 

#### Migrations

To start, the class names in the migration files must match their file names. For instance, a class in the migration file called `20141013204115_create_candies.rb` must be named `CreateCandies` while a class in a migration file called `20130915204319_add_addresses_to_houses.rb` must be called AddAddressesToHouses. 

You might notice that in both the examples above, the numbers at the front of the file name were ignored. These numbers are in the form `YYYYMMDDHHMMSS`. Later on, these timestamps will become important as Rails uses them to determine which migration should be run and in what order. For instance, if you made a table called `dog_walkers` and then added a column to it called `rating`, that would be fine as the timestamp on the table creation would be before adding a column to it. However, if you did this in reverse order, that is adding a column to a table that doesn't exist then creating the table, you would get an error.

#### Example 

For instance, let's say you wanted to make a `class Candy`, which has two attributes, a name (string) and the number of calories (integer), you would write the migration as seen below:

`db/migrations/20130915204319_create_candies.rb`

```ruby
class CreateCandies < ActiveRecord::Migration
  def change
    create_table :products do |t|
      t.string :name
      t.integer :calories
      t.timestamps
    end
  end
end
```

Meanwhile, the model would be singular.

`app/models/candy.rb`

```ruby
class CostumeStore < ActiveRecord::Base
end
```

After saving the code above, running `rake db:migrate` will apply the desired changes to the database by running the change method. Then you can alter the database with simple Ruby statements.

For instance, you could type

```ruby
Candy.create(:name => "Reese's Peanut Butter Cups", :calories => 210)
Candy.find_by(:name => "Reese's Peanut Butter Cups")
# => 
``` 


## Instructions

#### File Structure

You will only be altering code in two files, `costume_store.rb` in the `app/models/` folder and `001_create_costume_stores.rb` in the `db/migrations/` folder.

```
├── app
│   └── models
│       └── costume_store.rb
└──db
    └── migrations
        └──001_create_costume_stores.rb
```

#### Getting Started

**This is a test-driven lab so start with the first test and work your way down.**

* The first step is to run `bundle install`.
* Create the CostumeStore class in `app/models/`.
* Fill out the ActiveRecord migration such that it passes the specs.
* Remember to run `rake db:migrate` every time you change or create a migration. 
* Just like on any other lab, run `rspec` to view your progress.

## Resources
* [ActiveRecord Migrations](http://guides.rubyonrails.org/migrations.html)
  * Just look at the code for the example migrations
* [Creating Active Record Models](http://guides.rubyonrails.org/active_record_basics.html#creating-active-record-models) 