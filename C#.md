## Basic C# Questions

1. **What is C# and what are its main features?**
   - C# is a modern, object-oriented programming language developed by Microsoft as part of the .NET initiative. It is used for developing a wide range of applications, from web to mobile to desktop.
   - **Main features**: 
     - Object-oriented
     - Strongly typed
     - Component-oriented
     - Managed code with garbage collection
     - Rich standard library
     - Supports modern programming concepts like LINQ, async/await, and more.

2. **Explain the difference between a class and an object.**
   - A **class** is a blueprint for creating objects. It defines properties and methods.
   - An **object** is an instance of a class. It represents a specific entity that can hold data and perform actions defined by the class.

   ```csharp
   public class Car
   {
       public string Make { get; set; }
       public string Model { get; set; }
       
       public void Drive()
       {
           Console.WriteLine("Driving");
       }
   }

   // Creating an object
   Car myCar = new Car();
   myCar.Make = "Toyota";
   myCar.Model = "Corolla";
   myCar.Drive();
   ```

3. **What is inheritance in C#?**
   - Inheritance allows a class to inherit properties and methods from another class. It promotes code reuse.
   - Example:

   ```csharp
   public class Animal
   {
       public void Eat()
       {
           Console.WriteLine("Eating");
       }
   }

   public class Dog : Animal
   {
       public void Bark()
       {
           Console.WriteLine("Barking");
       }
   }

   Dog dog = new Dog();
   dog.Eat(); // Inherited from Animal
   dog.Bark(); // Defined in Dog
   ```

4. **Define polymorphism and provide an example.**
   - Polymorphism allows methods to do different things based on the object they are acting upon. It can be achieved through method overriding or interfaces.
   - Example:

   ```csharp
   public class Animal
   {
       public virtual void MakeSound()
       {
           Console.WriteLine("Animal sound");
       }
   }

   public class Dog : Animal
   {
       public override void MakeSound()
       {
           Console.WriteLine("Bark");
       }
   }

   public class Cat : Animal
   {
       public override void MakeSound()
       {
           Console.WriteLine("Meow");
       }
   }

   Animal myAnimal = new Dog();
   myAnimal.MakeSound(); // Output: Bark
   ```

5. **What is encapsulation in C#?**
   - Encapsulation is the concept of wrapping data (fields) and methods (functions) together as a single unit (class). It also restricts access to some of the object's components.
   - Example:

   ```csharp
   public class Person
   {
       private string name;

       public string Name
       {
           get { return name; }
           set { name = value; }
       }
   }

   Person person = new Person();
   person.Name = "John"; // Accessing private field via public property
   ```

6. **Explain the concept of interfaces in C#.**
   - An interface defines a contract that a class can implement. It can include methods, properties, events, and indexers without implementation.
   - Example:

   ```csharp
   public interface IAnimal
   {
       void MakeSound();
   }

   public class Dog : IAnimal
   {
       public void MakeSound()
       {
           Console.WriteLine("Bark");
       }
   }

   IAnimal myDog = new Dog();
   myDog.MakeSound(); // Output: Bark
   ```

7. **What is the difference between an interface and an abstract class?**
   - **Interface**:
     - Cannot have implementations for any members.
     - A class can implement multiple interfaces.
   - **Abstract class**:
     - Can have implementations for some members.
     - A class can inherit only one abstract class.

   ```csharp
   public interface IAnimal
   {
       void MakeSound();
   }

   public abstract class Animal
   {
       public abstract void MakeSound();
       public void Sleep() => Console.WriteLine("Sleeping");
   }

   public class Dog : Animal, IAnimal
   {
       public override void MakeSound()
       {
           Console.WriteLine("Bark");
       }
   }
   ```

8. **Explain the use of the `static` keyword in C#.**
   - The `static` keyword denotes that a member belongs to the type itself rather than to a specific object. It can be applied to variables, methods, properties, constructors, and classes.
   - Example:

   ```csharp
   public class MathHelper
   {
       public static int Add(int a, int b)
       {
           return a + b;
       }
   }

   int result = MathHelper.Add(3, 5); // Static method call
   ```

