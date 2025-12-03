---
description: Enable parallel tool execution in Roo Code with the experimental Parallel Tool Calls feature. Execute multiple tools in a single assistant turn when using native protocol.
keywords:
  - parallel tool calls
  - native protocol
  - tool execution
  - experimental features
  - multiple tools
  - performance optimization
image: /img/social-share.jpg
---

# Parallel Tool Calls

Execute multiple tools in a single assistant message turn—cut wait time when Roo needs to call several tools at once.

:::warning Experimental Feature
This feature is experimental and only works with native tool protocol (not XML). It may have edge cases or change behavior in future updates.
:::

---

## Why It Matters

By default, Roo executes one tool per assistant turn. With Parallel Tool Calls enabled, the native protocol can execute multiple tools in a single turn—for example, reading three files and running a command all at once instead of waiting for four separate approval cycles.

This speeds up tasks that require multiple independent operations.

---

## How to Enable

1. Open Roo Code settings (gear icon in the top right)
2. Navigate to the "Experimental" tab
3. Find "Parallel tool calls" in the list
4. Toggle the setting to enable it

---

## Prerequisites

- **Native tool protocol required**: Your model must use native tool calling (OpenAI, Anthropic with native tools, etc.). XML protocol does not support parallel execution.
- **Model support**: Works with models that support native tool calls (Claude 3.5+, GPT-4+, and compatible providers)

#### Check if you're using native protocol

Go to Settings → your active profile. If the "Tool Protocol" is set to "Native" or the model defaults to native tools, you're compatible.

---

## Trade-offs

**Benefits:**
- Faster execution for multi-tool tasks
- Fewer back-and-forth cycles with the model
- More efficient use of API requests

**Costs:**
- More complex to review (multiple tools at once)
- Harder to troubleshoot if one tool in the batch fails
- May increase cognitive load during approval

---

## When to Use

Enable this when:
- Using capable native protocol models
- Working on tasks that frequently need multiple independent operations
- Speed matters more than granular control

Keep disabled when:
- Using XML protocol models
- Prefer reviewing each tool use individually
- Troubleshooting complex workflows where sequential execution helps debugging

---

## Limitations

- **Protocol dependency**: Only works with native tool calling. If your model uses XML, this setting has no effect.
- **Disabled by default**: You must explicitly enable it in experimental settings.
- **Experimental status**: Behavior may evolve as the feature matures.

---

## Troubleshooting

### Parallel calls not happening despite being enabled

**Cause**: Your model is using XML protocol, not native.  
**Fix**: Check Settings → your profile → Tool Protocol. Switch to a model/provider that supports native tools.  
**Prevention**: Verify your model supports native protocol before enabling this feature.

### 400 errors with parallel tool calls

**Cause**: Bug in v3.35.0-v3.35.3 where tool_result blocks weren't preserved during context condensation.  
**Fix**: Update to v3.35.4 or later, which fixes the issue.  
**Prevention**: Keep Roo Code up to date.

---

## See Also

- [Experimental Features Overview](/features/experimental/experimental-features)
- [Native Tool Calling](/providers/openai-compatible#native-tool-calling-openai-native-endpoint)
- [v3.35 Release Notes](/update-notes/v3.35) - Mentions parallel tool calls bug fixes