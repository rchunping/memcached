#Memcache client for Go

##How to install
```
$ go get github.com/ningjh/memcached
```

##How to use
```js
// import package
import (
    "github.com/ningjh/memcached"
    "github.com/ningjh/memcached/common"
    
    "fmt"
)

// create a memcached client
var memcachedClient, err = memcached.NewMemcachedClient4T("127.0.0.1:11211", "127.0.0.1:11212")

// set an item
var element = &common.Element{
    Key     : "abcd",
    Flags   : 1,
    Exptime : 30, //second
    Value   : []byte("memcached client"),
}
err = memcachedClient.Add(element)

// get an item
item := memcachedClient.Get("abcd")
if item != nil {
    key   := item.Key()
    value := item.Value()
    flags := item.Flags()
    cas   := item.Cas()
}

// get items
keys  := []string{"abc", "def", "ghi"}
items := memcachedClient.GetArray(keys)
if items != nil {
    for _, key := range items {
        if item, ok := items[key]; ok {
            key   := item.Key()
            value := item.Value()
            flags := item.Flags()
            cas   := item.Cas()
        }
    }
}
```
