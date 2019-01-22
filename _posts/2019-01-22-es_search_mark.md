---
layout: post
title: "ES查询操作"
date: 2019-01-22
description: "ES简单查询操作"
tag: ElasticSearch
---

```
POST /outman1234/outman1234/_search
{
   "query": {
      "bool": {
         "filter": {
            "bool": {
               "must": [
                  {
                     "term": {
                        "portal.web_id": "7fbb00a73aa87902e90fcc4f49946513"
                     }
                  },
                  {
                     "term": {
                        "portal.status": 0
                     }
                  },
                  {
                     "bool": {
                        "should": [
                           {
                              "match": {
                                 "portal.publish_name": "名称"
                              }
                           },
                           {
                              "match": {
                                 "portal.desc": "名称"
                              }
                           },
                           {
                              "match": {
                                 "file_content": "名称"
                              }
                           }
                        ]
                     }
                  }
               ]
            }
         }
      }
   },
   "size": 10,
   "from": 0,
   "sort": [
      {
         "portal.publish_time": {
            "order": "DESC"
         }
      }
   ]
}
```
