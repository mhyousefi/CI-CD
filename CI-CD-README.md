# CI/CD Pipeline for XO Game

This repository contains GitHub Actions workflows for continuous integration and deployment of the XO (Tic-Tac-Toe) game.

## Workflow Files

### 1. `test.yml` - Simple Test Workflow
- **Purpose**: Basic testing and linting
- **Triggers**: Push to main/develop, pull requests, manual dispatch
- **Jobs**: 
  - Test and lint the codebase
  - Run unit tests
  - Test server health endpoint
  - Upload test results as artifacts

### 2. `ci-cd.yml` - Full CI/CD Pipeline
- **Purpose**: Complete CI/CD pipeline with testing, security, and deployment
- **Triggers**: Push to main/develop, pull requests, manual dispatch
- **Jobs**:
  - **Test and Lint**: Multi-node version testing (16.x, 18.x, 20.x)
  - **Security Audit**: npm audit with moderate level
  - **Build**: Create deployment package
  - **Deploy Staging**: Deploy to staging environment (develop branch)
  - **Deploy Production**: Deploy to production environment (main branch)
  - **Performance Test**: Optional performance testing

## Setup Instructions

### 1. Repository Setup
1. Push your code to a GitHub repository
2. Ensure your repository has the following structure:
   ```
   .github/
   └── workflows/
       ├── test.yml
       └── ci-cd.yml
   ```

### 2. Environment Setup
For the full CI/CD pipeline, you'll need to set up environments in GitHub:

1. Go to your repository settings
2. Navigate to "Environments"
3. Create two environments:
   - `staging`
   - `production`

### 3. Secrets Configuration (Optional)
If you're deploying to external services, add these secrets to your repository:
- `DEPLOY_SSH_KEY`: SSH private key for server deployment
- `DEPLOY_HOST`: Target server hostname
- `DEPLOY_PATH`: Path on target server
- `DOCKER_REGISTRY`: Docker registry URL
- `DOCKER_USERNAME`: Docker registry username
- `DOCKER_PASSWORD`: Docker registry password

## Usage

### Testing the Pipeline

1. **Simple Test**: Push to any branch to trigger the basic test workflow
   ```bash
   git add .
   git commit -m "Test CI/CD pipeline"
   git push origin main
   ```

2. **Manual Trigger**: Go to Actions tab in GitHub and manually trigger workflows

### Deployment

1. **Staging Deployment**: Push to `develop` branch
   ```bash
   git checkout develop
   git add .
   git commit -m "Deploy to staging"
   git push origin develop
   ```

2. **Production Deployment**: Push to `main` branch
   ```bash
   git checkout main
   git add .
   git commit -m "Deploy to production"
   git push origin main
   ```

## Customization

### Modify Deployment Commands
Edit the deployment steps in `ci-cd.yml`:

```yaml
- name: Deploy to production
  run: |
    # Example: Deploy to VPS via SSH
    echo "${{ secrets.DEPLOY_SSH_KEY }}" > deploy_key
    chmod 600 deploy_key
    rsync -avz -e "ssh -i deploy_key" dist/ user@${{ secrets.DEPLOY_HOST }}:${{ secrets.DEPLOY_PATH }}
    rm deploy_key
    
    # Example: Deploy to Docker
    docker build -t your-app .
    docker tag your-app ${{ secrets.DOCKER_REGISTRY }}/your-app:latest
    echo ${{ secrets.DOCKER_PASSWORD }} | docker login ${{ secrets.DOCKER_REGISTRY }} -u ${{ secrets.DOCKER_USERNAME }} --password-stdin
    docker push ${{ secrets.DOCKER_REGISTRY }}/your-app:latest
```

### Add Performance Testing
Install performance testing tools and add to package.json:

```json
{
  "scripts": {
    "test:performance": "artillery run performance-tests.yml"
  },
  "devDependencies": {
    "artillery": "^2.0.0"
  }
}
```

### Add Docker Support
Create a `Dockerfile`:

```dockerfile
FROM node:18-alpine
WORKDIR /app
COPY package*.json ./
RUN npm ci --only=production
COPY . .
EXPOSE 3000
CMD ["npm", "start"]
```

## Monitoring

### View Workflow Results
1. Go to your GitHub repository
2. Click on "Actions" tab
3. Select the workflow you want to view
4. Check the logs for any failures

### Artifacts
- Test results are uploaded as artifacts
- Security audit results are stored for 30 days
- Deployment packages are available for download

## Troubleshooting

### Common Issues

1. **Linting Fails**: Run `npm run lint:fix` locally to fix issues
2. **Tests Fail**: Check test output in the Actions logs
3. **Security Audit Fails**: Update dependencies with `npm audit fix`
4. **Deployment Fails**: Check your deployment configuration and secrets

### Debugging
- Enable debug logging by adding `ACTIONS_STEP_DEBUG: true` to repository secrets
- Check the "Actions" tab for detailed logs
- Use `workflow_dispatch` trigger for manual testing

## Best Practices

1. **Branch Protection**: Enable branch protection rules for main branch
2. **Required Checks**: Make CI checks required before merging
3. **Code Review**: Require code review for pull requests
4. **Environment Protection**: Use environment protection rules for production
5. **Secrets Management**: Use GitHub secrets for sensitive data
6. **Artifact Cleanup**: Set appropriate retention periods for artifacts

## Support

For issues with the CI/CD pipeline:
1. Check the Actions tab for error logs
2. Verify your repository structure matches the expected layout
3. Ensure all required dependencies are in package.json
4. Test locally before pushing to GitHub 