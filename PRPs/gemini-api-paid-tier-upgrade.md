name: "Gemini API Paid Tier Upgrade - Cost-Optimized Implementation"
description: |

## Purpose
Upgrade the "I'm That Kid AI" application from Gemini API free tier to the most cost-effective paid tier, maintaining all existing functionality while unlocking higher rate limits for production usage.

## Core Principles
1. **Cost Optimization**: Use Gemini 1.5 Flash as primary model (cheapest option with 70% recent price reduction)
2. **Maintain Functionality**: Preserve all existing prompt building, personalization, and error handling systems
3. **Rate Limit Optimization**: Update quotas to match paid tier limits for improved user experience
4. **Validation Loops**: Ensure smooth transition with comprehensive testing
5. **Global rules**: Follow all rules in CLAUDE.md

---

## PROJECT_SOURCE:

C:\Users\Gabe\source\repos\ImThatKidAI\GeminiService.cs
C:\Users\Gabe\source\repos\ImThatKidAI-SecurityFunctions\GeminiProxyFunction.cs

## Goal
Upgrade the Gemini API integration from free tier to paid tier, specifically targeting the most cost-effective option (Gemini 1.5 Flash) while maintaining all existing functionality and improving rate limits for production usage.

## Why
- **Production Readiness**: Free tier limits (15 RPM, 60 RPD) are insufficient for production app usage
- **Cost Optimization**: Gemini 1.5 Flash offers the best price-performance ratio with recent 70% price reduction
- **User Experience**: Higher rate limits reduce fallback responses and improve app reliability
- **Data Privacy**: Paid tier ensures prompts aren't used to improve Google products
- **Scalability**: Support for growing user base with higher throughput requirements

## What
Upgrade the Gemini API integration to use paid tier with optimized configuration:

### Success Criteria
- [ ] Update ModelQuota class constants to reflect paid tier limits
- [ ] Modify model preference order to prioritize Gemini 1.5 Flash (most cost-effective)
- [ ] Verify Azure Function proxy handles paid tier configuration
- [ ] Maintain all existing personalization and error handling features
- [ ] Test rate limit improvements with realistic load
- [ ] Ensure backward compatibility with existing user sessions
- [ ] Validate cost optimization through model selection strategy

## All Needed Context

### Documentation & References (list all context needed to implement the feature)
```yaml
# MUST READ - Include these in your context window
- url: https://ai.google.dev/gemini-api/docs/pricing
  why: Official Gemini API pricing structure and paid tier benefits
  
- url: https://ai.google.dev/gemini-api/docs/rate-limits
  why: Specific rate limits for free vs paid tiers across all models
  
- file: C:\Users\Gabe\source\repos\ImThatKidAI\GeminiService.cs
  why: Current quota management system and model selection logic
  
- file: C:\Users\Gabe\source\repos\ImThatKidAI-SecurityFunctions\GeminiProxyFunction.cs
  why: Azure Function proxy implementation that needs to support paid tier
  
- doc: https://ai.google.dev/gemini-api/docs/billing
  section: Billing activation and paid tier setup requirements
  critical: Must enable billing in Google Cloud Console to access paid tier
```

### Current Solution/Project Structure (run appropriate directory command to get overview)
```bash
# Current implementation uses Azure Functions proxy pattern:
# MAUI App → SecureAIService → Azure Function → Gemini API
# 
# Key files:
# - GeminiService.cs: Client-side service with quota management
# - GeminiProxyFunction.cs: Azure Function proxy with API key security
```

### Desired Solution/Project Structure with files to be added and responsibility of each
```bash
# No new files needed - updating existing components:
# 
# GeminiService.cs: 
#   - Update ModelQuota constants for paid tier limits
#   - Optimize model preference order for cost efficiency
#   - Enhance quota tracking for higher limits
#
# GeminiProxyFunction.cs:
#   - Verify configuration supports paid tier usage
#   - Enhance logging for paid tier monitoring
```

### Known Gotchas of our .NET codebase & Library Quirks
```csharp
// CRITICAL: Paid tier requires billing enabled in Google Cloud Console
// Example: User must manually enable billing before API calls will use paid tier
// Example: ModelQuota class has hardcoded free tier limits that need updating
// Example: Quota tracking system needs to handle much higher limits (15 RPM → 2000 RPM)
// Example: SecureAIService timeout values may need adjustment for higher throughput
// CRITICAL: Model preference order affects costs - Gemini 1.5 Flash is cheapest
// Example: Current quota persistence may overflow with higher daily limits
```

## Implementation Blueprint

### Data models and structure

