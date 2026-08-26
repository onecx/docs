# undefined

AI Migration Agent 

**Before You Start**

Make sure you have the Recommended MCP servers configured before running the migration agent. For detailed setup instructions, see the [MCP Server Setup Guide](../../../onecx-docs-dev/ai/mcp%5Fserver%5Fsetup.html).

**Setup**

1. Clone or pull the latest version of the repository:  
```bash  
git clone https://github.com/onecx/onecx-ai-refactoring-agents.git  
# or if already cloned:  
cd onecx-ai-refactoring-agents && git pull  
```
2. Follow the setup instructions in the repository [README](https://github.com/onecx/onecx-ai-refactoring-agents/blob/main/angular/updates/README.md).

**Usage**

To migrate from Angular 18 to Angular 19, use the following command in your AI assistant:

```bash
/migrate-21
```

The migration agent will guide you through the pre-migration and post-migration steps, including PrimeNG updates if applicable.
