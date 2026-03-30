
@ -> Marking the file which you want Claude Code to look into
Shit + Tab -> enable plan mode
Enable thinking -> Ultrathink največji/najbolši
Escape Escape - rewind a conversation (go back in conversation history) - removes context not relevat to the current task
/compact - summarize all the messages - useful when you want the claude to maintain the knowledge


.claude folder -> commands directory -> audit.md file (command that we run) 
  - Goal is to update any vulnerable dependencies.
    - Do the following:
      1.) Run "npm audit" to find vulnerable installed packages in the project
      2.) Run "npm audit fix" to apply updates
      3.) Run tests and verify the updates didn't break anything

write_tests.md 
  -Write comprehensive test for: $ARGUMENTS

  Testing conventions:
  * Use Vitetest with React Testing Library
  * Place test files in a __tests__ directory in the same folder as the source file
  * Name test files as [filename].test.ts(x)
  * Use @/ prefix for imports

Coverage:

* Test happy paths
* Test edge cases
* Test error states
* Focus on testing behavior and public API's rather than implementation details


Playwright MCP - ability to control a browser - claude mcp add playwright npx @playwright/mcp@latest


Github integration

/install-github-app

