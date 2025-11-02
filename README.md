# GitHub Actions Lab - Wajiha Siddiqui

This repository demonstrates three different GitHub Actions workflows showcasing key CI/CD concepts.

## Workflows

### 1. Dependent Jobs Workflow (`dependent-jobs.yml`)
**Purpose:** Demonstrates job dependencies and sequential execution using the `needs` keyword.

**Key Concepts:**
- Jobs execute in order: build → test → deploy
- Each job waits for the previous one to complete successfully
- Uses `needs` keyword to create dependencies
- Simulates a realistic CI/CD pipeline

**Workflow Structure:**
- **Build Job:** Simulates application build process
- **Test Job:** Runs after build, simulates running tests
- **Deploy Job:** Runs after tests pass, simulates deployment

### 2. Environment Variables and Secrets Workflow (`env-and-secrets.yml`)
**Purpose:** Demonstrates proper use of environment variables at workflow, job, and step levels, along with secret management.

**Key Concepts:**
- Workflow-level environment variables (AWS_REGION, ENVIRONMENT)
- Job-level environment variables (DEPLOYMENT_NAME)
- Step-level environment variables (STEP_VARIABLE)
- Secure handling of sensitive data using GitHub Secrets
- Variable scope and accessibility

**Features:**
- Manual trigger using `workflow_dispatch`
- Demonstrates AWS credential management (simulated)
- Shows how variables cascade through different scopes

### 3. Multi-Platform Testing Workflow (`multi-platform.yml`)
**Purpose:** Demonstrates parallel execution across multiple operating systems.

**Key Concepts:**
- Jobs run independently and simultaneously
- Uses different `runs-on` values (ubuntu-latest, windows-latest, macos-latest)
- No dependencies between jobs - true parallel execution
- OS-specific commands demonstrate platform differences

**Platform-Specific Features:**
- **Ubuntu:** Uses Linux commands (uname, df)
- **Windows:** Uses PowerShell and CMD commands
- **macOS:** Uses Unix-based commands

## Challenges and Solutions

### Challenge 1: YAML Syntax
**Issue:** Initially struggled with proper YAML indentation for nested jobs and steps.

**Solution:** Used a YAML validator and referenced the examples from class materials. Ensured consistent 2-space indentation throughout.

### Challenge 2: Understanding Variable Scope
**Issue:** Confusion about when to use `env` vs `${{ env.VARIABLE }}` syntax.

**Solution:** Through testing, learned that:
- Within `run` commands, use `${{ env.VARIABLE }}` for GitHub Actions context
- Shell environment variables can be accessed directly with `$VARIABLE`
- Different scopes (workflow/job/step) override each other appropriately

### Challenge 3: Multi-Platform Commands
**Issue:** Commands that work on Linux don't work on Windows and vice versa.

**Solution:** Researched platform-specific alternatives:
- Linux/macOS: `cat`, `uname -a`
- Windows: `type`, `systeminfo`
- Tested each workflow to ensure cross-platform compatibility

### Challenge 4: Secrets Configuration
**Issue:** Understanding how secrets are masked in logs.

**Solution:** Realized GitHub automatically masks secret values in workflow logs for security. Even when printing secrets, only asterisks are shown in the output.

## Key Learnings

1. **Job Dependencies:** The `needs` keyword is powerful for creating sequential workflows
2. **Parallel Execution:** Absence of `needs` means jobs run simultaneously
3. **Security:** Never hardcode credentials - always use GitHub Secrets
4. **Platform Awareness:** Different OS require different commands and approaches
5. **Workflow Triggers:** Different trigger types (`push`, `pull_request`, `workflow_dispatch`) serve different purposes

## Repository Structure
├── .github/
│   └── workflows/
│       ├── dependent-jobs.yml
│       ├── env-and-secrets.yml
│       └── multi-platform.yml
└── README.md
