name: "Multi-Service System: Research API with Email Service Integration"
description: |

## Purpose
Build a comprehensive .NET solution with ASP.NET Core Web API, Entity Framework Core, and MAUI client where a Research Service uses Bing Search API and integrates with an Email Service (using Microsoft Graph API). This demonstrates clean architecture patterns with external API integrations.

## Core Principles
1. **Context is King**: Include ALL necessary documentation, examples, and caveats
2. **Validation Loops**: Provide executable tests/builds the AI can run and fix
3. **Information Dense**: Use keywords and patterns from the .NET codebase
4. **Progressive Success**: Start simple, validate, then enhance

---

## Goal
Create a production-ready multi-service .NET solution where users can research topics via MAUI client or API, and the Research Service can delegate email operations to an Email Service. The system should support proper dependency injection, async patterns, and handle API authentication securely.

## Why
- **Business value**: Automates research and email workflows
- **Integration**: Demonstrates advanced .NET clean architecture patterns
- **Problems solved**: Reduces manual work for research-based email communications

## What
A full-stack .NET application where:
- Users input research queries via MAUI app or direct API calls
- Research Service searches using Bing Search API
- Research Service can invoke Email Service to send results via Microsoft Graph
- Results return with proper error handling and logging
- All services properly registered in dependency injection

### Success Criteria
- [ ] Research Service successfully searches via Bing Search API
- [ ] Email Service sends emails with Microsoft Graph authentication
- [ ] Research Service can invoke Email Service through clean interfaces
- [ ] MAUI client provides proper UI with async operations
- [ ] All tests pass and code meets quality standards

## All Needed Context

### Documentation & References
```yaml
# MUST READ - Include these in your context window
- url: https://docs.microsoft.com/en-us/aspnet/core/web-api/
  why: Core Web API patterns and best practices
  
- url: https://docs.microsoft.com/en-us/ef/core/
  why: Entity Framework patterns, DbContext configuration
  
- url: https://docs.microsoft.com/en-us/dotnet/maui/
  why: MAUI application patterns and async operations
  
- url: https://docs.microsoft.com/en-us/graph/api/user-sendmail
  why: Microsoft Graph email sending with authentication
  
- url: https://docs.microsoft.com/en-us/bing/search-apis/bing-web-search/overview
  why: Bing Search API REST endpoints and response format
  
- file: examples/Controllers/ProductController.cs
  why: Pattern for API controllers, dependency injection, error handling
  
- file: examples/Services/ProductService.cs
  why: Service layer patterns with interfaces and async methods
  
- file: examples/Program.cs
  why: Dependency injection registration and configuration patterns

- url: https://github.com/microsoftgraph/dotnet-core-console-sample
  why: Official Microsoft Graph authentication example
```

### Current Solution Structure
```bash
.
├── examples/
│   ├── Controllers/
│   │   └── ProductController.cs
│   ├── Services/
│   │   └── ProductService.cs
│   └── Program.cs
├── PRPs/
│   └── templates/
│       └── prp_base.md
├── INITIAL.md
├── CLAUDE.md
└── MyProject.sln
```

### Desired Solution Structure with files to be added
```bash
.
├── src/
│   ├── MyApp.Domain/
│   │   ├── Models/
│   │   │   ├── ResearchQuery.cs      # Domain models
│   │   │   ├── SearchResult.cs
│   │   │   └── EmailRequest.cs
│   │   └── Interfaces/
│   │       ├── IResearchService.cs   # Service contracts
│   │       └── IEmailService.cs
│   ├── MyApp.Infrastructure/
│   │   ├── Data/
│   │   │   ├── ApplicationDbContext.cs
│   │   │   └── Migrations/
│   │   ├── Services/
│   │   │   ├── BingSearchService.cs  # External API integrations
│   │   │   └── GraphEmailService.cs
│   │   └── Configuration/
│   │       └── ServiceCollectionExtensions.cs
│   ├── MyApp.Application/
│   │   ├── Services/
│   │   │   ├── ResearchService.cs    # Business logic
│   │   │   └── EmailService.cs
│   │   ├── DTOs/
│   │   │   ├── ResearchRequestDto.cs
│   │   │   └── ResearchResponseDto.cs
│   │   └── Validators/
│   │       └── ResearchRequestValidator.cs
│   ├── MyApp.API/
│   │   ├── Controllers/
│   │   │   ├── ResearchController.cs # API endpoints
│   │   │   └── EmailController.cs
│   │   ├── Program.cs               # API startup
│   │   └── appsettings.json
│   └── MyApp.MAUI/
│       ├── MainPage.xaml            # MAUI UI
│       ├── MainPage.xaml.cs
│       ├── ViewModels/
│       │   └── MainViewModel.cs
│       └── MauiProgram.cs
├── tests/
│   ├── MyApp.UnitTests/
│   │   ├── Services/
│   │   │   ├── ResearchServiceTests.cs
│   │   │   └── EmailServiceTests.cs
│   │   └── Controllers/
│   │       └── ResearchControllerTests.cs
│   └── MyApp.IntegrationTests/
│       └── ApiIntegrationTests.cs
├── appsettings.example.json         # Configuration template
├── MyApp.sln                        # Solution file
└── README.md                        # Updated documentation
```

