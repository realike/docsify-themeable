# grpc

## move omitempty
```
ls *.pb.go | xargs -n1 -IX bash -c 'sed s/,omitempty// X > X.tmp && mv X{.tmp,}'

注意：sed -i此处未使用（inline-replacement），因为该标志在标准OS-X和Linux之间不可移植。
```
```
grpc-gateway

gwmux := runtime.NewServeMux(runtime.WithMarshalerOption(runtime.MIMEWildcard, &runtime.JSONPb{OrigName: true, EmitDefaults: true}))
```