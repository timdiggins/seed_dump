Seed Dump
========

Seed Dump is a Rails 4 plugin that adds a rake task named `db:seed:dump`.

It allows you to create a `db/seeds.rb` from the existing data in your database.

Note: if you want to use Seed Dump with Rails 3 or earlier, use [version 0.5.3](http://rubygems.org/gems/seed_dump/versions/0.5.3).

Example Usage
-------------

Dump all data directly to `db/seeds.rb`:

    $ rake db:seed:dump

Dump only data from the users and products table and dump a maximum amount of 2 records:

    $ rake db:seed:dump MODELS=User,Product LIMIT=2

Result:

    $ cat db/seeds.rb
    # Autogenerated by the db:seed:dump task
    # Do not hesitate to tweak this to your needs

    products = Product.create!([
      { :category_id => 1, :description => "Long Sleeve Shirt", :name => "Long Sleeve Shirt" },
      { :category_id => 3, :description => "Plain White Tee Shirt", :name => "Plain T-Shirt" }
    ])

    users = User.create!([
      { :id => 1, :password => "123456", :username => "test_1" },
      { :id => 2, :password => "234567", :username => "tes2" }
    ])

Append to `db/seeds.rb` instead of overwriting it:

    rake db:seed:dump APPEND=true

Use another output file instead of `db/seeds.rb`:

    rake db:seed:dump FILE=db/categories.rb

If you want the dump to use `create` rather than `create!`:

    rake db:seed:dump CREATE_METHOD='create'

There are more environment variables that can be set— see below for all of them.


Installation
------------

Add it to your Gemfile with:

    gem 'seed_dump'

Or install it by hand:

    $ gem install seed_dump


All environment variables
-------------------------

`APPEND`: Append the data to the file instead of overwriting it.

`CREATE_METHOD`: Use the specified create method rather than `create!` (the default).

`FILE`: Use a different output file.  Default: `db/seeds.rb`.

`LIMIT`: Dump no more then this amount of data.  Default: no limit.

`MAX`: Split one create action per model into several create actions with MAX elements in each.  Default: no limit.  Useful for large data dumping to reduce memory usage.

`MODEL[S]`: A model name or a comma-separated list of models.  Default: all models.

`WITH_ID`: Include the `:id` in the `create` options.

`TIMESTAMPS`: If true, include the `:created_by` and `:updated_by` timestamps.  If false, don't include them.  Default: true.

