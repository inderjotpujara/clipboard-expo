# MCP (GitHub API) Integration Rules

## Token Configuration
### Fine-grained Personal Access Token Requirements
Required repository permissions:
- `Contents`: Read and write
- `Administration`: Read and write
- `Metadata`: Read-only (automatically included)

## Repository Creation Workflow

### 1. Create Repository
```javascript
// Always create repository first using mcp_github_create_repository
{
  name: "repo-name",
  description: "description",
  private: false,
  autoInit: false  // Set false when pushing existing code
}
```

### 2. Git Configuration
If not already configured:
```bash
git config --global user.name "Username"
git config --global user.email "email@example.com"
```

### 3. Remote Setup
For new repositories:
```bash
git remote add origin git@github.com:username/repo-name.git
```
For existing remotes:
```bash
git remote set-url origin git@github.com:username/repo-name.git
```

### 4. Code Push
```bash
git branch -M main
git push -u origin main
```

## Error Handling Guidelines

### Repository Creation Issues
- Verify token permissions if `mcp_github_create_repository` fails
- Check token expiration status
- Ensure repository name is available
- Verify organization access if creating in an organization

### Push Failures
- Verify SSH access is configured
- Confirm repository exists on GitHub
- Check branch protection rules
- Ensure local repository is properly initialized

## Best Practices

### Repository Initialization
- Initialize without README when pushing existing code
- Use SSH URLs for git remote (git@github.com:username/repo.git)
- Set up proper .gitignore before initial commit
- Include descriptive README.md in initial commit

### Code Management
- Use meaningful commit messages
- Create .gitignore appropriate for the project type
- Document setup steps in README.md
- Include license information when necessary

### Security
- Never commit tokens or sensitive credentials
- Use environment variables for sensitive data
- Regularly rotate access tokens
- Review repository visibility settings

## Workflow Order
1. Verify token permissions
2. Create repository via API
3. Set up local git configuration
4. Initialize local repository if needed
5. Add remote origin
6. Push code to repository

## Common Issues and Solutions
1. Token Permission Issues
   - Review token scope and permissions
   - Regenerate token if necessary
   - Verify organization access

2. SSH Access Problems
   - Verify SSH key is added to GitHub account
   - Test SSH connection
   - Check SSH key permissions

3. Repository Creation Failures
   - Verify unique repository name
   - Check organization permissions
   - Confirm token has admin rights 