9. **What are properties in C# and how are they used?**
   - Properties are members that provide a flexible mechanism to read, write, or compute the value of a private field. They use accessors `get` and `set`.
   - Example:

   ```csharp
   public class Person
   {
       private string name;

       public string Name
       {
           get { return name; }
           set { name = value; }
       }
   }

   Person person = new Person();
   person.Name = "John"; // Using property
   Console.WriteLine(person.Name);
   ```

10. **What is a constructor in C#?**
    - A constructor is a special method of a class that initializes objects. It has the same name as the class and does not have a return type.
    - Example:

    ```csharp
    public class Person
    {
        public string Name { get; set; }

        public Person(string name)
        {
            Name = name;
        }
    }

    Person person = new Person("John");
    ```

11. **What is the difference between `const` and `readonly`?**
    - `const`: 
      - Compile-time constant.
      - Must be initialized at declaration.
      - Implicitly static.
    - `readonly`: 
      - Run-time constant.
      - Can be initialized either at declaration or in the constructor.
      - Not implicitly static.
    - Example:

    ```csharp
    public class Constants
    {
        public const int MaxValue = 100;
        public readonly int MinValue;

        public Constants(int minValue)
        {
            MinValue = minValue;
        }
    }

    Constants constants = new Constants(1);
    ```

12. **Explain the concept of exception handling in C#.**
    - Exception handling in C# is done using `try`, `catch`, `finally`, and `throw` keywords. It provides a way to handle runtime errors.
    - Example:

    ```csharp
    try
    {
        int result = 10 / 0;
    }
    catch (DivideByZeroException ex)
    {
        Console.WriteLine("Cannot divide by zero");
    }
    finally
    {
        Console.WriteLine("Cleanup code");
    }
    ```

13. **What are delegates in C#?**
    - Delegates are type-safe pointers to methods. They are used to pass methods as arguments.
    - Example:

    ```csharp
    public delegate void PrintMessage(string message);

    public class Printer
    {
        public void Print(string message)
        {
            Console.WriteLine(message);
        }
    }

    PrintMessage printMessage = new Printer().Print;
    printMessage("Hello, World!");
    ```

14. **What are events in C# and how do they differ from delegates?**
    - Events are a way for a class to notify other classes or objects when something of interest occurs. Events are based on delegates.
    - Difference: 
      - Events can only be invoked within the class that declares them, whereas delegates can be called by any class.
    - Example:

    ```csharp
    public class Publisher
    {
        public delegate void Notify();
        public event Notify OnNotify;

        public void DoSomething()
        {
            OnNotify?.Invoke();
        }
    }

    public class Subscriber
    {
        public void OnNotified()
        {
            Console.WriteLine("Subscriber notified");
        }
    }

    Publisher publisher = new Publisher();
    Subscriber subscriber = new Subscriber();
    publisher.OnNotify += subscriber.OnNotified;
    publisher.DoSomething();
    ```

15. **What is the purpose of the `using` statement in C#?**
    - The `using` statement ensures that `IDisposable` objects are properly disposed of. It provides a convenient syntax for this.
    - Example:

    ```csharp
    using (StreamReader reader = new StreamReader("file.txt"))
    {
        string content = reader.ReadToEnd();
        Console.WriteLine(content);
    }
    ```

## Advanced C# Questions

16. **What are extension methods in C#?**
    - Extension methods allow you to add new methods to existing types without modifying them. They are defined as static methods in static classes.
    - Example:

    ```csharp
    public static class StringExtensions
    {
        public static string ToUpperCase(this string str)
        {
            return str.ToUpper();
        }
    }

    string message = "hello";
    Console.WriteLine(message.ToUpperCase()); // Using extension method
    ```

17. **Explain LINQ and provide an example.**
    - LINQ (Language Integrated Query) provides a consistent

 way to query various data sources.
    - Example:

    ```csharp
    int[] numbers = { 2, 3, 4, 5 };

    var squares = from n in numbers
                  select n * n;

    foreach (var square in squares)
    {
        Console.WriteLine(square);
    }
    ```

