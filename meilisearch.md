# Quickstart for MeiliSearch

- https://meilisearch.com
- https://docs.meilisearch.com/learn/getting_started/quick_start.html#download-and-launch
- https://docs.meilisearch.com/reference/features/authentication.html#adding-the-master-key


## Start

### No authentication: Accepts all requests
```
meilisearch
```

### With authentication

```
export MEILI_MASTER_KEY=[YOUR_MASTER_KEY]
meilisearch

meilisearch --master-key=[YOUR_MASTER_KEY]
```

## Add documents
https://docs.meilisearch.com/reference/api/documents.html

```
curl \
  -X POST 'http://127.0.0.1:7700/indexes/movies/documents' \
  -H 'Content-Type: application/json' \
  --data-binary @movies.json
```

**Example output**
```
{"updateId":1}
```

## Checking updates
```
curl \
  -X GET 'http://localhost:7700/indexes/movies/updates'
```


**Sample output**
```
[
  {
    "status":"processed",
    "updateId":0,
    "type": {
      "name":"DocumentsAddition",
      "number":19546
    },
    "duration":13.98,
    "enqueuedAt":"2021-12-13T10:47:59.087670Z",
    "processedAt":"2021-12-13T10:48:13.068510Z"
  },
  {"status":"processed","updateId":1,"type":{"name":"DocumentsAddition","number":19546},"duration":14.102,"enqueuedAt":"2021-12-13T10:48:16.178449Z","processedAt":"2021-12-13T10:48:30.280932Z"}
]
```
## Search
https://docs.meilisearch.com/reference/api/search.html
- POST route
   - preferred route when using API authentication
   - allows preflight request caching and better performances
- GET route
   - usage discouraged, unless you have good reason to do otherwise (specific caching abilities for example).

```
curl \
  -X POST 'http://127.0.0.1:7700/indexes/movies/search' \
  -H 'Content-Type: application/json' \
  --data-binary '{ "q": "the ninja" }'
``` 

```
curl \
  -X GET 'http://localhost:7700/indexes/movies/search?q=the%20ninja'
``` 

**Sample output**

```
{
  "hits":[
    {"id":"41378","title":"Five Element Ninjas","poster":"https://image.tmdb.org/t/p/w500/nUidOywTrK8kceDCOHQRuLGqs4y.jpg","overview":"A young martial artist seeks revenge on the ninja who kills his martial arts brothers and teacher.","release_date":388198800,"genres":["Action"]},
    {"id":"25684","title":"American Ninja 5","poster":"https://image.tmdb.org/t/p/w500/6ZSM6rDMEg4FNfqBn41kPLevwx9.jpg","overview":"When a scientists daughter is kidnapped, American Ninja, attempts to find her, but this time he teams up with a youngster he has trained in the ways of the ninja.","release_date":725846400,"genres":["Action","Thriller"]},
    ...
    ....
  ],
  "nbHits":48,
  "exhaustiveNbHits":false,
  "query":"the ninja",
  "limit":20,
  "offset":0,
  "processingTimeMs":3
}  
```

## Authentication

### Get keys
- Start with authentication
```
curl -X GET 'http://127.0.0.1:7700/keys' \
  -H 'X-Meili-API-Key: MASTER_KEY'
``` 
**Sample output**
```
{
  "private":"8c222193c4dff5a19689d637416820bc623375f2ad4c31a2e3a76e8f4c70440d"
  "public":"948413b6667024a0704c2023916c21eaf0a13485a586c43e4d2df520852a4fb8"
}
 ```
 
### Using Authentication/Keys
- Add `-H 'X-Meili-API-Key: KEY'` to requests
- The Master key grants access to all routes
- The Private key grants access to all routes except the `/keys` routes
- The Public key only grants access to the following routes:
    - GET `/indexes/:index_uid/search`
    - POST `/indexes/:index_uid/search`
    - GET `/indexes/:index_uid/documents`
    - GET `/indexes/:index_uid/documents/:document_id`

## Indexes

### Get Indexes
```
curl \
  -X GET 'http://localhost:7700/indexes'
```

**Sample Output**

```
[
  {"uid":"movies","name":"movies","createdAt":"2021-12-13T10:47:58.752975Z","updatedAt":"2021-12-13T12:42:46.328886Z","primaryKey":"id"},
  {"uid":"test","name":"test","createdAt":"2021-12-13T10:48:32.417408Z","updatedAt":"2021-12-13T10:48:58.689203Z","primaryKey":"id"}
]
```

### Get single Index

```
curl \
  -X GET 'http://localhost:7700/indexes/movies'
```

**Sample Output**
```
{
  "uid":"movies",
  "name":"movies",
  "createdAt":"2021-12-13T10:47:58.752975Z",
  "updatedAt":"2021-12-13T12:42:46.328886Z",
  "primaryKey":"id"
}
```

## Documents

### Get Documents

```
curl \        
  -X GET 'http://localhost:7700/indexes/movies/documents' 
```

**Sample Output**
```
[
  {
    "id": "100",
    "title": "Lock, Stock and Two Smoking Barrels",
    "poster": "https://image.tmdb.org/t/p/w500/8kSerJrhrJWKLk1LViesGcnrUPE.jpg",
    "overview": "A card shark and his unwillingly-enlisted friends need to make a lot of cash quick after losing a sketchy poker match. To do this they decide to pull a heist on a small-time gang who happen to be operating out of the flat next door.",
    "release_date": 889056000,
    "genres": [
      "Comedy",
      "Crime"
    ]
  },
  {
    "id": "10001",
    "title": "Young Einstein",
    "poster": "https://image.tmdb.org/t/p/w500/2OtWkhzdpsmE7gnY3VsJCiFr9U3.jpg",
    "overview": "Albert Einstein is the son of a Tasmanian apple farmer, who discovers the secret of splitting the beer atom to put the bubbles back into beer. When Albert travels to Sydney to patent his invention he meets beatuiful French scientist Marie Curie, as well as several unscrupulous types who try to take advantage of the naive genius and his invention.",
    "release_date": 598147200,
    "genres": [
      "Comedy",
      "Science Fiction"
    ]
  },
  ...
]  
```

### Get Single Document

```
curl \        
  -X GET 'http://localhost:7700/indexes/movies/documents/100' 
```

**Sample Output**
```
{
  "id": "100",
  "title": "Lock, Stock and Two Smoking Barrels",
  "poster": "https://image.tmdb.org/t/p/w500/8kSerJrhrJWKLk1LViesGcnrUPE.jpg",
  "overview": "A card shark and his unwillingly-enlisted friends need to make a lot of cash quick after losing a sketchy poker match. To do this they decide to pull a heist on a small-time gang who happen to be operating out of the flat next door.",
  "release_date": 889056000,
  "genres": [
    "Comedy",
    "Crime"
  ]
}
```

