![](https://raw.githubusercontent.com/sancovp/emergence-engine/refs/heads/master/ee_img.png)

[![Part of STARSYSTEM](https://img.shields.io/badge/Part%20of-STARSYSTEM-blue)](https://github.com/sancovp/starsystem-metarepo)

# Emergence Engine MCP

An auto-prompter and state tracker for the 3-pass systematic thinking methodology for guiding LLM specification-making and conceptualization.

## Role in the Compound Intelligence System

Emergence Engine is the **systematic thinking engine** in the compound intelligence toolkit. It provides:
- 3-pass methodology guidance (expanded to 9 passes across 3 layers)
- State tracking through the ontological → architectural → implementation flow
- Auto-prompting to keep agents on track

Works alongside:
- **STARSHIP**: Orchestrates sessions and workflows
- **STARLOG**: Maintains context and project history
- **GIINT**: Manages project structure and tasks
- **PayloadDiscovery**: Knowledge base integration

## Installation

It's not currently on PyPI but it is installable if you download the package.

```bash
# Clone the repository
git clone https://github.com/sancovp/emergence-engine.git

# Install locally
pip install ./emergence-engine
```

## MCP Configuration

Add to your MCP server configuration:

```json
{
  "mcpServers": {
    "emergence-engine": {
      "type": "stdio",
      "command": "emergence-engine-mcp",
      "args": []
    }
  }
}
```

## System Prompt Integration

**CRITICAL**: Before using Emergence Engine tools, you MUST integrate the system topology into your agent's system prompt.

1. Copy the **[Complete Compound Intelligence System Topology](https://github.com/sancovp/emergence-engine/blob/master/emergence_engine/3_pass_autonomous_research_system_v01/diagrams/00_complete_system_topology.md)**
2. Add it to your agent's system prompt/instructions
3. This enables the agent to understand:
   - The biphasic conversation pattern (Dev→Implement)
   - Where they are in the 9-pass nested structure
   - How tools integrate in the compound intelligence system

⚠️ **Without this integration, the agent won't understand the navigation context for the 3-pass methodology.**

## Available Tools

### `core_run(domain, starlog_path)`
Initiates a 3-pass thinking session for a domain. This starts Layer 0, Pass 1 - determining "What IS" your domain ontologically.

### `expanded_run(domain, starlog_path)`  
Full guided journey through all 9 passes (3 layers × 3 passes). Includes:
- Layer 0: Conceptualize (What IS it?)
- Layer 1: Generally Reify (How do we BUILD these?)
- Layer 2: Specifically Reify (Build THIS generator)

### `get_next_phase(starlog_path)`
Navigate through the 9-pass structure. Returns contextual prompts based on your position in the topology (e.g., "L₁P₂: How do we BUILD systems that BUILD?")

### `get_status(starlog_path)`
Show overall progress and what's next.
- Shows: "Pass 2 of 3, Phase 4 of 7", what files should exist, what's next

### `reset_journey(starlog_path)`
Reset journey back to the beginning (`L0P1W[0](0)`).

## DSL Notation

The system uses formal System Design DSL notation:
- **`L₀P₁W[0](3)`** = Layer 0, Pass 1, Workflow Phase 3
- **Layers**: L₀, L₁, L₂... (recursive application)
- **Passes**: P₁ (Conceptualize), P₂ (Generally Reify), P₃ (Specifically Reify)  
- **Phases**: 0-6 (AbstractGoal → SystemsDesign → Architecture → DSL → Topology → EngineeredSystem → FeedbackLoop)

## Three-Pass Methodology

1. **Pass 1 (Conceptualize)**: What IS this domain? (Ontological understanding)
2. **Pass 2 (Generally Reify)**: How do we MAKE things in this domain? (System building)
3. **Pass 3 (Specifically Reify)**: How do we make THIS specific instance? (Concrete creation)

## Example Usage

```python
# Start a session
core_run("Autobiography System", "/my/starlog/project")

# Get guidance for current phase  
get_next_phase("/my/starlog/project")

# Check progress
get_status("/my/starlog/project")

# Continue advancing through phases
get_next_phase("/my/starlog/project")
```

## State Persistence

State is persisted to JSON files using starlog paths as identifiers:
- Default location: `/tmp/emergence_engine_states/`
- Files named based on sanitized starlog paths
- Includes timestamps, domain, and full position tracking

## Integration

Designed to integrate with:
- **STARLOG**: Uses starlog paths as unique identifiers
- **PayloadDiscovery**: Can be combined with waypoint (includes set of MD files in package) 
- **GIINT**: Compatible with respond() workflow for complex implementations through blueprint configs
- **STARSHIP**: Flight configs can use these tools for 3-pass missions