18. **What are anonymous types in C#?**
    - Anonymous types provide a way to create an object without having to define a class.
    - Example:

    ```csharp
    var person = new { Name = "John", Age = 30 };

    Console.WriteLine($"Name: {person.Name}, Age: {person.Age}");
    ```

19. **What are lambda expressions?**
    - Lambda expressions are concise ways to represent anonymous methods using the `=>` syntax.
    - Example:

    ```csharp
    Func<int, int, int> add = (a, b) => a + b;
    Console.WriteLine(add(3, 4));
    ```

20. **Explain the `async` and `await` keywords.**
    - `async` and `await` are used for asynchronous programming. `async` marks a method as asynchronous, and `await` pauses the execution until the awaited task completes.
    - Example:

    ```csharp
    public async Task<int> GetDataAsync()
    {
        await Task.Delay(1000); // Simulate a delay
        return 42;
    }

    public async Task PrintDataAsync()
    {
        int data = await GetDataAsync();
        Console.WriteLine(data);
    }
    ```

21. **What is the difference between `Task` and `Thread`?**
    - `Task` is a higher-level abstraction for asynchronous operations. It represents a single operation that does not return a value.
    - `Thread` represents an actual OS thread. It is lower-level and more resource-intensive.
    
    ```csharp
    Task.Run(() => Console.WriteLine("Running a task"));

    Thread thread = new Thread(() => Console.WriteLine("Running a thread"));
    thread.Start();
    ```

22. **What is reflection in C#?**
    - Reflection allows inspecting metadata of assemblies, modules, and types at runtime. It is used for late binding, examining types, and dynamically invoking methods.
    - Example:

    ```csharp
    Type type = typeof(String);
    MethodInfo methodInfo = type.GetMethod("Contains", new[] { typeof(string) });
    Console.WriteLine(methodInfo);
    ```

23. **What are generics and why are they useful?**
    - Generics allow defining type-safe data structures and methods without specifying exact data types.
    - Example:

    ```csharp
    public class GenericList<T>
    {
        private List<T> _list = new List<T>();

        public void Add(T item)
        {
            _list.Add(item);
        }

        public T Get(int index)
        {
            return _list[index];
        }
    }

    GenericList<int> intList = new GenericList<int>();
    intList.Add(1);
    Console.WriteLine(intList.Get(0));
    ```

24. **Explain covariance and contravariance in C#.**
    - Covariance and contravariance provide a way to use a more derived type (covariance) or a less derived type (contravariance) than originally specified.
    - Example:

    ```csharp
    // Covariance
    IEnumerable<string> strings = new List<string>();
    IEnumerable<object> objects = strings;

    // Contravariance
    Action<object> actObject = obj => Console.WriteLine(obj);
    Action<string> actString = actObject;
    ```

25. **What is the difference between `Array` and `ArrayList`?**
    - `Array`:
      - Fixed size
      - Strongly typed
    - `ArrayList`:
      - Dynamically sized
      - Stores objects (not type-safe)
    - Example:

    ```csharp
    int[] numbers = new int[5];
    ArrayList list = new ArrayList();
    list.Add(1);
    list.Add("Hello");
    ```

## Object-Oriented Programming (OOP) Questions

26. **Explain the four principles of OOP.**
    - **Encapsulation**: Bundling the data and methods that operate on the data.
    - **Abstraction**: Hiding complex implementation details and exposing only necessary features.
    - **Inheritance**: Creating new classes from existing ones to reuse code.
    - **Polymorphism**: Allowing methods to do different things based on the object they are acting upon.

27. **What is method overloading and method overriding?**
    - **Method Overloading**: Multiple methods with the same name but different parameters within the same class.
    - **Method Overriding**: Redefining a method in a derived class with the same signature as in the base class.
    - Example:

    ```csharp
    // Overloading
    public void Print(int number) { }
    public void Print(string text) { }

    // Overriding
    public class BaseClass
    {
        public virtual void Show() { }
    }

    public class DerivedClass : BaseClass
    {
        public override void Show() { }
    }
    ```

