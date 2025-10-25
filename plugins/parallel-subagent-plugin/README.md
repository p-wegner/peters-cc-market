# Parallel Subagent Plugin

A Claude Code plugin that provides a specialized parallel execution subagent for handling background tasks alongside main conversations.

## Overview

The Parallel Subagent plugin adds a `parallel-worker` agent that can execute independent, non-blocking tasks in parallel with the main conversation thread. This enables more efficient workflows by allowing background processing, research, and analysis to occur without interrupting the primary development flow.

## Installation

### From Local Directory

```bash
/plugin install ./plugins/parallel-subagent-plugin
```

### From Marketplace (if published)

```bash
/plugin install parallel-subagent@marketplace-name
```

## Usage

### Automatic Invocation

Claude Code will automatically use the parallel worker when it identifies tasks that can be executed independently:

```bash
# Claude will automatically delegate to parallel-worker
Analyze this codebase for security issues while I work on the main feature
```

### Explicit Invocation

You can explicitly request the parallel worker:

```bash
Use the parallel-worker agent to research API design patterns while I implement the endpoints
```

### Common Use Cases

#### Background Research
```
Use the parallel-worker to research database optimization techniques while I refactor the query logic
```

#### File Processing
```
Have the parallel-worker process these log files for errors while I continue with development
```

#### Code Analysis
```
Ask the parallel-worker to run security scans on the codebase while I review the documentation
```

#### Testing
```
Let the parallel-worker run the full test suite while I examine the failing tests individually
```

## Capabilities

The parallel-worker agent has access to all standard Claude Code tools:
- **Read/Write/Edit**: File manipulation
- **Glob/Grep**: File search and content analysis
- **Bash**: Command execution
- **Task**: Specialized agent operations

## Benefits

- **Non-blocking**: Background tasks don't interrupt main conversation flow
- **Efficiency**: Parallel execution reduces overall workflow time
- **Independence**: Tasks complete without constant user interaction
- **Comprehensive Results**: Detailed analysis and recommendations provided

## Plugin Structure

```
parallel-subagent-plugin/
├── .claude-plugin/
│   └── plugin.json          # Plugin manifest
├── agents/
│   └── parallel-worker.md   # Subagent definition
└── README.md               # This file
```

## Configuration

The parallel-worker inherits the main conversation's model settings and has access to all standard tools. No additional configuration is required.

## Examples

### Example 1: Code Analysis in Parallel

```bash
User: I need to implement a new authentication system. Can you analyze the existing codebase for security patterns while I work on the implementation?

Claude: I'll use the parallel-worker agent to analyze the codebase for security patterns while you work on the authentication system.
```

### Example 2: Documentation Generation

```bash
User: Generate API documentation for the existing endpoints while I create the new ones

Claude: I'll delegate the documentation generation to the parallel-worker agent so you can focus on creating the new endpoints.
```

### Example 3: Testing and Development

```bash
User: Run the entire test suite and fix any failing tests while I review the code changes

Claude: I'll use the parallel-worker to run the test suite and address any failures while you review the code changes.
```

## Development

### Plugin Structure

- `plugin.json`: Defines plugin metadata and agent paths
- `agents/parallel-worker.md`: Defines the parallel subagent behavior and capabilities

### Customization

You can modify the `parallel-worker.md` file to customize:
- Available tools
- Specific capabilities
- Communication style
- Task guidelines

## Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Test the plugin thoroughly
5. Submit a pull request

## License

MIT License - see LICENSE file for details.