### Known Gotchas & Library Quirks
```csharp
// CRITICAL: Microsoft Graph requires specific scopes for email operations
// CRITICAL: Bing Search API has rate limits - implement proper retry policies
// CRITICAL: Entity Framework requires explicit async throughout the stack
// CRITICAL: MAUI requires platform-specific permissions in Platforms folders
// CRITICAL: Use IHttpClientFactory for external API calls to avoid socket exhaustion
// CRITICAL: Always use ConfigureAwait(false) in library code
// CRITICAL: Microsoft Graph authentication requires MSAL (Microsoft Authentication Library)
```

## Implementation Blueprint

### Data models and structure

```csharp
// Domain Models
public class ResearchQuery
{
    public int Id { get; set; }
    public string Query { get; set; } = string.Empty;
    public DateTime CreatedAt { get; set; }
    public List<SearchResult> Results { get; set; } = new();
}

public class SearchResult
{
    public int Id { get; set; }
    public string Title { get; set; } = string.Empty;
    public string Url { get; set; } = string.Empty;
    public string Snippet { get; set; } = string.Empty;
    public int ResearchQueryId { get; set; }
}

// DTOs for API
public class ResearchRequestDto
{
    public string Query { get; set; } = string.Empty;
    public int MaxResults { get; set; } = 10;
    public bool IncludeEmailOption { get; set; }
}

// Service Interfaces
public interface IResearchService
{
    Task<ResearchResponseDto> SearchAsync(ResearchRequestDto request, CancellationToken cancellationToken = default);
    Task<bool> SendResearchEmailAsync(int researchId, string recipientEmail, CancellationToken cancellationToken = default);
}
```

### List of tasks to be completed

```yaml
Task 1: Setup Solution Structure and Configuration
CREATE MyApp.sln:
  - Add all projects with proper references
  - Configure solution items

CREATE appsettings.example.json:
  - Include all required configuration sections
  - Document required API keys and connection strings

Task 2: Implement Domain Layer
CREATE MyApp.Domain/Models/:
  - PATTERN: Follow Entity Framework conventions
  - Include proper navigation properties
  - Use data annotations where appropriate

CREATE MyApp.Domain/Interfaces/:
  - Define clean service contracts
  - Use async Task<T> return types throughout

Task 3: Implement Infrastructure Layer
CREATE MyApp.Infrastructure/Data/ApplicationDbContext.cs:
  - PATTERN: Follow existing DbContext patterns
  - Configure entity relationships properly
  - Include proper DbSet declarations

CREATE MyApp.Infrastructure/Services/BingSearchService.cs:
  - Use IHttpClientFactory for HTTP calls
  - Implement proper retry policies
  - Handle rate limiting gracefully

CREATE MyApp.Infrastructure/Services/GraphEmailService.cs:
  - Implement Microsoft Graph authentication
  - Use MSAL for token management
  - Handle email sending with proper error handling

Task 4: Implement Application Layer
CREATE MyApp.Application/Services/ResearchService.cs:
  - Orchestrate search and email operations
  - Implement business logic validation
  - Use repository pattern for data access

CREATE MyApp.Application/Validators/:
  - Use FluentValidation for request validation
  - Include business rule validation

Task 5: Implement Web API
CREATE MyApp.API/Controllers/ResearchController.cs:
  - PATTERN: Follow REST conventions
  - Include proper HTTP status codes
  - Implement async endpoints throughout

CREATE MyApp.API/Program.cs:
  - Configure dependency injection
  - Set up authentication and authorization
  - Configure Entity Framework and external services

Task 6: Implement MAUI Client
CREATE MyApp.MAUI/MainPage.xaml:
  - Simple, functional UI for research input
  - Display results in ListView
  - Include email sending option

CREATE MyApp.MAUI/ViewModels/MainViewModel.cs:
  - Use MVVM pattern with ICommand
  - Implement async operations properly
  - Handle errors and loading states

Task 7: Add Comprehensive Tests
CREATE tests/MyApp.UnitTests/:
  - Mock external dependencies with Moq
  - Test business logic thoroughly
  - Achieve 80%+ code coverage

CREATE tests/MyApp.IntegrationTests/:
  - Test full API workflows
  - Use TestServer for integration testing
  - Include database integration tests

Task 8: Documentation and Configuration
UPDATE README.md:
  - Include setup instructions
  - Document API endpoints
  - Provide configuration guidance
```

