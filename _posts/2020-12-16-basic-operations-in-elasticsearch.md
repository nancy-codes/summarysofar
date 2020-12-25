---
layout: post
title: Basic operations in Elasticsearch
date: 2020-12-16 00:37 +0900
---

Elasticsearch (ES) is a JSON-based, distributed, RESTful search engine based on the Apache Lucene library.

Here is a diagram that illustrates the architectural relationship among units: `index > shard > segment`

<img src="/assets/images/es_architecture.png" alt="es architectural units" style="zoom:50%">


<h5>Terms</h5>
- document: the basic unit of data in ES
  - You say, "Index a document" when inserting data into ES.
- index: logical namespace of collection of documents
- shard: horizontal split of an index; a self-contained Lucene index in itself

<h5>Inverted Index</h5>
- created by tokenizing the terms in each document
- creates a sorted list of all unique terms (terms are normalized, stemmed, etc)
- associated list of documents where the word can be found


<h5>Cluster</h5>
- essentially a group of computers which can be logically seen as a unit, trying to accomplish a particular task
- a cluster consists of 4 nodes, of primary and replica shards.
- a copy (replica) exists for robustness and fault tolerance in case a primary shard is lost


<h5>Node Types</h5>
- master node: cluster-wide operations, coordination
- data node: hold data and index
- client node: load balancer (neither data nor master nodes)


<h5>3 Ways to connect to ES Cluster</h5>
- Kibana Console, `GET _alias`
- cURL, RESTful requests, `curl -XGET "http://localhost:9200/_alias?pretty"`
- Client (python, golang, java, etc)


<h5>Basic Operations in ES</h5>
1. **Write operations in ES**

  - For ES, the basic unit of storage is a shard
  - For Lucene, the basic unit of storage is a segment
  - Each segment is an inverted index
  - New docs are added to new segment
  - Segments are in memory and data is later persisted to disk

  - Translog (transaction log)
    - A lucene commit is a relatively resource-expensive operation
    - Since lucene commits are expensive, each shard copy writes operations into its translog before they are acknowledged
    - request written to translog; document added to memory buffer


<br>
2. **Refresh operation**

  - the `_refresh` operation is set to be executed every second by default
  - during this operation, the in-memory buffer contents is copied to a newly created segment in the memory
  - as a result, new data becomes available for search


<br>
3. **Flush operation**

  - all the documents in the in-memory buffer are written to new Lucene segments, they are combined, then committed to the disk, which clears the translog


<br>
4. **Delete operation**

	- Each segment on disk has a .del file associated with it
	- When a delete request is sent, the document is not really deleted, but marked as deleted in the .del file
	- During search, deleted docs are filtered out
	- During segment merge, they are not included so in this way they are deleted forever

<br>
5. **Update operation**

  - When an update is performed, the old version is marked as deleted in the .del file and the new version is indexed in a new segment


<br>
6. **Read operation**

	- a search request is sent to a coordinating node (cn)
  - cn sends requests to all shards in an index
  - each shard performs search locally and creates a priority queue, send back all the results (doc ids and relevance scores) to the cn
  - cn creates a priority queue to globally sort results returned by the shards
  - cn requests docs to be returned from individual shards
  - each shard fetches certain documents by requested doc id, enriches them and return them to the cn
  



- Boolean query example

```
GET candidates/_search
{
  "query": {
    "bool": {
      "must": [
        {"match": { "status": "single"}},
        {"match": { "job_status": "employeed"}}
      ], 
      "must_not": [
        {"match": {"smoking": false}}
      ],
      "should": [
        {"match": {"job_desc": "developer"}}
      ], 
      "filter": [
        {"range": {"age": {"gte": 27}}}
      ]
    }
  }
}
```



**References**
- [Elasticsearch tutorials for beginners](https://www.youtube.com/watch?v=3XK-6TRkw5I&list=PLa6iDxjj_9qVaf5CsXWP-GAgZoVwKowjx&index=3)

