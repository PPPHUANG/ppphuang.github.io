---
layout: post
title: "ES查询结果过滤操作"
date: 2019-01-22
description: "ES查询结果过滤操作"
tag: ElasticSearch
---

### 过滤不要的字段
```
{
    "_source": {
        "include": [ "obj1.*", "obj2.*" ],
        "exclude": [ "*.description" ]
    },
    "query" : {
        "term" : { "user" : "kimchy" }
    }
}
```

### 挑选需要的字段
```
{
    "_source": [ "*.description" ],
    "query" : {
        "term" : { "user" : "kimchy" }
    }
}
```
