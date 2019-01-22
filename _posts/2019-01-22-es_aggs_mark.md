---
layout: post
title: "ES聚合操作"
date: 2019-01-22
description: "ES聚合简单操作"
tag: ElasticSearch
---

### 查询18年每月的文档数量
```
POST /datrixdeveloper7u36n36q36x/datrixdeveloper7u36n36q36x/_search
{
  "size": 0, 
  "aggs": {  
    "group_by_state": {  
      "date_histogram": {  
        "field": "Basedata.Ctime",      
        "interval": "month",        
        "format": "yyyy-MM"
          }  
        }  
      }
    },
 "query": { 
    "range": {  
      "Basedata.Ctime": {  
        "gte": "2018-1-1 00:00:00",  
        "lt": "2018-12-31 23:59:59"  
      }  
    }  
  } 
```
返回结果
```
{
   "took": 2,
   "timed_out": false,
   "_shards": {
      "total": 25,
      "successful": 25,
      "skipped": 0,
      "failed": 0
   },
   "hits": {
      "total": 319,
      "max_score": 0,
      "hits": []
   },
   "aggregations": {
      "group_by_state": {
         "buckets": [
            {
               "key_as_string": "2018-09",
               "key": 1535760000000,
               "doc_count": 117
            },
            {
               "key_as_string": "2018-10",
               "key": 1538352000000,
               "doc_count": 202
            }
         ]
      }
   }
}
```
### 按某个字段聚合
```
POST /datrixdeveloper7u36n36q36x/datrixdeveloper7u36n36q36x/_search
{
  "size": 0, 
  "aggs": {  
    "group_by_type": {  
      "terms": {
            "field": "Basedata.type"
         }
    }  
  },
  "query": { 
        "range": {  
          "Basedata.Ctime": {  
            "gte": "2018-1-1 00:00:00",  
            "lt": "2018-12-31 23:59:59"  
          }  
        }  
      }    
}
```
返回结果
```
{
   "took": 2,
   "timed_out": false,
   "_shards": {
      "total": 25,
      "successful": 25,
      "skipped": 0,
      "failed": 0
   },
   "hits": {
      "total": 319,
      "max_score": 0,
      "hits": []
   },
   "aggregations": {
      "group_by_type": {
         "doc_count_error_upper_bound": 0,
         "sum_other_doc_count": 0,
         "buckets": [
            {
               "key": 1,
               "doc_count": 1
            },
            {
               "key": 3,
               "doc_count": 1
            }
         ]
      }
   }
}
```
