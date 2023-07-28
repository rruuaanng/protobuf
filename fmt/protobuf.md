# Protobuf

Google Protocol Buffer( 简称Protobuf) 是 Google 公司内部的混合语言数据标准, 可用于通讯协议, 数据存储等领域的语言无关,平台无关,可扩展的序列化数据格式

## 语法格式

```protobuf
message MsgName{
	[modifier] type varName; 
	...
	...
	[message MsgName{ ... }]
}
```

## 添加注释

若需要在.proto文件中添加注释, 请使用C/C++样式的//和/* ... */语法

```protobuf
/* 响应头信息 */
message RespHeader{
	string id = 1; // 响应id
	string msg = "hello world!"; // 响应信息
}
```

## 数据类型

| .Proto Type | C++ Type | Go Type | Java/Kotlin Type |
| ----------- | -------- | ------- | ---------------- |
| double      | double   | float64 | double           |
| float       | float    | float32 | float            |
| int32       | int32    | int32   | int              |
| int64       | int64    | int64   | long             |
| uint32      | uint32   | uint32  | int              |
| uint64      | uint64   | uint64  | long             |
| sint32      | int32    | int32   | int              |
| sint64      | int64    | int64   | long             |
| fixed32     | uint32   | uint32  | int              |
| fixed64     | uint64   | uint64  | long             |
| sfixed32    | int32    | int32   | int              |
| sfixed64    | int64    | int64   | long             |
| bool        | bool     | bool    | boolean          |
| string      | string   | string  | String           |
| bytes       | string   | []byte  | ByteString       |

## 默认值

解析消息时, 若消息不包含特定的单一元素, 则解析对象应设置为对应类型的默认值

- 对于string, 默认值为空字符串
- 对于bytes, 默认值为空字节
- 对于bool, 默认值为false
- 对于number, 默认值为0
- 对于enum, 默认值是第一个定义的枚举值, 该值必须为0
- 对于消息字段, 若未设置该字段, 则默认值取决于对应语言
- 重复字段的默认值为空, 通常是对应语言的空列表

## 生成规则

用户使用protoc工具将.proto文件编译后, 编译器会通过参数生成指定语言代码

- 对于C++, 编译器会生成一个.h和.cc文件, 其中包含每个消息类型的类和方法
- 对于Java, 编译器会生成一个.java文件, 其中包含每个消息类型的类和方法
- 对于Go, 编译器会生成一个.pb.go文件, 其中包含每个消息类型的结构体和函数
- 对于Python, 编译器会生成一个.py文件,将模块和元类一起使用以在运行时创建必要的Python访问类

此处仅对上述语言进行说明,若有其他需求请参考https://protobuf.dev/

## 枚举

定义消息类型时, 可使用枚举作为预定义值列表, 枚举中的每个值是一个常量

```protobuf
enum RequestT{
	REQUEST_GET = 0;
	REQUEST_POST = 1;
	REQUEST_DELETE = 2;
	REQUEST_PUT = 3;
}

message RequestHeader{
	string id = 1;
	string msg = "hello world!";
	RequestT type = 2; 
}
```

枚举在定义时必须包含一个元素值为零的常量, 这是因为:

- 必须有一个零值, 便于将0作为数字默认值
- 零值必须是第一个元素, 使得与proto2语义兼容, 其中第一个枚举值始终是默认值

