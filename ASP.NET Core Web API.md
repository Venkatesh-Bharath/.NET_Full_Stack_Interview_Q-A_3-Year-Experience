## General ASP.NET Core Questions (.NET 6+)

1. **What is ASP.NET Core, and how does it differ from ASP.NET?**
   - ASP.NET Core is a cross-platform, high-performance framework for building modern, cloud-based applications. Unlike ASP.NET, which was primarily designed for Windows, ASP.NET Core supports cross-platform development on Windows, Linux, and macOS. It is built to be more modular, flexible, and lightweight.

2. **Explain the middleware pipeline in ASP.NET Core.**
   - The middleware pipeline in ASP.NET Core is a sequence of middleware components that handle HTTP requests and responses. Each middleware can perform tasks like logging, authentication, or response modification. Middleware components are added to the pipeline in the `Program.cs` file using the `Use` methods of the `IApplicationBuilder`.

    ```csharp
    var builder = WebApplication.CreateBuilder(args);
    var app = builder.Build();

    app.Use(async (context, next) =>
    {
        // Custom logic before the next middleware
        await next();
        // Custom logic after the next middleware
    });

    app.UseRouting();
    app.UseEndpoints(endpoints =>
    {
        endpoints.MapControllers();
    });

    app.Run();
    ```

3. **What are some advantages of using ASP.NET Core?**
   - **Cross-Platform:** Can run on Windows, Linux, and macOS.
   - **Performance:** Offers improved performance and scalability over ASP.NET.
   - **Modular Design:** Allows inclusion of only required components.
   - **Unified Framework:** Combines MVC and Web API into a single framework.
   - **Dependency Injection:** Built-in support for dependency injection.
   - **Open Source:** Community-driven with active support.

4. **Describe the startup class and its role in an ASP.NET Core application.**
   - In .NET 6+, the `Startup` class is replaced by the `Program.cs` file, which combines the roles of configuration and middleware setup. The `Program.cs` file sets up services and middleware in a simplified and more streamlined way.

    ```csharp
    var builder = WebApplication.CreateBuilder(args);

    // Configure services
    builder.Services.AddControllers();

    var app = builder.Build();

    // Configure middleware
    if (app.Environment.IsDevelopment())
    {
        app.UseDeveloperExceptionPage();
    }
    else
    {
        app.UseExceptionHandler("/Home/Error");
        app.UseHsts();
    }

    app.UseHttpsRedirection();
    app.UseStaticFiles();
    app.UseRouting();
    app.UseAuthorization();

    app.MapControllers();

    app.Run();
    ```

5. **How do you configure services in ASP.NET Core?**
   - In .NET 6+, services are configured in the `Program.cs` file using the `CreateBuilder` method. You register services with the `IServiceCollection` through the `builder.Services` property.

    ```csharp
    var builder = WebApplication.CreateBuilder(args);

    // Register services
    builder.Services.AddControllers();
    builder.Services.AddScoped<IMyService, MyService>();

    var app = builder.Build();
    ```

6. **What are dependency injection and its benefits in ASP.NET Core?**
   - Dependency Injection (DI) is a design pattern used to manage dependencies in an application. In ASP.NET Core, DI is built into the framework, allowing for better separation of concerns, easier testing, and more maintainable code. Dependencies are injected into constructors, methods, or properties.

    ```csharp
    public class MyController : ControllerBase
    {
        private readonly IMyService _myService;

        public MyController(IMyService myService)
        {
            _myService = myService;
        }

        // Action methods using _myService
    }
    ```

7. **Explain the concept of routing in ASP.NET Core.**
   - Routing in ASP.NET Core is the process of mapping incoming HTTP requests to the appropriate controller actions. It is configured in the `Program.cs` file using the `UseRouting` and `MapControllers` methods.

    ```csharp
    var builder = WebApplication.CreateBuilder(args);

    var app = builder.Build();

    app.UseRouting();

    app.UseEndpoints(endpoints =>
    {
        endpoints.MapControllers();
    });

    app.Run();
    ```

8. **How do you define a custom middleware in ASP.NET Core?**
   - Custom middleware is defined as a delegate that takes `HttpContext` and `RequestDelegate` as parameters. It is added to the pipeline using the `Use` method.

    ```csharp
    var builder = WebApplication.CreateBuilder(args);
    var app = builder.Build();

    app.Use(async (context, next) =>
    {
        // Custom logic
        await next();
    });

    app.UseRouting();
    app.UseEndpoints(endpoints =>
    {
        endpoints.MapControllers();
    });

    app.Run();
    ```

