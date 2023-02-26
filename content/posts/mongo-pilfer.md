---
title: Mongo Pilfer
path: /ctf/kringlecon/2019/mongopilfer
date: '2019-12-15'
type: post
authors:
  - ryken-ab
draft: false
hero:
  image: ../images/dummy.jpg
  large: false
  overlay: true
tags:
  - kringlecon
---
When you try connecting to the default port that Mongo runs on, it gives you a message that says: 
`What if it isn't running on the main port?`


To check what port it is actually running on, we use the command: `ps aux | grep mongo` . This tells us the port that Mongo is running on is: `12121` .


We use this command to connect to a specific Mongo port: `mongo --port 12121`


Now that we are connected to the Mongo database, we can start searching through the collections. We use the command `show dbs` to show all of the databases. They are: `admin`, `elfu`, `local`, and `test`

Now we can assume that we should be looking through elfu. Let's use the command `use elfu` to switch to that database. The command `show collections` will show all of the collections in elfu. There are a lot of them but we only need to focus on the one called `solution`. You can try using that as your data base but it has no collections. What we need to do is to use the command for displaying the contents of a collection. That command would be `db.solution.find()`. And if you want it to look fancy use the command `db.solution.find().pretty()` \

The output of this funstion would be: 

```
        "_id" : "You did good! Just run the command between the stars: ** db.loadServerScripts();displaySolution(); **"
```

Now just run this function inside of the database `elfu` and you will get the acheivement and a nice picture of a Christmas Tree.