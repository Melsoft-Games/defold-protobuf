![](docs/logo.png)

# Defold-Protobuf

Defold-Protobuf [Native Extension](https://www.defold.com/manuals/extensions/) for the [Defold Game Engine](https://www.defold.com) 

This extension allow you work with google protobuf protocol (files .proto), encode and decode them.


## Platforms

* **iOS**
* **Android**
* **MacOS**
* **Windows**

## Setup

You can use the Defold-Protobuf extension in your own project by adding this project as a [Defold library dependency](https://www.defold.com/manuals/libraries/). Open your game.project file and in the dependencies field under project add:

> https://github.com/Melsoft-Games/defold-protobuf/archive/master.zip

Or point to the ZIP file of a [specific release](https://github.com/Melsoft-Games/defold-protobuf/releases).

## Short API:

``` lua 
local protoc = require("pb.protoc")

protoc:loadfile("/resources/test.proto")
local data = {
	values = {
		first = {
		number = 1.5,
		unumber = 20,
		string = "hello"
	}
}

-- some.Example - name of message from test.proto
local bytes = pb.encode("some.Example", data)
local unpackage = pb.decode("some.Example", bytes)
```

## API

### **protoc** - lua module to parse proto files
This part of docs from [lua-protobuf README](https://github.com/starwing/lua-protobuf/blob/master/README.md)

| Function                | Returns       | Descriptions                                         |
| ----------------------- | ------------- | ---------------------------------------------------- |
| `protoc.reload()`       | true          | reload all google standard messages into `pb` module |
| `protoc:parse(string)`       | table         | transform schema to `DescriptorProto` table          |
| `protoc:parsefile(string)`   | table         | like `protoc:parse()`, but accept filename                |
| `protoc:compile(string)`     | string        | transform schema to binary *.pb format data          |
| `protoc:compilefile(string)` | string        | like `protoc:compile()`, but accept filename              |
| `protoc:load(string)`        | true          | load schema into `pb` module                         |
| `protoc:loadfile(string)`    | true          | like `pb:loadfile()`, but accept filename (you can point file from custom resouces in Defold)            |
| `protoc.loaded`              | table         | contains all parsed `DescriptorProto` table          |
| `protoc.paths`               | table         | a table contains import search directories           |
| `protoc.unknown_module`      | see below     | handle schema import error                           |
| `protoc.unknown_type`        | see below     | handle unknown type in schema                        |
| `protoc.include_imports`     | bool          | auto load imported proto                             |


### **pb** - native extension symbol
#### `pb.encode(message_name, data)`
returns bytes of lua table *data*. Data should be match to proto description *message_name*
If proto file has `package {name};` *message_name* will be `{name}.{message_name}`

#### `pb.decode(message_name, bytes)`
returns lua table from bytes. Bytes should be match to proto description *message_name*


Full README to **pb** and **protoc** read [here](https://github.com/starwing/lua-protobuf/blob/master/README.md)


## License, Authors
*MIT license*
This NE wrapped by [AKashpur](https://github.com/AKashpur)

Original module: [lua-protobuf](https://github.com/starwing/lua-protobuf)

## Issues and suggestions

If you have any issues, questions or suggestions please [create an issue](https://github.com/Melsoft-Games/defold-protobuf/issues) or contact me: insality@gmail.com
