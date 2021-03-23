# EF/ASP.NET Cheat Sheet

## Get Started with Installing EF

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
