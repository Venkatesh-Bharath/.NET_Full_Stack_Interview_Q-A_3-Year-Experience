## JavaScript and Promises

1. **What are the different data types in JavaScript?**
   - **Answer:**
     JavaScript has seven primitive data types:
       - `undefined`
       - `null`
       - `boolean`
       - `number`
       - `string`
       - `bigint`
       - `symbol`
     And one complex data type:
       - `object`

2. **What is the difference between `null` and `undefined`?**
   - **Answer:**
     `undefined` means a variable has been declared but not yet assigned a value. `null` is an assignment value that represents no value.

3. **What does `"use strict"` do in JavaScript?**
   - **Answer:**
     `"use strict"` is a directive that enforces stricter parsing and error handling in your JavaScript code, preventing the use of undeclared variables and other common JavaScript pitfalls.

4. **What is the difference between `==` and `===` in JavaScript?**
   - **Answer:**
     `==` checks for value equality, performing type conversion if necessary. `===` checks for both value and type equality.

5. **What is a closure in JavaScript?**
   - **Answer:**
     A closure is a function that retains access to its lexical scope, even when the function is executed outside that scope.

     ```javascript
     function outerFunction() {
       let outerVariable = 'I am outside!';
       
       function innerFunction() {
         console.log(outerVariable); // Accesses the outer scope
       }
       
       return innerFunction;
     }

     const closure = outerFunction();
     closure(); // Outputs: I am outside!
     ```

6. **What are the states in a promise?**
   - **Answer:**
     A promise can be in one of three states:
       - **Pending:** Initial state, neither fulfilled nor rejected.
       - **Fulfilled:** The operation completed successfully.
       - **Rejected:** The operation failed.

     ```javascript
     const promise = new Promise((resolve, reject) => {
       let success = true; // Simulating a condition
       
       if (success) {
         resolve('Operation was successful!');
       } else {
         reject('Operation failed!');
       }
     });

     promise
       .then(result => console.log(result))
       .catch(error => console.error(error));
     ```

## Entity Framework

1. **What is `Include` and `ThenInclude` in Entity Framework?**
   - **Answer:**
     `Include` is used for eager loading of related entities. `ThenInclude` is used to specify additional levels of eager loading after the initial `Include`.

     ```csharp
     var order = context.Orders
                        .Include(o => o.Customer)
                        .ThenInclude(c => c.Address)
                        .FirstOrDefault(o => o.OrderId == orderId);
     ```

2. **What is the difference between `First` and `FirstOrDefault`?**
   - **Answer:**
     `First` throws an exception if no elements are found. `FirstOrDefault` returns the default value (`null` for reference types) if no elements are found.

3. **What are the approaches in Entity Framework?**
   - **Answer:**
     - **Code-First:** The model is created through code classes, and the database is generated from these classes.
     - **Database-First:** The model is created from an existing database.
     - **Model-First:** The model is created through a designer, and the database and classes are generated from the model.

4. **How do you handle many-to-many relationships in Entity Framework code-first?**
   - **Answer:**
     Define the relationship using a junction table (entity) that contains the foreign keys of the two related entities.

     ```csharp
     public class Student
     {
         public int StudentId { get; set; }
         public string Name { get; set; }
         public ICollection<StudentCourse> StudentCourses { get; set; }
     }

     public class Course
     {
         public int CourseId { get; set; }
         public string Title { get; set; }
         public ICollection<StudentCourse> StudentCourses { get; set; }
     }

     public class StudentCourse
     {
         public int StudentId { get; set; }
         public Student Student { get; set; }
         public int CourseId { get; set; }
         public Course Course { get; set; }
     }
     ```

5. **What is the difference between `IQueryable` and `IEnumerable`?**
   - **Answer:**
     - `IQueryable` allows for querying against a data source where the query is translated to the data source's query language (e.g., SQL).
     - `IEnumerable` is used for in-memory collections and does not support further query composition.

6. **What are `AddSingleton`, `AddScoped`, and `AddTransient` in ASP.NET Core?**
   - **Answer:**
     - **AddSingleton:** Creates a single instance throughout the application's lifetime.
     - **AddScoped:** Creates a new instance per request.
     - **AddTransient:** Creates a new instance every time it is requested.

7. **What is the difference between `Configure` and `Configuration` in ASP.NET Core?**
   - **Answer:**
     - `Configure` is used to set up the application's request pipeline.
     - `Configuration` is used to access the application's configuration settings.

8. **What are middlewares in ASP.NET Core?**
   - **Answer:**
     Middleware are components that form the request pipeline in ASP.NET Core, handling requests and responses.

     ```csharp
      var builder = WebApplication.CreateBuilder(args);

      // Add services to the container.
      builder.Services.AddControllers();

      var app = builder.Build();

      // Configure the HTTP request pipeline.
      app.Use(async (context, next) =>
      {
        // Do work before the next middleware
       await next.Invoke();
        // Do work after the next middleware
      });

      app.UseRouting();

      app.UseEndpoints(endpoints =>
        {
        endpoints.MapControllers();
        });
      app.Run();

     ```

## Object-Oriented Programming (OOP)

1. **What is object-oriented programming (OOP)?**
   - **Answer:**
     OOP is a programming paradigm based on the concept of "objects", which can contain data and code: data in the form of fields (properties or attributes), and code in the form of procedures (methods).

## SQL and Database

1. **What is a stored procedure?**
   - **Answer:**
     A stored procedure is a precompiled collection of one or more SQL statements stored in the database, which can be executed as needed.

2. **What is an index in a database?**
   - **Answer:**
     An index is a database object that improves the speed of data retrieval operations on a table at the cost of slower data modifications (inserts, updates, deletes).