### Per task pseudocode

```csharp
// Task 3: Bing Search Service
public class BingSearchService : IBingSearchService
{
    private readonly HttpClient _httpClient;
    private readonly IConfiguration _configuration;
    
    public async Task<IEnumerable<SearchResult>> SearchAsync(string query, int maxResults, CancellationToken cancellationToken)
    {
        // PATTERN: Use retry policy for external API calls
        var policy = Policy
            .Handle<HttpRequestException>()
            .WaitAndRetryAsync(3, retryAttempt => 
                TimeSpan.FromSeconds(Math.Pow(2, retryAttempt)));
        
        return await policy.ExecuteAsync(async () =>
        {
            var request = new HttpRequestMessage(HttpMethod.Get, 
                $"https://api.bing.microsoft.com/v7.0/search?q={Uri.EscapeDataString(query)}&count={maxResults}");
            
            request.Headers.Add("Ocp-Apim-Subscription-Key", _configuration["BingSearch:ApiKey"]);
            
            // GOTCHA: Bing API returns 429 for rate limit exceeded
            var response = await _httpClient.SendAsync(request, cancellationToken);
            response.EnsureSuccessStatusCode();
            
            var content = await response.Content.ReadAsStringAsync(cancellationToken);
            var searchResponse = JsonSerializer.Deserialize<BingSearchResponse>(content);
            
            return searchResponse.WebPages.Value.Select(item => new SearchResult
            {
                Title = item.Name,
                Url = item.Url,
                Snippet = item.Snippet
            });
        });
    }
}

// Task 5: Research Controller
[ApiController]
[Route("api/[controller]")]
public class ResearchController : ControllerBase
{
    private readonly IResearchService _researchService;
    private readonly IValidator<ResearchRequestDto> _validator;
    
    [HttpPost("search")]
    public async Task<ActionResult<ResearchResponseDto>> SearchAsync(
        [FromBody] ResearchRequestDto request, 
        CancellationToken cancellationToken)
    {
        // PATTERN: Always validate input first
        var validationResult = await _validator.ValidateAsync(request, cancellationToken);
        if (!validationResult.IsValid)
            return BadRequest(validationResult.Errors);
        
        try
        {
            var result = await _researchService.SearchAsync(request, cancellationToken);
            return Ok(result);
        }
        catch (ExternalServiceException ex)
        {
            _logger.LogError(ex, "External service error during research");
            return StatusCode(502, "External service unavailable");
        }
        catch (Exception ex)
        {
            _logger.LogError(ex, "Unexpected error during research");
            return StatusCode(500, "Internal server error");
        }
    }
}
```

### Integration Points
```yaml
DATABASE:
  - migration: "Add-Migration InitialCreate"
  - connection: "Server=(localdb)\\mssqllocaldb;Database=MyAppDb;Trusted_Connection=true"
  
CONFIGURATION:
  - add to: appsettings.json
  - pattern: |
      {
        "ConnectionStrings": {
          "DefaultConnection": "Server=(localdb)\\mssqllocaldb;Database=MyAppDb;Trusted_Connection=true"
        },
        "BingSearch": {
          "ApiKey": "your-bing-api-key",
          "BaseUrl": "https://api.bing.microsoft.com/v7.0"
        },
        "MicrosoftGraph": {
          "ClientId": "your-client-id",
          "TenantId": "your-tenant-id",
          "ClientSecret": "your-client-secret"
        }
      }
  
DEPENDENCY_INJECTION:
  - add to: Program.cs  
  - pattern: |
      builder.Services.AddDbContext<ApplicationDbContext>(options =>
          options.UseSqlServer(builder.Configuration.GetConnectionString("DefaultConnection")));
      
      builder.Services.AddScoped<IResearchService, ResearchService>();
      builder.Services.AddScoped<IEmailService, EmailService>();
      builder.Services.AddHttpClient<IBingSearchService, BingSearchService>();
```

