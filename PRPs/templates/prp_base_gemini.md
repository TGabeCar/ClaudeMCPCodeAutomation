name: "Base .NET PRP Template - Gemini CLI Compatible"
description: |

## Purpose
Template optimized for Gemini CLI to implement .NET features with sufficient context and self-validation capabilities to achieve working code through iterative refinement.

## Core Principles
1. **Context is King**: Include ALL necessary documentation, examples, and caveats
2. **Validation Loops**: Provide executable tests/builds the AI can run and fix
3. **Information Dense**: Use keywords and patterns from the codebase
4. **Progressive Success**: Start simple, validate, then enhance
5. **Global rules**: Be sure to follow all rules in GEMINI.md

---

## PROJECT_SOURCE:

[Provide a GitHub repo URL or a local path to the project. Leave blank to create a new project.]

## Goal
[What needs to be built - be specific about the end state and desires]

## Why
- [Business value and user impact]
- [Integration with existing .NET services]
- [Problems this solves and for whom]

## What
[User-visible behavior and technical requirements]

### Success Criteria
- [ ] [Specific measurable outcomes]

## All Needed Context

### Documentation & References (list all context needed to implement the feature)
```yaml
# MUST READ - Include these in your context window
- url: [Official documentation URL]
  why: [Specific sections/APIs you'll need]
  
- file: [path/to/ExampleFile.ext]
  why: [Pattern to follow, gotchas to avoid]
  
- doc: [Library documentation URL] 
  section: [Specific section about common pitfalls]
  critical: [Key insight that prevents common errors]

- docfile: [PRPs/ai_docs/file.md]
  why: [docs that the user has pasted in to the project]
```

### Current Solution/Project Structure (run appropriate directory command to get overview)
```bash

```

### Desired Solution/Project Structure with files to be added and responsibility of each
```bash

```

### Known Gotchas & Library Quirks
```csharp
// CRITICAL: [Library name] requires [specific setup]
// Example: Entity Framework requires DbContext registration in DI
// Example: ASP.NET Core requires explicit CORS configuration
// Example: We use nullable reference types - ensure proper null handling
// Example: MAUI requires platform-specific permissions in Platforms folders
```

## Implementation Blueprint

### Data models and structure

Create the core data models, ensuring type safety and consistency.
```csharp
Examples: 
 - Entity Framework models
 - DTOs (Data Transfer Objects)
 - Domain models
 - FluentValidation validators
 - API request/response models
```

### List of tasks to be completed to fulfill the PRP in the order they should be completed

```yaml
Task 1:
  MODIFY src/existing_module.[ext]:
    - FIND pattern: "existing_function_or_class"
    - INJECT after: "specific_location"
    - PRESERVE: existing_configuration_patterns

  CREATE src/new_feature.[ext]:
    - MIRROR: src/similar_feature.[ext]
    - MODIFY: core_logic_and_naming
    - KEEP: error_handling_pattern

# ... additional tasks ...

Task N:
...
```

### Per task pseudocode as needed added to each task
```csharp
// Task 1 pseudocode - C# approach
public async Task<ActionResult<FeatureResponse>> CreateFeatureAsync(CreateFeatureRequest request)
{
    // PATTERN: Always validate input first (see FluentValidation setup)
    var validationResult = await _validator.ValidateAsync(request);
    if (!validationResult.IsValid)
        return BadRequest(validationResult.Errors);
    
    // GOTCHA: Entity Framework requires explicit transaction for complex operations
    using var transaction = await _context.Database.BeginTransactionAsync();
    try
    {
        // PATTERN: Use existing service pattern
        var result = await _featureService.CreateAsync(request);
        
        await transaction.CommitAsync();
        return Ok(result);
    }
    catch (Exception ex)
    {
        await transaction.RollbackAsync();
        _logger.LogError(ex, "Failed to create feature");
        return StatusCode(500, "Internal server error");
    }
}
```

### Integration Points
```yaml
DATABASE:
  - migration: "Add-Migration AddFeatureTable"
  - context: "Add DbSet<Feature> Features to ApplicationDbContext"
  
CONFIGURATION:
  - add to: appsettings.json
  - pattern: |
      "FeatureSettings": {
        "Timeout": 30,
        "MaxRetries": 3
      }
  
DEPENDENCY_INJECTION:
  - add to: Program.cs  
  - pattern: "builder.Services.AddScoped<IFeatureService, FeatureService>();"
```

## Validation Loop

### Level 1: Build & Style
```bash
# .NET specific commands
dotnet build --configuration Release
dotnet format --verify-no-changes

# Expected: No compilation errors. If errors, READ and fix.
```

### Level 2: Unit Tests
```csharp
// CREATE FeatureServiceTests.cs with these test cases:
[Fact]
public async Task CreateFeatureAsync_ValidInput_ReturnsSuccess()
{
    // Arrange
    var request = new CreateFeatureRequest { Name = "Test Feature" };
    
    // Act
    var result = await _service.CreateAsync(request);
    
    // Assert
    result.Should().NotBeNull();
    result.IsSuccess.Should().BeTrue();
}

[Fact]
public async Task CreateFeatureAsync_InvalidInput_ThrowsValidationException()
{
    // Arrange
    var request = new CreateFeatureRequest { Name = "" };
    
    // Act & Assert
    await Assert.ThrowsAsync<ValidationException>(() => _service.CreateAsync(request));
}

[Fact]
public async Task CreateFeatureAsync_DatabaseError_HandlesGracefully()
{
    // Arrange
    _mockContext.Setup(x => x.SaveChangesAsync(default))
              .ThrowsAsync(new DbUpdateException());
    
    // Act & Assert
    var exception = await Assert.ThrowsAsync<ServiceException>(() => _service.CreateAsync(validRequest));
    exception.Message.Should().Contain("database error");
}
```

```bash
# Run tests
dotnet test --configuration Release --verbosity normal

# If failing: Read error, understand root cause, fix code, re-run
```

### Level 3: Integration Test
```bash
# Start the ASP.NET Core application
dotnet run --project src/MyApp.API --environment Development

# Test the endpoint
curl -X POST https://localhost:7001/api/features \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer [token]" \
  -d '{"name": "Test Feature", "description": "Test Description"}'

# Expected: {"id": 1, "name": "Test Feature", "isSuccess": true}
# If error: Check logs in console output for stack trace
```

## Final Validation Checklist
- [ ] All tests pass: `dotnet test --configuration Release`
- [ ] No build errors: `dotnet build --configuration Release`
- [ ] Code formatted: `dotnet format --verify-no-changes`
- [ ] Manual test successful: [specific curl/Postman command]
- [ ] Error cases handled gracefully
- [ ] Logging is informative but not verbose
- [ ] Documentation updated if needed
- [ ] NuGet packages properly referenced

---

## Anti-Patterns to Avoid
- ❌ Don't create new patterns when existing .NET conventions work
- ❌ Don't skip validation because "it should compile"  
- ❌ Don't ignore failing tests - fix them
- ❌ Don't use blocking calls in async methods (use ConfigureAwait(false))
- ❌ Don't hardcode values that should be in appsettings.json
- ❌ Don't catch Exception without logging - be specific
- ❌ Don't forget to register services in dependency injection

## Confidence Score: [X/10]
[Explain confidence level and any concerns]