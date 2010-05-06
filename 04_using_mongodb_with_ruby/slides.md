!SLIDE bullets

# Agenda #

* About MongoDB
* Using MongoDB
* <span class="current">Using MongoDB with Ruby</span>
* Scaling Out
* The Dark Side of MongoDB

!SLIDE bullets incremental

# Options #

* MongoDB Native Driver
* MongoMapper
* Mongoid

!SLIDE ruby

# Native Driver #

    @@@ ruby
    db = Mongo::Connection.new.db('blog')
    
    db['users'].insert(:name => "Jonathan Weiss",
                       :dark_side => true)
                       
    db['users'].find.collect{|u| u['name']}
  

!SLIDE bullets incremental

# MongoMapper #

* It's like ActiveRecord
* <http://mongomapper.com>

!SLIDE ruby

# MongoMapper #

    @@@ ruby
    
    class User
      include MongoMapper::Document
      
      connection Mongo::Connection.new
      set_database_name 'blog'
      
      key :name, String
      key :tweets, Integer
      key :offspring, Array
    end

!SLIDE ruby

# MongoMapper #

    @@@ ruby
    
    user = User.create(:name => "Thomas Metschke")
    User.all(:name => /Thomas/)
    
    # => [#<User name: "Thomas Metschke", _id: ...

!SLIDE bullets incremental

# Mongoid #

* It's also like ActiveRecord
* and like MongoMapper
* <http://mongoid.org>

!SLIDE ruby

# Mongoid #

    @@@ ruby
    class User
      include Mongoid::Document
      field :name
      field :offspring, :type => Array
    end

!SLIDE ruby

# Mongoid #

    @@@ ruby
    User.find(:all, :conditions => {:name => /Thomas/})

!SLIDE bullets incremental

# There are more #

* But they're also like ActiveRecord
* Callbacks, Validations, Embedded Documents