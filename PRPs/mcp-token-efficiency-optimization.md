name: "MCP Server Token Efficiency Optimization PRP"
description: |

## Purpose
Optimize the MCP Server Automated Workflow Coding Assistant to use fewer tokens while maintaining the same quality of results. Focus on strategic optimizations to reduce input/output token consumption across all workflows.

## Core Principles
1. **Token Efficiency First**: Reduce token usage without sacrificing functionality
2. **Smart Context Management**: Use dynamic context loading and strategic clearing
3. **Lean Templates**: Streamline verbose templates while preserving essential patterns
4. **Progressive Optimization**: Start with high-impact, low-risk changes
5. **Quality Preservation**: Maintain code quality and AI assistant effectiveness

---

## PROJECT_SOURCE:

C:\Users\Gabe\source\repos\MCPServerAutomation-master -COPY

## Goal
Transform the MCP Server Automated Workflow Coding Assistant into a token-efficient system that delivers the same quality results while significantly reducing AI usage costs and token consumption.

## Why
- **Cost Reduction**: Token consumption directly impacts operational costs for AI coding assistants
- **Performance Improvement**: Smaller context windows lead to faster response times and better focus
- **Scalability**: More efficient token usage allows handling larger projects within context limits
- **User Experience**: Faster responses and reduced wait times improve developer productivity
- **Resource Optimization**: Better allocation of compute resources across development tasks

## What
Implement comprehensive token optimization across all system components:

### Success Criteria
- [ ] Reduce average token usage by 40-60% while maintaining code quality
- [ ] Create lightweight command variants for common tasks
- [ ] Implement strategic context management with auto-clearing
- [ ] Optimize templates to be 50% more concise
- [ ] Add lightweight tracking system for common issues/solutions
- [ ] Reduce test generation to validation-essential tests only
- [ ] Maintain identical final code quality and functionality

## All Needed Context

### Documentation & References (list all context needed to implement the feature)
```yaml
# MUST READ - Include these in your context window
- url: https://docs.anthropic.com/en/docs/claude-code/costs
  why: Token management best practices and cost optimization strategies
  
- url: https://www.philschmid.de/context-engineering
  why: Context engineering principles for token efficiency
  
- url: https://docs.anthropic.com/en/docs/claude-code
  section: Memory management, /clear, /compact commands
  critical: Strategic context clearing to prevent token accumulation
  
- file: CLAUDE.md
  why: Current project rules and conventions to optimize
  
- file: .claude/commands/generate-prp.md
  why: Current verbose PRP generation process to streamline
  
- file: .claude/commands/execute-prp.md
  why: Current execution workflow to optimize
  
- file: PRPs/templates/prp_base_claude.md
  why: Verbose template structure that needs optimization
  
- file: .gemini/commands/generate-prp.md
  why: Gemini CLI version for comparison and optimization

- docfile: README.md
  why: System overview and architecture understanding
```

### Current Solution/Project Structure
```bash
MCPServerAutomation-master/
├── .claude/commands/           # Claude Code command definitions (VERBOSE)
├── .gemini/commands/           # Gemini CLI command definitions (VERBOSE)
├── PRPs/templates/             # Template files (VERY VERBOSE)
├── CLAUDE.md                   # Global rules (COMPREHENSIVE)
├── GEMINI.md                   # Gemini rules (COMPREHENSIVE)
├── README.md                   # Documentation (EXTENSIVE)
└── examples/                   # Code examples directory
```

### Desired Solution/Project Structure with files to be added
```bash
MCPServerAutomation-master/
├── .claude/commands/
│   ├── generate-prp.md         # OPTIMIZED: Reduced verbosity by 50%
│   ├── execute-prp.md          # OPTIMIZED: Strategic compacting
│   ├── generate-prp-quick.md   # NEW: Lightweight version for small tasks
│   └── execute-prp-quick.md    # NEW: Streamlined execution workflow
├── .gemini/commands/           # Same optimizations as Claude
├── PRPs/templates/
│   ├── prp_base_claude.md      # OPTIMIZED: 60% more concise
│   ├── prp_base_gemini.md      # OPTIMIZED: 60% more concise
│   ├── prp_quick_claude.md     # NEW: Minimal template for simple tasks
│   └── prp_quick_gemini.md     # NEW: Minimal template for simple tasks
├── optimization/
│   ├── command-patterns.md     # NEW: Common command patterns and solutions
│   ├── token-tracking.md       # NEW: Lightweight usage tracking
│   └── quick-reference.md      # NEW: Condensed reference for AI
├── CLAUDE.md                   # OPTIMIZED: More focused rules
├── GEMINI.md                   # OPTIMIZED: More focused rules
└── README.md                   # OPTIMIZED: Essential information only
```

