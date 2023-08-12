# Protobuf  
> protobuf 是一种 安全、高效的数据压缩格式，用于在网络通讯中高效地传输数据。
---
# 食用
```proto
// 编译指令
// protoc --go_out=./ ./proto/helloworld.proto

syntax = "proto3";

// 生成文件适配 (防止出现版本不兼容问题)
option go_package = "/proto";

message HelloRequest {
   string name = 1; // 1 是编号
}
```
