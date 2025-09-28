# GitHub Copilot Agent Configuration

This directory contains specialized instructions for GitHub Copilot coding agents working on the TypeAgent repository.

## Configuration Files

### Core Agent Instructions
- **`general.md`** - Repository-wide guidelines, principles, and workflow
- **`coding.md`** - Language-specific coding standards and build commands
- **`testing.md`** - Testing strategies across all languages and frameworks
- **`security.md`** - Security best practices and vulnerability prevention
- **`documentation.md`** - Documentation standards and maintenance guidelines
- **`github-workflows.md`** - GitHub Actions and workflow management

## How It Works

These files work together with the root `.copilot-instructions.md` to provide comprehensive guidance:

1. **`.copilot-instructions.md`** - Contains language-specific rules using `applyTo` filters
2. **`.github/agents/*.md`** - Provides role-specific detailed instructions for different types of work

## Repository Structure

TypeAgent is a multi-language monorepo:

```
├── ts/                 # TypeScript (Electron shell, dispatcher, agents)
├── python/             # Python (Structured RAG, memory system)
├── dotnet/             # .NET/C# implementation
├── android/            # Android/Kotlin implementation
└── docs/               # Documentation
```

## Quick Start Commands

### TypeScript Development
```bash
cd ts/
pnpm install
pnpm run build
pnpm run test
```

### Python Development  
```bash
cd python/ta/
make venv
source .venv/bin/activate
make check test format
```

### .NET Development
```bash
cd dotnet/
dotnet restore
dotnet build
dotnet test
```

## Key Principles

1. **Make Minimal Changes** - Only modify what's necessary
2. **Don't Break Working Code** - Test thoroughly
3. **Follow Language Conventions** - Each language has specific patterns
4. **Security First** - Never commit secrets, validate inputs
5. **Test Before and After** - Validate changes don't break functionality

## Architecture Understanding

### Core Components
- **TypeAgent Shell** - Main Electron application for user interaction
- **Dispatcher** - Routes natural language requests to appropriate agents  
- **Structured RAG** - Python-based memory and knowledge system
- **Individual Agents** - Specialized capabilities (browser, email, calendar, etc.)

### Key Technologies
- **TypeChat** - Structured prompting with LLMs
- **Azure OpenAI** - Language model services
- **SQLite** - Local data storage
- **Electron** - Desktop application framework

## Development Workflow

1. **Understand the Task** - Read requirements carefully
2. **Explore the Codebase** - Examine existing patterns and structure
3. **Test Current State** - Run builds and tests to establish baseline
4. **Make Focused Changes** - Implement minimal necessary modifications
5. **Validate Changes** - Test functionality and run existing test suites
6. **Update Documentation** - If interfaces or usage changes

## Special Considerations

- **Experimental Code** - Focus on functionality over perfection
- **Network Restrictions** - Some features may not work in restricted environments
- **API Dependencies** - Azure/OpenAI services require API keys
- **Multi-Platform** - Test on Windows, macOS, Linux where applicable

## Support

- Check component-specific README files
- Review existing documentation in `docs/` directory
- Look at similar implementations within the codebase
- Ask for clarification if requirements are unclear