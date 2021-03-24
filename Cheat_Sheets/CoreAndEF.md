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


## Connection Strings in `appsettings.json` and Wire Up

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
  * I set this to Copy If Newer. You can also set to Always Copy. Point being, make sure this always up to date.

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

## The Data - Let's *Model*

* [Modeling on MS Docs...](https://docs.microsoft.com/en-us/ef/core/modeling/)

* Consider *conventions*
  * Property named `Id` or `<type name>Id` -> *key* of an entity
  * Keys that are `int` or `Guid` -> *generated values on add*
  * Nullable CLR types (e.g. `string`, `int?`, `byte[]`) -> optional (string, int?, byte[], etc.)<br/>
    Not nullable CLR types (e.g. `decimal`, `int`, `bool`) -> required
  * Default maximum length is provider-specific. Example: SQL Server strings -> `nvarchar(max)`
  * *Shadow properties* will be *auto-created* in the DB for foreign keys if no foreign key property is found in the dependent class.
  * *Index* is created for each property that is used as a foreign key
  * Name of the `DbSet<TEntity>` property -> table name<br/>, if not property exists, class name -> table name
  * Default behavior for inheritance: *Table-per-Hierarchy (TPH)*

* Configure your model using...
  * ...*Fluent API* in [`DbContext.OnModelCreating`](https://docs.microsoft.com/en-us/dotnet/api/microsoft.entityframeworkcore.dbcontext.onmodelcreating) or
  * ...*Data Annotations*
      * Make sure you have ```using System.ComponentModel.DataAnnotations;``` On the model class

```csharp
// Data Annotations Example:

public class Blog
{
    public int BlogId { get; set; }
    [Required]
    public string Url { get; set; }
}
```

  * [Fluent to do a Model on Docs...](https://docs.microsoft.com/en-us/ef/core/modeling/#use-fluent-api-to-configure-a-model)

Next page: [01-Notes.md](https://github.com/ScottGeek/Docs/blob/main/_includes/01-Notes.md)
