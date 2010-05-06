!SLIDE bullets

# Agenda #

* About MongoDB
* Using MongoDB
* Using MongoDB with Ruby
* Scaling Out
* <span class="current">The Dark Side of MongoDB</span>

!SLIDE bullets

# It's not all pretty flowers #

!SLIDE bullets incremental

# Problem Areas #

* Concurrency
* Durability
* Consistency

!SLIDE bullets incremental

# Concurrency #

* Everyone reads
* Everyone writes
* Nothing in between except atomic updates

!SLIDE bullets incremental

# Durability #

* Data is held in memory
* Flushed every 60 seconds

!SLIDE bullets incremental

# Durability #

* Really?
* 60 seconds?

!SLIDE bullets incremental

# Durability #

* If your MongoDB instance crashes
* Data modifications since the last flush
* are lost

!SLIDE bullets incremental

# Durability #

* Want better durability?
* Use replication

!SLIDE bullets incremental

# Consistency #

* Writes to disk are not atomic
* Crash during a write?
* Potentially corrupt data

!SLIDE bullets incremental

# So it's fast for a reason #

* Or several to be exact
* Tradeoffs vs. Awesomeness