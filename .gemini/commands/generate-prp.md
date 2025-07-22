# Create .NET PRP for Gemini CLI

## Feature file: $ARGUMENTS

Generate a complete PRP for .NET feature implementation with thorough research. Ensure context is passed to the AI agent to enable self-validation and iterative refinement. Read the feature file first to understand what needs to be created, how the examples provided help, and any other considerations.

The AI agent only gets the context you are appending to the PRP and training data. Assume the AI agent has access to the codebase and the same knowledge cutoff as you, so it's important that your research findings are included or referenced in the PRP. The Agent has web search capabilities, so pass URLs to Microsoft documentation and examples.

## Research Process

1. **Read Project Context**
   - READ: GEMINI.md - Global rules and conventions
   - READ: README.md - Project overview and setup
   - READ: INITIAL.md or $ARGUMENTS - The feature request
   - READ: PRPs/templates/prp_base_gemini.md - PRP structure template

2. **Focused Codebase Analysis** 🎯
   - Use the file and directory paths from the `RELEVANT_CODE` section as your primary search area.
   - Analyze these specific areas to identify projects, services, patterns, and conventions to reference in the PRP.
   - Note existing conventions to follow from this focused context.
   - If the provided paths are insufficient, you may explore parent or related directories, but always prioritize the specified context.

3. **External Research**
   - Search for similar .NET features/patterns online
   - Microsoft documentation (include specific URLs)
   - Implementation examples (GitHub/Stack Overflow/Microsoft samples)
   - Best practices and common .NET pitfalls

4. **User Clarification** (if needed)
   - Specific patterns to mirror and where to find them?
   - Integration requirements and where to find them?

## PRP Generation

Using PRPs/templates/prp_base_gemini.md as template:

### Critical Context to Include and pass to the AI agent as part of the PRP
- **Project Source**: Copy the `PROJECT_SOURCE` section from the feature file (`$ARGUMENTS`) directly into the PRP. This is critical for the `execute-prp` command.
- **Relevant Code**: Copy the `RELEVANT_CODE` list from the feature file into the PRP so the executor AI also knows where to focus.
- **Documentation**: Official documentation URLs with specific sections
- **Code Examples**: Real code snippets from codebase
- **Gotchas**: Language/framework library quirks, version issues, common pitfalls
- **Patterns**: Existing approaches to follow

### Implementation Blueprint
- Start with pseudocode showing language-appropriate approach
- Reference real projects and files for patterns
- Include error handling strategy
- List tasks to be completed to fulfill the PRP in the order they should be completed

### Validation Gates (Must be Executable) for .NET
```bash
# Build and Analyze
dotnet build --configuration Release
dotnet format --verify-no-changes

# Unit Tests
dotnet test --configuration Release --verbosity normal

# Code Analysis (if configured)
dotnet run --project CodeAnalysis
```

*** CRITICAL AFTER YOU ARE DONE RESEARCHING AND EXPLORING THE CODEBASE BEFORE YOU START WRITING THE PRP ***

*** ULTRATHINK ABOUT THE PRP AND PLAN YOUR APPROACH THEN START WRITING THE PRP ***

## Output
Save as: `PRPs/{feature-name}.md`

## Quality Checklist
- [ ] All necessary .NET context included
- [ ] Validation gates are executable by AI
- [ ] References existing .NET patterns
- [ ] Clear implementation path
- [ ] Error handling documented
- [ ] NuGet package dependencies identified
- [ ] Project structure defined

Score the PRP on a scale of 1-10 (confidence level to succeed in one-pass implementation using Gemini CLI)

Remember: The goal is one-pass implementation success through comprehensive .NET context.