# Skill: Git Workflow

## Description
Manages Git workflows including commits, branches, PRs, and repository management following best practices.

## When to Use
- Starting new features
- Creating commits
- Managing branches
- Creating pull requests
- Publishing to GitHub

## Instructions

### Commit Convention
Follow Conventional Commits:
```
<type>(<scope>): <description>

Types:
- feat: New feature
- fix: Bug fix
- docs: Documentation
- style: Formatting
- refactor: Code restructuring
- test: Adding tests
- chore: Maintenance

Examples:
feat(portfolio): add dark mode toggle
fix(navbar): resolve mobile menu bug
docs(readme): update installation steps
```

### Branch Naming
```
feature/<name>    — New features
fix/<name>        — Bug fixes
hotfix/<name>     — Urgent fixes
release/<name>    — Release prep
```

### Workflow
```bash
# 1. Create feature branch
git checkout -b feature/new-project

# 2. Make changes and commit
git add .
git commit -m "feat: add new project"

# 3. Push to remote
git push -u origin feature/new-project

# 4. Create PR on GitHub
gh pr create --title "feat: Add new project" --body "Description"

# 5. Merge after review
git checkout main
git merge feature/new-project
git push
```

### GitHub Pages Deploy
```bash
# After merging to main
git checkout gh-pages
git merge main
git push
```

## References
- [[Git - Referência Completa]]
- [[Metodologias Ágeis - Scrum e Kanban]]
