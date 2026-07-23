登录功能：

### `@RestController`

这是 Spring 的注解。它的作用就一句话：**告诉 Spring"这个类是用来处理 HTTP 请求的"**。当你启动项目，Spring 会扫描到这个注解，然后把里面的方法自动映射成 HTTP 接口。

### `@RequestMapping("/admin/employee")`

给这个 Controller 下所有接口加一个**统一的前缀**。比如 `@PostMapping("/login")` 加上这个前缀，实际访问路径就是 `POST /admin/employee/login`。

### `@Slf4j`

这是 Lombok 提供的注解。它在编译时**自动给你生成一个 `log` 对象**，让你可以在代码里写 `log.info("xxx")` 打印日志，而不需要手动 new 一个日志对象。属于减少模板代码的语法糖。

### `@Autowired`

这个是 Spring 的核心机制 —— **依赖注入**。你不写 `new EmployeeService()`，而是声明 `@Autowired`，Spring 启动时会自动帮你把 `EmployeeService` 的实现类对象创建好并塞进来。意思就是说，@Autowired会直接帮你把对象new好。具体理解如图所示。

> **类比理解**：就像你去餐厅吃饭，你不用自己进厨房炒菜（new 对象），服务员（Spring）会把做好的菜端到你桌上（注入）。

![](C:\Users\29737\AppData\Roaming\marktext\images\2026-07-23-18-19-38-image.png)

## `@RequestBody EmployeeLoginDTO employeeLoginDTO`

前端发来的 JSON 数据是这样的：

JSON

```json
{
    "username": "admin",
    "password": "123456"
}
```

`@RequestBody` 做的就是：**自动把 JSON 转换成 Java 对象**。

对照 EmployeeLoginDTO：

Java

```java
public class EmployeeLoginDTO {
    private String username;   // JSON的 "username" → 存到这个字段
    private String password;   // JSON的 "password" → 存到这个字段
}
```

Spring 自动做了这件事：

Plain Text

```
JSON:  { "username": "admin", "password": "123456" }
                    ↓  @RequestBody 自动转换
Java:  一个 EmployeeLoginDTO 对象，username="admin", password="123456"
```

你不用自己解析 JSON，Spring 帮你把前端传过来的 JSON **自动装填**进了这个对象。

简单来说，@RequestBody的意思就是spring把前端传过来的JSON转换成Java对象，具体转成什么样，看EmployeeLoginDTO，转完之后赋给employeeLoginDTO。
