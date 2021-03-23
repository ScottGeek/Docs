# EF/ASP.NET Cheat Sheet

## Get Started with Installing EF and Using in an App

* [MS Documentation site - Getting Started...](https://docs.microsoft.com/en-us/ef/core/get-started/)

* The Unicorn - Install or Update EF Tools globally
  * **Installing** `dotnet tool install --global dotnet-ef`
  * **Updating**   `dotnet tool update --global dotnet-ef` (add `--version ...` to install a prerelease)
  
* **Nuget** Packages Needed in your Project
  * `dotnet add package Microsoft.EntityFrameworkCore.SqlServer`  *If you are using SQL Server*
    * [DB providers Docs...](https://docs.microsoft.com/en-us/ef/core/providers/)
  * `dotnet add package Microsoft.EntityFrameworkCore.Design`     *Required for Migrations Tools*

* **Logging Nuget** If you want to print generated SQL statements: `dotnet add package Microsoft.Extensions.Logging.Console`
* **Reading** *appsettings.json*, Nuget: `dotnet add package Microsoft.Extensions.Configuration.Json` *Note: Not necessary in ASP.NET*

## Connection Strings in `appsettings.json`

* [Connection Strings on Docs...](https://docs.microsoft.com/en-us/ef/core/miscellaneous/connection-strings#aspnet-core)

* Create *appsettings.json* file:

```json
{
  "ConnectionStrings": {
    "DefaultConnection": "Server=(localdb)\\MSSQLLocalDB;Database=AddressBook;Trusted_Connection=True"
  }
}
```

* Don't forget to *copy the file to output directory* if you build a console app. In ASP.NET Core, this is done automatically.
  ![Copy To Output Directory](https://user-images.githubusercontent.com/1904228/112211591-74a13300-8bf2-11eb-90f7-b4d4deab97e1.PNG)


* Read connection string in ASP.NET Core's startup class:

```csharp
public class Startup
{
    private IConfiguration configuration;

    public Startup(IConfiguration configuration)
    {
        this.configuration = configuration;
    }

    public void ConfigureServices(IServiceCollection services)
    {
        ...
        services.AddDbContext<AddressBookContext>(options => options.UseSqlServer(
            Configuration["ConnectionStrings:DefaultConnection"]));
        ...
    }

    ...
}
```
