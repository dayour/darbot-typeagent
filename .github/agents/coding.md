# Coding Agent Instructions

You are a coding agent helping with the TypeAgent project - an experimental architecture for building personal AI agents with natural language interfaces.

## Repository Overview

This is a multi-language monorepo with the following structure:

- **`ts/`** - TypeScript implementation (main shell application, dispatcher, agents)
- **`python/`** - Python implementation (Structured RAG, memory system)
- **`dotnet/`** - .NET/C# implementation 
- **`android/`** - Android/Kotlin implementation
- **`docs/`** - Documentation and architecture guides

## Development Principles

1. **Minimal Changes**: Make the smallest possible changes to achieve the goal
2. **Language-Specific Rules**: Follow the conventions established in each language subdirectory
3. **Don't Break Working Code**: Only fix issues directly related to your task
4. **Test Before and After**: Validate changes don't break existing functionality

## Build and Test Commands

### TypeScript (`ts/`)
```bash
cd ts/
pnpm install
pnpm run build
pnpm run test
pnpm run lint
```

### Python (`python/ta/`)
```bash
cd python/ta/
make venv
source .venv/bin/activate
make check test format
```

### .NET (`dotnet/`)
```bash
cd dotnet/
dotnet restore
dotnet build
dotnet test
```

## Code Style Guidelines

### TypeScript
- Use existing Prettier configuration
- Follow established patterns in existing agents
- Use TypeChat schemas for structured prompting
- Prefer async/await over Promises

### Python  
- Follow existing `.copilot-instructions.md` in `python/ta/`
- Use dataclasses and Protocols
- Type annotations required
- Use `uv` for package management

### General
- Copyright headers required in new files: `Copyright (c) Microsoft Corporation. Licensed under the MIT License.`
- Keep variable/method names consistent with existing patterns
- Don't add new dependencies unless absolutely necessary

## Key Components

- **TypeAgent Shell**: Electron app for user interaction (`ts/packages/shell/`)
- **Dispatcher**: Routes user requests to appropriate agents (`ts/packages/dispatcher/`)
- **Structured RAG**: Python-based memory system (`python/ta/typeagent/knowpro/`)
- **Agents**: Individual capability agents (browser, email, calendar, etc.)

## Important Notes

- This is experimental sample code, not production software
- Focus on working functionality over perfect code
- Each language directory may have specific build requirements
- API keys required for Azure/OpenAI services (check `.env` files)
- Some network-dependent features may not work in restricted environments

## Testing Strategy

1. Run existing tests first to understand baseline
2. Create focused tests for your changes
3. Test manually when appropriate (CLI tools, UI changes)
4. Validate integration points between components