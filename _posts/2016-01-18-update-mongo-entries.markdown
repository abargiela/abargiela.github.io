---
layout: post
title:  "find and update simple and nasted  entry on mongoDB"
date:   2016-01-18 13:45:29 -0200
categories: mongoDB 
---

### Connect on your mongoDB, then connect in your dabatase.
"mymongo":PRIMARY> show dbs;
admin         0.203GB
foo_db        0.078GB
test          (empty)


use foo_db;


### Display your collections
"mymongo":PRIMARY> show collections;
settings
system.indexes
users


### In my case I want to search a user named user1 
db.foo.find({"username":"user1"} )                                                                                                      
{ "_id" : ObjectId("55d09bfd9f9c7e617300001b"), "username" : "user1"} 

### Now I want to change the username user1 to updatedUser1

db.foo.update({ "username" : "user1"},
    { $set:
      { "username" : "updatedUser1"}
    })


### For nasted entries you will first search normally for the user you want:

db.foo.find({"username":"nasted_user1"} )  

### The return will be something like below, here you can see that inside address you have zipcode.                                                                                                    
{
  "username" : "nasted_user1",
  "addresses" : [
    {
      "zipcode" : "01156040"
    }
  ],
}

### To access the entry above and change you need to use . like the example below with the user nasted_user1 where is changed his zicode.

```
db.foo.update({ "username" : "nasted_user1"},
    { $set:
      { "addresses.zipcode": "12341234"}
    })
```

Jekyll also offers powerful support for code snippets:

Check out the [Jekyll docs][jekyll-docs] for more info on how to get the most out of Jekyll. File all bugs/feature requests at [Jekyll’s GitHub repo][jekyll-gh]. If you have questions, you can ask them on [Jekyll Talk][jekyll-talk].

[jekyll-docs]: http://jekyllrb.com/docs/home
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-talk]: https://talk.jekyllrb.com/
