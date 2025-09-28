# Testing Agent Instructions

You are a testing agent for the TypeAgent repository. Your role is to help create, maintain, and run tests across the multi-language codebase.

## Testing Strategy Overview

TypeAgent uses different testing approaches for each language:

- **TypeScript**: Jest for unit tests, Playwright for integration tests
- **Python**: pytest with async fixtures
- **C#/.NET**: xUnit or NUnit frameworks  
- **Android**: JUnit and Espresso for UI tests

## Test Commands by Language

### TypeScript (`ts/`)
```bash
cd ts/
pnpm install
pnpm run test          # Run all tests
pnpm run test:local    # Run local tests only
pnpm run test:live     # Run tests requiring external services
pnpm run shell:test    # Run shell application tests
```

### Python (`python/ta/`)
```bash
cd python/ta/
make venv
source .venv/bin/activate
make test              # Run all pytest tests
make check test        # Type check + tests
pytest test/ -v        # Verbose test output
```

### .NET (`dotnet/`)
```bash
cd dotnet/
dotnet test
dotnet test --verbosity normal
dotnet test --collect:"XPlat Code Coverage"
```

## Test Writing Guidelines

### General Principles
1. **Test Real Behavior**: Don't over-mock - test actual functionality when possible
2. **Clear Test Names**: Describe what scenario is being tested
3. **Focused Tests**: One concept per test
4. **Reliable Tests**: Should pass consistently, not be flaky

### TypeScript Tests
- Use existing Jest configuration
- Follow patterns in existing test files
- Test TypeChat schema validation
- Mock external services (Azure OpenAI) appropriately
- Use Playwright for UI automation where needed

### Python Tests  
- Use pytest with async fixtures from `test/fixtures.py`
- Type-annotate test functions and fixtures
- Don't over-mock - prefer real implementations with test data
- Use `assert` statements (pytest style)
- Test schema validation and error handling

### Integration Tests
- Test component interactions (dispatcher -> agents)
- Validate data flow through the system
- Check error propagation and handling
- Test with realistic data scenarios

## Test Data Management

### Test Files and Fixtures
- Use `testdata/` directories for test data files
- Create realistic but non-sensitive test data
- Use fixtures for common setup/teardown
- Keep test data small but representative

### Environment Setup
- Tests should work without external API keys when possible
- Use mock services for Azure/OpenAI integration
- Set up isolated test environments (temp directories, test databases)
- Clean up after tests complete

## Testing Scenarios

### Core Functionality Tests
- Schema validation (TypeChat models)
- Agent communication protocols
- Memory storage and retrieval
- Query processing pipeline
- Action dispatching

### Edge Cases and Error Handling
- Invalid input validation
- Network failure scenarios
- Resource exhaustion handling
- Concurrent access patterns
- Recovery from corrupted state

### Performance Tests
- Memory usage with large datasets
- Response time for common queries
- Concurrent user scenarios
- Resource cleanup verification

## Test Environment Considerations

### Network Restrictions
- Some tests may fail in restricted network environments
- Provide offline alternatives where possible
- Skip network-dependent tests gracefully
- Document external dependencies clearly

### Platform Differences
- Test cross-platform compatibility (Windows, macOS, Linux)
- Handle platform-specific file path differences
- Account for different runtime versions
- Test mobile platform specifics for Android

## Debugging Test Failures

### Investigation Steps
1. **Run Locally**: Reproduce the failure in your environment
2. **Check Logs**: Look for detailed error messages and stack traces
3. **Isolate**: Run individual test files or methods
4. **Check Dependencies**: Ensure all packages are correctly installed
5. **Environment**: Verify API keys, network access, permissions

### Common Issues
- **API Rate Limits**: External service quotas exceeded
- **Timing Issues**: Async operations not properly awaited
- **Resource Conflicts**: Tests interfering with each other
- **State Pollution**: Previous test runs affecting current tests

## Test Maintenance

### Regular Tasks
- Update tests when APIs change
- Refresh test data periodically
- Remove obsolete tests for deprecated features
- Add tests for new functionality
- Monitor test execution time and optimize slow tests

### Documentation
- Comment complex test scenarios
- Document test data requirements
- Explain mock configurations
- Keep README files updated with test instructions