## Validation Loop

### Level 1: Build & Style
```bash
# Run these FIRST - fix any errors before proceeding
dotnet build --configuration Release
dotnet format --verify-no-changes

# Expected: No compilation errors. If errors, READ and fix.
```

### Level 2: Unit Tests
```csharp
// ResearchServiceTests.cs
[Fact]
public async Task SearchAsync_ValidQuery_ReturnsResults()
{
    // Arrange
    var mockBingService = new Mock<IBingSearchService>();
    mockBingService.Setup(x => x.SearchAsync(It.IsAny<string>(), It.IsAny<int>(), It.IsAny<CancellationToken>()))
               .ReturnsAsync(new List<SearchResult> { new() { Title = "Test Result" } });
    
    var service = new ResearchService(mockBingService.Object, Mock.Of<IEmailService>());
    var request = new ResearchRequestDto { Query = "test query", MaxResults = 10 };
    
    // Act
    var result = await service.SearchAsync(request);
    
    // Assert
    result.Should().NotBeNull();
    result.Results.Should().HaveCount(1);
    result.Results.First().Title.Should().Be("Test Result");
}

[Fact]
public async Task SearchAsync_EmptyQuery_ThrowsValidationException()
{
    // Arrange
    var service = new ResearchService(Mock.Of<IBingSearchService>(), Mock.Of<IEmailService>());
    var request = new ResearchRequestDto { Query = "", MaxResults = 10 };
    
    // Act & Assert
    await Assert.ThrowsAsync<ValidationException>(() => service.SearchAsync(request));
}

[Fact]
public async Task SearchAsync_BingServiceFailure_HandlesGracefully()
{
    // Arrange
    var mockBingService = new Mock<IBingSearchService>();
    mockBingService.Setup(x => x.SearchAsync(It.IsAny<string>(), It.IsAny<int>(), It.IsAny<CancellationToken>()))
               .ThrowsAsync(new HttpRequestException("Service unavailable"));
    
    var service = new ResearchService(mockBingService.Object, Mock.Of<IEmailService>());
    var request = new ResearchRequestDto { Query = "test", MaxResults = 10 };
    
    // Act & Assert
    var exception = await Assert.ThrowsAsync<ExternalServiceException>(() => service.SearchAsync(request));
    exception.Message.Should().Contain("search service");
}
```

```bash
# Run tests iteratively until passing:
dotnet test --configuration Release --verbosity normal --collect:"XPlat Code Coverage"

# If failing: Debug specific test, fix code, re-run
```

### Level 3: Integration Test
```bash
# Start the API
dotnet run --project src/MyApp.API --environment Development

# Test the research endpoint
curl -X POST https://localhost:7001/api/research/search \
  -H "Content-Type: application/json" \
  -d '{"query": "artificial intelligence", "maxResults": 5, "includeEmailOption": true}'

# Expected: 200 OK with search results
# Test the MAUI app by running:
dotnet run --project src/MyApp.MAUI

# Expected: UI loads, can input search terms, displays results
```

## Final Validation Checklist
- [ ] All tests pass: `dotnet test --configuration Release`
- [ ] No build errors: `dotnet build --configuration Release`
- [ ] Code formatted: `dotnet format --verify-no-changes`
- [ ] API responds correctly: Manual testing with curl/Postman
- [ ] MAUI app launches and functions: Manual UI testing
- [ ] Database migrations work: `dotnet ef database update`
- [ ] External API integration works: Bing Search returns results
- [ ] Microsoft Graph authentication configured: Email sending works
- [ ] Error cases handled gracefully: Test with invalid inputs
- [ ] Logging is informative: Check console and log files
- [ ] Documentation complete: README includes setup steps

---

## Anti-Patterns to Avoid
- ❌ Don't use blocking calls in async methods (avoid .Result, .Wait())
- ❌ Don't skip dependency injection registration
- ❌ Don't hardcode API keys - use configuration
- ❌ Don't ignore cancellation tokens in async methods
- ❌ Don't forget to dispose HttpClient properly (use IHttpClientFactory)
- ❌ Don't catch Exception without logging specific error details
- ❌ Don't forget platform-specific configurations for MAUI

## Confidence Score: 8/10

High confidence due to:
- Clear .NET patterns and Microsoft documentation
- Well-established ASP.NET Core and Entity Framework conventions
- Comprehensive validation gates
- Extensive examples from Microsoft samples

Minor uncertainty on Microsoft Graph first-time authentication flow in MAUI, but documentation provides clear guidance.