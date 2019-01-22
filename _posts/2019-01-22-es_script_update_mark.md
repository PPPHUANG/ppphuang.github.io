---
layout: post
title: "ES script更新操作"
date: 2019-01-22
description: "ES script更新操作"
tag: ElasticSearch
---

把URL字段为2222的改为1111
```
POST /datrix_web/datrix_web/_update
{
    "script":"if (ctx._source.url == \"2222\") ctx._source.url=data",
    "params":{
            "data":"1111"
    }
}
```
