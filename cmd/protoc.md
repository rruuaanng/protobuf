# Protoc

是protobuf的编译器

## 命令行参数

| 参数 (--KEY=VALUE)      | VALUE        | 说明                                                         |
| ----------------------- | :----------- | :----------------------------------------------------------- |
| proto_path              | PATH         |                                                              |
| version                 | NULL         | 查看版本信息                                                 |
| help                    | NULL         | 查看帮助文档(English)                                        |
| encode                  | MESSAGE_TYPE | 从标准输入读取指定类型的文本消息并以二进制格式写入标准输出, 且MESSAGE_TYPE必须在PROTO_FILES中定义 |
| deterministic_output    | NULL         |                                                              |
| decode                  | MESSAGE_TYPE | 从标准输入读取指定类型的二进制消息并以文本格式写入标准输出, 且MESSAGE_TYPE必须在PROTO_FILES中定义 |
| decode_raw              | NULL         |                                                              |
| descriptor_set_in       | FILES        |                                                              |
| descriptor_set_out      | FILE         |                                                              |
| include_imports         | NULL         |                                                              |
| include_source_info     | NULL         |                                                              |
| retain_options          | NULL         |                                                              |
| dependency_out          | FILE         |                                                              |
| error_format            | FORMAT       |                                                              |
| fatal_warnings          | NULL         |                                                              |
| print_free_field_number | NULL         |                                                              |
| enable_codegen_trace    | NULL         |                                                              |
| plugin                  | EXECUTABLE   |                                                              |
| cpp_out                 | OUT_DIR      | 生成C++头文件和源文件                                        |
| java_out                | OUT_DIR      | 生成Java源文件                                               |
| pyi_out                 | OUT_DIR      | 生成python pyi存根文件                                       |
| python_out              | OUT_DIR      | 生成Python源文件                                             |
| go_out                  | OUT_DIR      | 生成Go源文件                                                 |

