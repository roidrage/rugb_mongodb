!SLIDE center

# Installation #

    brew install mongodb

!SLIDE center

# Running #

    mongod --dbpath=./mongodb

!SLIDE center

# The Mongo Shell #

    mongo

!SLIDE center

# Show me how to use it already! #

!SLIDE 

# Creating documents #

    @@@ javascript
    > db.users.save({
        name: "Mathias Meyer",
        job_title: "Chief Visionary",
        dark_side: true})

!SLIDE

# Finding documents #

    @@@ javascript
    > db.findOne({name: "Mathias Meyer"})
    
    {"_id": ObjectId("4be1d50323173"), "name": ...


    > db.find({dark_side: true})

!SLIDE

# Saving documents #

    @@@ javascript
    var user = db.findOne({name: "Mathias Meyer"})
    
    user.name = "Darth Vader"
    
    db.users.save(user)

!SLIDE bullets incremental

# Saving documents #

* Updates are in-place
* Directly modify objects in memory

!SLIDE bullets incremental

# Atomic Operations #

* Partial updates
* Incrementing a value
* Pushing/pulling on lists

!SLIDE

# Partial updates #

    @@@ javascript
    > db.users.update({name: "Mathias Meyer"},
        { 
          $set: {dark_side: false}
        }
      )

!SLIDE

# Incrementing #

    @@@ javascript
    > db.users.update({name: "Mathias Meyer"},
        { 
          $inc: {tweets: 10}
        }
      )
!SLIDE

# Pushing/Pulling #

    @@@ javascript
    > db.users.update({name: "Mathias Meyer"},
      {
        $push: {offspring: "Mari"}
      }
    )