9. **What are tag helpers in ASP.NET Core?**
   - Tag Helpers are server-side components in ASP.NET Core that enable you to create HTML elements and attributes in a more readable and maintainable way. They are used in Razor views to simplify HTML generation.

    ```html
    <form asp-controller="Home" asp-action="Submit">
        <input asp-for="Name" />
        <button type="submit">Submit</button>
    </form>
    ```

10. **What is the purpose of the IApplicationBuilder interface?**
    - The `IApplicationBuilder` interface is used to configure the middleware pipeline in ASP.NET Core. It provides methods to add middleware components to the request processing pipeline.

    ```csharp
    var builder = WebApplication.CreateBuilder(args);
    var app = builder.Build();

    app.Use(async (context, next) =>
    {
        // Custom middleware logic
        await next();
    });

    app.UseRouting();
    app.UseEndpoints(endpoints =>
    {
        endpoints.MapControllers();
    });

    app.Run();
    ```
## ASP.NET Core Web API Specific Questions

11. **What is a Web API, and how is it different from a Web Application?**
   - A Web API (Application Programming Interface) is a service that exposes data and functionality over HTTP for use by other applications or clients. It typically returns data in formats such as JSON or XML. In contrast, a Web Application provides a user interface and is primarily focused on presenting content to end-users through a browser. Web APIs are used for building RESTful services and are often consumed by client-side applications or other servers.

12. **Explain how to create a simple ASP.NET Core Web API.**
   - To create a simple ASP.NET Core Web API in .NET 6+, follow these steps:

    1. **Create the Project:**
       ```bash
       dotnet new webapi -n MyApi
       ```

    2. **Define a Model:**
       ```csharp
       public class TodoItem
       {
           public int Id { get; set; }
           public string Name { get; set; }
           public bool IsComplete { get; set; }
       }
       ```

    3. **Create a Controller:**
       ```csharp
       [ApiController]
       [Route("api/[controller]")]
       public class TodoController : ControllerBase
       {
           private static readonly List<TodoItem> Todos = new List<TodoItem>
           {
               new TodoItem { Id = 1, Name = "Sample Todo", IsComplete = false }
           };

           [HttpGet]
           public ActionResult<IEnumerable<TodoItem>> GetTodos()
           {
               return Ok(Todos);
           }

           [HttpGet("{id}")]
           public ActionResult<TodoItem> GetTodoById(int id)
           {
               var todo = Todos.FirstOrDefault(t => t.Id == id);
               if (todo == null) return NotFound();
               return Ok(todo);
           }

           [HttpPost]
           public ActionResult CreateTodo(TodoItem todo)
           {
               Todos.Add(todo);
               return CreatedAtAction(nameof(GetTodoById), new { id = todo.Id }, todo);
           }
       }
       ```

    4. **Run the Application:**
       ```bash
       dotnet run
       ```

13. **What are the HTTP methods supported by ASP.NET Core Web API?**
   - ASP.NET Core Web API supports standard HTTP methods such as:
     - **GET:** Retrieve data from the server.
     - **POST:** Submit data to be processed by the server.
     - **PUT:** Update existing data on the server.
     - **DELETE:** Remove data from the server.
     - **PATCH:** Partially update data on the server.
     - **OPTIONS:** Describe the communication options for the target resource.

14. **How do you implement CRUD operations in ASP.NET Core Web API?**
   - CRUD operations can be implemented by defining appropriate endpoints in a controller:

    ```csharp
    [ApiController]
    [Route("api/[controller]")]
    public class ItemsController : ControllerBase
    {
        private readonly List<Item> _items = new List<Item>();

        [HttpGet]
        public ActionResult<IEnumerable<Item>> GetItems()
        {
            return Ok(_items);
        }

        [HttpGet("{id}")]
        public ActionResult<Item> GetItem(int id)
        {
            var item = _items.FirstOrDefault(i => i.Id == id);
            if (item == null) return NotFound();
            return Ok(item);
        }

        [HttpPost]
        public ActionResult<Item> CreateItem(Item item)
        {
            _items.Add(item);
            return CreatedAtAction(nameof(GetItem), new { id = item.Id }, item);
        }

        [HttpPut("{id}")]
        public IActionResult UpdateItem(int id, Item updatedItem)
        {
            var item = _items.FirstOrDefault(i => i.Id == id);
            if (item == null) return NotFound();
            item.Name = updatedItem.Name;
            item.Description = updatedItem.Description;
            return NoContent();
        }

        [HttpDelete("{id}")]
        public IActionResult DeleteItem(int id)
        {
            var item = _items.FirstOrDefault(i => i.Id == id);
            if (item == null) return NotFound();
            _items.Remove(item);
            return NoContent();
        }
    }
    ```

