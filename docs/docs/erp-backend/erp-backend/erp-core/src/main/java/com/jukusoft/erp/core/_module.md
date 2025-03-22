# 基础信息

|      |      |
|------|------|
| 名称 | core |
| 编码语言 | .java |
| 代码路径 | erp-backend/erp-core/src/main/java/com/jukusoft/erp/core |
| 包名 | erp-backend.erp-core.src.main.java.com.jukusoft.erp.core |
| 概述说明 | ERP核心模块处理登录、权限、菜单、缓存和群组管理，提供加法API，确保系统安全、数据准确和用户体验优化。 |

# 说明

## 概述

该代码模块是一个企业资源规划（ERP）系统的核心模块，主要负责用户登录、权限管理、菜单管理、缓存管理、群组管理以及简单的加法运算等功能。模块通过多个控制器类处理不同的业务场景，确保系统的安全性、数据的准确性和用户体验的优化。`BaseModule`类继承自`AbstractModule`，在初始化过程中添加了多个仓库、设置了权限管理器，并注册了多个控制器，完成了模块的基本配置和功能集成。此外，`CalculatorModule`类实现了一个加法API，该API通过`/add_integer`路径接收参数，并返回这些参数的和，提供简洁的加法运算功能。

## 主要业务场景

1. **用户登录与身份验证**：
   - `LoginFormController`负责生成登录表单，处理用户输入的用户名和密码，提供用户与系统交互的界面。
   - `登录控制器`处理用户的登录、登出及登录状态检查，通过验证用户输入的用户名和密码来确认身份，并管理用户的会话状态，确保用户身份验证的安全性。

2. **权限管理**：
   - `PermissionController`提供`listPermissions`方法，用于获取用户的权限信息，确保权限控制的准确性和及时性。
   - `PermissionManagerImpl`类负责权限管理功能，其中已弃用的`hasPermission`方法不再推荐使用，建议开发者使用其他替代方案来进行权限验证。

3. **菜单管理**：
   - `MenuController`处理菜单列表的请求，首先进行权限验证，确保用户具备访问权限，然后筛选并返回符合条件的菜单项，确保菜单列表的安全性和准确性。

4. **缓存管理**：
   - `CacheController`负责提供清除缓存的功能，在执行清除操作之前进行权限验证，确保操作的安全性，并返回被清除缓存项的列表，有助于管理系统缓存，确保数据的及时更新和系统性能的优化。

5. **群组管理**：
   - `GroupController`处理用户群组列表及相关ID查询，返回详细的群组信息以及对应的ID数组，确保用户能够准确获取所需群组数据，便于后续操作和管理。

6. **加法运算**：
   - `CalculatorModule`类通过`/add_integer`路径接收整数参数，并返回这些参数的和，提供简洁的加法运算功能，方便用户获取计算结果。

7. **异常处理**：
   - `TestException`类用于表示测试过程中可能发生的异常情况，有助于提高代码的可维护性和可读性，使得异常处理更加明确和集中。

8. **引擎功能**：
   - `Engine`类作为一个公共类，可能包含与引擎相关的核心功能或数据，为进一步扩展和实现其功能提供了基础。


### 包内部结构视图

```mermaid
graph TD
    core --> Engine.java
    core --> module
    core --> permission
    core --> exception
    module --> calculator
    module --> base
    calculator --> CalculatorModule.java
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
    permission --> PermissionManagerImpl.java
    exception --> TestException.java
```

该流程图展示了ERP核心模块的层级结构，包括核心类、模块、权限管理和异常处理等部分。每个模块下包含多个服务或控制器，如登录表单、菜单、权限、缓存、组和登录等，每个服务或控制器都有对应的实现类。

# 文件列表 File List

| 名称   | 类型  | 说明 |
|-------|------|-------------|
| [Engine.java](Engine.md) | file | 定义了一个公共类Engine。 |
| [exception](exception/_module.md) | package | 定义公共类TestException。 |
| [permission](permission/_module.md) | package | PermissionManagerImpl类管理权限，hasPermission方法已弃用。 |
| [module](module/_module.md) | package | CalculatorModule实现加法API，ERP核心模块处理登录、权限、菜单、缓存和群组管理。 |