3. **What are triggers in a database?**
   - **Answer:**
     Triggers are database objects that automatically execute a specified set of actions in response to certain events on a particular table or view.

4. **Write a query to find the second highest salary.**
   - **Answer:**
     ```sql
     SELECT MAX(salary) AS SecondHighestSalary
     FROM employees
     WHERE salary < (SELECT MAX(salary) FROM employees);
     ```

## ASP.NET Core and Related Concepts

1. **How do you create a registration service layer in ASP.NET Core Web API?**
  - To create a registration service layer in ASP.NET Core Web API, follow these steps:
**User.cs** (Entity Model)
```csharp
public class User
{
    public int Id { get; set; }
    public string Username { get; set; }
    public string PasswordHash { get; set; }
    public string Email { get; set; }
}
```

**UserDto.cs** (Data Transfer Object)
```csharp
public class UserDto
{
    public string Username { get; set; }
    public string Password { get; set; }
    public string Email { get; set; }
}
```

### 2. **Create the User Service Interface**

**IUserService.cs**
```csharp
public interface IUserService
{
    Task<RegistrationResult> RegisterUserAsync(UserDto userDto);
}
```

### 3. **Create the User Service Implementation**

**UserService.cs**
```csharp
public class UserService : IUserService
{
    private readonly ApplicationDbContext _context;
    private readonly IPasswordHasher<User> _passwordHasher;

    public UserService(ApplicationDbContext context, IPasswordHasher<User> passwordHasher)
    {
        _context = context;
        _passwordHasher = passwordHasher;
    }

    public async Task<RegistrationResult> RegisterUserAsync(UserDto userDto)
    {
        var existingUser = await _context.Users
                                         .AnyAsync(u => u.Username == userDto.Username || u.Email == userDto.Email);

        if (existingUser)
        {
            return new RegistrationResult { Success = false, Message = "Username or email already in use." };
        }

        var user = new User
        {
            Username = userDto.Username,
            Email = userDto.Email,
            PasswordHash = _passwordHasher.HashPassword(null, userDto.Password)
        };

        _context.Users.Add(user);
        await _context.SaveChangesAsync();

        return new RegistrationResult { Success = true, Message = "User registered successfully." };
    }
}
```

**RegistrationResult.cs** (Result Model)
```csharp
public class RegistrationResult
{
    public bool Success { get; set; }
    public string Message { get; set; }
}
```

### 4. **Register the Service in Dependency Injection**

**Program.cs**
```csharp
var builder = WebApplication.CreateBuilder(args);

// Add services to the container.
builder.Services.AddControllers();
builder.Services.AddDbContext<ApplicationDbContext>(options =>
    options.UseSqlServer(builder.Configuration.GetConnectionString("DefaultConnection")));
builder.Services.AddTransient<IUserService, UserService>();
builder.Services.AddScoped<IPasswordHasher<User>, PasswordHasher<User>>();

var app = builder.Build();

// Configure the HTTP request pipeline.
app.UseRouting();
app.UseEndpoints(endpoints =>
{
    endpoints.MapControllers();
});

app.Run();
```

### 5. **Create the API Controller**

**RegistrationController.cs**
```csharp
[ApiController]
[Route("api/[controller]")]
public class RegistrationController : ControllerBase
{
    private readonly IUserService _userService;

    public RegistrationController(IUserService userService)
    {
        _userService = userService;
    }

    [HttpPost]
    public async Task<IActionResult> Register(UserDto userDto)
    {
        var result = await _userService.RegisterUserAsync(userDto);
        if (result.Success)
        {
            return Ok(result);
        }
        return BadRequest(result.Message);
    }
}
```

2. **What is `DbContext` and `DbSet` in Entity Framework?**
   - **Answer:**
     - `DbContext` is the primary class responsible for interacting with the database.
     - `DbSet` represents a collection of entities that can be queried from the database.

     ```csharp
     public class ApplicationDbContext : DbContext
     {
         public DbSet<User> Users { get; set; }
         public DbSet<Order> Orders { get; set; }
     }
     ```

3. **What is SignalR?**
   - **Answer:**
     SignalR is a library for ASP.NET Core that enables real-time web functionality, allowing server-side code to push content to connected clients instantly.

4. **What is dependency injection in ASP.NET Core?**
   - **Answer:**
     Dependency injection is a design pattern used to achieve Inversion of Control (IoC) between classes and their dependencies. ASP.NET Core provides built-in support for dependency injection.

     ```csharp
     public void ConfigureServices(IServiceCollection services)
     {
         services.AddTransient<IMyService, MyService>();
     }
     ```

## Git

1. **What is Git-stash?**
   - **Answer:**
     `git stash` temporarily shelves (or stashes) changes you've made to your working directory so you can work on something else and then come back and re-apply them later.

     ```bash
     git stash
     git stash pop
     ```

## Jira

1. **What is Jira and what is it used for?**
   - **Answer:**
     Jira is a project management and issue tracking

 tool developed by Atlassian. It is used for tracking bugs, issues, and project management tasks in software development.

## Synchronous and Asynchronous

1. **What is synchronous programming?**
   - **Answer:**
     Synchronous programming executes tasks sequentially, where each task must complete before the next one begins.

2. **What is asynchronous programming?**
   - **Answer:**
     Asynchronous programming allows tasks to be executed independently of the main program flow, enabling concurrent operations without blocking the main thread.

     ```javascript
     async function fetchData() {
       let response = await fetch('https://api.example.com/data');
       let data = await response.json();
       console.log(data);
     }
     fetchData();
     ```
