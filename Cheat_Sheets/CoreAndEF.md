# EF/ASP.NET Cheat Sheet

## Install EF

* [Documentation...](https://docs.microsoft.com/en-us/ef/core/get-started/)

* Install EF Tools globally
  * `dotnet tool install --global dotnet-ef`
  * Update with `dotnet tool update --global dotnet-ef` (add `--version ...` to install a prerelease)
* `dotnet add package Microsoft.EntityFrameworkCore.SqlServer`
  * [Choose your DB provider...](https://docs.microsoft.com/en-us/ef/core/providers/)
* `dotnet add package Microsoft.EntityFrameworkCore.Design`
* If you want to print generated SQL statements: `dotnet add package Microsoft.Extensions.Logging.Console`
* To read *appsettings.json*, add: `dotnet add package Microsoft.Extensions.Configuration.Json`
  * Note: Not necessary in ASP.NET