28. **What is a virtual method in C#?**
    - A virtual method is a method that can be overridden in derived classes.
    - Example:

    ```csharp
    public class BaseClass
    {
        public virtual void Display()
        {
            Console.WriteLine("Base display");
        }
    }

    public class DerivedClass : BaseClass
    {
        public override void Display()
        {
            Console.WriteLine("Derived display");
        }
    }
    ```

29. **What is the purpose of the `base` keyword?**
    - The `base` keyword is used to access members of the base class from a derived class.
    - Example:

    ```csharp
    public class BaseClass
    {
        public void Display()
        {
            Console.WriteLine("Base display");
        }
    }

    public class DerivedClass : BaseClass
    {
        public new void Display()
        {
            base.Display();
            Console.WriteLine("Derived display");
        }
    }
    ```

30. **What is a sealed class in C#?**
    - A sealed class cannot be inherited.
    - Example:

    ```csharp
    public sealed class SealedClass
    {
        // Members of sealed class
    }

    // The following class will produce an error
    // public class DerivedClass : SealedClass
    // {
    // }
    ```

## ASP.NET Questions

31. **What is ASP.NET?**
    - ASP.NET is a web application framework developed by Microsoft for building dynamic web sites, web applications, and web services.

32. **Explain the MVC architecture.**
    - MVC (Model-View-Controller) is an architectural pattern that separates an application into three main components:
      - **Model**: Represents the application's data and business logic.
      - **View**: Represents the UI and displays data from the model.
      - **Controller**: Handles user input and interactions, updating the model and view accordingly.

33. **What are Razor pages?**
    - Razor Pages are a simplified model for building web UI in ASP.NET Core. It is a page-based programming model that uses the Razor syntax.

34. **What is the difference between ASP.NET Web Forms and ASP.NET MVC?**
    - **ASP.NET Web Forms**:
      - Event-driven model
      - Uses ViewState for state management
      - Complex page life cycle
    - **ASP.NET MVC**:
      - MVC architectural pattern
      - No ViewState, uses HTTP directly
      - Clear separation of concerns

35. **What is dependency injection and how is it used in ASP.NET Core?**
    - Dependency injection (DI) is a design pattern that allows for the creation of dependent objects outside of a class and provides those objects to the class.
    - In ASP.NET Core, it is used to inject services into controllers, views, and other services.

    ```csharp
    public interface IMyService
    {
        void DoWork();
    }

    public class MyService : IMyService
    {
        public void DoWork() { }
    }

    public class MyController : Controller
    {
        private readonly IMyService _service;

        public MyController(IMyService service)
        {
            _service = service;
        }
    }

    public class Startup
    {
        public void ConfigureServices(IServiceCollection services)
        {
            services.AddScoped<IMyService, MyService>();
        }
    }
    ```

36. **What is middleware in ASP.NET Core?**
    - Middleware are components that form the request pipeline in an ASP.NET Core application. Each component can process and modify requests and responses.
    - Example:

    ```csharp
    public class Startup
    {
        public void Configure(IApplicationBuilder app)
        {
            app.Use(async (context, next) =>
            {
                // Middleware logic before the next component
                await next.Invoke();
                // Middleware logic after the next component
            });

            app.Run(async context =>
            {
                await context.Response.WriteAsync("Hello, World!");
            });
        }
    }
    ```

37. **Explain the purpose of the `appsettings.json` file.**
    - The `appsettings.json` file is used to store configuration settings in a JSON format for an ASP.NET Core application. It can include connection strings, app-specific settings, and more.

38. **What is Entity Framework?**
    - Entity Framework (EF) is an ORM (Object-Relational

 Mapper) that enables .NET developers to work with a database using .NET objects, eliminating the need for most of the data-access code.

