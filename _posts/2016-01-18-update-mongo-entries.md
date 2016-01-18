---
layout: post
title:  "find and update simple and nasted  entry on mongoDB"
date:   2016-01-18 13:45:29 -0200
categories: mongoDB 
---

### Connect on your mongoDB, then connect in your dabatase.
{% highlight javascript %}
"mymongo":PRIMARY> show dbs;
admin         0.203GB
foo_db        0.078GB
test          (empty)
{% endhighlight %}

{% highlight javascript %}
use foo_db;
{% endhighlight %}

### Display your collections
{% highlight javascript %}
"mymongo":PRIMARY> show collections;
settings
system.indexes
users
{% endhighlight %}


### In my case I want to search a user named user1 
{% highlight javascript %}
db.foo.find({"username":"user1"} )                                                                                                      
{ "_id" : ObjectId("55d09bfd9f9c7e617300001b"), "username" : "user1"} 
{% endhighlight %}

### Now I want to change the username user1 to updatedUser1

{% highlight javascript %}
db.foo.update({ "username" : "user1"},
    { $set:
      { "username" : "updatedUser1"}
    })
{% endhighlight %}


### For nasted entries you will first search normally for the user you want:

{% highlight javascript %}
db.foo.find({"username":"nasted_user1"} )  
{% endhighlight %}

### The return will be something like below, here you can see that inside address you have zipcode.                                                                                                    
{% highlight javascript %}
{
  "username" : "nasted_user1",
  "addresses" : [
    {
      "zipcode" : "01156040"
    }
  ],
}
{% endhighlight %}

### To access the entry above and change you need to use . like the example below with the user nasted_user1 where is changed his zicode.

{% highlight javascript %}
db.foo.update({ "username" : "nasted_user1"},
  { $set:
    { "addresses.zipcode": "12341234"}
  })
{% endhighlight %}
