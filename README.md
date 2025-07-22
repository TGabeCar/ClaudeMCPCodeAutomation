# Context Engineering Template - Microsoft Stack

A comprehensive template for getting started with Context Engineering for .NET applications - the discipline of engineering context for AI coding assistants so they have the information necessary to get the job done end to end with C#, ASP.NET Core, Entity Framework, and MAUI.

> **Context Engineering is 10x better than prompt engineering and 100x better than vibe coding.**

## 🔀 Dual AI Platform Support

This repository supports both **Claude Code** and **Gemini CLI** for .NET development:

- **Claude Code**: Use `.claude/` directory with `/generate-prp` commands  
- **Gemini CLI**: Use `.gemini/` directory with `gemini context generate-prp` commands

**Both systems focus on the same Microsoft technology stack** (C#, MAUI, SQL Server, ASP.NET Core, Entity Framework).

## 🚀 Quick Start

### Claude Code (Original System)
```bash
# 1. Clone this template
git clone https://github.com/TGabeCar/ClaudeMCPCodeAutomation.git
cd ClaudeMCPCodeAutomation

# 2. Set up your project rules (optional - template provided)
# Edit CLAUDE.md to add your project-specific guidelines

# 3. Add examples (highly recommended)
# Place relevant C# code examples in the examples/ folder

# 4. Create your initial feature request
# Edit INITIAL.md with your feature requirements

# 5. Generate a comprehensive PRP (Product Requirements Prompt)
# In Claude Code, run:
/generate-prp INITIAL.md

# 6. Execute the PRP to implement your feature
# In Claude Code, run:
/execute-prp PRPs/your-feature-name.md
```

### Gemini CLI (New Option)
```bash
# 1. Same clone and setup steps as above

# 2. Edit GEMINI.md for Gemini-specific project rules (optional)

# 3. Add examples (same examples/ folder as Claude Code)

# 4. Create your initial feature request (same INITIAL.md format)

# 5. Generate PRP using Gemini CLI:
gemini context generate-prp INITIAL.md

# 6. Execute PRP using Gemini CLI:
gemini context execute-prp PRPs/your-feature-name.md
```

## 📚 Table of Contents

- [What is Context Engineering?](#what-is-context-engineering)
- [Template Structure](#template-structure)
- [Choosing Your AI Platform](#choosing-your-ai-platform)
- [Step-by-Step Guide](#step-by-step-guide)
- [Writing Effective INITIAL.md Files](#writing-effective-initialmd-files)
- [The PRP Workflow](#the-prp-workflow)
- [Using Examples Effectively](#using-examples-effectively)
- [Best Practices](#best-practices)

## What is Context Engineering?

Context Engineering represents a paradigm shift from traditional prompt engineering:

### Prompt Engineering vs Context Engineering

**Prompt Engineering:**
- Focuses on clever wording and specific phrasing
- Limited to how you phrase a task
- Like giving someone a sticky note

**Context Engineering:**
- A complete system for providing comprehensive context
- Includes documentation, examples, rules, patterns, and validation
- Like writing a full screenplay with all the details

### Why Context Engineering Matters

1. **Reduces AI Failures**: Most agent failures aren't model failures - they're context failures
2. **Ensures Consistency**: AI follows your .NET project patterns and conventions
3. **Enables Complex Features**: AI can handle multi-project implementations with proper context
4. **Self-Correcting**: Validation loops allow AI to fix its own mistakes

## Template Structure

```
ClaudeMCPCodeAutomation/
├── .claude/                       # Claude Code support
│   ├── commands/
│   │   ├── generate-prp.md       # Generates comprehensive PRPs
│   │   └── execute-prp.md        # Executes PRPs to implement features
│   └── settings.local.json       # Claude Code permissions
├── .gemini/                      # Gemini CLI support
│   ├── commands/
│   │   ├── generate-prp.md       # Generates comprehensive PRPs
│   │   └── execute-prp.md        # Executes PRPs to implement features
│   └── settings.local.json       # Gemini CLI permissions
├── PRPs/
│   ├── templates/
│   │   ├── prp_base_claude.md    # Base template for Claude Code PRPs
│   │   └── prp_base_gemini.md    # Base template for Gemini CLI PRPs
│   └── EXAMPLE_api_service_prp.md # Example of a complete PRP
├── examples/                      # Your C# code examples (shared by both systems)
├── CLAUDE.md                     # Global rules for Claude Code
├── GEMINI.md                     # Global rules for Gemini CLI
├── INITIAL.md                    # Template for feature requests (shared)
├── INITIAL_EXAMPLE_CLAUDE.md     # Example feature request for Claude Code
├── INITIAL_EXAMPLE_GEMINI.md     # Example feature request for Gemini CLI
└── README.md                     # This file
```

This template focuses on .NET-specific patterns for both AI platforms.

## Choosing Your AI Platform

Both systems support the same Microsoft technology stack but offer different interfaces:

| Feature | Claude Code | Gemini CLI |
|---------|-------------|-----------|
| **Technology Focus** | .NET/C# | .NET/C# |
| **Command Style** | `/generate-prp` | `gemini context generate-prp` |
| **Validation Tools** | dotnet build/test | dotnet build/test |
| **Templates** | .NET patterns | Same .NET patterns |
| **Workspace Handling** | Windows-focused | Cross-platform |

### Use Claude Code When:
- You prefer Claude's .NET expertise and patterns
- Working in Windows-centric development environment  
- Want proven Claude Code integration
- Prefer the `/command` syntax

### Use Gemini CLI When:
- You want to try Gemini's approach to .NET development
- Need cross-platform workspace handling
- Prefer the `gemini context` command syntax
- Want to experiment with Gemini's code generation

## Step-by-Step Guide

### 1. Set Up Global Rules

Choose the appropriate global rules file for your AI platform:

**Claude Code**: The `CLAUDE.md` file contains project-wide rules that Claude will follow. It includes:
- **Project awareness**: Reading planning docs, checking tasks
- **Code structure**: Project organization, namespace conventions  
- **Testing requirements**: xUnit test patterns, coverage expectations
- **Style conventions**: C# language preferences, formatting rules
- **Documentation standards**: XML documentation formats, commenting practices

**Gemini CLI**: The `GEMINI.md` file contains the same .NET-focused rules adapted for Gemini CLI usage.

**You can use the provided templates as-is or customize them for your specific .NET project.**

### 2. Create Your Initial Feature Request

Edit `INITIAL.md` to describe what you want to build (same format for both AI platforms):

```markdown
## PROJECT_SOURCE:
[GitHub URL, local path, or blank for new project]

## FEATURE:
[Describe what you want to build - be specific about functionality and requirements]

## RELEVANT_CODE:
[Files/directories to focus on during analysis]

## EXAMPLES:
[List any example files in the examples/ folder and explain how they should be used]

## DOCUMENTATION:
[Include links to relevant Microsoft documentation, NuGet packages, or API resources]

## OTHER CONSIDERATIONS:
[Mention any gotchas, specific requirements, or things AI assistants commonly miss with .NET]
```

**See `INITIAL_EXAMPLE_CLAUDE.md` or `INITIAL_EXAMPLE_GEMINI.md` for complete examples.**

### 3. Generate the PRP

PRPs (Product Requirements Prompts) are comprehensive implementation blueprints that include:

- Complete context and documentation
- Implementation steps with validation
- Error handling patterns  
- Test requirements

They are similar to PRDs (Product Requirements Documents) but are crafted specifically to instruct an AI coding assistant for .NET development.

**Claude Code:**
```bash
/generate-prp INITIAL.md
```

**Gemini CLI:**
```bash
gemini context generate-prp INITIAL.md
```

**Note:** The commands are defined in their respective directories:
- `.claude/commands/` - Claude Code command implementations
- `.gemini/commands/` - Gemini CLI command implementations

Both will:
1. Read your feature request
2. Research the codebase for .NET patterns
3. Search for relevant Microsoft documentation
4. Create a comprehensive PRP in `PRPs/your-feature-name.md`

### 4. Execute the PRP

Once generated, execute the PRP to implement your feature:

**Claude Code:**
```bash
/execute-prp PRPs/your-feature-name.md
```

**Gemini CLI:**
```bash
gemini context execute-prp PRPs/your-feature-name.md
```

Both AI platforms will:
1. Read all context from the PRP
2. Create a detailed implementation plan
3. Execute each step with validation
4. Run tests and fix any issues
5. Ensure all success criteria are met

## Writing Effective INITIAL.md Files

### Key Sections Explained

**PROJECT_SOURCE**: Specify where your code lives
- GitHub URL for existing repositories
- Local path for existing projects
- Leave blank for new projects

**FEATURE**: Be specific and comprehensive
- ❌ "Build a web API"
- ✅ "Build an ASP.NET Core Web API using Entity Framework Core that manages product inventory, implements JWT authentication, and provides real-time updates via SignalR"

**RELEVANT_CODE**: Guide the AI's focus
- List specific files, folders, or functions
- Help the AI understand where to look for patterns

**EXAMPLES**: Leverage the examples/ folder
- Place relevant C# code patterns in `examples/`
- Reference specific files and patterns to follow
- Explain what aspects should be mimicked

**DOCUMENTATION**: Include all relevant resources
- Microsoft Docs URLs
- NuGet package documentation
- API documentation
- Database schema references

**OTHER CONSIDERATIONS**: Capture important details
- Authentication requirements
- Performance requirements
- Common .NET pitfalls
- Cross-platform considerations for MAUI

## The PRP Workflow

### How PRP Generation Works

Both AI platforms follow this process:

1. **Research Phase**
   - Analyzes your codebase for .NET patterns
   - Searches for similar implementations
   - Identifies conventions to follow

2. **Documentation Gathering**
   - Fetches relevant Microsoft documentation
   - Includes NuGet package documentation
   - Adds .NET-specific gotchas and quirks

3. **Blueprint Creation**
   - Creates step-by-step implementation plan
   - Includes validation gates
   - Adds test requirements

4. **Quality Check**
   - Scores confidence level (1-10)
   - Ensures all context is included

### How PRP Execution Works

1. **Load Context**: Reads the entire PRP
2. **Plan**: Creates detailed task list
3. **Execute**: Implements each component
4. **Validate**: Runs tests and analyzers (`dotnet build`, `dotnet test`, etc.)
5. **Iterate**: Fixes any issues found
6. **Complete**: Ensures all requirements met

See `PRPs/EXAMPLE_api_service_prp.md` for a complete example of what gets generated.

## Using Examples Effectively

The `examples/` folder is **critical** for success. Both AI platforms perform much better when they can see .NET patterns to follow.

### What to Include in Examples

1. **Project Structure Patterns**
   - How you organize solutions and projects
   - Namespace conventions
   - Dependency injection patterns

2. **Testing Patterns**
   - xUnit test project structure
   - Mocking approaches with Moq
   - Integration testing patterns

3. **API Patterns**
   - Controller implementations
   - Service layer patterns
   - Authentication and authorization

4. **Data Access Patterns**
   - Entity Framework contexts
   - Repository patterns
   - Migration strategies

### Example Structure

```
examples/
├── README.md           # Explains what each example demonstrates
├── Program.cs         # Startup and DI configuration pattern
├── Controllers/       # API controller patterns
│   └── ProductController.cs
├── Services/          # Service layer patterns
│   ├── IProductService.cs
│   └── ProductService.cs
├── Models/            # Domain models and DTOs
│   └── Product.cs
└── Tests/            # Testing patterns
    ├── ProductServiceTests.cs
    └── ProductControllerTests.cs
```

## Best Practices

### 1. Be Explicit in INITIAL.md
- Don't assume the AI knows your .NET preferences
- Include specific requirements and constraints
- Reference examples liberally

### 2. Provide Comprehensive Examples
- More examples = better implementations
- Show both what to do AND what not to do
- Include error handling patterns

### 3. Use Validation Gates
- PRPs include commands that must pass
- AI will iterate until all validations succeed
- This ensures working code on first try

### 4. Leverage Microsoft Documentation
- Include official Microsoft Docs links
- Add NuGet package resources
- Reference specific documentation sections

### 5. Customize Global Rules
- Add your .NET conventions to `CLAUDE.md` or `GEMINI.md`
- Include project-specific rules
- Define coding standards

### 6. Choose Your AI Platform
- Both support the same .NET stack
- Pick based on interface preference and workflow needs
- You can switch between platforms for different projects

## Validation

Both AI platforms use the same .NET validation tools:

```bash
# Build and test validation
dotnet build --configuration Release
dotnet test --configuration Release --verbosity normal
dotnet format --verify-no-changes

# Entity Framework migrations (if applicable)
dotnet ef database update

# Code analysis (if configured)
dotnet run --project CodeAnalysis
```

## Resources

- [Claude Code Documentation](https://docs.anthropic.com/en/docs/claude-code)
- [Gemini CLI Documentation](https://cloud.google.com/gemini/docs/codeassist/gemini-cli)
- [ASP.NET Core Documentation](https://docs.microsoft.com/en-us/aspnet/core/)
- [Entity Framework Core Documentation](https://docs.microsoft.com/en-us/ef/core/)
- [.NET MAUI Documentation](https://docs.microsoft.com/en-us/dotnet/maui/)
- [Context Engineering Best Practices](https://www.philschmid.de/context-engineering)