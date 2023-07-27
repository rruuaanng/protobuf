# Protobuf

Google Protocol Buffer( 简称Protobuf) 是 Google 公司内部的混合语言数据标准，可以用于结构化数据串行化，或者说序列化。它很适合做数据存储或 RPC 数据交换格式。可用于通讯协议、数据存储等领域的语言无关、平台无关、可扩展的序列化结构数据格式。

## 语法格式

```protobuf
message MsgName{
	[modifier] type varName 
	...
}
```

## 数据类型

| proto Type | C++ Type | Java/Kotlin Type | Go Type |
| ---------- | -------- | ---------------- | ------- |
| double     | double   | double           | float64 |
| float      | float    | float            | float32 |
| int32      | int32    | int              | int32   |
| int64      | int64    | long             | int64   |
| uint32     | uint32   | int              | uint32  |
| uint64     | uint64   | long             | uint64  |
| sint32     | int32    | int              | int32   |
| sint64     | int64    | long             | int64   |
| fixed32    | uint32   | int              | uint32  |
| fixed64    | uint64   | long             | uint64  |
| sfixed32   | int32    | int              | int32   |
| sfixed64   | int64    | long             | int64   |
| bool       | bool     | boolean          | bool    |
| string     | string   | String           | string  |
| bytes      | string   | ByteString       | []byte  |

