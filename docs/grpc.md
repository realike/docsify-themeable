# grpc

## move omitempty
```
ls *.pb.go | xargs -n1 -IX bash -c 'sed s/,omitempty// X > X.tmp && mv X{.tmp,}'

注意：sed -i此处未使用（inline-replacement），因为该标志在标准OS-X和Linux之间不可移植。

OR

sed -i 's/,omitempty//g' *.pb.go
```
```
grpc-gateway

gwmux := runtime.NewServeMux(runtime.WithMarshalerOption(runtime.MIMEWildcard, &runtime.JSONPb{OrigName: true, EmitDefaults: true}))
```

```
https://www.liwenzhou.com/posts/Go/protobuf/
https://mileslin.github.io/2020/04/Golang/Import-%E5%85%B6%E4%BB%96-proto/

Import "google/protobuf/timestamp.proto" was not found or had errors.
goctl rpc protoc *.proto --go_out=../ --go-grpc_out=../  --zrpc_out=../ --style=goZero --proto_path=/usr/local/include --proto_path=./
```