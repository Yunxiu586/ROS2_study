# Claude Code



| Keyboard Shortcuts |        Function        |
| :----------------: | :--------------------: |
|      Ctrl + C      | Cancel current command |
|      Ctrl + L      | Clear terminal screen  |
|      Ctrl + N      |    Create new file     |
|      Ctrl + O      |   Open existing file   |
|      Ctrl + S      |   Save current file    |



Use the `-c` parameter when starting Claude Code from the command line. The `claude -c` continues the most recent conversation in the current directory.

```
claude -c
```

**Bypass/YOLO mode** - Claude skips all permission checks and executes all operations without any permission confirmations.

```
claude --dangerously-skip-permission
```

```
bypass permission on
```



Claude Code provides three permission modes that control how much autonomy it has when working with your code. You can cycle through these modes using the **Shift+Tab** shortcut.

**Default mode** - Claude asks for your approval before every file edit and command execution.

```
？for shortcuts
```

```
1.Yes
2.Yes, allow all edits during this session (shift+tab)
3.No
```

**Accept edits mode** - Claude automatically applies file edits without asking for permission each time.

```
accept edits on
```

**Plan mode** - Claude only creates plans and proposals without modifying files or executing commands.

```
plan mode on
```



Type `!` followed by a space at the beginning of your message to enter **Bash Mode**, which allows Claude to execute shell commands directly in your terminal.

```
! for bash mode
```



**Checkpoint-based undo system** - Claude automatically creates checkpoints  for each user prompt, allowing selective restoration of code and  conversation states.

Press **ESC twice** (ESC + ESC) or use the **/rewind** command.

```
1.Restore code and conversation
2.Restore conversation
3.Restore code
4.Never mind
```



**MCP** (Model Context Protocol) allows Claude Code to securely connect with external tools, data sources, and services. MCP servers expose capabilities through a standardized interface; Claude Code acts as an MCP client to access these resources.



Clear conversation history and free up context.

```
/clear
```

Compact conversation with optional focus instructions. The `/compact` reduces token usage while preserving key conversation context, allowing you to continue long sessions without losing important details or slowing down performance.

```
/compact
```

The `/init` scans your project files and generates a `claude.md` document at the root directory, creating **persistent project memory** that Claude Code automatically reads on startup to understand your project's  structure, conventions, and context.

```
/init
```

The `/memory` provides access to manage memory.

```
/memory
```

```
1.Project memory
2.User memory
```

**Hooks** execute custom scripts at specific points in Claude Code's workflow.

The `/hooks`  provides an interactive menu for managing hooks.

```
/hooks
```

 **Skills** are reusable toolkits created as `skill.md` files that Claude can automatically load in relevant contexts or that you can manually invoke via `/skill-name`. They're suitable for handling specific domain operation workflows.

The `\skills` lists all available skills that extend Claude's capabilities.

```
/skills
```

```
/skill-name
```

**Subagents** have their own system prompt defining role and behavior, independent context that doesn't pollute the main conversation, and restrict tool access. They're suitable for tasks requiring independent reasoning like code review, test execution, or security scanning.

The `/agents` provides an interactive interface to manage subagents.

```
/agents
```

**Plugins** are packaged collections of custom functionality that extend Claude Code's capabilities through slash commands, subagents, skills,  hooks, and MCP/LSP servers for easy sharing and installation .

The `/plugins`  is the interactive interface for managing plugins.

```
/plugins
```

