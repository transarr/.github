# Contributing to Transarr

Thank you for your interest in contributing to Transarr! This document provides guidelines and instructions for contributing.

## 📋 Table of Contents

- [Code of Conduct](#code-of-conduct)
- [Getting Started](#getting-started)
- [Development Setup](#development-setup)
- [Project Structure](#project-structure)
- [Development Workflow](#development-workflow)
- [Coding Standards](#coding-standards)
- [Testing](#testing)
- [Pull Request Process](#pull-request-process)
- [Security](#security)

---

## Code of Conduct

This project adheres to a code of conduct. By participating, you are expected to uphold this code. Please report unacceptable behavior to the project maintainers.

### Our Standards

- **Be Respectful**: Treat everyone with respect and kindness
- **Be Constructive**: Provide constructive feedback
- **Be Inclusive**: Welcome contributors of all backgrounds
- **Be Patient**: Help new contributors learn

---

## Getting Started

### Prerequisites

- **Node.js**: 20.12.2 or later
- **pnpm**: 9.1.1 (managed by corepack)
- **Python**: 3.11 or later (for whisper service)
- **Docker**: Latest version (for containerized development)
- **Git**: For version control

### Install Tools

```bash
# Enable corepack (Node.js 16+)
corepack enable

# Verify installations
node --version  # Should be 20.12.2+
pnpm --version  # Should be 9.1.1
python --version  # Should be 3.11+
docker --version
```

---

## Development Setup

### 1. Clone the Repository

```bash
# Clone with submodules
git clone --recursive https://github.com/transarr/transarr.git
cd transarr

# If already cloned, initialize submodules
git submodule update --init --recursive
```

### 2. Install Dependencies

```bash
# Install app dependencies
cd apps/app
pnpm install

# Install whisper dependencies
cd ../../services/whisper
pip install -r requirements.txt
```

### 3. Start Development Servers

```bash
# Terminal 1: Start API
cd apps/app
pnpm run dev:api

# Terminal 2: Start Web UI
cd apps/app
pnpm run dev:web

# Terminal 3: Start Translation Service
cd services/whisper
python server.py
```

### 4. Verify Setup

```bash
# Check API
curl http://localhost:3000/jobs

# Check Web UI
open http://localhost:5173

# Check Translation Service
curl http://localhost:5000/health
```

---

## Project Structure

```
transarr/                      # Main orchestrator repository
├── .github/                   # GitHub configuration
│   ├── workflows/            # CI/CD workflows
│   └── ISSUE_TEMPLATE/       # Issue templates
├── apps/
│   └── app/                  # transarr-app submodule
│       ├── src/              # NestJS backend
│       ├── client/           # React frontend
│       └── packages/         # Shared packages
│           ├── core/         # Types & interfaces
│           ├── llm/          # Translation logic
│           └── utils/        # Utilities
├── services/
│   └── whisper/              # transarr-whisper submodule
│       ├── server.py         # Flask server
│       └── requirements.txt  # Python dependencies
├── docker-compose.yml        # Production compose
├── docker-compose.dev.yml    # Development compose
├── Makefile                  # Development commands
└── README.md                 # Main documentation
```

### Repository Relationships

- **transarr/transarr**: Main orchestrator (uses submodules)
- **transarr/transarr-app**: Independent repo for app component
- **transarr/transarr-whisper**: Independent repo for whisper service

---

## Development Workflow

### Working with Submodules

Each component (app, whisper) is an independent Git repository. Changes should be made in the component repository and then updated in the main orchestrator.

#### Option 1: Work Directly in Component Repos

```bash
# Clone component repository
git clone https://github.com/transarr/transarr-app.git
cd transarr-app

# Make changes
git checkout -b feature/my-feature
# ... make changes ...
git commit -m "Add feature"
git push origin feature/my-feature

# Open PR in component repository
```

#### Option 2: Work via Orchestrator

```bash
# Navigate to submodule
cd apps/app

# Create feature branch
git checkout -b feature/my-feature

# Make changes
# ... make changes ...

# Commit and push to component repo
git add .
git commit -m "Add feature"
git push origin feature/my-feature

# Update orchestrator to track new commit
cd ../..
git add apps/app
git commit -m "Update app submodule"
git push
```

### Branch Naming

- `feature/description` - New features
- `fix/description` - Bug fixes
- `docs/description` - Documentation updates
- `refactor/description` - Code refactoring
- `test/description` - Test additions/changes

---

## Coding Standards

### TypeScript

- **Style**: Follow [TypeScript Style Guide](https://google.github.io/styleguide/tsguide.html)
- **Linting**: ESLint (configured in project)
- **Formatting**: Prettier (configured in project)

```bash
# Format code
pnpm run format

# Lint code
pnpm run lint
```

### Python

- **Style**: Follow [PEP 8](https://pep8.org/)
- **Type Hints**: Use type hints where possible
- **Docstrings**: Use Google-style docstrings

```python
def translate_text(text: str, source: str, target: str) -> str:
    """Translate text from source to target language.
    
    Args:
        text: Text to translate
        source: Source language code (e.g., 'en')
        target: Target language code (e.g., 'es')
        
    Returns:
        Translated text
    """
    pass
```

### Commit Messages

Follow [Conventional Commits](https://www.conventionalcommits.org/):

```
<type>(<scope>): <subject>

<body>

<footer>
```

**Types:**
- `feat`: New feature
- `fix`: Bug fix
- `docs`: Documentation
- `style`: Formatting
- `refactor`: Code refactoring
- `test`: Tests
- `chore`: Maintenance

**Examples:**

```
feat(api): add retry endpoint for failed jobs

Add POST /jobs/:id/retry endpoint to allow retrying failed translation jobs.

Closes #123
```

```
fix(translate): handle empty subtitle cues

Prevent crash when processing empty subtitle cues by adding validation.

Fixes #456
```

---

## Testing

### Run Tests

```bash
# API tests
cd apps/app
pnpm test

# Integration tests
./test-api.sh

# Manual testing
make test-create
make test-list
make test-health
```

### Test Coverage

- Write tests for new features
- Maintain >80% code coverage
- Test edge cases and error handling

### Test Structure

```typescript
describe('JobsService', () => {
  describe('create', () => {
    it('should create a new job', () => {
      // Arrange
      const request = { ... };
      
      // Act
      const result = service.create(request);
      
      // Assert
      expect(result.status).toBe('pending');
    });
  });
});
```

---

## Pull Request Process

### 1. Create Feature Branch

```bash
git checkout -b feature/my-feature
```

### 2. Make Changes

- Write clean, documented code
- Add tests for new functionality
- Update documentation if needed

### 3. Commit Changes

```bash
git add .
git commit -m "feat: add my feature"
```

### 4. Push Branch

```bash
git push origin feature/my-feature
```

### 5. Open Pull Request

- Go to GitHub and create a PR
- Fill out the PR template completely
- Link related issues
- Request review from maintainers

### 6. Address Review Comments

- Make requested changes
- Push updates to the same branch
- Respond to comments

### 7. Merge

- PRs require approval from at least one maintainer
- All CI checks must pass
- Squash and merge is preferred

### PR Checklist

- [ ] Code follows project style guidelines
- [ ] Tests pass locally
- [ ] New tests added for new functionality
- [ ] Documentation updated
- [ ] Commit messages follow conventions
- [ ] PR description is clear and complete
- [ ] Related issues are linked

---

## Security

### Dependency Management

Transarr uses **strict pinned versions** for security:

- **NO** `^` or `~` in package.json
- All versions explicitly pinned
- Regular security audits

### Adding Dependencies

Before adding a new dependency:

1. Check for known CVEs
2. Verify license compatibility
3. Evaluate maintenance status
4. Pin exact version

```bash
# Add dependency with exact version
pnpm add package-name@1.2.3

# Check for vulnerabilities
pnpm audit --audit-level=moderate
```

### Reporting Security Issues

**DO NOT** open public issues for security vulnerabilities.

Instead:
1. Email security concerns to maintainers
2. Provide detailed information
3. Allow time for fix before disclosure

---

## Documentation

### Code Documentation

- Document all public APIs
- Add JSDoc/TSDoc comments
- Explain complex logic
- Provide examples

```typescript
/**
 * Translate subtitle cues to target language.
 * 
 * @param parsed - Parsed subtitle data
 * @param sourceLanguage - Source language code (e.g., 'en')
 * @param targetLanguage - Target language code (e.g., 'es')
 * @returns Translation result with translated cues
 * 
 * @example
 * ```typescript
 * const result = await translator.translate(
 *   parsed,
 *   'en',
 *   'es'
 * );
 * ```
 */
async translate(
  parsed: ParsedSrt,
  sourceLanguage: string,
  targetLanguage: string
): Promise<TranslationResult>
```

### README Updates

Update README.md when:
- Adding new features
- Changing API endpoints
- Updating dependencies
- Modifying setup process

---

## Questions?

- **GitHub Discussions**: https://github.com/transarr/transarr/discussions
- **Issues**: https://github.com/transarr/transarr/issues
- **Documentation**: https://github.com/transarr/transarr#documentation

---

Thank you for contributing to Transarr! 🎉
