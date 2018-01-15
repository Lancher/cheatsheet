
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

#### Scale:

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









