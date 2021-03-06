#####In this section

In this section you'll learn about how to use caching for your apps in CloudBoost. Caching is great for your apps because it helps you to access data much faster when compared to the database. On the downside, querying is limited and it is very expensive (money-wise) because all the data is on the memory (which is expensive) instead of being on a disk. It is recommended that you use cache only for frequently accessed data.  

<p>&nbsp;</p>
><span class="tut-info">Info</span> Cache can only be used with a master key, and not with any of the client keys.

#Create Cache

Before you save and query data from the cache. You need to create a cache instance which can be done by calling create method of the <span class="tut-snippet">CB.CloudCache</span> instance. create method takes no parameters and returns an empty CB.CloudCache instance.

==JavaScript==
<span class="js-lines" data-query="create">
```
var cache = new CB.CloudCache('CacheName');
    cache.create({
    success : function(cache){
        //cache is an empty the object of the CB.CloudCache instance.
        console.log(cache);
    }, error : function(error){
        console.log(error);
    }
});
```
</span>

==NodeJS==
<span class="nodejs-lines" data-query="create">
```
var cache = new CB.CloudCache('CacheName');
    cache.create({
    success : function(cache){
        //cache is an empty the object of the CB.CloudCache instance.
        console.log(cache);
    }, error : function(error){
        console.log(error);
    }
});
```
</span>

==cURL==
<span class="curl-lines" data-query="create">
```
curl -X POST --header 'Content-Type: application/json' --header 'Accept: application/json' -d '{
  "key": ${master_key}
}' 'http://api.cloudboost.io/cache/${app_id}/${cache_name}/create'
```
</span>

#Adding / Updating Item

To add or update an item into the Cache, you need to call the set method of the <span class="tut-snippet">CB.CloudCache</span> instance. <span class="tut-snippet">put</span> function takes in a key as the first parameter and an item of any datatype as the second parameter.

==JavaScript==
<span class="js-lines" data-query="put">
```
var cache = new CB.CloudCache('CacheName');
var item = {'name':'John Doe', 'age':24, 'sex':'MALE'};
cache.set('sample',item, {
    success : function(item){
        //item is the object that you added to the cache.
        console.log(item);
    }, error : function(error){
        console.log(error);
    }
});
```
</span>

==NodeJS==
<span class="nodejs-lines" data-query="put">
```
var cache = new CB.CloudCache('CacheName');
var item = {'name':'John Doe', 'age':24, 'sex':'MALE'};
cache.set('sample',item, {
    success : function(item){
        //item is the object that you added to the cache.
        console.log(item);
    }, error : function(error){
        console.log(error);
    }
});
```
</span>

==cURL==
<span class="curl-lines" data-query="put">
```
curl -X PUT --header 'Content-Type: application/json' --header 'Accept: text/html' -d '{
  "item": ${data_to_cache},
  "key": ${master_key}}
}' 'http://api.cloudboost.io/cache/${app_id}/${cache_name}/${data_key}}'
```
</span>

#Get Item

To get an item from the Cache, you need to call the get method of the <span class="tut-snippet">CB.CloudCache</span> instance with the parameter of the item key.

==JavaScript==
<span class="js-lines" data-query="get">
```
cache.get('sample',{
    success : function(item){
        //item is the object that you added to the cache..
        console.log(item);
    }, error : function(error){
        console.log(error);
    }
});
```
</span>

==NodeJS==
<span class="nodejs-lines" data-query="get">
```
cache.get('sample',{
    success : function(item){
        //item is the object that you added to the cache..
        console.log(item);
    }, error : function(error){
        console.log(error);
    }
});
```
</span>

==cURL==
<span class="curl-lines" data-query="get">
```
curl -X POST --header 'Content-Type: application/json' --header 'Accept: application/json' -d '{
  "key": ${master_key}
}' 'http://api.cloudboost.io/cache/${app_id}/${cache_name}/${data_key}/item'
```
</span>

#Delete item

To delte an item from the Cache, you need to call the DeleteItem method of the <span class="tut-snippet">CB.CloudCache</span> instance with the parameter of the item key.

==JavaScript==
<span class="js-lines" data-query="delete">
```
cache.deleteItem('sample',{
    success : function(key){
        //deleted
    }, error : function(error){
        console.log(error);
    }
});
```
</span>

==NodeJS==
<span class="nodejs-lines" data-query="delete">
```
cache.deleteItem('sample',{
    success : function(deleted){
        //deleted
    }, error : function(error){
        console.log(error);
    }
});
```
</span>

