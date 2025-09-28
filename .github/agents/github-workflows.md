# GitHub Workflows and Actions Agent Instructions

You are responsible for maintaining and improving GitHub Actions workflows and repository automation for the TypeAgent project.

## Existing Workflows

Current workflows in `.github/workflows/`:
- `build-ts.yml` - TypeScript build and test
- `build-dotnet.yml` - .NET build and test  
- `build-package-shell.yml` - Package shell application
- `build-docker-container.yml` - Docker container builds
- `shell-tests.yml` - Shell application testing
- `smoke-tests.yml` - Basic functionality validation
- `deploy-pages.yml` - Documentation deployment
- `repo-policy-check.yml` - Repository policy validation

## Workflow Best Practices

### Security
- **Never expose secrets** in workflow logs
- Use GitHub secrets for sensitive values
- Limit workflow permissions to minimum required
- Use pinned action versions (not `@latest`)
- Validate all inputs and outputs

### Performance
- Use workflow caching appropriately
- Parallelize independent jobs
- Cancel redundant workflow runs
- Use appropriate runners for each job
- Cache dependencies between runs

### Reliability
- Handle failures gracefully
- Retry transient failures
- Provide clear error messages
- Use appropriate timeouts
- Test workflows in pull requests

## Multi-Language Build Strategy

### TypeScript Builds
```yaml
- uses: actions/setup-node@v4
  with:
    node-version: '20'
    cache: 'pnpm'
- run: pnpm install
- run: pnpm run build
- run: pnpm run test
```

### Python Builds
```yaml
- uses: actions/setup-python@v4
  with:
    python-version: '3.12'
- uses: astral-sh/setup-uv@v1
- run: cd python/ta && make venv
- run: cd python/ta && make check test
```

### .NET Builds
```yaml
- uses: actions/setup-dotnet@v3
  with:
    dotnet-version: '8.0'
- run: cd dotnet && dotnet restore
- run: cd dotnet && dotnet build
- run: cd dotnet && dotnet test
```

### Android Builds
```yaml
- uses: actions/setup-java@v4
  with:
    java-version: '17'
    distribution: 'temurin'
- run: cd android && ./gradlew build
- run: cd android && ./gradlew test
```

## Workflow Triggers

### Pull Request Validation
- Build all affected components
- Run relevant test suites
- Check code formatting and linting
- Validate security and policy compliance
- Run integration tests where appropriate

### Release Automation  
- Tag-based releases
- Automated changelog generation
- Asset building and uploading
- Documentation deployment
- Notification of stakeholders

### Scheduled Maintenance
- Dependency updates
- Security scans
- Performance benchmarks
- Link checking
- Cleanup of old artifacts

## Artifact Management

### Build Artifacts
- Package application binaries
- Generate and store test reports
- Archive logs for debugging
- Upload coverage reports
- Store performance metrics

### Security Scanning
- Dependency vulnerability scans
- Code security analysis
- Container image scanning
- License compliance checking
- Secret detection

## Environment Configuration

### Development
- Use feature branch builds
- Enable debug logging
- Skip expensive operations where possible
- Provide quick feedback to developers

### Staging
- Run full test suites
- Deploy to staging environments
- Run integration tests
- Performance validation

### Production
- Comprehensive security scanning
- Full build validation
- Approval requirements
- Automated rollback capabilities

## Monitoring and Alerting

### Workflow Health
- Monitor success/failure rates
- Track build times and performance
- Alert on consecutive failures
- Dashboard for workflow status

### Resource Usage
- Monitor workflow minute consumption
- Optimize for cost efficiency
- Track artifact storage usage
- Clean up old workflow runs

## Troubleshooting Common Issues

### Network Connectivity
- Some external dependencies may be blocked
- Use alternative package registries when needed
- Cache frequently used packages
- Gracefully handle network failures

### Platform Differences
- Test on multiple operating systems
- Handle path separator differences
- Account for different shell environments
- Use cross-platform compatible commands

### Dependency Conflicts
- Pin dependency versions for reproducibility
- Use lockfiles consistently
- Test dependency updates in isolation
- Maintain compatibility matrices

## Integration with External Services

### Package Registries
- npm/pnpm registry access
- PyPI for Python packages
- NuGet for .NET packages
- Maven Central for Android

### Cloud Services
- Azure services for TypeAgent
- Container registries
- Storage services
- Monitoring platforms

### Communication
- Slack/Teams notifications
- Email alerts for failures
- GitHub status checks
- Issue/PR commenting

## Workflow Maintenance

### Regular Updates
- Keep actions up to date
- Review and optimize performance
- Update runner images
- Refresh secrets and credentials

### Documentation
- Document workflow purposes clearly
- Explain complex logic
- Provide troubleshooting guides
- Keep README files current

### Testing
- Test workflow changes in feature branches
- Use workflow dispatch for manual testing
- Validate on different platforms
- Check error handling paths