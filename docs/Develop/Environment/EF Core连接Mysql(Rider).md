# EF Core连接Mysql

## 1.方法

当使用Entity Framework Core（EF Core）连接数据库时，以下是一些关键要点：

### 数据库连接配置

1. **appsettings.json配置：** 在`appsettings.json`文件中配置数据库连接字符串，包括服务器地址、数据库名称、用户名和密码等信息。

   ```json
   {
     "ConnectionStrings": {
       "DefaultConnection":
         "Server=localhost;Database=mydatabase;User=myusername;Password=mypassword;"
     }
   }
   ```

2. **DbContext配置：** 创建`ApplicationDbContext`类，继承自`DbContext`，并在构造函数中使用`DbContextOptions`接受配置信息。

   ```csharp
   public class ApplicationDbContext : DbContext
   {
       public ApplicationDbContext(DbContextOptions<ApplicationDbContext> options)
           : base(options)
       {
       }
   
       public DbSet<User> Users { get; set; }
   }
   ```

### 模型定义

1. **实体类定义：** 创建实体类（如`User`），定义数据库表的结构。使用数据注解或Fluent API配置实体类与数据库表的映射关系。

   ```csharp
   public class User
   {
       public int Id { get; set; }
       public string Username { get; set; }
       public string Password { get; set; }
       // 其他属性...
   }
   ```

### 数据库迁移（可选）

1. **迁移命令：** 使用EF Core的CLI工具或Package Manager Console，运行命令生成迁移文件。

   ```
   dotnet ef migrations add InitialCreate
   ```

2. **数据库更新：** 运行迁移命令应用数据库更改。

   ```
   dotnet ef database update
   ```

### 数据库操作

1. **CRUD操作：** 在需要的地方使用`DbContext`进行数据库的增删改查操作。

   ```csharp
   var user = new User { Username = "example", Password = "password" };
   dbContext.Users.Add(user);
   dbContext.SaveChanges();
   ```

2. **查询操作：** 使用LINQ查询语法或方法链式调用进行数据查询。

   ```csharp
   var users = dbContext.Users.Where(u => u.Username == "example").ToList();
   ```

### 异常处理

1. **异常处理：** 在数据库操作时，要考虑异常处理，处理可能发生的数据库操作异常。

   ```csharp
   try
   {
       // 数据库操作
       dbContext.SaveChanges();
   }
   catch (Exception ex)
   {
       // 处理异常
   }
   ```





## 2.示例

下面是一个很简单的连接数据库的示例。

#### 准备工作

- 用rider创建web api框架。
- 安装MySql.EntityFrameworkCore
- 安装Mysql，创建库websystem，创建表 user，user信息如下：
  - ID (自增序列)：唯一标识每个用户的数字。    
  - Account：用户的账号信息。    
  - Pass：用户的密码信息（需要加密存储）。   
  -  Status（INT）：用户的状态，通常表示用户的账号状态，如正常、风险或待审核

#### 项目结构

为了让读者清楚每个文件在什么位置发挥作用，先展示部分项目结构。

```
├───Controllers
│   └───User
├───Properties
└───src
    └───MysqlModels
        ├───Data
        └───Models
```

以下是代码位于项目的位置：

1. `ApplicationDbContext` 类代码应该位于 `MysqlModels/Data` 文件夹中。这个类用于定义数据库上下文和表的映射关系。

   ```c#
   using Microsoft.EntityFrameworkCore;
   using Microsoft.Extensions.Configuration;
   using MysqlModels.Models;
   
   namespace MysqlModels.Data
   {
       public class ApplicationDbContext : DbContext
       {
           private readonly IConfiguration _configuration;
   
           public ApplicationDbContext(DbContextOptions<ApplicationDbContext> options, IConfiguration configuration)
               : base(options)
           {
               _configuration = configuration;
           }
   
           // DbSet 属性用于表示数据库中的表
           public DbSet<User> User { get; set; }
   
           protected override void OnConfiguring(DbContextOptionsBuilder optionsBuilder)
           {
               if (!optionsBuilder.IsConfigured)
               {
                   string connectionString = _configuration.GetConnectionString("DefaultConnection");
                   optionsBuilder.UseMySQL(connectionString);
               }
           }
       }
   }
   ```

2. 模型类，例如 `User` 类代码，应该位于 `MysqlModels/Models` 文件夹中。这些模型类用于映射数据库表的结构。

   ```c#
   namespace MysqlModels.Models
   {
       public class User
       {
           public int ID { get; set; }
           public string Account { get; set; }
           public string Pass { get; set; }
           public string Status { get; set; }
       }
   }
   ```

3. 控制器类，例如 `UserController` 类代码，应该位于 `Controllers/User` 文件夹中。这些控制器类用于处理 HTTP 请求和响应。

   ```c#
   using Microsoft.AspNetCore.Mvc;
   using MysqlModels.Data;
   using MysqlModels.Models;
   
   namespace YourNamespace.Controllers
   {
       [ApiController]
       [Route("api/[controller]")]
       public class UserController : ControllerBase
       {
           private readonly ApplicationDbContext _context;
   
           public UserController(ApplicationDbContext context)
           {
               _context = context;
           }
   
           [HttpGet]
           public IActionResult GetUsers()
           {
               var users = _context.User.ToList();
               return Ok(users);
           }
   
           // 其他操作...
       }
   }
   ```

4. 在 `Program.cs` 中，你应该配置依赖注入和应用程序的构建过程。这些配置代码应该位于启动文件的适当位置。

   ```c#
   // 添加配置
   builder.Configuration.AddJsonFile("appsettings.json", optional: false);
   // 添加数据库上下文
   builder.Services.AddDbContext<ApplicationDbContext>(options =>
   {
       options.UseMySQL(builder.Configuration.GetConnectionString("DefaultConnection"));
   });
   ```

5. 配置文件 `appsettings.json` 应该位于你的项目根目录下，用于存储数据库连接字符串等配置信息。

   ```json
   {
     "Logging": {
       "LogLevel": {
         "Default": "Information",
         "Microsoft.AspNetCore": "Warning"
       }
     },
     "AllowedHosts": "*",
   
     "ConnectionStrings": {
       "DefaultConnection": "Server=localhost;Port=3306;Database=<databasename>;User=<name>;Password=<password>;"
     }
   }
   
   ```

   