==cURL==
<span class="curl-lines" data-query="delete">
```
curl -X PUT --header 'Content-Type: application/json' --header 'Accept: application/json' -d '{
  "key": ${master_key},
  "method":"DELETE"
}' 'http://api.cloudboost.io/cache/${app_id}/${cache_name}/item/${data_key}'
```
</span>


#Get all items

To get all the Cache items, you need to call the getAll method of the <span class="tut-snippet">CB.CloudCache</span> instance with no parameters.

getAll method returns an array of all the items stored in the cache.

==JavaScript==
<span class="js-lines" data-query="getall">
```
cache.getAll({
    success : function(items){
        //items is an array of all the items stored in that cache instance..
        console.log(items);
    }, error : function(error){
        console.log(error);
    }
});
```
</span>

==NodeJS==
<span class="nodejs-lines" data-query="getall">
```
cache.getAll({
    success : function(items){
        //items is an array of all the items stored in that cache instance..
        console.log(items);
    }, error : function(error){
        console.log(error);
    }
});
```
</span>

==cURL==
<span class="curl-lines" data-query="getall">
```
curl -X POST --header 'Content-Type: application/json' --header 'Accept: application/json' -d '{
  "key": "${master_key}"
}' 'http://api.cloudboost.io/cache/${app_id}/${cache_name}/items'
```
</span>

#Count Items

To get the number of items stored in the cache, you need to call the GetItemsCount method of the <span class="tut-snippet">CB.CloudCache</span> instance with no parameters.

GetItemsCount method returns the number of items stored in the cache.

==JavaScript==
<span class="js-lines" data-query="getitemscount">
```
cache.getItemsCount({
    success : function(count){
        //count is the number of items stored in the cache instance..
        console.log(count);
    }, error : function(error){
        console.log(error);
    }
});
```
</span>

==NodeJS==
<span class="nodejs-lines" data-query="getitemscount">
```
cache.getItemsCount({
    success : function(count){
        //count is the number of items stored in the cache instance..
        console.log(count);
    }, error : function(error){
        console.log(error);
    }
});
```
</span>

==cURL==
<span class="curl-lines" data-query="getitemscount">
```
curl -X POST --header 'Content-Type: application/json' --header 'Accept: application/json' -d '{
  "key": "${master_key}"
}' 'http://api.cloudboost.io/cache/${app_id}/${cache_name}/items/count'
```
</span>

#Get size of a cache

To get the size of the  cache, you need to call the getInfo method of the <span class="tut-snippet">CB.CloudCache</span> instance.

GetInfo method returns the updated cache instance which has the size of the cache in KB.

==JavaScript==
<span class="js-lines" data-query="getinfo">
```
cache.getInfo({
    success : function(cache){
        //cache is the instace of the cache.
        //to get cache size,
        console.log(cache.size);
    }, error : function(error){
        console.log(error);
    }
});
```
</span>

==NodeJS==
<span class="nodejs-lines" data-query="getinfo">
```
cache.getInfo({
    success : function(cache){
        //cache is the instace of the cache.
        //to get cache size,
        console.log(cache.size);
    }, error : function(error){
        console.log(error);
    }
});
```
</span>

==cURL==
<span class="curl-lines" data-query="getinfo">
```
curl -X POST --header 'Content-Type: application/json' --header 'Accept: application/json' -d '{
  "key": ${master_key}
}' 'http://api.cloudboost.io/cache/${app_id}/${cache_name}'
```
</span>

#Clear Cache

To clear an instance of the cache, you need to call the Clear method of the <span class="tut-snippet">CB.CloudCache</span> instance.

Clear method returns an empty cache object which is an instance of the CB.CloudCache.
the object is of the following format.

==JavaScript==
<span class="js-lines" data-query="clear">
```
cache.clear({
    success : function(cache){
        //cache is the an empty instance of CB.CloudCache
        console.log(cache);
    }, error : function(error){
        console.log(error);
    }
});
```
</span>

==NodeJS==
<span class="nodejs-lines" data-query="clear">
```
cache.clear({
    success : function(cache){
        //cache is the an empty instance of CB.CloudCache
        console.log(cache);
    }, error : function(error){
        console.log(error);
    }
});
```
</span>

