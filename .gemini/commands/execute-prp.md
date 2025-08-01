# Execute .NET PRP

Implement a feature using the PRP file for .NET applications.

## PRP File: $ARGUMENTS

## Execution Process

0. **Prepare Workspace** ⚙️
   - **First, determine the project name.** Derive a unique name from the PRP filename. (e.g., for `PRPs/api-user-auth.md`, the name is `api-user-auth`).
   - **Next, define the full workspace path.** All work for this task will occur in a dedicated folder at: `./workspace/{project-name}`.
   - **Then, populate the workspace based on the project source:**
     - READ: The `PROJECT_SOURCE` field from the PRP file ($ARGUMENTS).
     - **IF `PROJECT_SOURCE` is a GitHub URL:**
       - CLONE the repository directly into the workspace path.
       - `git clone <URL> ./workspace/{project-name}`
       - **CRITICAL**: You MUST NOT perform any `git push` operations.
     - **IF `PROJECT_SOURCE` is a local path:**
       - COPY the entire contents of the original project into the workspace path.
       - `cp -r <path> ./workspace/{project-name}` (or equivalent)
       - **CRITICAL**: You MUST NOT modify the original source folder.
     - **IF `PROJECT_SOURCE` is blank (for a new project):**
       - CREATE the empty workspace directory at the path.
       - `mkdir -p ./workspace/{project-name}`
   - **Finally, set this prepared workspace path as the current working directory for all subsequent steps.**

1. **Load Context**
   - READ: The specified PRP file ($ARGUMENTS)
   - READ: GEMINI.md - Global project rules
   - VERIFY: All referenced files in PRP exist

2. **Load PRP**
   - Read the specified PRP file
   - Understand all context and requirements
   - Follow all instructions in the PRP and extend the research if needed
   - Ensure you have all needed context to implement the PRP fully
   - Do more web searches and codebase exploration as needed

3. **ULTRATHINK**
   - Think hard before you execute the plan. Create a comprehensive plan addressing all requirements.
   - Break down complex tasks into smaller, manageable steps.
   - Identify implementation patterns from existing code to follow.

4. **Execute the plan**
   - Execute the PRP
   - Implement all the code, projects, and configurations

4a. **Compact Context** 🧠
    - To conserve context for the next steps, summarize the implementation phase before validation.

5. **Validate**
   - Run each validation command (dotnet build, dotnet test, etc.)
   - Fix any compilation errors or test failures
   - Re-run until all pass

6. **Complete**
   - Ensure all checklist items done
   - Run final validation suite
   - Report completion status
   - Read the PRP again to ensure you have implemented everything

7. **Reference the PRP**
   - You can always reference the PRP again if needed

## .NET Validation Commands

### Build and Test
```bash
# Restore NuGet packages
dotnet restore

# Build solution
dotnet build --configuration Release

# Run unit tests
dotnet test --configuration Release --verbosity normal

# Format code
dotnet format
```

### Code Analysis (if configured)
```bash
# Static code analysis
dotnet run --project CodeAnalysis

# Entity Framework migrations (if applicable)
dotnet ef database update
```

Note: If validation fails, use error patterns in PRP to fix and retry. Pay special attention to .NET-specific issues like nullable reference types, dependency injection, and async/await patterns.