Update existing quota management to handle paid tier limits:
```csharp
Examples: 
 - ModelQuota class constants update (MinuteRequestLimit, DailyRequestLimit)
 - Model preference optimization for cost efficiency
 - Enhanced quota tracking for higher throughput
 - Backward compatibility with existing quota persistence
```

### List of tasks to be completed to fulfill the PRP in the order they should be completed

```yaml
Task 1: Research and Document Paid Tier Specifications
  - ANALYZE current free tier limits in ModelQuota class
  - RESEARCH exact paid tier limits for each Gemini model
  - IDENTIFY most cost-effective model (Gemini 1.5 Flash)
  - DOCUMENT billing requirements and setup process

Task 2: Update ModelQuota Class for Paid Tier Limits
  - MODIFY MinuteRequestLimit from 15 to 2000 (Gemini 1.5 Flash)
  - MODIFY DailyRequestLimit from 60 to 30000 (paid tier standard)
  - VERIFY MinuteTokenLimit (120000) remains appropriate
  - UPDATE comments to reflect paid tier status

Task 3: Optimize Model Selection for Cost Efficiency
  - REORDER _availableModels list to prioritize Gemini 1.5 Flash
  - VERIFY model preference logic uses most cost-effective option first
  - MAINTAIN fallback system for model availability
  - PRESERVE existing model rotation functionality

Task 4: Enhance Quota Management for Higher Limits
  - REVIEW quota persistence mechanism for larger numbers
  - UPDATE quota tracking logic to handle 133x increase in daily limits
  - VERIFY integer overflow protection in quota calculations
  - TEST quota reset mechanisms with new limits

Task 5: Validate Azure Function Configuration
  - VERIFY GeminiProxyFunction.cs supports paid tier API calls
  - CONFIRM Azure Key Vault API key is billing-enabled
  - TEST timeout configurations for higher throughput
  - REVIEW error handling for paid tier specific scenarios

Task 6: Update Logging and Monitoring
  - ADD logging for tier detection and model costs
  - ENHANCE quota tracking logs for paid tier monitoring
  - UPDATE performance metrics collection
  - ADD cost tracking capabilities if beneficial

Task 7: Test Paid Tier Functionality
  - CREATE unit tests for updated ModelQuota class
  - TEST model selection prioritization
  - VERIFY quota management with higher limits
  - VALIDATE error handling and fallback systems

Task 8: Documentation and User Communication
  - UPDATE inline comments explaining paid tier usage
  - DOCUMENT billing setup requirements for deployment
  - CREATE cost monitoring recommendations
  - PROVIDE troubleshooting guide for common issues
```

### Per task pseudocode as needed added to each task

```csharp
// Task 2: Update ModelQuota Class Constants
public class ModelQuota
{
    // UPDATED: Paid tier limits for Gemini 1.5 Flash (most cost-effective)
    public const int MinuteRequestLimit = 2000; // Was 15 (free tier)
    public const int DailyRequestLimit = 30000; // Was 60 (free tier)
    public const int MinuteTokenLimit = 120000; // Unchanged (same for paid tier)
    
    // PATTERN: Keep existing quota tracking logic
    public bool IsAvailable =>
        !IsRateLimited &&
        (DateTime.UtcNow > RateLimitExpiresAt) &&
        (MinuteRequestsUsed < MinuteRequestLimit) &&
        (DailyRequestsUsed < DailyRequestLimit) &&
        (MinuteTokensUsed < MinuteTokenLimit);
}

// Task 3: Optimize Model Selection Order
private readonly List<string> _availableModels = new List<string>
{
    "gemini-1.5-flash", // MOVED: Most cost-effective option first
    "gemini-1.5-pro",   // SECOND: Higher capability but more expensive
    "gemini-pro"        // FALLBACK: Legacy model
};

// Task 5: Validate Azure Function Timeout
// In SecureAIService.cs - verify timeout handling for higher throughput
_httpClient.Timeout = TimeSpan.FromSeconds(60); // May need adjustment for paid tier
```

### Integration Points
```yaml
GOOGLE_CLOUD_BILLING:
  - requirement: "Enable billing in Google Cloud Console"
  - activation: "Switch from free to paid tier in project settings"
  - verification: "API calls will automatically use paid tier limits"
  
AZURE_FUNCTIONS:
  - verify: "Current proxy function supports paid tier"
  - timeout: "Ensure adequate timeout for higher throughput"
  - monitoring: "Add logging for paid tier usage tracking"
  
MODEL_PREFERENCE:
  - primary: "gemini-1.5-flash (most cost-effective)"
  - secondary: "gemini-1.5-pro (fallback)"
  - legacy: "gemini-pro (final fallback)"
  
QUOTA_PERSISTENCE:
  - format: "JSON serialization in Preferences"
  - validation: "Handle larger numeric values for daily limits"
  - compatibility: "Backward compatible with existing quota data"
```