### Known Gotchas & Token Efficiency Patterns
```markdown
// CRITICAL: Claude Code auto-compacts at 95% context capacity
// PATTERN: Use /clear frequently between unrelated tasks
// GOTCHA: Full conversation history is sent with each request (stateless)
// OPTIMIZATION: Break complex tasks into focused interactions
// PATTERN: Use specific, targeted queries instead of broad requests
// GOTCHA: AI repeatedly tries wrong commands (cp vs xcopy on Windows)
// PATTERN: Include successful command patterns in quick reference
// OPTIMIZATION: Load context dynamically, not all at once
// PATTERN: Use summaries instead of full documentation dumps
```

## Implementation Blueprint

### Data models and structure

Focus on configuration and tracking structures:
```csharp
Examples: 
 - Command pattern configuration files
 - Token usage tracking structures
 - Quick reference lookup tables
 - Optimization metrics tracking
 - Context management rules
```

### List of tasks to be completed to fulfill the PRP in the order they should be completed

```yaml
Task 1: Analyze Current Token Usage Patterns
  ANALYZE: Current command verbosity and token consumption
  IDENTIFY: Highest impact optimization opportunities
  DOCUMENT: Baseline metrics for comparison

Task 2: Create Optimized Command Templates
  MODIFY: .claude/commands/generate-prp.md
    - REDUCE verbosity by 50% while preserving essential patterns
    - ADD strategic /compact usage points
    - OPTIMIZE research process instructions
  
  MODIFY: .claude/commands/execute-prp.md
    - STREAMLINE workspace setup instructions
    - ADD automatic context clearing at validation steps
    - REDUCE redundant instruction repetition

Task 3: Create Quick Command Variants
  CREATE: .claude/commands/generate-prp-quick.md
    - MIRROR: Simplified version of generate-prp
    - FOCUS: Tasks under 3 steps or 200 lines of code
    - OPTIMIZE: 70% reduction in template verbosity
  
  CREATE: .claude/commands/execute-prp-quick.md
    - FOCUS: Simple implementations without complex validation
    - SKIP: Extensive testing for small modifications
    - ADD: Automatic /compact after implementation

Task 4: Optimize PRP Templates
  MODIFY: PRPs/templates/prp_base_claude.md
    - CONDENSE: Verbose sections while keeping critical patterns
    - RESTRUCTURE: Use bullet points instead of paragraph explanations
    - OPTIMIZE: Remove redundant examples and explanations
  
  CREATE: PRPs/templates/prp_quick_claude.md
    - DESIGN: Minimal template for simple features
    - INCLUDE: Essential validation only
    - TARGET: 80% reduction in template size

Task 5: Implement Lightweight Issue Tracking
  CREATE: optimization/command-patterns.md
    - DOCUMENT: Frequently failing commands and successful alternatives
    - INCLUDE: Windows-specific command patterns (xcopy vs cp)
    - FORMAT: Quick lookup table format for AI reference
  
  CREATE: optimization/token-tracking.md
    - DESIGN: Simple tracking system for token usage metrics
    - INCLUDE: Before/after optimization measurements
    - FORMAT: Lightweight data structure

Task 6: Optimize Global Rules
  MODIFY: CLAUDE.md
    - CONDENSE: Verbose explanations into bullet points
    - PRIORITIZE: Most critical rules first
    - REDUCE: Example code to essential patterns only
  
  MODIFY: GEMINI.md
    - APPLY: Same optimizations as CLAUDE.md
    - MAINTAIN: Platform-specific differences

Task 7: Create Quick Reference System
  CREATE: optimization/quick-reference.md
    - COMPILE: Essential patterns in lookup format
    - INCLUDE: Common command solutions
    - FORMAT: JSON-like structure for quick AI parsing

Task 8: Reduce Test Generation Requirements
  MODIFY: All PRP templates to specify:
    - ONLY generate tests needed for validation
    - SKIP comprehensive test suites for small changes
    - FOCUS on integration tests over unit tests for AI validation

Task 9: Implement Strategic Context Management
  ADD: Automatic /compact instructions at key workflow points
  ADD: /clear recommendations between unrelated tasks
  MODIFY: Commands to include context size monitoring

Task 10: Documentation and Deployment
  UPDATE: README.md with optimization features
  CREATE: Migration guide for existing workflows
  TEST: All optimized commands with real scenarios
```

