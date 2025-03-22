# 基础信息

|      |      |
|------|------|
| 名称 | ApiRequestCodec |
| 编码语言 | .java |
| 代码路径 | erp-backend/erp-library/src/main/java/com.jukusoft/erp/lib/message/request/ApiRequestCodec.java |
| 包名 | com.jukusoft.erp.lib.message.request |
| 依赖项 | ['io.vertx.core.buffer.Buffer', 'io.vertx.core.eventbus.MessageCodec', 'io.vertx.core.json.JsonArray', 'org.json.JSONArray', 'org.json.JSONObject', 'java.util.ArrayList'] |
| 概述说明 | ApiRequestCodec类负责ApiRequest对象与JSON间的编码解码。 |

# 说明

ApiRequestCodec类负责实现消息的编码与解码功能，主要处理ApiRequest对象与JSON格式之间的相互转换。该类确保数据在传输过程中能够正确编码为JSON格式，并在接收时准确解码为ApiRequest对象，从而实现高效的数据交换与通信。

# 类列表 Class Summary

| 名称   | 类型  | 说明 |
|-------|------|-------------|
| ApiRequestCodec | class | ApiRequestCodec类实现消息编码解码，处理ApiRequest对象与JSON转换。 |



## 类 ApiRequestCodec

|      |      |
|------|------|
| 访问范围 | public |
| 类型 | class |
| 名称 | ApiRequestCodec |
| 说明 | ApiRequestCodec类实现消息编码解码，处理ApiRequest对象与JSON转换。 |


### UML类图

```mermaid
classDiagram
    class ApiRequestCodec {
        +void encodeToWire(Buffer buffer, ApiRequest req)
        +ApiRequest decodeFromWire(int position, Buffer buffer)
        +ApiRequest transform(ApiRequest apiRequest)
        +String name()
        +byte systemCodecID()
    }

    class Buffer {
        +void appendInt(int value)
        +void appendString(String value)
        +int getInt(int position)
        +String getString(int start, int end)
    }

    class JSONObject {
        +void put(String key, Object value)
        +String getString(String key)
        +JSONObject getJSONObject(String key)
        +long getLong(String key)
        +boolean getBoolean(String key)
        +JSONArray getJSONArray(String key)
        +String toString()
    }

    class JSONArray {
        +void put(Object value)
        +int length()
        +String getString(int index)
    }

    class ApiRequest {
        -String eventName
        -JSONObject data
        -String ackID
        -long messageID
        -String externalID
        -JSONObject meta
        -String sessionID
        -boolean isLoggedIn
        -long userID
        -List~String~ permissions
        +long getMessageID()
        +String getExternalID()
    }

    ApiRequestCodec --> Buffer : 使用
    ApiRequestCodec --> JSONObject : 使用
    ApiRequestCodec --> JSONArray : 使用
    ApiRequestCodec --> ApiRequest : 处理
```

这段代码定义了一个名为 `ApiRequestCodec` 的类，它实现了 `MessageCodec` 接口，用于对 `ApiRequest` 对象进行编码和解码。`encodeToWire` 方法将 `ApiRequest` 对象编码为 JSON 格式并写入 `Buffer`，而 `decodeFromWire` 方法则从 `Buffer` 中读取 JSON 数据并解码为 `ApiRequest` 对象。`transform` 方法直接返回传入的 `ApiRequest` 对象，`name` 方法返回类名，`systemCodecID` 方法返回系统编解码器的 ID。代码中使用了 `Buffer`、`JSONObject` 和 `JSONArray` 等辅助类来完成编码和解码操作。


### 内部方法调用关系图

```mermaid
graph TD
    A["类ApiRequestCodec"]
    B["方法: encodeToWire(Buffer buffer, ApiRequest req)"]
    C["方法: decodeFromWire(int position, Buffer buffer)"]
    D["方法: transform(ApiRequest apiRequest)"]
    E["方法: name()"]
    F["方法: systemCodecID()"]

    A --> B
    A --> C
    A --> D
    A --> E
    A --> F

    B --> B1["创建JSONObject对象"]
    B1 --> B2["将req的属性放入JSONObject"]
    B2 --> B3["创建JSONArray对象并放入权限"]
    B3 --> B4["将JSONObject转换为字符串"]
    B4 --> B5["计算字符串长度并写入buffer"]

    C --> C1["获取JSON字符串的长度"]
    C1 --> C2["从buffer中读取JSON字符串"]
    C2 --> C3["解析JSON字符串为JSONObject"]
    C3 --> C4["将JSONObject的属性赋值给req"]
    C4 --> C5["解析权限并添加到req的permissions中"]
```

这段代码定义了一个名为`ApiRequestCodec`的类，实现了`MessageCodec`接口，用于对`ApiRequest`对象进行编码和解码。`encodeToWire`方法将`ApiRequest`对象转换为JSON格式并写入缓冲区，而`decodeFromWire`方法则从缓冲区中读取JSON字符串并解析为`ApiRequest`对象。`transform`方法直接返回传入的`ApiRequest`对象，`name`方法返回类名，`systemCodecID`方法返回固定的编码ID。

### 字段列表 Field List

| 名称  | 类型  | 说明 |
|-------|-------|------|

### 方法列表 Method List

| 名称  | 类型  | 说明 |
|-------|-------|------|
| encodeToWire | void | 将ApiRequest对象编码为JSON并写入缓冲区。 |
| name | String | 重写name方法，返回当前类的简单名称。 |
| systemCodecID | byte | 重写systemCodecID方法，返回值为-1。 |
| decodeFromWire | ApiRequest | 从缓冲区解码JSON数据并构建ApiRequest对象。 |
| transform | ApiRequest | 重写transform方法，直接返回传入的ApiRequest对象。 |




