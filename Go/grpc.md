# gRPC相关问题

## protoc编译".proto"文件具体步骤

1. 安装protocol buffers编译器：用chocolatey安装
2. 安装gRPC库：
```
go get -u google.golang.org/grpc
```
3. 安装Go语言的protoc插件：
```
go get google.golang.org/protobuf/cmd/protoc-gen-go
go install google.golang.org/protobuf/cmd/protoc-gen-go
// go get获取protoc-gen-go的源码，go install将protoc-gen-go.exe安装到GOPATH的bin中（只要执行一次确保有exe文件在可执行路径上就行）

go get google.golang.org/grpc/cmd/protoc-gen-go-grpc
go install google.golang.org/grpc/cmd/protoc-gen-go-grpc
// go get获取protoc-gen-go-grpc的源码，go install将protoc-gen-go-grpc.exe安装到GOPATH的bin中（只要执行一次确保有exe文件在可执行路径上就行）
```
4. 编译".proto"文件：
```
protoc .\ecommerce\product_info.proto --go_out=".\ecommerce\" --go-grpc_out=".\ecommerce\"
// protoc <proto文件路径> --go_out=<输出go代码文件夹> --go-grpc_out=<输出go代码文件夹> 
// go_out参数用protoc-gen-go.exe生成go代码，代码中包含Message（消息）的相关定义
// go-grpc_out参数用protoc-gen-go-grpc.exe生成gRPC相关的go代码，代码中包含Service（服务）的相关定义
```
5. 输出go代码文件夹将与proto文件中的go_package指定的路径拼接，比如go_out="./ecommerce/"，go_package="./"，生成的代码在"./ecommerce/xxx.go"；如果go_package="./service"，生成的代码在"./ecommerce/service/xxx.go"

## gRPC服务器实现时出现的问题
新版protoc-gen-go-grpc生成的gRPC的Service相关代码要求Service还要包含一个`mustEmbedUnimplementedServiceServer()`方法，用于保证前向兼容性（forward compatibility）。

如果不想实现这个方法，有一种偷懒方法。在Service的定义中嵌入proto编译后的包中的`UnsafeServiceServer`接口，这个接口定义了上述方法。例子：
```GO
type server struct {
	productMap map[string]*pb.Product
	pb.UnsafeProductInfoServer //Embed了临时接口，接口定义了上述方法
}
```
