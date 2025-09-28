# General Agent Instructions - TypeAgent Repository

You are working with the TypeAgent repository, an experimental project exploring AI agent architectures with natural language interfaces.

## Core Principles

1. **Make Minimal Changes**: Only modify what's necessary to achieve the specific goal
2. **Don't Break Working Code**: Test thoroughly and avoid changing unrelated functionality  
3. **Follow Language Conventions**: Each language subdirectory has specific patterns to follow
4. **Experimental Nature**: This is research code, focus on functionality over perfection

## Repository Guidelines

### Security & Git
- **NEVER commit sensitive data** (API keys, credentials, etc.)
- **Don't use git commands that modify state** (`git commit`, `git push`, etc.)
- Use `git status` and `git diff` for inspection only
- For file operations, use `git mv`, `git cp`, `git rm`

### Dependencies
- **Avoid adding new dependencies** unless absolutely necessary
- Use existing package managers:
  - TypeScript: `pnpm`
  - Python: `uv` 
  - .NET: `dotnet` CLI
  - Android: Gradle
- Check security advisories before adding packages

### Code Standards
- **Copyright headers** required in new files:
  ```
  Copyright (c) Microsoft Corporation.
  Licensed under the MIT License.
  ```
- Follow existing code style in each language
- Use appropriate linting and formatting tools
- Write tests for new functionality when testing infrastructure exists

## Project Structure Understanding

### Core Components
- **TypeAgent Shell** (`ts/packages/shell/`) - Main Electron application
- **Dispatcher** (`ts/packages/dispatcher/`) - Routes requests to agents
- **Structured RAG** (`python/ta/`) - Memory and knowledge system
- **Individual Agents** - Specialized capabilities (browser, email, etc.)

### Key Technologies
- **TypeChat** - Structured prompting with LLMs
- **Electron** - Desktop application framework
- **SQLite** - Local data storage
- **Azure OpenAI** - LLM services
- **Multiple Language Runtimes** - Node.js, Python, .NET, Android

## Development Workflow

1. **Understand the Goal**: Read issues/requirements carefully
2. **Explore First**: Examine existing code patterns and structure
3. **Test Current State**: Run builds/tests to understand baseline
4. **Make Focused Changes**: Implement minimal necessary modifications
5. **Validate Changes**: Test functionality and run existing test suites
6. **Document When Needed**: Update docs if interfaces/usage changes

## Common Pitfalls to Avoid

- Don't modify working configuration files without understanding their purpose
- Don't install global dependencies that might conflict with the project setup
- Don't ignore existing error handling patterns
- Don't skip testing in environments with test infrastructure
- Don't assume all components work in restricted network environments

## When You Need Help

- Check existing documentation in `docs/` directory
- Look at similar implementations within the codebase
- Review component-specific README files
- Ask for clarification if requirements are ambiguous

## Quality Standards

- Code should compile/run without warnings in the target environment
- Existing tests should continue to pass
- New functionality should include tests where testing infrastructure exists
- Changes should not introduce security vulnerabilities
- Performance should not significantly degrade