## PROJECT_SOURCE:

[Provide a GitHub repo URL or a local path to the project. Leave blank to create a new project.]

## FEATURE:

- ASP.NET Core Web API that integrates with multiple AI services using dependency injection.
- Research Service for the primary business logic and then an Email Service for email operations.
- MAUI cross-platform application to interact with the API.
- Microsoft Graph for email operations, Bing Search API for research functionality.

## EXAMPLES:

In the `examples/` folder, there is a README for you to read to understand what the example is all about and also how to structure your own README when you create documentation for the above feature.

- `examples/Program.cs` - use this as a template to create the API startup and dependency injection configuration
- `examples/Services/` - read through all of the files here to understand best practices for creating services with dependency injection, handling service dependencies, and implementing business logic.
- `examples/Controllers/` - understand patterns for ASP.NET Core controllers and API endpoints.

Don't copy any of these examples directly, it is for a different project entirely. But use this as inspiration and for best practices.

## DOCUMENTATION:

ASP.NET Core documentation: https://docs.microsoft.com/en-us/aspnet/core/
Entity Framework Core documentation: https://docs.microsoft.com/en-us/ef/core/
.NET MAUI documentation: https://docs.microsoft.com/en-us/dotnet/maui/
Microsoft Graph documentation: https://docs.microsoft.com/en-us/graph/

## OTHER CONSIDERATIONS:

- Include a appsettings.example.json, README with instructions for setup including how to configure Microsoft Graph and Bing Search API.
- Include the project structure in the README.
- NuGet packages and project references should be properly configured.
- Use IConfiguration and dependency injection for configuration management
- Follow .NET naming conventions and use nullable reference types