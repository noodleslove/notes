1. .NET framework vs. .NET core
2. difference between AddMvc(), AddControllersWithViews() and AddControllers()
3. razor view engine (.cshtml)

**General ASP.NET Core**

1. What is Kestrel? How to use Kestrel in asp.net Core application?

Kestrel is a cross-platform web server for ASP.NET Core applications. It is a default web server included in the ASP.NET Core project templates.

3. What is asp.net core Middleware and How is it different from HttpModule? What are some built-in

Middleware in ASP.NET Core is a component that sits in the HTTP request pipeline, processing requests and responses as they pass through the application. 

**ASP.NET HttpModule:**
- **Legacy System**
- **Synchronous Processing**
- **Limited Flexibility**
- **No Dependency Injection**

**Built-in Middleware**
- Static Files Middleware
- Routing Middleware
- Authorization Middleware
- Endpoints Middleware
- CORS Middleware

middleware(s) with asp.net Core?

3. What are some custom Middlewares you created? How did you register them?

4. What do the Configure () and ConfigureServices () methods do Startup.cs do

- `ConfigureServices` method is used to register services with the dependency injection (DI) container.
- `Configure` method is used to define how the application responds to HTTP requests. Middleware Pipeline Configuration, Order of Middleware.

5. What is Dependency Injection and what are different scopes in asp.net core

Dependency Injection (DI) is a design pattern used to implement Inversion of Control (IoC) between classes and their dependencies.

1. Transient
- **Lifetime**: Created each time they are requested.
- **Use Case**: Best suited for lightweight, stateless services.
2. Scoped
- **Lifetime**: Created once per request (HTTP request in web applications).
- **Use Case**: Best suited for services that maintain state within a single request but not across multiple requests.
3. Singleton
- **Lifetime**: Created once and shared throughout the application's lifetime.
- **Use Case**: Best suited for services that maintain state that needs to be shared across the entire application.

Dependency Injection

● AddTransient

● AddScoped

● AddSingleton

6. What is the use of the “launchsettings.json” file and “appsettings.json” file?

7. What is the “Developer Exception Page” in asp.net Core? How can we configure a custom exception

handling page in asp.net core?

8. How to configure the logging framework in asp.net core? What is a third party logging framework that is

supported by asp.net core?

9. What is the use of a filter in the asp.net core application? Explain the filter types available in the asp.net

core application?

10. What are some custom Filters you created? How to define a Global filter in asp.net core?

11. What is your understanding of Caching? How did you use Caching in your application? In-memory or

Distributed caching? Give me some examples where caching is useful.

12. Do you know what is model binding in asp.net core, how is it useful for developers?

13. Explain what Routing is along with attribute Routing

14. How did you validate your models? Any experience with the Fluent Validation library?

15. How did you handle exceptions in your .net core application?

**MVC (Model-View-Controller)**

1. What are all the advantages of MVC?

2. Explain various action results in MVC.

3. How do you pass data from Controller to View and from View to Controller?

4. What are Partial Views in MVC? Give me some examples where you have used them?

5. Explain what ViewBag, ViewData & TempData are along with examples from your project.

6. What are HTML Helpers in old MVC and compare them with Tag Helpers in asp.net Core MVC?

7. What is ViewModel? What is the purpose of ViewModel? Could you explain where you have used

ViewModel?

8. Could you explain all the filters in MVC and tell me what are all the custom filters that you have?

9. What are all the different state management techniques in asp.net(Server-side: Sessions, Caching,

Database, TempData & Client-side: localStorage, cookies, sessionStorage etc.)

10. How would you display a grid in Razor? How did you do Server-side Pagination?