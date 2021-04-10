[相关教程](https://mp.weixin.qq.com/mp/appmsgalbum?action=getalbum&__biz=MzI3MjU4Njk3Ng==&scene=24&album_id=1368991005374234626&count=3#wechat_redirect)

## 开篇语

找一些现成的库、框架等，快速的去搭建开发环境，然后拷贝些代码，做出来一些简单的东西，因为很快、很方便、很迅速，并且效果很好。

研究框架的源代码，那真是一行行的看，了解原理以及设计架构和思想

## Gorilla Context

一般都是Map对象，存储对应的Request以及附加的值，然后在需要的时候取出来

在Go1.7之前，Go标准库还没有内置Context

### 判断存储的Key是否存在

注意：

- map的获取值操作
  
- mutex.Lock()和mutex.RLock()的读写锁使用
  

```go
func GetOk(r *http.Request, key interface{}) (interface{}, bool) {
    mutex.RLock()
    if _, ok := data[r]; ok {
        value, ok := data[r][key]
        mutex.RUnlock()        
        return value, ok
    }
    mutex.RUnlock()
    return nil, false
}

func Get(r *http.Request, key interface{}) interface{} {
    mutex.RLock()
    if ctx := data[r]; ctx != nil {
        value := ctx[key]
        mutex.RUnlock()        
        return value
    }
    mutex.RUnlock()
    return nil
}
```

### 获取存储的所有键值对

```go
func GetAll(r *http.Request) map[interface{}]interface{} {
    mutex.RLock()
    if context, ok := data[r]; ok {
        result := make(map[interface{}]interface{}, len(context))
        for k, v := range context {
            result[k] = v
        }
        mutex.RUnlock()        
        return result
    }
    mutex.RUnlock()    
    return nil
}
```

亮点技巧：

- 返回一个map的拷贝: map是一个引用类型，如果我们直接返回了存储的map，调用者就可能会对这个map进行修改，破坏了map的存储.
  
- 创建的拷贝map一定要指定大小，并且大小和原map一样，这样做的好处是map不用进行自动扩充，可以提高性能.