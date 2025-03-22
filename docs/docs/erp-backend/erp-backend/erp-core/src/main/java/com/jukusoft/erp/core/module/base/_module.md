# 基础信息

|      |      |
|------|------|
| 名称 | base |
| 编码语言 | .java |
| 代码路径 | erp-backend/erp-core/src/main/java/com/jukusoft/erp/core/module/base |
| 包名 | erp-backend.erp-core.src.main.java.com.jukusoft.erp.core.module.base |
| 概述说明 | ERP核心模块，含登录、权限、菜单、缓存、群组管理，确保安全、数据准确和用户体验优化。 |

# 说明

## 概述
该代码模块是一个企业资源规划（ERP）系统的核心模块，主要负责用户登录、权限管理、菜单管理、缓存管理和群组管理等功能。模块通过多个控制器类处理不同的业务场景，确保系统的安全性、数据的准确性和用户体验的优化。`BaseModule`类继承自`AbstractModule`，在初始化过程中添加了多个仓库、设置了权限管理器，并注册了多个控制器，完成了模块的基本配置和功能集成。

## 主要业务场景
1. **用户登录与身份验证**：
   - `LoginFormController`负责生成登录表单，处理用户输入的用户名和密码，提供用户与系统交互的界面。
   - `登录控制器`处理用户的登录、登出及登录状态检查，通过验证用户输入的用户名和密码来确认身份，并管理用户的会话状态，确保用户身份验证的安全性。

2. **权限管理**：
   - `PermissionController`提供`listPermissions`方法，用于获取用户的权限信息，确保权限控制的准确性和及时性。

3. **菜单管理**：
   - `MenuController`处理菜单列表的请求，首先进行权限验证，确保用户具备访问权限，然后筛选并返回符合条件的菜单项，确保菜单列表的安全性和准确性。

4. **缓存管理**：
   - `CacheController`负责提供清除缓存的功能，在执行清除操作之前进行权限验证，确保操作的安全性，并返回被清除缓存项的列表，有助于管理系统缓存，确保数据的及时更新和系统性能的优化。

5. **群组管理**：
   - `GroupController`处理用户群组列表及相关ID查询，返回详细的群组信息以及对应的ID数组，确保用户能够准确获取所需群组数据，便于后续操作和管理。


### 包内部结构视图

```mermaid
graph TD
    base --> BaseModule.java
    base --> service
    service --> loginform
    service --> menu
    service --> permission
    service --> cache
    service --> group
    service --> login
    loginform --> LoginFormController.java
    menu --> MenuController.java
    permission --> PermissionController.java
    cache --> CacheController.java
    group --> GroupController.java
    login --> LoginController.java
```

该流程图展示了`erp-core`模块中`base`目录下的层级结构。`base`目录包含`BaseModule.java`文件以及`service`子目录。`service`目录下进一步细分为多个子目录，如`loginform`、`menu`、`permission`等，每个子目录中分别包含对应的控制器文件，如`LoginFormController.java`、`MenuController.java`等。

# 文件列表 File List

| 名称   | 类型  | 说明 |
|-------|------|-------------|
| [BaseModule.java](BaseModule.md) | file | BaseModule继承AbstractModule，初始化时添加仓库、设置权限管理器并注册控制器。 |
| [service](service/_module.md) | package | LoginFormController处理登录表单，MenuController验证并返回菜单，PermissionController管理用户权限，CacheController清除缓存，GroupController处理群组信息，登录控制器管理用户会话。 |