39. **What is the difference between Entity Framework and ADO.NET?**
    - **Entity Framework**:
      - ORM tool
      - Higher level of abstraction
      - Uses LINQ to query databases
    - **ADO.NET**:
      - Low-level data access
      - More control over database operations
      - Requires more boilerplate code

40. **What is the purpose of the `DbContext` class?**
    - `DbContext` is the primary class for interacting with a database using Entity Framework. It provides methods for querying and saving data.

    ```csharp
    public class MyDbContext : DbContext
    {
        public DbSet<Customer> Customers { get; set; }
    }
    ```

## .NET Core Questions

41. **What is .NET Core?**
    - .NET Core is a cross-platform, high-performance, open-source framework for building modern, cloud-based, and internet-connected applications.

42. **Explain the differences between .NET Core and .NET Framework.**
    - **.NET Core**:
      - Cross-platform
      - Open-source
      - Modular architecture
    - **.NET Framework**:
      - Windows-only
      - Proprietary
      - Monolithic architecture

43. **What is the .NET Standard?**
    - .NET Standard is a set of APIs that all .NET implementations must support. It ensures portability across different .NET platforms.

44. **What is the Global Assembly Cache (GAC)?**
    - The GAC is a machine-wide code cache that stores assemblies shared by multiple applications on a computer. It is used to avoid duplication and to share assemblies.

45. **What are the main components of the .NET Core runtime?**
    - **CoreCLR**: The .NET Core runtime for executing applications.
    - **CoreFX**: The foundational libraries for .NET Core applications.
    - **ASP.NET Core**: The framework for building web applications.

## Memory Management Questions

46. **What is garbage collection in .NET?**
    - Garbage collection (GC) is the process of automatically reclaiming memory that is no longer in use by the application. It helps in managing the memory and preventing memory leaks.

47. **Explain the concept of managed and unmanaged code.**
    - **Managed Code**: Code that runs under the control of the .NET runtime (CLR), which handles memory management and other system services.
    - **Unmanaged Code**: Code that is executed directly by the operating system, outside the control of the CLR.

48. **What are the different types of garbage collectors in .NET?**
    - **Workstation GC**: Optimized for desktop applications.
    - **Server GC**: Optimized for server applications.
    - **Concurrent GC**: Runs concurrently with the application to minimize pause times.

49. **What is a memory leak and how can it be prevented in C#?**
    - A memory leak occurs when memory that is no longer needed is not released, leading to a gradual decrease in available memory.
    - Prevent it by:
      - Disposing of unmanaged resources
      - Avoiding static references
      - Using memory profiling tools to detect leaks

50. **Explain the concept of Finalize and Dispose methods.**
    - **Finalize**: Called by the GC before an object is reclaimed. Used to clean up unmanaged resources.
    - **Dispose**: Explicitly called by the user to free unmanaged resources. Implements the `IDisposable` interface.

    ```csharp
    public class Resource : IDisposable
    {
        public void Dispose()
        {
            // Clean up resources
            GC.SuppressFinalize(this);
        }

        ~Resource()
        {
            // Finalizer logic
        }
    }
    ```

## Multithreading and Asynchronous Programming Questions

51. **What is multithreading?**
    - Multithreading is the ability of a CPU to execute multiple threads concurrently, which can lead to more efficient use of resources.

52. **Explain the difference between `Thread` and `Task`.**
    - **Thread**: Represents an OS-level thread.
    - **Task**: Represents a higher-level abstraction of an asynchronous operation.

53. **What is the `lock` statement in C#?**
    - The `lock` statement ensures that a block of code runs to completion without being interrupted by other threads. It helps in preventing race conditions.
    - Example:

    ```csharp
    private readonly object _lockObj = new object();

    public void SafeMethod()
    {
        lock (_lockObj)
        {
            // Critical section
        }
    }
    ```

54. **What are thread pools?**
    - Thread pools manage a pool of worker threads that can be reused to execute multiple tasks. This improves performance by reducing the overhead of creating and destroying threads.

55. **Explain the `volatile` keyword.**
    - The `volatile` keyword ensures that a variable is always read from and written to memory, not cached, ensuring visibility across threads.
    - Example:

    ```csharp
    private volatile bool _isRunning;
    ```

