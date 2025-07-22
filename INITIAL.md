## PROJECT_SOURCE:

C:\Users\Gabe\source\repos\MCPServerAutomation-master -COPY

## FEATURE:

Make my MCP Server Automated Workflow Coding Assistant more token efficient. I want to make the coding assistant use less tokens / input and output less, without making the result any worse. Help me plan the best ways to do this, where the best improvements are in my code. 

Here are some things I have though of, but don't limit yourself to these, think of and find more optimization methods:
Things like strategically placed /clear and /compact commands. 
I don't use the unit tests, so maybe we could reduce these to only ones which are used by the AI coding assistant to verify its output?
Maybe we can have a generate-prp-quick and execute-prp-quick command which still do the same things, but at a smaller scale, for smaller tasks.
What about having the AI write notes itself of issues it frequently runs into? Maybe some simple and lightweight system to track commands / things that work, and things that didn't work? An example of this is it constantly uses the wrong command in command line to clone a local folder, and so it tries it every time, then goes and tries another version, if we could track important and useful hangups like this maybe? But it would have to be in a light weight way that doesn't just use way more tokens and usage and cancel out the rest of our optimization.

## RELEVANT_CODE:

CLAUDE.md
GEMINI.md
README.md
.claude\commands\execute-prp.md
.claude\commands\generate-prp.md
.gemini\commands\execute-prp.md
.gemini\commands\generate-prp.md
PRPs\templates\prp_base_claude.md
PRPs\templates\prp_base_gemini.md

## EXAMPLES:

## DOCUMENTATION:

- [Claude Code Documentation](https://docs.anthropic.com/en/docs/claude-code)
- [Gemini CLI Documentation](https://cloud.google.com/gemini/docs/codeassist/gemini-cli)
- [Context Engineering Best Practices](https://www.philschmid.de/context-engineering)
- [Claude Token Management](https://docs.anthropic.com/en/docs/claude-code/costs)

## OTHER CONSIDERATIONS:

The goal is to still have the code assistant get the same amount of context, and achieve the same quality of work, while saving on token and usage.