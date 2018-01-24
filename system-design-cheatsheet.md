
# System Desgin 🦄

- https://www.mitbbs.com/article_t/JobHunting/32777529.html
- https://www.youtube.com/watch?v=-W9F__D3oY4

## Shorten Url Service

#### Use Case:

1. Shorten url.
2. Redirect shorten url to original url.
3. Custom url.
4. Analystic url.
5. Automatic url expiration.
6. Manual url removal.
7. Provide Web UI or API.
8. High availability of system.

#### Constraint and Math:

1. New shorten urls per month: 1 MLN
2. Requests per month: 1BL
3. 10% from shorten urls and 90% from redirect urls.
4. Requests per second: 400 (40: shorten, 360: redirects).
5. 6 BN urls in 5 years.
6. 500 bytes per url and 6 bytes per shorten url
7. 3TBs for all url, 36GBs for all shorten url
8. Data wriiten to disk per sec: 40 * (500 + 6) = 20k
9. Data read from disk per sec: 380 * (500 + 6) = 180k

#### Abstract Layer:

1. Application service:
	* shorten service
	* redirect service
2. Data storage layer (keep tracks of hash <=> url mapping)
	* Act as big hash table
	* Hash Algorithm ?

#### Bottleneck:

1. Traffic is light but data is more interesting.

#### Harvard Web Scale:

1. Watch the https://www.youtube.com/watch?v=-W9F__D3oY4.
	* Vertical Scaling (one good expensive hardware)
	* Horizontal Scaling (multiple slower cheaper hardware)
	* Load Balance (man in the middle between clients and servers)
	* Cache the DNS records in modern browsers.
	* Shared sessions between servers because loading balance rotate the server and send different IPs.
	* RAID (RAID0: 2 same drive for speed, RAID1: mirror drive, RAID10: combine RAID0 and RAID1 with 4 drives)
	* Load Balance (ELB, HAProxy, LVS, Barracuda, Cisco, Citrix)
	* Session Affinity or Sticky Session (Store the random number in session and let the loading balance remeber belong to which server)
	* Caching (.htmls scale very fast, MySQL query caching, memcached: read heavy than write heavy)
	* MySQL (innoerDB support transaction, MyISAM use logs, Memory Engine store in memory, Archive Engine store in compression way to save the space)
	* Database Replication (Master-Slave Database to solve one single point failure, good for read heavy than write heavy throung slaves)
	* Load Balances to avoid single point failure with heatbeats sending between them.
	* Partition (divide the users by name to different data centers)

### Scalability for Dummies

- __Part 1__
	* Public servers should behind a load balancer.
	* Each request should disrtibuted evenly to each application servers
	* Session should be stored in a centralized data servers like redis or memcached
- __Part 2 - MySQL__
	* First, use master-slave replication and keep add RAMs
	* Second, use "sharding", "denormalization" and SQL tuning"
	* Finally, you might want to use NoSQL Database
- __Part 2 - NoSQL__
	* Use MongoDB or CouchDB
	* But sooner your database will again be slower and slower. Then you need to introduce cache
- __Part 3 - In-Memory Caches__
	* Redis
	* Memcached
- __Part 3 - Cached Database Queries__
	* Hash your query
	* The issue is expiration. When a piece of objects changed, you need to delete al related values in cache
- __Part 3 - Cached objects__
	* Recommendation One !!!
	* For exmaple, user sessions, fully reendered blod articles, activity streams, friend relations
	* Redis: persistence and built-in data structures like set and list
	* Memcached: Scaled like a charm
- __Part 4 - Async__
	* Stored pre-Rendered static HTML files
	* RabbitMQ is one of systems to implement async processing

### Sharding
- __Advantages:__
	* Data are denormalized (separate from their comments, blogs, email, media, etc)
	* Data are parallelized across many physical instances
	* Data are kept small (isolating data into smaller shards the data you are accessing is more likely to stay in cache)
	* Data are more highly available
	* It doesn't use replication (At that point read operations can be handled by the slaves, but all writes happen on the master.)
- __Problems__:
	* Rebalancing data (when a shard outgrows your storage and needs to be split?)
	* Joining data from multiple shards (Thankfully, because of caching and fast networks this process is usually fast enough that your page load times can be excellent.)
	* How do you partition your data in shards? (How to seperate your data)
	* Less leverage (With sharding you are on your own becasue not so much tools)
	* Implementing shards is not well supported ()