56. **What are asynchronous delegates?**
    - Asynchronous delegates allow methods to be called asynchronously using the `BeginInvoke` and `EndInvoke` methods.

    ```csharp
    public delegate void MyDelegate();

    public void StartDelegate()
    {
        MyDelegate del = new MyDelegate(Method);
        IAsyncResult asyncResult = del.BeginInvoke(null, null);
        del.EndInvoke(asyncResult);
    }
    ```

## Design Patterns Questions

57. **What are design patterns?**
    - Design patterns are reusable solutions to common problems in software design. They provide templates for solving particular design issues.

58. **Explain the Singleton pattern.**
    - The Singleton pattern ensures that a class has only one instance and provides a global point of access to it.
    - Example:

    ```csharp
    public class Singleton
    {
        private static Singleton _instance;

        private Singleton() { }

        public static Singleton Instance
        {
            get
            {
                if (_instance == null)
                {
                    _instance = new Singleton();
                }
                return _instance;
            }
        }
    }
    ```

59. **What is the Factory pattern?**
    - The Factory pattern provides a way to create objects without specifying the exact class of the object that will be created.
    - Example:

    ```csharp
    public abstract class Product { }

    public class ConcreteProductA : Product { }

    public class ConcreteProductB : Product { }

    public class Factory
    {
        public static Product CreateProduct(string type)
        {
            switch (type)
            {
                case "A": return new ConcreteProductA();
                case "B": return new ConcreteProductB();
                default: throw new ArgumentException("Invalid type");
            }
        }
    }
    ```

60. **Explain the Observer pattern.**
    - The Observer pattern defines a one-to-many dependency between objects so that when one object changes state, all its dependents are notified and updated automatically.
    - Example:

    ```csharp
    public interface IObserver
    {
        void Update();
    }

    public class Subject
    {
        private List<IObserver> _observers = new List<IObserver>();

        public void Attach(IObserver observer)
        {
            _observers.Add(observer);
        }

        public void Notify()
        {
            foreach (var observer in _observers)
            {
                observer.Update();
            }
        }
    }
    ```

61. **What is the Repository pattern?**
    - The Repository pattern abstracts data access logic and provides a central location for managing data access, making the code more maintainable.
    - Example:

    ```csharp
    public interface IRepository<T>
    {
        void Add(T entity);
        T Get(int id);
    }

    public class Repository<T> : IRepository<T>
    {
        // Implementation of IRepository
    }
    ```

62. **What is the Dependency Injection pattern?**
    - The Dependency Injection (DI) pattern allows injecting dependencies into a class, rather than the class creating them itself. This promotes loose coupling and testability.
    - Example:

    ```csharp
    public class Service
    {
        private readonly IRepository _repository;

        public Service(IRepository repository)
        {
            _repository = repository;
        }
    }
    ```

## Unit Testing Questions

63. **What is unit testing?**
    - Unit testing is the process of testing individual units or components of a software to ensure they work as expected.

64. **What are some popular unit testing frameworks for C#?**
    - **NUnit**
    - **xUnit**
    - **MSTest**

65. **Explain the Arrange-Act-Assert pattern.**
    - **Arrange**: Set up the test environment.
    - **Act**: Execute the code under test.
    - **Assert**: Verify that the outcome is as expected.

66. **What is mocking in unit testing?**
    - Mocking is the process of creating mock objects to simulate the behavior of real objects in order to isolate the code under test.

67. **What is the difference between a stub and a mock?**
    - **Stub**: Provides predefined responses to method calls.
    - **Mock**: Records interactions and can verify the behavior of the code under test.

68. **Explain code coverage and its importance.**
    - Code coverage is a metric that measures the percentage of code executed during testing. Higher coverage generally indicates more thorough testing.

## Data Access Questions

69. **What is ADO.NET?**

- ADO.NET is a data access technology in .NET that provides a set of classes to interact with data sources such as databases and XML files. It allows for efficient data retrieval and manipulation.

