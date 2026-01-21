# 🥔 Agent Potato Quick Start Guide

Howdy! This guide will help you get started with **Agent Potato**, your friendly demo navigator for exploring GitHub Copilot with the OctoCAT Supply Chain demo.

## What is Agent Potato?

Agent Potato is a specialized Copilot agent persona that's an expert in all the demo resources in this repository. Think of Agent Potato as your demo sherpa - knowing every walkthrough, patch set, and demo scenario inside and out!

## Getting Started

### 1. Clone This Repository

```bash
git clone https://github.com/ekuris-repos/QuestPublicPotato.git
cd QuestPublicPotato
```

### 2. Open in VS Code or Codespaces

**Option A: GitHub Codespaces** (Easiest!)
- Click the green "Code" button on GitHub
- Select "Codespaces" → "Create codespace on QuestPotato"
- Everything is pre-configured!

**Option B: Local VS Code**
- Open the folder in VS Code
- Accept the prompt to reopen in Dev Container (recommended)
- Or run `npm install` manually if not using containers

### 3. Meet Agent Potato!

Once your environment is ready, open GitHub Copilot Chat and mention **@agent-potato**:

```
@agent-potato Howdy! What demos are available in this repo?
```

## What Can Agent Potato Help You With?

### 🎭 Discover Demos
```
@agent-potato What Copilot demos can I run?
@agent-potato Show me all the security demos
@agent-potato What's the best demo for showing AI capabilities?
```

### 📍 Navigate Your Demo Environment
```
@agent-potato What's the current state of this repo?
@agent-potato Have any patch sets been applied?
@agent-potato Where am I in the demo flow?
```

### 🔧 Apply Patch Sets
```
@agent-potato How do I apply the secret-scanning patch set?
@agent-potato Walk me through the Dependabot demo setup
@agent-potato What patch sets are available?
```

### 📚 Get Walkthrough Guidance
```
@agent-potato Walk me through the GHAS demo
@agent-potato What's next in the Copilot Agent Mode demo?
@agent-potato How do I demo custom instructions?
```

### 🛠️ Troubleshoot Issues
```
@agent-potato My MCP server isn't working
@agent-potato I'm getting CORS errors
@agent-potato How do I fix port visibility in Codespaces?
```

### 📋 Plan Your Demo
```
@agent-potato I have 30 minutes to show AI features, what should I demo?
@agent-potato Create a demo plan for a security-focused audience
@agent-potato How do I combine Copilot and GHAS in one demo?
```

## Available Demo Walkthroughs

Agent Potato knows all of these inside and out:

- **[copilot.md](./walkthroughs/copilot.md)** - GitHub Copilot & AI Features
- **[ghas.md](./walkthroughs/ghas.md)** - GitHub Advanced Security
- **[actions.md](./walkthroughs/actions.md)** - Actions & CI/CD
- **[governance.md](./walkthroughs/governance.md)** - Governance & Compliance
- **[issues-and-projects.md](./walkthroughs/issues-and-projects.md)** - Project Management
- **[patch-sets.md](./walkthroughs/patch-sets.md)** - How patch sets work

## Example Demo Flow with Agent Potato

Here's a typical interaction:

**You:**
```
@agent-potato I want to demo how Copilot can find and fix security vulnerabilities. 
What's the best way to do this?
```

**Agent Potato:**
```
Well howdy! Perfect timing - we've got a great demo for that very thing! 
Here's what you'll want to do:

1. Start with the GHAS walkthrough at demo/walkthroughs/ghas.md
2. Apply the secret-scanning patch set to inject vulnerable code
3. Show CodeQL detection and Autofix capabilities
4. The whole flow takes about 15-20 minutes

Want me to walk you through applying that patch set?
```

**You:**
```
@agent-potato Yes, please walk me through it
```

And Agent Potato will guide you step-by-step!

## Patch Sets Available

Agent Potato can help you apply these demo scenarios:

- **secret-scanning** - Inject secrets for GHAS demos
- **dependabot** - Add vulnerable dependencies
- **copilot-self-healing-devops** - DevOps self-healing scenarios
- **copilot-custom-instructions** - Custom instruction examples

Use VS Code Command Palette → "Run Task" to see all available patch set tasks, or just ask Agent Potato!

## Tips for a Great Demo

1. **Practice First**: Run through scenarios with Agent Potato before live demos
2. **Non-Deterministic AI**: Copilot responses vary - Agent Potato can help you adapt
3. **Mix & Match**: Combine different scenarios based on your audience
4. **Ask Questions**: Agent Potato knows the repo inside and out - don't hesitate to ask!

## Common Issues & Solutions

### "My MCP server won't start"
Ask Agent Potato:
```
@agent-potato My MCP server isn't working, what should I check?
```

### "CORS errors when frontend calls API"
Ask Agent Potato:
```
@agent-potato I'm getting CORS errors in Codespaces
```

### "Which demo should I run?"
Ask Agent Potato:
```
@agent-potato I need a demo for [your audience type], what do you recommend?
```

## Agent Potato's Personality

Agent Potato brings a friendly, southern charm to technical guidance:
- Uses phrases like "Howdy!", "Y'all", "Partner"
- Delivers precise technical information
- Never sacrifices accuracy for personality
- Makes demos feel less stressful and more fun!

## Ready to Get Started?

1. Open GitHub Copilot Chat in VS Code
2. Type: `@agent-potato Howdy! I'm ready to explore GitHub Copilot demos. Where should I start?`
3. Follow Agent Potato's guidance!

---

**Need More Help?**
- Check the [main demo README](./walkthroughs/README.md)
- Review the [architecture docs](../docs/architecture.md)
- Ask Agent Potato - that's what they're here for! 🥔
