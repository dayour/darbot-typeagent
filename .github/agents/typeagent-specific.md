# TypeAgent-Specific Instructions

This file contains guidance specific to working with the TypeAgent architecture and its unique patterns.

## TypeAgent Architecture Overview

TypeAgent explores building a **single personal agent** with natural language interfaces using three core principles:

1. **Distill models into logical structures** - Replace some model calls with pattern matching
2. **Use structure to control information density** - Fit more into attention budgets  
3. **Use structure to enable collaboration** - Humans, programs, and models work together

## Key Components Deep Dive

### TypeAgent Shell (`ts/packages/shell/`)
- **Electron application** providing unified user interface
- Handles **voice input/output** and conversation management
- Coordinates between **dispatcher** and **individual agents**
- Manages **conversational memory** using Structured RAG

### Dispatcher (`ts/packages/dispatcher/`)
- **Routes natural language requests** to appropriate agents
- Uses **TypeChat schemas** for structured prompting
- Implements **action translation patterns** to reduce LLM calls
- Handles **agent registration** and capability discovery

### Structured RAG (`python/ta/typeagent/knowpro/`)
- **Memory system** that extracts structured information from conversations
- **4-stage query pipeline**: Natural language → SearchQuery → Execution → Answer
- **Semantic reference indexing** for precise recall
- **SQLite-based storage** with specialized indexes

### Individual Agents
Located in `ts/packages/agents/`, each provides specialized capabilities:
- **Browser** - Web navigation and interaction
- **Email** - Email management via Microsoft Graph
- **Calendar** - Calendar operations and scheduling
- **Music Player** - Media playback control
- **Desktop** - System automation
- **Image/Photo** - Image processing and management

## Development Patterns

### TypeChat Integration
```typescript
// Define schema for structured prompting
interface ActionSchema {
    action: "send_email" | "schedule_meeting" | "browse_web";
    parameters: { [key: string]: any };
}

// Use translator for validation
const translator = createTranslator<ActionSchema>(model, schema);
const result = await translator.translate(userInput);
```

### Agent Communication Protocol
```typescript
// Agents implement standard interface
interface IAgent {
    processRequest(request: ActionRequest): Promise<ActionResult>;
    getCapabilities(): AgentCapabilities;
    registerActions(): ActionSchema[];
}
```

### Memory Integration
```python
# Python memory system integration
from typeagent.knowpro import ConversationManager

# Store conversation turn
await conversation.add_message(user_input, agent_response)

# Query memory  
results = await conversation.search("what books did we discuss?")
```

## Configuration and Setup

### API Keys and Environment
- **Azure OpenAI** credentials required for LLM services
- **Microsoft Graph** tokens needed for email/calendar agents
- Environment variables loaded from `ts/.env` (shared across languages)
- Use `typeagent.aitools.utils.load_dotenv()` in Python

### Agent Registration
```typescript
// Register new agent with shell
const agentInfo = {
    name: "my-agent",
    description: "Custom agent description", 
    actions: await agent.registerActions()
};
await shell.registerAgent(agentInfo, agent);
```

### Memory Configuration
```python
# Configure Structured RAG system
config = {
    "storage_provider": "sqlite",  # or "memory" for testing
    "embedding_model": "text-embedding-3-small", 
    "index_types": ["message", "property", "secondary"]
}
```

## Common Development Scenarios

### Adding New Agent Capability
1. **Define TypeChat schema** for the action
2. **Implement agent interface** with action handlers
3. **Register with dispatcher** for request routing
4. **Add memory integration** for conversation context
5. **Test with shell application** end-to-end

### Extending Memory System
1. **Define new semantic ref types** in Python schemas
2. **Update indexing logic** to extract new information
3. **Modify search expressions** to query new data
4. **Test with evaluation datasets** in `testdata/`

### Debugging Common Issues

#### LLM Integration Problems
- Check API keys and endpoint configuration
- Verify TypeChat schema validation
- Monitor token usage and rate limits
- Test with simplified prompts first

#### Agent Communication Failures  
- Validate action schemas match between components
- Check agent registration completed successfully
- Verify message serialization/deserialization
- Test individual agent methods in isolation

#### Memory System Issues
- Confirm SQLite database permissions
- Check embedding model availability  
- Validate search query compilation
- Use debug flags in `tools/utool.py`

## Testing Strategies

### Unit Testing
- Test individual agent actions in isolation
- Mock LLM responses for consistent behavior
- Validate TypeChat schema parsing
- Check error handling paths

### Integration Testing  
- Test full conversation flows through shell
- Validate memory persistence across sessions
- Check multi-agent coordination scenarios
- Test with realistic user input patterns

### Performance Testing
- Monitor LLM token usage and costs
- Test memory system scalability
- Validate response times for common actions
- Check resource usage under load

## Security Considerations

### LLM Security
- **Never pass secrets** to LLM prompts
- **Validate all generated actions** before execution
- **Implement rate limiting** for LLM calls
- **Log security-relevant operations** for audit

### Agent Security
- **Validate all inter-agent communications**
- **Sanitize user inputs** before processing
- **Check permissions** before system operations
- **Use least privilege principle** for agent capabilities

### Memory Security
- **Encrypt sensitive conversation data** at rest
- **Implement access controls** for memory queries
- **Audit data access patterns** for anomalies
- **Secure backup and recovery** procedures

## Performance Optimization

### LLM Call Reduction
- Use **action translation patterns** to cache common requests
- Implement **schema-based validation** before LLM calls
- **Batch similar requests** when possible
- **Cache responses** for repeated queries

### Memory System Optimization
- Use **appropriate index types** for query patterns
- **Optimize SQLite queries** with proper indexes
- **Batch storage operations** for better performance
- **Use memory providers** for testing/development

## Contribution Guidelines

### Code Style
- Follow language-specific conventions in each directory
- Use **TypeChat schemas** for all structured data
- Implement **proper error handling** throughout
- Add **comprehensive logging** for debugging

### Documentation
- Update README files for new capabilities
- Document **schema changes** and migrations
- Provide **usage examples** for new features
- Keep **architecture diagrams** current

### Testing Requirements
- All new agents need **unit and integration tests**
- Memory system changes require **evaluation runs**
- UI changes need **manual validation screenshots**
- Performance changes need **benchmark comparisons**