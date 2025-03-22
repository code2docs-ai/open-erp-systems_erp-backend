# 基础信息

|      |      |
|------|------|
| 名称 | ApiResponseCodec |
| 编码语言 | .java |
| 代码路径 | erp-backend/erp-library/src/main/java/com.jukusoft/erp/lib/message/response/ApiResponseCodec.java |
| 包名 | com.jukusoft.erp.lib.message.response |
| 依赖项 | ['com.jukusoft.erp.lib.message.StatusCode', 'io.vertx.core.buffer.Buffer', 'io.vertx.core.eventbus.MessageCodec', 'io.vertx.core.json.JsonObject'] |
| 概述说明 | ApiResponseCodec实现MessageCodec接口，处理ApiResponse的编码与解码。 |

# 说明

ApiResponseCodec是一个实现了MessageCodec接口的类，其主要职责是处理ApiResponse的编码与解码工作。它负责将ApiResponse对象转换为适合传输的格式，并在接收时将其还原为原始对象，确保数据在通信过程中的完整性和正确性。

# 类列表 Class Summary

| 名称   | 类型  | 说明 |
|-------|------|-------------|
| ApiResponseCodec | class | ApiResponseCodec实现MessageCodec接口，负责ApiResponse的编码与解码。 |



## 类 ApiResponseCodec

|      |      |
|------|------|
| 访问范围 | public |
| 类型 | class |
| 名称 | ApiResponseCodec |
| 说明 | ApiResponseCodec实现MessageCodec接口，负责ApiResponse的编码与解码。 |


### UML类图

```mermaid
classDiagram
    class ApiResponseCodec {
        +void encodeToWire(Buffer buffer, ApiResponse res)
        +ApiResponse decodeFromWire(int position, Buffer buffer)
        +ApiResponse transform(ApiResponse apiResponse)
        +String name()
        +byte systemCodecID()
    }

    class Buffer {
        +void appendInt(int value)
        +void appendString(String value)
        +int getInt(int position)
        +String getString(int start, int end)
    }

    class ApiResponse {
        -String eventName
        -JsonObject data
        -String ackID
        -StatusCode statusCode
        -long messageID
        -String externalID
        -String sessionID
        -String type
        +ApiResponse(long messageID, String externalID, String sessionID, String event)
        +long getMessageID()
        +String getExternalID()
        +String getSessionID()
        +String getType()
        +StatusCode getStatusCode()
    }

    class JsonObject {
        +JsonObject()
        +JsonObject(String jsonStr)
        +void put(String key, Object value)
        +String getString(String key)
        +JsonObject getJsonObject(String key)
        +long getLong(String key)
        +String toString()
    }

    class StatusCode {
        +static StatusCode getByString(String statusCode)
    }

    ApiResponseCodec --> Buffer : 依赖
    ApiResponseCodec --> ApiResponse : 依赖
    ApiResponseCodec --> JsonObject : 依赖
    ApiResponseCodec --> StatusCode : 依赖
    ApiResponse --> JsonObject : 依赖
```

这段代码定义了一个 `ApiResponseCodec` 类，它实现了 `MessageCodec` 接口，用于将 `ApiResponse` 对象编码为 `Buffer` 中的字节流，以及从 `Buffer` 中解码为 `ApiResponse` 对象。`ApiResponse` 类包含了多个字段，如 `eventName`、`data`、`ackID` 等，`JsonObject` 类用于处理 JSON 数据的序列化和反序列化。`StatusCode` 类提供了根据字符串获取状态码的功能。整个代码结构清晰，职责分明，主要用于处理 API 响应的编码和解码操作。


### 内部方法调用关系图

```mermaid
graph TD
    A["类ApiResponseCodec"]
    B["方法: encodeToWire(Buffer buffer, ApiResponse res)"]
    C["创建Json对象: JsonObject json = new JsonObject()"]
    D["检查res.data是否为null"]
    E["抛出异常: NullPointerException"]
    F["填充Json对象: json.put('event', res.eventName)等"]
    G["将Json对象转换为字符串: String jsonToStr = json.toString()"]
    H["计算字符串长度: int length = jsonToStr.getBytes().length"]
    I["将数据写入buffer: buffer.appendInt(length)和buffer.appendString(jsonToStr)"]
    J["方法: decodeFromWire(int position, Buffer buffer)"]
    K["获取JSON长度: int length = buffer.getInt(_pos)"]
    L["获取JSON字符串: String jsonStr = buffer.getString(_pos+=4, _pos+=length)"]
    M["创建Json对象: JsonObject json = new JsonObject(jsonStr)"]
    N["创建ApiResponse对象: ApiResponse res = new ApiResponse(...)"]
    O["填充ApiResponse对象: res.eventName = json.getString('event')等"]
    P["方法: transform(ApiResponse apiResponse)"]
    Q["返回apiResponse: return apiResponse"]
    R["方法: name()"]
    S["返回类名: return this.getClass().getSimpleName()"]
    T["方法: systemCodecID()"]
    U["返回-1: return -1"]

    A --> B
    B --> C
    C --> D
    D -->|是| E
    D -->|否| F
    F --> G
    G --> H
    H --> I
    A --> J
    J --> K
    K --> L
    L --> M
    M --> N
    N --> O
    A --> P
    P --> Q
    A --> R
    R --> S
    A --> T
    T --> U
```

这段代码定义了一个名为`ApiResponseCodec`的类，实现了`MessageCodec`接口，用于对`ApiResponse`对象进行编码和解码。`encodeToWire`方法将`ApiResponse`对象转换为JSON格式并写入缓冲区，而`decodeFromWire`方法则从缓冲区中读取JSON字符串并还原为`ApiResponse`对象。此外，`transform`方法直接返回传入的`ApiResponse`对象，`name`方法返回类名，`systemCodecID`方法返回固定值-1。

### 字段列表 Field List

| 名称  | 类型  | 说明 |
|-------|-------|------|

### 方法列表 Method List

| 名称  | 类型  | 说明 |
|-------|-------|------|
| systemCodecID | byte | 重写方法，返回系统编解码器ID为-1。 |
| encodeToWire | void | 将API响应编码为JSON并写入缓冲区。 |
| decodeFromWire | ApiResponse | 解码缓冲区的JSON数据并构建ApiResponse对象。 |
| name | String | 重写name方法，返回当前类名。 |
| transform | ApiResponse | 重写transform方法，直接返回ApiResponse对象。 |




