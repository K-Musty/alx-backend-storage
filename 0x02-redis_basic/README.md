# 0x02-redis_basic
=======================

## Introduction

Redis (Remote Dictionary Server) is an open-source, in-memory data structure store used as a database, cache, and message broker. It supports data structures such as strings, hashes, lists, sets, sorted sets with range queries, bitmaps, hyperloglogs, geospatial indexes, and streams.

This README will guide you through installing Redis, setting it up, and performing basic operations. We'll also cover using Redis as a simple cache.
Prerequisites

*    Redis installed on your system
*    Basic knowledge of command-line interface

#### Installation
* On Linux
- sudo apt update
- sudo apt install redis-server

### Starting Redis

*To start the Redis server:

redis-server

*To connect to the Redis server using the CLI:

- redis-cli

Basic Operations
1. Strings

Strings are the most basic type of value you can store in Redis, and they are binary safe.

*    Set a string value

- SET key "value"

*    Get a string value

- GET key

2. Hashes

Hashes are maps between string fields and string values, perfect for representing objects.

*    Set a hash field

- HSET user:1 name "John Doe"

*    Get a hash field

- HGET user:1 name

3. Lists

Lists are collections of ordered values.

*    Add to a list

- LPUSH mylist "value"

*    Retrieve from a list

- LRANGE mylist 0 -1

4. Sets

Sets are collections of unique, unordered values.

*    Add to a set

- SADD myset "value"

*    Retrieve from a set


- SMEMBERS myset

5. Sorted Sets

Sorted sets are similar to sets but with a score associated with each value.

*    Add to a sorted set

- ZADD myzset 1 "value"

*    Retrieve from a sorted set

- ZRANGE myzset 0 -1 WITHSCORES

#### Using Redis as a Cache

 Redis is often used as a cache to speed up applications by storing frequently accessed data in memory.
1. Set a cache value with an expiration time

- SETEX cacheKey 3600 "cachedValue"

This command sets a key with an expiration time of 3600 seconds (1 hour).
2. Get a cache value

- GET cacheKey

#### Example: Using Redis in a Node.js Application
---------------------------------------------------
1. Install Redis client for Node.js

- npm install redis

2. Create a simple Node.js script

const redis = require('redis');
const client = redis.createClient();

client.on('connect', () => {
    console.log('Connected to Redis');
});

// Set a value
client.set('my_key', 'Hello, Redis!', (err, reply) => {
    console.log(reply); // OK
});

// Get a value
client.get('my_key', (err, reply) => {
    console.log(reply); // Hello, Redis!
});

// Set a value with expiration
client.setex('cache_key', 3600, 'Cached Value', (err, reply) => {
    console.log(reply); // OK
});

// Get a value from cache
client.get('cache_key', (err, reply) => {
    console.log(reply); // Cached Value
});

client.quit();

### Conclusion

This README covered the basics of using Redis, including installation, basic operations, and using Redis as a cache. For more advanced usage and configurations, refer to the official Redis documentation.