70. **Explain the difference between connected and disconnected architecture.**

- **Connected Architecture**: Maintains a continuous connection to the data source. Suitable for real-time data operations.
- **Disconnected Architecture**: Retrieves data, performs operations on it without a continuous connection to the data source, and updates the data source in batch operations.

71. **What are data adapters and data readers?**

- **Data Adapter**: Acts as a bridge between a DataSet and a data source for retrieving and saving data. Works in disconnected architecture.
- **Data Reader**: Provides a fast, forward-only, read-only cursor to read data from a data source. Works in connected architecture.

   ```csharp
   SqlDataReader reader = command.ExecuteReader();
   while (reader.Read())
   {
       Console.WriteLine(reader["ColumnName"]);
   }
   ```

72. **What is a connection string?**

- A connection string is a string that specifies information about a data source and how to connect to it. It includes parameters like the data source, database name, user ID, and password.

   ```csharp
   string connectionString = "Server=myServerAddress;Database=myDataBase;User Id=myUsername;Password=myPassword;";
   ```

73. **What is the purpose of the SqlCommand object?**

- The `SqlCommand` object is used to execute SQL queries and commands against a SQL Server database. It can execute queries that return data (e.g., SELECT) or commands that modify data (e.g., INSERT, UPDATE, DELETE).

   ```csharp
   SqlCommand command = new SqlCommand("SELECT * FROM Table", connection);
   ```

74. **What is the difference between ExecuteNonQuery, ExecuteScalar, and ExecuteReader?**

- **ExecuteNonQuery**: Executes a command that does not return any data, such as INSERT, UPDATE, or DELETE.
  
  ```csharp
  int rowsAffected = command.ExecuteNonQuery();
  ```

- **ExecuteScalar**: Executes a query and returns a single value.

  ```csharp
  object result = command.ExecuteScalar();
  ```

- **ExecuteReader**: Executes a query that returns rows of data.

  ```csharp
  SqlDataReader reader = command.ExecuteReader();
  ```

## Web Services and APIs Questions

75. **What are web services?**

- Web services are software applications that can be accessed over the internet using standard protocols such as HTTP. They allow different applications to communicate with each other.

76. **Explain the difference between SOAP and REST.**

- **SOAP (Simple Object Access Protocol)**: A protocol for exchanging structured information in web services. Uses XML for message format.
- **REST (Representational State Transfer)**: An architectural style for designing networked applications. Uses standard HTTP methods (GET, POST, PUT, DELETE) and can use various formats like JSON and XML.

77. **What is WCF?**

- WCF (Windows Communication Foundation) is a framework for building service-oriented applications. It enables developers to build secure, reliable, and high-performance services that can be integrated across platforms.

78. **What is Web API?**

- Web API is a framework for building HTTP services that can be consumed by various clients, including browsers and mobile devices. It supports RESTful services and can return data in formats like JSON and XML.

79. **How do you handle authentication in Web API?**

- Authentication in Web API can be handled using various methods such as:
- **Basic Authentication**
- **Token-based Authentication (e.g., JWT)**
- **OAuth**

   ```csharp
   [Authorize]
   public class ValuesController : ApiController
   {
       public IHttpActionResult Get()
       {
           return Ok("Authenticated");
       }
   }
   ```

80. **What is CORS and why is it important?**

- CORS (Cross-Origin Resource Sharing) is a mechanism that allows restricted resources on a web page to be requested from another domain outside the domain from which the resource originated. It's important for enabling secure cross-domain data sharing.

   ```csharp
   public void Configure(IApplicationBuilder app, IHostingEnvironment env)
   {
       app.UseCors(builder => builder
           .AllowAnyOrigin()
           .AllowAnyMethod()
           .AllowAnyHeader());
   }
   ```

## Miscellaneous Questions

81. **What is the dynamic keyword in C#?**

- The `dynamic` keyword allows variables to bypass compile-time type checking, meaning their type is resolved at runtime.

   ```csharp
   dynamic dynamicVariable = "Hello";
   dynamicVariable = 10; // No compile-time error
   ```

