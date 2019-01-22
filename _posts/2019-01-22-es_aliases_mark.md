---
layout: post
title: "ES别名操作"
date: 2019-01-22
description: "ES别名简单操作"
tag: ElasticSearch
---

### 创建一个别名
```
POST _aliases
{
   "actions": [
      {
         "add": {
            "index": "datrixdeveloper7u36n36q36x",
            "alias": "datrixdeveloper7u36n36q36x_datrix4_transcode",
            "filter" : { "term" : { "Basedata.Space" : "datrix4_transcode" } }
         }
      }
   ]
}
```
### 移除一个别名
```
POST _aliases
{
   "actions": [
      {
         "remove": {
            "index": "datrixdeveloper7u36n36q36x",
            "alias": "datrixdeveloper7u36n36q36x_datrix4_transcode"
         }
      }
   ]
}
```
### 移除一个别名 添加一个别名
```
POST _aliases
{
   "actions": [
      {
         "remove": {
            "index": "datrixdeveloper7u36n36q36x",
            "alias": "datrixdeveloper7u36n36q36x_datrix4_transcode"
         }
      },
      {
         "add": {
            "index": "datrixdeveloper7u36n36q36x",
            "alias": "datrixdeveloper7u36n36q36x_datrix4_transcode",
            "filter" : { "term" : { "Basedata.Space" : "datrix4_transcode" } }
         }
      }
   ]
}
```
### 添加两个别名
```
POST _aliases
{
   "actions": [
      {
         "add": {
            "index": "indexname",
            "alias": "aliasname"
         }
      },
      {
         "add": {
            "index": "datrixdeveloper7u36n36q36x",
            "alias": "datrixdeveloper7u36n36q36x_datrix4_transcode",
            "filter" : { "term" : { "Basedata.Space" : "datrix4_transcode" } }
         }
      }
   ]
}
```
