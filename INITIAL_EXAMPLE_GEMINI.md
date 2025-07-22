## PROJECT_SOURCE:

[Leave blank to create a new project, or provide GitHub URL/local path]

## FEATURE:

Create an ASP.NET Core Web API application with the following capabilities:
- REST API for managing user tasks with CRUD operations
- SQL Server database integration using Entity Framework Core
- JWT authentication middleware with ASP.NET Core Identity
- Pydantic-style validation using FluentValidation
- Comprehensive test suite with xUnit and FluentAssertions
- MAUI client application for cross-platform access
- API documentation with Swagger/OpenAPI generation
- Docker configuration for easy deployment

## RELEVANT_CODE:

[Since this is a new project, no existing code to analyze]
- Focus on creating clean, testable ASP.NET Core patterns
- Follow .NET best practices for project structure
- Implement proper error handling and logging with ILogger

## EXAMPLES:

In the `examples/` folder (if they exist), reference:
- `examples/Program.cs` - ASP.NET Core startup and dependency injection patterns
- `examples/Controllers/TaskController.cs` - Controller patterns with proper HTTP status codes
- `examples/Services/TaskService.cs` - Service layer patterns with interfaces
- `examples/Models/TaskModel.cs` - Entity Framework models and DTOs
- `examples/Tests/TaskControllerTests.cs` - xUnit test patterns with FluentAssertions

Don't copy these examples directly - use them for inspiration on .NET project structure and patterns.

## DOCUMENTATION:

- ASP.NET Core documentation: https://docs.microsoft.com/en-us/aspnet/core/
- Entity Framework Core documentation: https://docs.microsoft.com/en-us/ef/core/
- .NET MAUI documentation: https://docs.microsoft.com/en-us/dotnet/maui/
- ASP.NET Core Identity documentation: https://docs.microsoft.com/en-us/aspnet/core/security/authentication/identity
- FluentValidation documentation: https://fluentvalidation.net/
- xUnit documentation: https://xunit.net/
- FluentAssertions documentation: https://fluentassertions.com/

## OTHER CONSIDERATIONS:

- Use IConfiguration for connection strings and JWT secrets
- Include an `appsettings.example.json` file with all required configuration sections
- Use proper NuGet package management with PackageReference
- Add Entity Framework migrations support
- Include proper error handling for database operations with try-catch patterns
- Use dependency injection for services and DbContext
- Add structured logging with ILogger<T>
- Include Docker and docker-compose configuration for SQL Server
- Follow .NET solution structure with separate projects for API, Domain, Application, Infrastructure
- Use nullable reference types and proper null handling
- Add Swagger/OpenAPI documentation with XML comments
- Use async/await patterns throughout with proper ConfigureAwait usage
- Include xUnit test projects with proper mocking using Moq