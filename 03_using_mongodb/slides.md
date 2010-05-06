!SLIDE bullets

# Agenda #

* About MongoDB
* <span class="current">Using MongoDB</span>
* Using MongoDB with Ruby
* Scaling Out
* The Dark Side of MongoDB

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
    db.users.save({
        name: "Mathias Meyer",
        job_title: "Chief Visionary",
        dark_side: true})

!SLIDE

# Finding documents #

    @@@ javascript
    db.findOne({name: "Mathias Meyer"})
    {"_id": ObjectId("4be1d50323173"), "name": ...

    
    db.find({dark_side: true})

!SLIDE

# Cursors #

    @@@ javascript
    var cursor = db.users.find()
    cursor.forEach(function(user) {
      print(tojson(user));
    })

!SLIDE smaller

# Cursors #

    @@@ javascript
    {
      "_id" : ObjectId("4be1d50323173d2c1f55fa71"),
      "dark_side" : false,
      "job_title" : "Chief Visionary",
      "name" : "Mathias Meyer",
      "offspring" : [
        "Mari"
      ],
      "tweets" : 10
    }

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

!SLIDE javascript

# Partial updates #

    @@@ javascript
    db.users.update({name: "Mathias Meyer"},
      { 
        $set: {dark_side: false}
      }
    )

!SLIDE javascript

# Incrementing #

    @@@ javascript
    db.users.update({name: "Mathias Meyer"},
      { 
        $inc: {tweets: 10}
      }
    )

!SLIDE javascript

# Pushing/Pulling #

    @@@ javascript
    db.users.update({name: "Mathias Meyer"},
      {
        $push: {offspring: "Mari"}
      }
    )

!SLIDE javascript

# Complex Queries #

    @@@ javascript
    db.users.find({
      tweets: {$gt: 9},
      tweets: {$lt: 12}
    })

!SLIDE javascript

# Complex Queries #

    @@@ javascript
    db.users.find({
      offspring: {$size: 1}
    })

!SLIDE javascript

# Regular Expressions #

    @@@ javascript
    db.users.find({
      name: /mathias/i
    })

!SLIDE javascript

# Sorting #

    @@@ javascript
    db.users.find()
      .sort({name: -1})

!SLIDE javascript

# Grouping #

    @@@ javascript
    db.users.group({
      key: {dark_side:true},
      reduce: function (obj, previous) {
        previous.csum +=
          (obj.offspring || []).length
      },
      initial: {csum: 0}
    })

!SLIDE javascript smaller

# Map/Reduce #

    @@@javascript
    var result = db.users.mapReduce(function() {
      (this.offspring || []).forEach(function(o) {
        emit(o, {count: 1});
      })
    }, function(key, values) {
      var total = 0;
      for (var i = 0; i < values.length; i++) {
        total += values[i].count;
      }
      return {count:total};
    })

!SLIDE javascript

    @@@ javascript
    db[result.result].find()
    {"_id": "Jared", "value": {"count": 1 }}
    {"_id": "Mari", "value": {"count": 2 }}