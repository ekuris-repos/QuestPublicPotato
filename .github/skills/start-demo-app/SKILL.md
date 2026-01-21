---
name: start-demo-app
description: Step-by-step instructions for starting the OctoCAT Supply demo application in different environments (Codespaces, local dev container, local native). Use this when users need to run the app or when troubleshooting startup issues.
---

# Starting the OctoCAT Supply Demo Application

This skill provides the correct procedures for starting the demo application in various environments.

## Quick Reference: Use VS Code Tasks

**Preferred Method:** Use VS Code tasks to avoid terminal conflicts:
- Command Palette (`Cmd/Ctrl+Shift+P`) → `Tasks: Run Task`
- Select `Start All Services` to run both API and frontend
- Or use `Start API` / `Start Frontend` for individual services

## Environment-Specific Instructions

### Option 1: GitHub Codespaces (Recommended for Demos)

**Prerequisites:**
- Codespaces instance created from the repository
- **CRITICAL:** Set API port (3000) to `public` visibility to avoid CORS errors

**Steps:**

1. **Check Port Visibility** (Do this FIRST!)
   - Open the "Ports" panel in VS Code
   - Find port `3000` (API)
   - Right-click → Change Port Visibility → Select `Public`
   - Port `3001` (Frontend) can remain private or public

2. **Start Services Using Tasks:**
   - Press `Cmd/Ctrl+Shift+P`
   - Type `Tasks: Run Task`
   - Select `Start All Services`
   
   OR start individually:
   - `Start API` - Starts the Express backend on port 3000
   - `Start Frontend` - Starts the React frontend on port 3001

3. **Verify Startup:**
   - API should show: `Server is running on http://localhost:3000`
   - Frontend should show: `Local: http://localhost:3001`
   - Check terminal output for any errors

4. **Access the Application:**
   - Click the "Open in Browser" button that appears for port 3001
   - Or use the Ports panel to open the frontend URL

**Common Codespaces Issues:**

- **CORS Errors:** Port 3000 not set to public → Fix: Change port visibility
- **Port Already in Use:** Restart the Codespace or kill existing processes
- **Build Failures:** Run `Build All` task first if source changes exist

### Option 2: Local Dev Container (Full Functionality)

**Prerequisites:**
- Docker Desktop or compatible container runtime installed
- VS Code with Dev Containers extension
- Repository cloned locally

**Steps:**

1. **Open in Container:**
   - Open folder in VS Code
   - Click "Reopen in Container" when prompted
   - OR: Command Palette → `Dev Containers: Reopen in Container`

2. **Wait for Container Build:**
   - First time takes 2-5 minutes
   - Watch the progress in the notification

3. **Start Services Using Tasks:**
   - Press `Cmd/Ctrl+Shift+P`
   - Type `Tasks: Run Task`
   - Select `Start All Services`

4. **Access the Application:**
   - Frontend: http://localhost:3001
   - API: http://localhost:3000
   - No port visibility issues with local containers!

**Common Dev Container Issues:**

- **Container Build Fails:** Check Docker daemon is running
- **Ports Unavailable:** Ensure ports 3000 and 3001 aren't in use on host
- **Permission Issues:** May need to rebuild container: Command Palette → `Dev Containers: Rebuild Container`

### Option 3: Local Native (Without Containers)

**Prerequisites:**
- Node.js 24+ installed
- npm or compatible package manager
- Git

**Steps:**

1. **Install Dependencies:**
   ```bash
   npm install
   ```

2. **Build Projects:**
   - Use task: `Build All`
   - OR manually: `npm run build`

3. **Initialize Database (First Time Only):**
   ```bash
   npm run db:init --workspace=api
   ```
   This runs migrations and seeds sample data.

4. **Start Services:**
   - Use task: `Start All Services`
   - OR manually in separate terminals:
     ```bash
     # Terminal 1
     npm run dev:api
     
     # Terminal 2
     npm run dev:frontend
     ```

5. **Access the Application:**
   - Frontend: http://localhost:3001
   - API: http://localhost:3000

**Common Native Issues:**

- **Node Version:** Requires Node 24+ (check with `node --version`)
- **Database Missing:** Run `npm run db:init --workspace=api`
- **Build Required:** Run `Build All` task if you get module errors

## Database Management

**Available Database Commands (API Workspace):**

```bash
# Initialize: migrations + seed data (use on first run)
npm run db:init --workspace=api

# Run migrations only (schema changes)
npm run db:migrate --workspace=api

# Seed data only (sample data)
npm run db:seed --workspace=api
```

**Database Location:**
- File: `api/data/app.db` (created automatically)
- Override: Set `DB_FILE=/absolute/path/to/file.db` environment variable
- Tests: Uses in-memory database (`:memory:`)

## Troubleshooting Checklist

When the app won't start:

1. **Check Prerequisites:**
   - [ ] Correct environment (Codespaces/Container/Native)
   - [ ] Dependencies installed (`npm install` completed)
   - [ ] Built successfully (`Build All` task ran)

2. **Check Ports:**
   - [ ] Ports 3000 and 3001 are available
   - [ ] In Codespaces: Port 3000 is PUBLIC
   - [ ] No other instances running

3. **Check Database:**
   - [ ] Database file exists at `api/data/app.db`
   - [ ] Migrations ran successfully
   - [ ] Seed data loaded (or not required)

4. **Check Logs:**
   - [ ] Review terminal output for error messages
   - [ ] Check for TypeScript compilation errors
   - [ ] Look for missing dependencies

5. **Clean Restart:**
   - [ ] Stop all services
   - [ ] Run `Build All` task
   - [ ] Run `Start All Services` task

## MCP Server Setup (Optional - For Advanced Demos)

**When Needed:**
- Playwright testing demos
- GitHub API integration demos

**Requirements:**
- Docker/Podman installed
- GitHub Personal Access Token with repo permissions

**Setup:**
1. VS Code Command Palette → `MCP: List servers`
2. Select server (`playwright` or `github`)
3. Click `Start server`
4. Configure with PAT when prompted

**Note:** Some MCP features don't work in Codespaces - use local development for full functionality.

## Quick Command Reference

| Task | VS Code Task | Manual Command |
|------|-------------|----------------|
| Build Everything | `Build All` | `npm run build` |
| Build API | `Build API` | `npm run build --workspace=api` |
| Build Frontend | `Build Frontend` | `npm run build --workspace=frontend` |
| Start Everything | `Start All Services` | `npm run dev:api` + `npm run dev:frontend` |
| Start API Only | `Start API` | `npm run dev:api` |
| Start Frontend Only | `Start Frontend` | `npm run dev:frontend` |
| Init Database | N/A | `npm run db:init --workspace=api` |
| Run Migrations | N/A | `npm run db:migrate --workspace=api` |
| Seed Data | N/A | `npm run db:seed --workspace=api` |

## When to Reference This Skill

Use this skill when:
- User asks how to start/run the application
- Troubleshooting startup failures
- Explaining environment differences
- User is getting CORS errors in Codespaces
- Database initialization issues
- First-time setup questions
- Port conflict resolution
