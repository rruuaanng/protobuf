# Protobuf

GoogleProtocolBuffer(简称Protobuf)是Google公司内部的混合语言数据标准,可用于通讯协议,数据存储等领域的语言无关,平台无关,可扩展的序列化数据格式

## 语法格式

```protobuf
messageMsgName{
	[label]typefieldName[=fieldId];
	...
	...
	[messageMsgName{...}]
}
```

## 分配字段编号

在定义消息时,必须为每个字段指定一个1到536870911之间的值,且具有如下限制

- 给定的编号必须在字段中是唯一的
- 字段编号19000到19999是protobuf的保留编号,若使用这些编号则抛出警告

通常将1到15作为字段编号,因为数值较低的字段编号占用较少字节,例如1到15范围内的编号需要一字节进行编码,而16到2047需要占用两个字节

## 字段标签

消息中的字段标签包含如下两个标签

- optional:将字段声明为可选,若字段存在值则序列化,否则不会序列化该字段
- repeated:将字段声明为数组类型
- map:将字段声明为键值对类型

示例如下

```protobuf
messagePack{
	optionalint32id = 1;
	repeatedint64set = 2;
	map<string,int32>map = 3;
}
```

## 添加注释

若需要在.proto文件中添加注释,请使用C/C++样式的//和/*...*/语法

```protobuf
/*响应头信息*/
messageRespHeader{
	stringid = 1;//响应id
	stringmsg = "helloworld!";//响应信息
}
```

## 数据类型

| .ProtoType | C++Type | GoType  | Java/KotlinType |
| ---------- | ------- | ------- | --------------- |
| double     | double  | float64 | double          |
| float      | float   | float32 | float           |
| int32      | int32   | int32   | int             |
| int64      | int64   | int64   | long            |
| uint32     | uint32  | uint32  | int             |
| uint64     | uint64  | uint64  | long            |
| sint32     | int32   | int32   | int             |
| sint64     | int64   | int64   | long            |
| fixed32    | uint32  | uint32  | int             |
| fixed64    | uint64  | uint64  | long            |
| sfixed32   | int32   | int32   | int             |
| sfixed64   | int64   | int64   | long            |
| bool       | bool    | bool    | boolean         |
| string     | string  | string  | String          |
| bytes      | string  | []byte  | ByteString      |

## 默认值

解析消息时,若消息不包含特定的单一元素,则解析对象应设置为对应类型的默认值

- 对于string,默认值为空字符串
- 对于bytes,默认值为空字节
- 对于bool,默认值为false
- 对于number,默认值为0
- 对于enum,默认值是第一个定义的枚举值,该值必须为0
- 对于消息字段,若未设置该字段,则默认值取决于对应语言
- 重复字段的默认值为空,通常是对应语言的空列表

## 生成规则

用户使用protoc工具将.proto文件编译后,编译器会通过参数生成指定语言代码

- 对于C++,编译器会生成一个.h和.cc文件,其中包含每个消息类型的类和方法
- 对于Java,编译器会生成一个.java文件,其中包含每个消息类型的类和方法
- 对于Go,编译器会生成一个.pb.go文件,其中包含每个消息类型的结构体和函数
- 对于Python,编译器会生成一个.py文件,将模块和元类一起使用以在运行时创建必要的Python访问类

此处仅对上述语言进行说明,若有其他需求请参考https://protobuf.dev/

## 枚举

定义消息类型时,可使用枚举作为预定义值列表,枚举中的每个值是一个常量

```protobuf
enum RequestT{
	REQUEST_GET = 0;
	REQUEST_POST = 1;
	REQUEST_DELETE = 2;
	REQUEST_PUT = 3;
}

message RequestHeader{
	stringid = 1;
	stringmsg = "helloworld!";
	RequestTtype = 2;
}
```

枚举在定义时必须包含一个元素值为零的常量,这是因为:

- 必须有一个零值,便于将0作为数字默认值
- 零值必须是第一个元素,使得与proto2语义兼容,其中第一个枚举值始终是默认值

## 其他消息作为数据类型

定义消息字段时可以使用其他以及定义的消息作为数据类型(与类相似),如下所示

```protobuf
message Result{
	string id = 1;
	map<string,string> msg = 2;
}

message SearchResp{
	repeated Result resp = 1;
}
```

## 导入定义

在proto文件中,可以通过import语句将其他proto文件中定义的消息类型导入到当前文件中

```protobuf
import "path/other_files.proto"
```

## 嵌套消息类型

定义消息时,可以在消息内部定义多个消息,如下所示

```protobuf
message SearchResp{
    message Result{
        string id = 1;
        map<string,string> msg = 2;
    }
    message Flag{
    	int32 flag = 1;
    }
	repeated Result resp = 1;
	Flag f = 2;
}
// other ...
```

如果需要在消息类型外部重用某个消息内的消息类型,可使用如下方式

```protobuf
// other message type ...
message OtherMsg{
	SearchResp.Result result = 1;
}
```



