# Contributing to GoNode

Thank you for your interest in contributing to GoNode! This document describes how to contribute effectively and what we expect from contributors.

GoNode is part of the broader SimpleGo ecosystem maintained by IT and More Systems. We welcome contributions from developers, security researchers, technical writers, translators, designers, and community organisers. Every contribution is valued.

---

## Code of Conduct

All contributors must follow our [Code of Conduct](CODE_OF_CONDUCT.md). Treat others with respect, engage constructively, and help maintain an inclusive community.

---

## Before you contribute

### Understand the project

Before writing code or opening issues, please read:

- [README](README.md) for project overview
- [CONCEPT](docs/CONCEPT.md) for strategic rationale
- [ARCHITECTURE_AND_SECURITY](docs/ARCHITECTURE_AND_SECURITY.md) for technical design
- [ROADMAP](docs/ROADMAP.md) for current phase and priorities

### Check existing work

- Search [open issues](https://github.com/saschadaemgen/GoNode/issues) before filing new ones
- Check [open pull requests](https://github.com/saschadaemgen/GoNode/pulls) before starting duplicate work
- Ask in GitHub Discussions if unsure whether your idea fits the project direction

### Legal prerequisites

By contributing, you agree that your contributions will be licensed under AGPL-3.0 (the same license as the project). You must also sign off every commit with a Developer Certificate of Origin (see below).

---

## Ways to contribute

### 1. Report bugs

Found a bug? Please file an issue with:

- Clear description of the bug
- Steps to reproduce
- Expected behaviour
- Actual behaviour
- Environment (OS, Go version, GoNode version)
- Logs or screenshots if applicable

For security vulnerabilities, follow the [Security Policy](SECURITY.md) instead of opening a public issue.

### 2. Suggest features

Have an idea? Open a GitHub Discussion first to gauge interest before filing a feature request. Good feature suggestions include:

- The problem you're trying to solve
- How this feature would solve it
- Alternative approaches considered
- Whether you'd be willing to implement it

### 3. Improve documentation

Documentation improvements are always welcome. This includes:

- Fixing typos, grammar, or unclear wording
- Adding examples to confusing sections
- Translating documents to other languages
- Creating tutorials, videos, or blog posts
- Improving inline code comments

### 4. Contribute code

See "How to contribute code" below.

### 5. Review pull requests

We welcome reviews from anyone with relevant expertise. Code review feedback helps improve quality and spreads knowledge across the community.

### 6. Answer questions

Help others in GitHub Discussions, Matrix channels, and community forums. Good answers become reference material.

---

## How to contribute code

### Development setup

**Prerequisites:**

- Go 1.24 or later
- Git
- Foundry (for smart contract development)
- Node.js 20+ (for frontend tools, if applicable)

**Setup:**

```bash
# Fork the repository on GitHub first, then:
git clone https://github.com/YOUR_USERNAME/GoNode.git
cd GoNode

# Add upstream remote
git remote add upstream https://github.com/saschadaemgen/GoNode.git

# Install Go dependencies
go mod download

# Run tests
go test ./...

# Install git hooks
./scripts/install-hooks.sh
```

### Development workflow

1. **Sync with upstream**

```bash
git fetch upstream
git checkout main
git merge upstream/main
```

2. **Create a feature branch**

Branch names should follow Conventional Commits format:

```
feat/add-swarm-reshuffling
fix/race-condition-in-replication
docs/update-tokenomics-table
refactor/simplify-audit-response
test/add-slashing-integration-tests
```

```bash
git checkout -b feat/your-feature-name
```

3. **Make your changes**

- Keep changes focused on a single concern
- Follow code style (see below)
- Write tests for new functionality
- Update documentation as needed

4. **Test your changes**

```bash
# Unit tests
go test ./...

# Integration tests
go test -tags=integration ./...

# Smart contract tests (if applicable)
cd contracts
forge test

# Linting
golangci-lint run

# Format
gofmt -w .
```

5. **Commit your changes**

Commits must follow Conventional Commits format and include a DCO sign-off:

```bash
git commit -s -m "feat(swarm): add deterministic member reshuffling at epoch boundary"
```

The `-s` flag adds the DCO sign-off. You can configure this to be automatic:

```bash
git config --global commit.gpgsign true
git config --global user.email "you@example.com"
git config --global user.name "Your Name"
```

6. **Push and open a pull request**

```bash
git push origin feat/your-feature-name
```

Then open a pull request on GitHub targeting the `main` branch.

### Pull request requirements

Every PR must:

- [ ] Follow Conventional Commits in title and commit messages
- [ ] Include DCO sign-off on every commit
- [ ] Pass all CI checks (tests, linting, formatting)
- [ ] Include tests for new functionality (aim for coverage no less than current)
- [ ] Update documentation for user-facing changes
- [ ] Be focused on a single concern (split large changes into multiple PRs)
- [ ] Have a clear description explaining what and why

PR description template:

```markdown
## What does this PR do?
Brief description of the changes.

## Why is this change needed?
Link to issue or explanation of motivation.

## How has this been tested?
Description of testing performed.

## Checklist
- [ ] Tests added for new functionality
- [ ] Documentation updated
- [ ] Breaking changes noted
- [ ] DCO sign-off on all commits
```

---

## Code style

### Go code

Follow [Effective Go](https://go.dev/doc/effective_go) and these additional conventions:

**File organisation:**

```
package gonode

import (
    // stdlib
    "context"
    "errors"
    "fmt"

    // third-party
    "github.com/ethereum/go-ethereum/common"
    "github.com/klauspost/reedsolomon"

    // local
    "github.com/saschadaemgen/GoNode/internal/swarm"
    "github.com/saschadaemgen/GoNode/pkg/types"
)
```

**Naming:**

- Exported: `CamelCase`
- Unexported: `camelCase`
- Constants: `SCREAMING_SNAKE_CASE` for groups, `CamelCase` for individuals
- Interfaces end in `-er` when possible: `Replicator`, `Auditor`, `Signer`

**Error handling:**

```go
// Good: errors wrapped with context
if err := storage.Put(key, value); err != nil {
    return fmt.Errorf("storing swarm state: %w", err)
}

// Bad: errors swallowed or re-returned naked
if err := storage.Put(key, value); err != nil {
    return err
}
```

**Comments:**

- Every exported identifier needs a doc comment starting with the identifier name
- Comments explain *why*, not *what* (the code shows what)
- TODO comments include author and issue reference: `// TODO(sascha): implement per #123`

### Solidity code

Follow [Solidity Style Guide](https://docs.soliditylang.org/en/latest/style-guide.html) with these additions:

**File headers:**

```solidity
// SPDX-License-Identifier: AGPL-3.0
pragma solidity ^0.8.24;

/// @title NodeStaking
/// @notice Manages node registration and stake for GoNode network
/// @dev Deploys to Arbitrum One. See SMART_CONTRACTS.md for full spec.
```

**Naming:**

- Contracts: `PascalCase`
- Functions: `camelCase`
- Events: `PascalCase`
- Constants: `SCREAMING_SNAKE_CASE`
- Parameters: `camelCase`

**Security:**

- All external functions have `nonReentrant` modifier or explicit justification
- All input parameters validated
- Access control via OpenZeppelin `AccessControl`
- No `tx.origin` usage except where explicitly justified

### Documentation

Markdown files use:

- Header hierarchy: one H1 per document, then H2 for sections
- Tables with left alignment: `|:--|:--|`
- Code blocks with language specifier: ` ```go ` not ` ``` `
- Cross-references via relative links: `[see roadmap](../ROADMAP.md)`
- American English spelling
- Sentence case for headers (not Title Case)
- No em dashes (use hyphens)

---

## Commit message format

We use [Conventional Commits](https://www.conventionalcommits.org/) strictly:

```
<type>(<scope>): <description>

<body>

<footer>
```

### Types

| Type | Purpose |
|:-----|:--------|
| feat | New feature |
| fix | Bug fix |
| docs | Documentation only |
| style | Formatting, no code change |
| refactor | Refactoring without feature or fix |
| test | Adding or updating tests |
| chore | Build, dependencies, tooling |
| perf | Performance improvement |
| ci | CI/CD changes |

### Scopes

Common scopes for GoNode:

- `core` - core service node runtime
- `swarm` - swarm protocol
- `onion` - onion routing
- `audit` - audit protocol
- `consensus` - BFT appchain
- `contracts` - Solidity smart contracts
- `client` - client library
- `docs` - documentation
- `ci` - CI/CD
- `deps` - dependencies

### Examples

```
feat(swarm): add deterministic member reshuffling at epoch boundary

Implements VRF-based swarm membership recalculation every 24 hours.
Previously swarm membership was fixed at registration, leading to
imbalance as nodes churned.

Closes #42
Signed-off-by: Your Name <you@example.com>
```

```
fix(audit): prevent race condition in concurrent challenge responses

When multiple challenges arrived simultaneously for the same block,
race condition could cause one response to be overwritten before
delivery. Added mutex around response map access.

Signed-off-by: Your Name <you@example.com>
```

```
docs(tokenomics): clarify held-back payment schedule

Rewording "months 1-3" to "first 3 calendar months of operation"
to eliminate ambiguity about when the period starts.

Signed-off-by: Your Name <you@example.com>
```

---

## Developer Certificate of Origin (DCO)

Every commit must include a DCO sign-off:

```
Signed-off-by: Your Name <you@example.com>
```

This certifies that you have the right to contribute your work under AGPL-3.0. The full text of the DCO is available at https://developercertificate.org/.

Commits without sign-off will be rejected by CI. To add sign-off:

```bash
# For a new commit
git commit -s -m "feat(scope): description"

# To amend the last commit
git commit --amend -s --no-edit

# To sign off multiple recent commits
git rebase -i HEAD~3 --signoff
```

---

## Testing requirements

### Code coverage

New code should maintain or increase overall test coverage. Current target: 80% for critical paths, 60% overall.

### Test types

**Unit tests** (required for all code):

```go
func TestSwarmMemberSelection(t *testing.T) {
    t.Run("selects correct number of members", func(t *testing.T) {
        // test implementation
    })

    t.Run("handles edge case of insufficient nodes", func(t *testing.T) {
        // test implementation
    })
}
```

**Integration tests** (required for protocol changes):

```go
//go:build integration

func TestFullReplicationFlow(t *testing.T) {
    // Spin up multiple nodes, verify message propagation
}
```

**Fuzz tests** (encouraged for input validation):

```go
func FuzzParseFrame(f *testing.F) {
    f.Add([]byte{0, 0, 0, 10, 0x01, 0, 0, 0, 0, 0})
    f.Fuzz(func(t *testing.T, data []byte) {
        _, _ = ParseFrame(data) // should never panic
    })
}
```

### Smart contract testing

All Solidity changes require:

- Unit tests with 95%+ coverage using Foundry
- Gas cost measurements documented
- Invariant tests for state changes
- Integration tests for cross-contract flows

---

## Review process

### Timeline

Typical PR review timeline:

- First response within 48 hours (for any PR)
- First code review within 1 week (for substantial PRs)
- Merge or decision within 2 weeks (for non-controversial PRs)
- Complex changes may take longer after discussion

### Review criteria

Reviewers check:

- Does the change solve a real problem?
- Is the approach appropriate?
- Is the code quality acceptable?
- Are there sufficient tests?
- Is documentation updated?
- Does it follow project conventions?
- Are there security implications?

### Decision authority

| Change type | Approver |
|:-----------|:---------|
| Documentation | Any maintainer |
| Bug fixes | 1 maintainer |
| Small features | 1 maintainer |
| Large features | 2 maintainers |
| Protocol changes | 2 maintainers + architecture review |
| Security-sensitive | 2 maintainers + security review |

---

## Maintainer responsibilities

Current maintainers:

| Role | Name | Areas |
|:-----|:-----|:------|
| Technical Lead | Sascha Daemgen | Overall architecture |
| Protocol Engineer | TBD | Wire protocol, consensus |
| Smart Contract Lead | TBD | Solidity, DeFi integration |
| DevRel | TBD | Community, documentation |

Becoming a maintainer requires:

- Sustained high-quality contributions over 6+ months
- Demonstrated expertise in relevant area
- Alignment with project values
- Endorsement from existing maintainers

---

## Getting help

**Stuck on something?** Here are resources in order of speed:

1. **GoLab Community** - Real-time help from other contributors
2. **GitHub Discussions** - Persistent technical discussions
3. **GitHub Issues** - If you've found a bug
4. **Office Hours** - Weekly call every Thursday, details in GoLab

**Still stuck?** Reach out to a maintainer directly on Matrix or via email (contact@simplego.dev).

---

## Recognition

Contributors are recognised in:

- Repository CONTRIBUTORS.md file (auto-generated from Git history)
- Release notes for their contributions
- Annual contributor report
- Airdrop eligibility (for substantial contributions, per Season 5 snapshot)
- Potential for paid work on high-impact features

---

## License

By contributing, you agree that your contributions will be licensed under the AGPL-3.0 license, the same license as the project. See [LICENSE](LICENSE) for full terms.

The AGPL-3.0 patent grant covers your contributions. Before submitting, ensure your contribution does not contain code from incompatible licenses.

---

## Related components

| Component | Role | Documentation |
|:----------|:-----|:-------------|
| [Code of Conduct](CODE_OF_CONDUCT.md) | Community standards | This repo |
| [Security Policy](SECURITY.md) | Vulnerability disclosure | This repo |
| [Architecture](docs/ARCHITECTURE_AND_SECURITY.md) | Technical design | This repo |
| [Roadmap](docs/ROADMAP.md) | Current priorities | This repo |
| [SimpleGo Contributing](https://github.com/saschadaemgen/SimpleGo/blob/main/CONTRIBUTING.md) | Ecosystem-wide conventions | SimpleGo repo |

---

*GoNode Contributing Guide v1 - April 2026*
*IT and More Systems, Recklinghausen, Germany*