## Validation Loop

### Level 1: Build & Compile
```bash
# Verify code compiles with updated constants
dotnet build --configuration Release
# Expected: Clean compilation, no errors related to quota changes

# Verify Azure Function builds
dotnet build --project path/to/GeminiProxyFunction --configuration Release
# Expected: Function app builds successfully
```

### Level 2: Unit Testing
```csharp
// Test updated ModelQuota class
[Fact]
public void ModelQuota_PaidTierLimits_ShouldReflectCorrectValues()
{
    // Arrange & Act
    var quota = new ModelQuota("gemini-1.5-flash");
    
    // Assert
    Assert.Equal(2000, ModelQuota.MinuteRequestLimit);
    Assert.Equal(30000, ModelQuota.DailyRequestLimit);
    Assert.Equal(120000, ModelQuota.MinuteTokenLimit);
}

[Fact]
public void GeminiService_ModelSelection_ShouldPrioritizeFlash()
{
    // Arrange
    var service = new GeminiService();
    
    // Act
    var selectedModel = service.GetBestAvailableModel();
    
    // Assert
    Assert.Equal("gemini-1.5-flash", selectedModel);
}

[Fact]
public void ModelQuota_HighUsage_ShouldHandlePaidTierVolume()
{
    // Arrange
    var quota = new ModelQuota("gemini-1.5-flash");
    
    // Act - Simulate high usage (within paid tier limits)
    for (int i = 0; i < 1000; i++)
    {
        quota.UpdateUsage(100);
    }
    
    // Assert
    Assert.True(quota.IsAvailable); // Should still be available
    Assert.True(quota.MinuteRequestsUsed < ModelQuota.MinuteRequestLimit);
}
```

```bash
# Run comprehensive tests
dotnet test --configuration Release --verbosity normal
# Expected: All tests pass, quota management works with new limits
```

### Level 3: Integration Testing
```bash
# Test actual API calls through Azure Function
# Prerequisites: Billing must be enabled in Google Cloud Console

# Test text request
curl -X POST https://your-function-url/api/gemini-proxy \
  -H "Content-Type: application/json" \
  -d '{"prompt": "Test paid tier", "model": "gemini-1.5-flash", "requestType": "text"}'

# Expected: Successful response, function logs show paid tier usage
# Monitor: Check Azure Function logs for any rate limit or billing errors
```

### Level 4: Load Testing
```bash
# Test higher rate limits with simulated load
# Run 100 requests per minute for 5 minutes to verify paid tier limits
# Expected: No rate limiting until approaching 2000 RPM for Flash model
```

## Final Validation Checklist
- [ ] ModelQuota constants updated to paid tier limits (2000 RPM, 30000 RPD)
- [ ] Model selection prioritizes Gemini 1.5 Flash (most cost-effective)
- [ ] Billing enabled in Google Cloud Console (user requirement)
- [ ] Azure Function proxy handles paid tier API calls
- [ ] Quota tracking works with higher limits
- [ ] All existing functionality preserved (personalization, error handling)
- [ ] Unit tests pass with new quota values
- [ ] Integration tests confirm paid tier activation
- [ ] Load testing validates improved rate limits
- [ ] Cost optimization verified through model selection

---

## Anti-Patterns to Avoid
- ❌ Don't change model selection logic unnecessarily - keep existing fallback system
- ❌ Don't break quota persistence - ensure backward compatibility
- ❌ Don't ignore billing requirements - paid tier requires enabled billing
- ❌ Don't use expensive models by default - prioritize Gemini 1.5 Flash for cost efficiency
- ❌ Don't remove free tier fallback responses - keep for rate limit scenarios
- ❌ Don't hardcode new limits elsewhere - use ModelQuota constants consistently
- ❌ Don't skip testing quota overflow scenarios with new higher limits

## Additional Improvements (Optional)
Since the user mentioned implementing improvements for efficiency and error handling:

### Cost Optimization Enhancements
- Add cost tracking and reporting capabilities
- Implement request batching where possible for reduced costs
- Add intelligent model switching based on request complexity

### Error Handling Improvements
- Enhanced billing error detection and user feedback
- Better rate limit handling for paid tier scenarios
- Improved quota exhaustion warnings before limits are reached

### Efficiency Optimizations
- Context caching improvements for reduced token usage
- Request deduplication for identical queries
- Smart retry logic with exponential backoff optimized for paid tier

## Confidence Score: 9/10
This PRP provides comprehensive context for upgrading to Gemini API paid tier with focus on cost optimization (Gemini 1.5 Flash), maintaining existing functionality, and proper quota management. The implementation is straightforward with clear validation steps and addresses all user requirements while suggesting beneficial improvements.