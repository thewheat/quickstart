# Redis

https://redis.io/
https://redis.io/commands/


- A key value store


## Interactive mode

- Start by running `redis-cli` and it should get a shell/prompt
- From there you can run commands

```
redis-cli
redis 127.0.0.1:6379> ping

PONG
redis 127.0.0.1:6379> 
```

## Running commands directly without interactive mode

- `redis-cli COMMAND`

```
redis-cli ping

PONG
```

## Set key value
```
redis 127.0.0.1:6379> SET mykey somevalue

OK
```

```
redis-cli SET mykey somevalue

OK
```

## Get key value

- Returns `nil` if doesn't exist

```
redis 127.0.0.1:6379> GET mykey

"somevalue"
```

```
redis-cli GET mykey

"somevalue"
```

## Delete key value

- Delete single / multiple entries
- Returns number of keys deleted

```
DEL key
DEL key1 key2 key3
```

## Search keys

- `KEYS PATTERN`
- All keys in this database
```
KEYS *
```
- All keys starting with 2

```
KEYS 2*
```

## Set expiry

- Sets time in seconds. Once expired returns `nil`

```
EXPIRE mykey 5
SETEX mykey 5 somevalue
SET mykey somevalue EX 5
```

## Get TTL 

- Returns time to live in seconds
- `-1` if no expiry
- `-2` if expired
```
TTL mykey
```

## Selecting database

- Redis has 16 databases to store keys into
- Index values `0` to `15`

```
SELECT index
```

## Find number of keys in database

```
DBSIZE
```


## Administration

### View general info
```
redis-cli INFO
```

### View database usage

- See 
   - which database are in use
   - how many keys they have
   - how many keys have expiry times
   - average TTL values

```
redis-cli INFO keyspace

# Keyspace
db0:keys=5577,expires=0,avg_ttl=0
db1:keys=1,expires=0,avg_ttl=0
```

### View memory details
```
redis-cli INFO memory
```

### Find keys with no expirty

```
redis-cli keys * | while read LINE ; do TTL=`redis-cli TTL "$LINE"`; if [ $TTL -eq  -1 ]; then echo "$LINE"; fi; done;
```