82. **What are value types and reference types?**

- **Value Types**: Stored in the stack, hold the data directly.
  
  ```csharp
  int a = 10; // Value type
  ```

- **Reference Types**: Stored in the heap, hold a reference to the data.

  ```csharp
  string s = "Hello"; // Reference type
  ```

83. **What is the difference between == and Equals method?**

- **==**: Compares the values of objects.
- **Equals**: Compares the contents or state of objects.

   ```csharp
   string a = "hello";
   string b = "hello";
   bool result = (a == b); // True
   bool result2 = a.Equals(b); // True
   ```

84. **Explain the purpose of the Nullable type.**

- The `Nullable` type allows value types to represent undefined or missing values.

   ```csharp
   int? age = null;
   ```

85. **What is the difference between String and StringBuilder?**

- **String**: Immutable, each modification creates a new instance.
  
  ```csharp
  string str = "Hello";
  str += " World"; // New instance created
  ```

- **StringBuilder**: Mutable, modifications do not create new instances.

  ```csharp
  StringBuilder sb = new StringBuilder("Hello");
  sb.Append(" World"); // No new instance
  ```

86. **Explain the concept of type conversion and type casting.**

- **Type Conversion**: Converting one data type to another.

  ```csharp
  int num = Convert.ToInt32("123");
  ```

- **Type Casting**: Forcing a variable to be of another type.

  ```csharp
  double d = 123.45;
  int i = (int)d;
  ```

87. **What is the enum type in C#?**

- An `enum` is a distinct value type that consists of a set of named constants called enumerators.

   ```csharp
   enum Days { Sunday, Monday, Tuesday, Wednesday, Thursday, Friday, Saturday }
   ```

88. **What are tuples in C#?**

- Tuples provide a way to store multiple values in a single data structure.

   ```csharp
   var tuple = (1, "Hello", true);
   ```

89. **What is the purpose of the Partial keyword?**

- The `partial` keyword allows the definition of a class, struct, or method to be split across multiple files.

   ```csharp
   partial class MyClass
   {
       public void Method1() { }
   }
   ```

90. **What are attributes in C#?**

- Attributes provide a way to add metadata to code elements such as classes, methods, and properties.

   ```csharp
   [Obsolete("This method is obsolete.")]
   public void OldMethod() { }
   ```

## Best Practices and Coding Standards Questions

91. **What are coding standards and why are they important?**

- Coding standards are guidelines for writing code in a consistent manner. They are important for readability, maintainability, and reducing errors.

92. **Explain the concept of SOLID principles.**

- **S**: Single Responsibility Principle
- **O**: Open/Closed Principle
- **L**: Liskov Substitution Principle
- **I**: Interface Segregation Principle
- **D**: Dependency Inversion Principle

93. **What are naming conventions in C#?**

- Naming conventions are a set of rules for naming variables, methods, classes, etc. in a consistent manner. For example, using PascalCase for class names and camelCase for variables.

94. **What is the purpose of code comments?**

- Code comments are used to explain and document code. They help others (and yourself) understand the code better.

   ```csharp
   // This is a single-line comment

   /*
   This is a
   multi-line comment
   */
   ```

95. **What are code smells?**

- Code smells are indicators of potential problems in the code that may affect its readability, maintainability, and performance.

96. **What is refactoring?**

- Refactoring is the process of improving the structure and readability of existing code without changing its behavior.

97. **What is the purpose of code reviews?**

- Code reviews are a process where peers review code to find errors, improve quality, and ensure adherence to coding standards.

98. **Explain the DRY principle.**

- DRY (Don't Repeat Yourself) principle states that every piece of knowledge should be expressed only once in the codebase to avoid redundancy.

99. **What is YAGNI?**

- YAGNI (You Aren't Gonna Need It) is a principle that states you should not add functionality until it is necessary.

100. **What is KISS?**

- KISS (Keep It Simple, Stupid) is a principle that emphasizes simplicity in design and implementation. The idea is to avoid unnecessary complexity.
