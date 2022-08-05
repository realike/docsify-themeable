# go-zero

## go-zero-looklook
```
5-民宿服务.md
一般我们自己维护db cache会写的零零散散，但是go-zero使用了配套内置工具goctl生成的model，自带sqlc+sqlx实现的代码，实现了自动缓存管理，我们根本不需要去管理缓存，只需要用sqlx写 sql数据，sqlc会自动帮我们管理缓存，并且是通过singleflight ,也就是说即使缓存在某个时间失效，在失效那一刻同时有大量并发请求进来时，go-zero在查询db时候也只会放行一个线程进来，其他线程是在等待，当这个线程从数据库拿数据回来之后将该数据缓存到redis同时所有之前等待线程共享此数据返回，后续在进来的线程查相同数据时，就只会进入到redis中而不会进入到db。

这样rpc拿到所有数据之后，就可以返回给前端显示了一般我们自己维护db cache会写的零零散散，但是go-zero使用了配套内置工具goctl生成的model，自带sqlc+sqlx实现的代码，实现了自动缓存管理，我们根本不需要去管理缓存，只需要用sqlx写 sql数据，sqlc会自动帮我们管理缓存，并且是通过singleflight ,也就是说即使缓存在某个时间失效，在失效那一刻同时有大量并发请求进来时，go-zero在查询db时候也只会放行一个线程进来，其他线程是在等待，当这个线程从数据库拿数据回来之后将该数据缓存到redis同时所有之前等待线程共享此数据返回，后续在进来的线程查相同数据时，就只会进入到redis中而不会进入到db。


? if mysql更新, go-zero redis是否有刷新机制
ref: https://blog.51cto.com/u_11140372/2366439

? 手动remove omitempty, response json是否还会生效, 还是使用grpc-gateway
```