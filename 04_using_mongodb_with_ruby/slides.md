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
  

!SLIDE ruby

# MongoMapper #

    @@@ ruby