### Per task pseudocode as needed added to each task

```markdown
// Task 4: Template Optimization Pattern
BEFORE (Verbose):
```
### Success Criteria
- [ ] All tests pass: `dotnet test --configuration Release`
- [ ] No build errors: `dotnet build --configuration Release`
- [ ] Code formatted: `dotnet format --verify-no-changes`
- [ ] Manual test successful: [specific curl/Postman command]
- [ ] Error cases handled gracefully
- [ ] Logging is informative but not verbose
```

AFTER (Optimized):
```
### Success Criteria
- [ ] Build: `dotnet build --configuration Release`
- [ ] Tests: `dotnet test --configuration Release`
- [ ] Format: `dotnet format --verify-no-changes`
- [ ] Manual test successful
```

// Task 5: Issue Tracking Pattern
```json
{
  "common_failures": {
    "clone_folder": {
      "fails": ["cp -r", "copy"],
      "succeeds": ["xcopy /E /I", "robocopy"],
      "platform": "windows"
    },
    "build_errors": {
      "missing_reference": "Check project.csproj references",
      "namespace_errors": "Verify using statements"
    }
  }
}
```
```

### Integration Points
```yaml
COMMANDS:
  - modify: All .claude/commands/*.md files
  - add: Quick variants with -quick suffix
  
TEMPLATES:
  - optimize: Existing PRP templates (50-60% reduction)
  - create: Quick templates for simple tasks
  
DOCUMENTATION:
  - update: Global rule files (CLAUDE.md, GEMINI.md)
  - create: Quick reference and tracking systems
  
TRACKING:
  - implement: Token usage monitoring
  - add: Command success/failure patterns
```

## Validation Loop

### Level 1: Command Validation
```bash
# Test optimized commands generate functional PRPs
# Compare token usage before/after optimization
# Verify quick commands work for simple tasks

# Expected: 40-60% reduction in generated token count
# Expected: Identical code quality in final output
```

### Level 2: Template Testing
```bash
# Generate PRPs using optimized templates
# Compare comprehensiveness with original versions
# Test quick templates on simple features

# Expected: Templates produce working implementation plans
# Expected: No loss of essential context or patterns
```

### Level 3: Integration Testing
```bash
# Run complete workflows with optimized system
# Monitor token consumption throughout process
# Test issue tracking and quick reference systems

# Expected: Significant token savings across entire workflow
# Expected: AI assistant maintains same code quality
```

## Final Validation Checklist
- [ ] Token usage reduced by target percentage (40-60%)
- [ ] All optimized commands generate functional PRPs
- [ ] Quick command variants work for simple tasks
- [ ] Code quality remains identical to original system
- [ ] Issue tracking system captures common problems
- [ ] Documentation reflects optimization features
- [ ] Gemini CLI versions match Claude Code optimizations

---

## Anti-Patterns to Avoid
- ❌ Don't sacrifice essential context for token savings
- ❌ Don't remove validation that prevents broken code
- ❌ Don't make commands so terse they become unclear
- ❌ Don't optimize at the expense of maintainability
- ❌ Don't remove error handling patterns
- ❌ Don't eliminate project-specific conventions

## Token Efficiency Patterns to Follow
- ✅ Use bullet points instead of verbose paragraphs
- ✅ Provide examples only when essential for understanding
- ✅ Use strategic /clear and /compact commands
- ✅ Load context dynamically based on task needs
- ✅ Create task-specific templates instead of one-size-fits-all
- ✅ Use quick reference lookup tables for common patterns
- ✅ Implement progressive disclosure of information
- ✅ Track and reuse successful command patterns

## Confidence Score: 9/10

High confidence due to:
- Clear optimization targets backed by research
- Well-defined scope with measurable outcomes
- Preservation of existing functionality
- Strategic approach to token reduction
- Comprehensive validation framework

Minor concerns:
- Need to balance optimization with maintainability
- Risk of over-optimization losing essential context
- Require careful testing to ensure quality preservation