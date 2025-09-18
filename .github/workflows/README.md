# GitHub Actions Workflows

This repository includes three GitHub Actions workflows for automated building and publishing:

## 🔧 Workflows

### 1. `build-mcpb.yml` - MCPB Package Builder
- **Triggers**: Push to main, Pull requests, Manual dispatch
- **Purpose**: Builds the MCPB package for Claude Desktop
- **Outputs**: 
  - MCPB artifact (`.mcpb` file)
  - GitHub release with MCPB package
- **Features**:
  - Runs tests before building
  - Creates production bundle
  - Generates MCPB manifest
  - Uploads artifacts
  - Creates releases on main branch pushes

### 2. `npm-publish.yml` - NPM Publisher
- **Triggers**: Push to main, Tag pushes (`v*`), Manual dispatch
- **Purpose**: Publishes the package to NPM registry
- **Outputs**:
  - NPM package publication
  - GitHub release with NPM package info
- **Features**:
  - Checks if version already exists
  - Runs tests before publishing
  - Publishes to NPM (if new version)
  - Creates releases on tag pushes
  - Skips publish if version exists

### 3. `build-and-publish.yml` - Combined Workflow
- **Triggers**: Push to main, Tag pushes (`v*`), Manual dispatch
- **Purpose**: Builds MCPB package AND publishes to NPM
- **Outputs**:
  - MCPB artifact
  - NPM package publication
  - GitHub release with both packages
- **Features**:
  - Single workflow for both operations
  - Comprehensive release notes
  - Artifact uploads
  - Version checking

## 🚀 Usage

### Automatic Triggers
- **Push to main**: Builds MCPB package and publishes to NPM (if new version)
- **Tag push** (`v1.0.1`): Creates release with both packages
- **Pull request**: Runs tests and builds MCPB package

### Manual Triggers
- Go to Actions tab → Select workflow → Run workflow

### Required Secrets
Add these secrets to your repository settings:

1. **`NPM_TOKEN`**: NPM authentication token
   - Get from: https://www.npmjs.com/settings/tokens
   - Required for: NPM publishing

2. **`GITHUB_TOKEN`**: Automatically provided by GitHub
   - Required for: Creating releases

## 📦 Outputs

### MCPB Package
- **File**: `mcp-echo-server-mcpb-*.mcpb`
- **Usage**: Double-click to install in Claude Desktop
- **Features**: User configuration dialog, single-click installation

### NPM Package
- **Name**: `mcp-echo-input-server`
- **Installation**: `npm install -g mcp-echo-input-server`
- **Usage**: `mcp-echo-server` or `npx -y mcp-echo-input-server`

### GitHub Releases
- **Artifacts**: Both MCPB and NPM packages
- **Documentation**: Installation and usage instructions
- **Tags**: Automatic version tagging

## 🔄 Workflow Examples

### Publishing a New Version
1. Update version in `package.json`
2. Commit and push to main
3. Workflows automatically run
4. New version published to NPM
5. MCPB package built and released

### Creating a Release
1. Create and push a tag: `git tag v1.0.1 && git push origin v1.0.1`
2. GitHub Actions creates a release
3. Both packages included in release
4. Release notes generated automatically

## 🛠️ Customization

### Modifying MCPB Manifest
Edit the manifest.json template in the workflow files to customize:
- Bundle metadata
- User configuration options
- Server configuration
- Tool definitions

### Adding Tests
The workflows run `npm test` before building/publishing. Add your tests to the `test` script in `package.json`.

### Environment Variables
Add environment variables to the workflow files for:
- Different NPM registries
- Custom build configurations
- Additional metadata