==cURL==
<span class="curl-lines" data-query="clear">
```
curl -X PUT --header 'Content-Type: application/json' --header 'Accept: application/json' -d '{
  "key": ${master_key},
  "method":"DELETE"
}' 'http://api.cloudboost.io/cache/${app_id}/${cache_name}/clear'
```
</span>

#Delete Cache

To delete an instance of the cache, you need to call the delete method of the <span class="tut-snippet">CB.CloudCache</span> instance with no parameters.

Delete method returns an empty cache object which is an instance of the CB.CloudCache.

==JavaScript==
<span class="js-lines" data-query="deletecache">
```
cache.delete({
    success : function(cache){
        //cache is the an empty instance of CB.CloudCache
        console.log(cache);
    }, error : function(error){
        console.log(error);
    }
});
```
</span>

==NodeJS==
<span class="nodejs-lines" data-query="deletecache">
```
cache.delete({
    success : function(cache){
        //cache is the an empty instance of CB.CloudCache
        console.log(cache);
    }, error : function(error){
        console.log(error);
    }
});
```
</span>

==cURL==
<span class="curl-lines" data-query="deletecache">
```
curl -X PUT --header 'Content-Type: application/json' --header 'Accept: application/json' -d '{
  "key": ${master_key},
  "method":"DELETE"
}' 'http://api.cloudboost.io/cache/${app_id}/${cache_name}'
```
</span>

#Get All Caches

To get all the app caches, you need to call the getAll method a static method of the <span class="tut-snippet">CB.CloudCache</span>  with no parameters.

getAll method returns an array of CB.CloudCache objects.


==JavaScript==
<span class="js-lines" data-query="getallappcache">
```
CB.CloudCache.getAll({
    success : function(caches){
        //caches is the an array of CloudCache Objects
        console.log(caches);
    }, error : function(error){
        console.log(error);
    }
});
```
</span>

==NodeJS==
<span class="nodejs-lines" data-query="getallappcache">
```
CB.CloudCache.getAll({
    success : function(caches){
        //caches is the an array of CloudCache Objects
        console.log(caches);
    }, error : function(error){
        console.log(error);
    }
});
```
</span>

==cURL==
<span class="curl-lines" data-query="getallappcache">
```
curl -X POST --header 'Content-Type: application/json' --header 'Accept: application/json' -d '{
  "key": ${master_key}
}' 'http://api.cloudboost.io/cache/${app_id}'
```
</span>

#Delete All Caches

To delete all the app caches, you need to call the deleteAll method a static method of the <span class="tut-snippet">CB.CloudCache</span>  with no parameters.


==JavaScript==
<span class="js-lines" data-query="deleteallappcache">
```
CB.CloudCache.deleteAll({
    success : function(caches){
        //caches is an array of CB.CloudCache onjects
        console.log(caches);
    }, error : function(error){
        console.log(error);
    }
});
```
</span>

==NodeJS==
<span class="nodejs-lines" data-query="deleteallappcache">
```
CB.CloudCache.deleteAll({
    success : function(caches){
        //caches is an array of CB.CloudCache onjects
        console.log(caches);
    }, error : function(error){
        console.log(error);
    }
});
```
</span>

==cURL==
<span class="curl-lines" data-query="deleteallappcache">
```
curl -X PUT --header 'Content-Type: application/json' --header 'Accept: application/json' -d '{
  "key": ${master_key},
  "method":"DELETE"
}' 'http://api.cloudboost.io/cache/${app_id}'
```
</span>

#Name

To get name of the cache, you need to call the name property on the <span class="tut-snippet">CB.CloudCache</span> .

==JavaScript==
<span class="js-lines" data-query="name">
```
var cache = new CB.CloudCache('sample');
var cacheName = cache.name;
```
</span>

==NodeJS==
<span class="nodejs-lines" data-query="name">
```
var cache = new CB.CloudCache('sample');
var cacheName = cache.name;
```
</span>

==cURL==
<span class="curl-lines" data-query="name">
```
//
```
</span>

#Size

To get size of the cache, you need to call the size property on the <span class="tut-snippet">CB.CloudCache</span> .

Size property returns the size of the cache in kilobytes(kb).

==JavaScript==
<span class="js-lines" data-query="size">
```
var cache = new CB.CloudCache('sample');
var cacheSize = cache.size;
```
</span>

==NodeJS==
<span class="nodejs-lines" data-query="size">
```
var cache = new CB.CloudCache('sample');
var cacheSize = cache.size;
```
</span>

==cURL==
<span class="curl-lines" data-query="size">
```
//
```
</span>