15. **What is model binding in ASP.NET Core Web API?**
   - Model binding is the process of mapping data from HTTP requests (such as query strings, form data, route data, or request bodies) to .NET objects. ASP.NET Core uses model binding to automatically populate action method parameters based on the incoming request data.

16. **Explain the concept of attribute routing in ASP.NET Core Web API.**
   - Attribute routing allows you to define routes using attributes directly on controller actions. This gives you more control over the URL structure and mapping. 

    ```csharp
    [ApiController]
    [Route("api/[controller]")]
    public class ProductsController : ControllerBase
    {
        [HttpGet("category/{categoryId}")]
        public ActionResult<IEnumerable<Product>> GetByCategory(int categoryId)
        {
            // Logic to get products by category
        }
    }
    ```

17. **How do you handle exceptions in an ASP.NET Core Web API?**
   - You can handle exceptions using middleware or by implementing exception filters. A common approach is to use the built-in exception handling middleware:

    ```csharp
    var builder = WebApplication.CreateBuilder(args);

    var app = builder.Build();

    app.UseExceptionHandler("/error");
    app.UseHsts();

    app.Map("/error", (HttpContext context) =>
    {
        context.Response.ContentType = "application/json";
        return context.Response.WriteAsync(new
        {
            StatusCode = context.Response.StatusCode,
            Message = "An error occurred."
        }.ToString());
    });

    app.Run();
    ```

18. **What is CORS, and how do you enable it in an ASP.NET Core Web API?**
   - CORS (Cross-Origin Resource Sharing) is a security feature that allows or restricts resources on a web server to be requested from another domain. You enable CORS in ASP.NET Core by configuring it in the `Program.cs` file.

    ```csharp
    var builder = WebApplication.CreateBuilder(args);

    builder.Services.AddCors(options =>
    {
        options.AddDefaultPolicy(policy =>
        {
            policy.WithOrigins("https://example.com")
                  .AllowAnyHeader()
                  .AllowAnyMethod();
        });
    });

    var app = builder.Build();

    app.UseCors();

    app.Run();
    ```

19. **How can you secure an ASP.NET Core Web API?**
   - You can secure an ASP.NET Core Web API using various techniques:
     - **Authentication:** Use JWT, OAuth, or Identity to authenticate users.
     - **Authorization:** Implement role-based or policy-based access control.
     - **HTTPS:** Enforce HTTPS to secure data in transit.
     - **CORS:** Configure CORS to restrict which domains can access your API.

    ```csharp
    builder.Services.AddAuthentication(JwtBearerDefaults.AuthenticationScheme)
        .AddJwtBearer(options =>
        {
            options.TokenValidationParameters = new TokenValidationParameters
            {
                ValidateIssuer = true,
                ValidateAudience = true,
                ValidateLifetime = true,
                ValidateIssuerSigningKey = true,
                ValidIssuer = "yourIssuer",
                ValidAudience = "yourAudience",
                IssuerSigningKey = new SymmetricSecurityKey(Encoding.UTF8.GetBytes("yourSecret"))
            };
        });

    builder.Services.AddAuthorization();

    var app = builder.Build();

    app.UseAuthentication();
    app.UseAuthorization();
    ```

20. **Explain the concept of versioning in ASP.NET Core Web API.**
    - API versioning allows you to manage and support multiple versions of your API simultaneously. You can implement versioning using query string parameters, URL segments, or custom headers.

    ```csharp
    builder.Services.AddApiVersioning(options =>
    {
        options.AssumeDefaultVersionWhenUnspecified = true;
        options.DefaultApiVersion = new ApiVersion(1, 0);
        options.ReportApiVersions = true;
    });

    [ApiVersion("1.0")]
    [Route("api/v{version:apiVersion}/products")]
    public class ProductsV1Controller : ControllerBase
    {
        // Version 1 implementation
    }

    [ApiVersion("2.0")]
    [Route("api/v{version:apiVersion}/products")]
    public class ProductsV2Controller : ControllerBase
    {
        // Version 2 implementation
    }
    ```

## Entity Framework Core Questions

21. **What is Entity Framework Core?**
   - Entity Framework Core (EF Core) is an open-source, cross-platform ORM (Object-Relational Mapper) that enables .NET developers to work with relational databases using .NET objects. It simplifies data access by allowing developers to interact with a database using C# code instead of SQL.

22. **Explain Code-First, Database-First, and Model-First approaches in EF Core.**
   - **Code-First:** Start with defining your model classes in code, and EF Core generates the database schema based on these classes.
   - **Database-First:** Start with an existing database, and EF Core generates the model classes and context based on the existing schema.
   - **Model-First:** Design the model using a designer or a visual tool, and EF Core generates the database schema and context based on the model.

    ```bash
    # Code-First migration
    dotnet ef migrations add InitialCreate
    dotnet ef database update
    ```

