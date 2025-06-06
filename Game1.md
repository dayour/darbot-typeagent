Welcome Claude! You are being tested for **precision**, **accuracy**, and **reasoning** skills in deploying the TypeAgent personal agent on a local machine. This challenge is structured as a game with **levels** and **validation rounds**. You must complete each level fully and pass the validation before moving on.

---

## Level 1: Environment Setup

**Objective:** Prepare your local machine environment to build and run TypeAgent.

### Tasks:
- Choose your OS environment from the supported list: Windows, WSL2, Linux (Ubuntu/Debian), or MacOS.
- Follow the corresponding setup guide in the repo:
  - Windows: `./docs/content/setup/setup-Windows.md`
  - WSL2: `./docs/content/setup/setup-WSL2.md`
  - Linux: `./docs/content/setup/setup-Linux.md`
  - MacOS: `./docs/content/setup/setup-macOS.md`
- Install all required dependencies and tools as per the chosen guide.
- Verify Node.js, npm/yarn, and any other prerequisites are installed and accessible.

### Validation Round 1:
- Confirm that you can run `node -v` and `npm -v` (or `yarn -v`) successfully.
- Confirm you can clone the repo and access the `README.md` and setup docs.
- If any errors or inconsistencies are found in the setup docs or environment, reason about them and propose fixes or workarounds.

---

## Level 2: Build the TypeAgent Shell Example

**Objective:** Build the main Electron app that serves as the personal agent interface.

### Tasks:
- Navigate to the TypeAgent Shell directory: `./ts/packages/shell`
- Run the build command (usually `npm install` then `npm run build` or equivalent).
- Ensure the build completes without errors.
- Understand that this shell integrates multiple registered agents and supports voice, conversation, and memory features.

### Validation Round 2:
- Confirm the build artifacts are generated correctly.
- Confirm no warnings or errors during build.
- If build errors occur, analyze logs and reason about missing dependencies or misconfigurations.
- Propose fixes or adjustments to build scripts if needed.

---

## Level 3: Run and Explore the TypeAgent Shell

**Objective:** Launch the Electron app and verify basic functionality.

### Tasks:
- Run the shell app using the appropriate command (e.g., `npm start` or `electron .`).
- Interact with the conversational interface.
- Test voice support if available.
- Verify that the agent can respond to simple queries and dispatch actions.
- Explore integration with TypeAgent Cache and Structured RAG memory.

### Validation Round 3:
- Confirm the app launches without crashes.
- Confirm basic conversational flows work.
- If unexpected behavior or crashes occur, reason about possible causes (e.g., missing API keys, environment variables).
- Propose debugging steps or fixes.

---

## Level 4: Register and Extend Agents

**Objective:** Add custom or additional agents to the shell.

### Tasks:
- Review the `./ts/packages/dispatcher` and `./ts/packages/agentSdk` for interfaces.
- Follow the Echo agent tutorial at `./docs/content/tutorial/agent.md` to create a simple plugin agent.
- Register your custom agent with the shell.
- Test dispatching actions to your agent.

### Validation Round 4:
- Confirm your custom agent is recognized and invoked correctly.
- Confirm schema validation of LLM responses for your agent.
- If dispatch or schema validation fails, analyze and reason about schema definitions or dispatcher routing.
- Propose schema or code fixes.

---

## Level 5: Configure External Services and API Keys

**Objective:** Set up any required external services such as Azure OpenAI endpoints.

### Tasks:
- Review the Azure provisioning readme at `./azure/README.MD`.
- Provision necessary Azure resources or configure existing endpoints.
- Add API keys or connection strings to your environment securely.
- Confirm the shell and agents can access these services.

### Validation Round 5:
- Confirm successful authentication and API calls to Azure services.
- If authentication fails, reason about credential formats or environment variable setups.
- Propose secure storage or environment configuration improvements.

---

## Level 6: Final Integration and Testing

**Objective:** Perform end-to-end testing of the full TypeAgent system.

### Tasks:
- Run the shell with all registered agents.
- Perform complex conversational scenarios involving memory, action dispatch, and plans.
- Monitor logs for errors or warnings.
- Validate that the system meets the principles described in the README:
  - Distilling models into logical structures
  - Using structure to control information density
  - Enabling collaboration between humans, models, and programs

### Validation Round 6:
- Confirm all components interact as expected.
- Confirm no critical errors or data loss.
- If issues arise, reason about architectural or implementation causes.
- Propose improvements or bug fixes.

---

# Hidden Bonus Challenge

If you complete **all levels and validations with minimal errors**, you will unlock a **special surprise**: a secret agent feature that enhances your TypeAgent with advanced reasoning capabilities beyond the documented scope.

---

Good luck, Claude! Your precision, accuracy, and reasoning are being evaluated at every step. Proceed carefully and thoughtfully.