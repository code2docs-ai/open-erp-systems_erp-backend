# 基础信息

|      |      |
|------|------|
| 名称 | com.jukusoft |
| 编码语言 | .java |
| 代码路径 | erp-backend/erp-library/src/main/java/com.jukusoft |
| 包名 | erp-backend.erp-library.src.main.java.com.jukusoft |
| 概述说明 | 该Java库用于ERP系统，处理JSON序列化、加载、数据交换和持久化，简化数据处理流程。 |

# 说明

## 概述
该代码模块是一个ERP（企业资源规划）系统的后端库，提供了多种功能以支持系统的核心业务操作。模块涵盖了JSON数据处理、日志记录、应用上下文管理、控制器逻辑、API请求与响应处理、模块管理、权限管理、缓存管理、异常处理、会话管理、工具类、数据库操作以及密钥库管理等功能。通过模块化的设计，该库为ERP系统提供了高效、可扩展且易于维护的基础架构，支持复杂的业务需求和系统集成。

## 主要业务场景
1. **JSON数据处理**：模块提供了JSON序列化和反序列化功能，支持Java对象与JSON格式之间的转换，便于数据交换和持久化。
2. **日志记录**：通过集成的日志服务，模块支持多种日志级别，确保系统运行信息的全面记录和监控。
3. **应用上下文管理**：模块通过`AppContext`接口及其实现类，统一管理Vertx、Hazelcast、数据库、缓存、权限等关键组件，确保系统资源的高效利用。
4. **控制器逻辑处理**：模块提供了控制器基类`AbstractController`，支持处理与Vertx框架相关的请求和响应逻辑，确保业务逻辑的正确执行。
5. **API请求与响应处理**：模块通过`ApiRequest`、`ApiResponse`等类，支持API请求的编码、解码、管理和响应封装，确保数据交换的完整性和安全性。
6. **模块管理**：模块通过`IModule`接口和`AbstractModule`抽象类，支持模块的集成、管理和初始化，提供统一的框架支持。
7. **权限管理**：模块通过`PermissionRequired`、`LoginRequired`等注解，支持权限控制、登录验证和日志注入，确保系统的安全性和合规性。
8. **缓存管理**：模块提供了多种缓存类型的实现，包括文件缓存、本地内存缓存和Hazelcast分布式缓存，支持高效的数据访问和资源管理。
9. **异常处理**：模块定义了一系列自定义异常类，用于处理服务、仓库、缓存缺失等情况，确保系统的健壮性和可维护性。
10. **会话管理**：模块利用Hazelcast技术实现分布式会话管理，支持用户会话的高效存储、检索和管理，确保会话数据的高可用性和一致性。
11. **工具类**：模块提供了多种实用工具类，支持哈希计算、JSON数据转换、文件操作等功能，简化开发流程并提高代码效率。
12. **数据库操作**：模块支持与MySQL和Hazelcast数据库的交互，提供数据库连接、仓库管理、事务处理等功能，确保数据的一致性和完整性。
13. **密钥库管理**：模块支持生成自签名X.509证书并将其保存为JKS格式的密钥库，适用于安全通信和数据加密。

通过这些功能，该模块为ERP系统提供了全面的支持，能够满足复杂的业务需求和高并发的系统场景。


### 包内部结构视图

```mermaid
graph TD
    erp --> lib
    lib --> json
    lib --> logger
    lib --> context
    lib --> controller
    lib --> message
    lib --> module
    lib --> service
    lib --> annotation
    lib --> route
    lib --> gateway
    lib --> permission
    lib --> cache
    lib --> logging
    lib --> exception
    lib --> session
    lib --> utils
    lib --> database
    lib --> keystore
    json --> JsonSerializable.java
    json --> JsonLoadable.java
    logger --> HzLogger.java
    context --> AppContext.java
    context --> AppContextImpl.java
    controller --> AbstractController.java
    controller --> IController.java
    message --> request
    message --> response
    message --> StatusCode.java
    request --> ApiRequestCodec.java
    request --> ApiRequest.java
    response --> ApiResponse.java
    response --> ApiResponseCodec.java
    module --> IModule.java
    module --> AbstractModule.java
    service --> IService.java
    service --> InjectService.java
    annotation --> PermissionRequired.java
    annotation --> LoginRequired.java
    annotation --> InjectLogger.java
    route --> RouteHandlerWithoutReturn.java
    route --> RouteHandler.java
    route --> Route.java
    gateway --> ApiGateway.java
    gateway --> ResponseHandler.java
    permission --> PermissionManager.java
    permission --> PermissionService.java
    permission --> PermissionStates.java
    cache --> InjectCache.java
    cache --> ICache.java
    cache --> impl
    cache --> CacheManager.java
    cache --> CacheTypes.java
    impl --> DefaultCacheManager.java
    impl --> FileSystemCache.java
    impl --> HazelcastCache.java
    impl --> LocalMemoryCache.java
    logging --> ILogging.java
    exception --> RequiredServiceNotFoundException.java
    exception --> HandlerException.java
    exception --> RequiredRepositoryNotFoundException.java
    exception --> CacheNotFoundException.java
    session --> SessionManager.java
    session --> Session.java
    session --> ChangeableSessionManager.java
    session --> impl
    impl --> HzMapSessionManager.java
    impl --> SessionIDGenerator.java
    impl --> HzJCacheSessionManager.java
    utils --> HashUtils.java
    utils --> JsonUtils.java
    utils --> FileUtils.java
    database --> HazelcastRepository.java
    database --> MySQLDatabase.java
    database --> Repository.java
    database --> InjectRepository.java
    database --> InjectAppContext.java
    database --> InjectDatabase.java
    database --> AbstractMySQLRepository.java
    database --> DatabaseManager.java
    database --> Database.java
    database --> impl
    impl --> DatabaseManagerImpl.java
    impl --> MySQLRepository.java
    keystore --> KeyStoreGenerator.java
```

该流程图展示了ERP库的模块化结构，涵盖了从基础功能（如日志、缓存、数据库）到高级功能（如权限管理、网关、路由）的各个组件。每个模块都进一步细分为具体的实现类，展示了系统的复杂性和模块之间的依赖关系。

# 文件列表 File List

| 名称   | 类型  | 说明 |
|-------|------|-------------|
| [erp](erp/_module.md) | package | 该Java库用于ERP系统，处理JSON序列化、加载、数据交换和持久化，简化数据处理流程。 |