23. **How do you configure a DbContext in EF Core?**
   - Configure `DbContext` by overriding the `OnConfiguring` method or by using the `DbContext` options in the `Program.cs` file.

    ```csharp
    public class MyDbContext : DbContext
    {
        public DbSet<Product> Products { get; set; }

        protected override void OnConfiguring(DbContextOptionsBuilder optionsBuilder)
        {
            optionsBuilder.UseSqlServer("YourConnectionString");
        }
    }
    ```

    ```csharp
    var builder = WebApplication.CreateBuilder(args);

    builder.Services.AddDbContext<MyDbContext>(options =>
        options.UseSqlServer(builder.Configuration.GetConnectionString("DefaultConnection")));
    ```

24. **What are migrations in EF Core, and how do you use them?**
   - Migrations are a way to update the database schema to reflect changes made in the model classes. You create and apply migrations using the Entity Framework Core CLI tools.

    ```bash
    # Create a new migration
    dotnet ef migrations add MigrationName

    # Apply migrations to the database
    dotnet ef database update
    ```

25. **How do you handle relationships (one-to-many, many-to-many) in EF Core?**
   - **One-to-Many:** Define a navigation property in the dependent entity and use foreign key annotations or fluent API.

    ```csharp
    public class Author
    {
        public int AuthorId { get; set; }
        public string Name { get; set; }
        public ICollection<Book> Books { get; set; }
    }

    public class Book
    {
        public int BookId { get; set; }
        public string Title { get; set; }
        public int AuthorId { get; set; }
        public Author Author { get; set; }
    }
    ```

   - **Many-to-Many:** Use a junction table to represent the relationship.

    ```csharp
    public class Student
    {
        public int StudentId { get; set; }
        public string Name { get; set; }
        public ICollection<Course> Courses { get; set; }
    }

    public class Course
    {
        public int CourseId { get; set; }
        public string Title { get; set; }
        public ICollection<Student> Students { get; set; }
    }
    ```

26. **Explain lazy loading, eager loading, and explicit loading in EF Core.**
   - **Lazy Loading:** Automatically loads related entities when they are accessed for the first time. Requires virtual navigation properties and a proxy provider.

    ```csharp
    var author = dbContext.Authors.FirstOrDefault();
    var books = author.Books; // Books are loaded here
    ```

   - **Eager Loading:** Loads related entities as part of the initial query using `Include`.

    ```csharp
    var authors = dbContext.Authors.Include(a => a.Books).ToList();
    ```

   - **Explicit Loading:** Loads related entities on demand using the `Load` method.

    ```csharp
    var author = dbContext.Authors.FirstOrDefault();
    dbContext.Entry(author).Collection(a => a.Books).Load();
    ```

27. **How do you seed data in EF Core?**
   - Seed data by overriding the `OnModelCreating` method in the `DbContext` class.

    ```csharp
    public class MyDbContext : DbContext
    {
        public DbSet<Product> Products { get; set; }

        protected override void OnModelCreating(ModelBuilder modelBuilder)
        {
            modelBuilder.Entity<Product>().HasData(
                new Product { ProductId = 1, Name = "Product1", Price = 10.0 },
                new Product { ProductId = 2, Name = "Product2", Price = 20.0 }
            );
        }
    }
    ```

28. **What is the purpose of the DbSet class?**
   - `DbSet` represents a collection of entities in the database. It provides methods for querying and saving instances of the entity type. Each `DbSet` corresponds to a table in the database.

    ```csharp
    public class MyDbContext : DbContext
    {
        public DbSet<Product> Products { get; set; }
    }
    ```

29. **Explain the concept of change tracking in EF Core.**
   - Change tracking is the process of monitoring changes made to entities in the `DbContext`. EF Core tracks these changes to determine what needs to be updated in the database when `SaveChanges` is called.

    ```csharp
    var product = dbContext.Products.First();
    product.Price = 15.0; // EF Core tracks this change
    dbContext.SaveChanges(); // Updates the database with the new price
    ```

30. **How do you execute raw SQL queries in EF Core?**
    - Execute raw SQL queries using `FromSqlRaw` or `ExecuteSqlRaw` methods.

    ```csharp
    // Query with raw SQL
    var products = dbContext.Products
        .FromSqlRaw("SELECT * FROM Products WHERE Price > {0}", 10)
        .ToList();

    // Execute raw SQL
    dbContext.Database.ExecuteSqlRaw("UPDATE Products SET Price = Price + 5 WHERE ProductId = {0}", 1);
    ```
