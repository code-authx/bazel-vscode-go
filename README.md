# Bazel Go Extension for VS Code

This extension provides integration between Visual Studio Code and Bazel workspaces for Go projects. It allows you to define project scopes using `.bazelproject` files in Bazel monorepos, making it easier to navigate and work with Go code in large repositories.

## Installation

### Installing from GitHub Releases (Pre-Marketplace)

Until the extension is published to the Visual Studio Code Marketplace, you can install it directly from the GitHub release artifacts:

1. Go to the [GitHub Releases](https://github.com/linkedin-sandbox/bazel-vscode-go/releases) page
2. Download the latest `.vsix` file (e.g., `bazel-go-project-view-0.0.9.vsix`)
3. Install the extension in VS Code:
   - Open VS Code
   - Go to the Extensions view (Ctrl+Shift+X or Cmd+Shift+X on macOS)
   - Click the "..." (More Actions) button in the Extensions panel
   - Select "Install from VSIX..."
   - Navigate to and select the downloaded `.vsix` file
   - Restart VS Code when prompted

Alternatively, you can install the extension from the command line:
```bash
code --install-extension path/to/bazel-go-project-view-0.0.9.vsix
```

## Features

- **Project View Management**: Uses `.bazelproject` files to define which Go directories should be included in your workspace
- **Scoped Project Views**: Support for multiple `.bazelproject` files allowing you to switch between different project scopes
- **Bazel Go Target Integration**: View, build, test, and run Bazel Go targets directly from VS Code
- **Automatic Sync**: Automatically updates project view when `.bazelproject` files change
- **Bazel Query Integration**: Uses Bazel query to find all Go targets in the workspace

## Requirements

- Bazel installed and available in your PATH
- A Bazel workspace (containing a WORKSPACE or WORKSPACE.bazel file)
- Go installed for Go language features

## Getting Started

1. Open a Bazel workspace in VS Code
2. The extension will automatically create a default `.vscode/.bazelproject` file if one doesn't exist
3. Edit the `.bazelproject` file to include your Go directories:

```
directories:
  src/go/cmd
  src/go/pkg

exclude_directories:
  vendor/
  third_party/

derive_targets_from_directories: true
```

4. The extension will automatically update your project view based on the `.bazelproject` file

## Working with Scoped Project Views

In large monorepos, you may want to focus on specific parts of the codebase. This extension allows you to create multiple scoped project views:

1. Use the "Bazel Go: Create Project View" command to create a new project view in a specific directory
2. Switch between project views using the Project Views panel in the explorer
3. Each project view can have its own set of included/excluded directories
4. The active project view determines which directories and targets are visible in VS Code

Example: Creating multiple scoped views for different services in your monorepo:
- `/services/api/.bazelproject` - Focus on API service
- `/services/frontend/.bazelproject` - Focus on Frontend service
- `/services/worker/.bazelproject` - Focus on Worker service

## Extension Commands

This extension provides the following commands:

- **Bazel Go: Sync Project View** - Manually sync the project view with the active `.bazelproject` file
- **Bazel Go: Build Target** - Build the selected Bazel Go target
- **Bazel Go: Test Target** - Run tests for the selected Bazel Go target
- **Bazel Go: Run Target** - Run the selected Bazel Go target
- **Bazel Go: Create Project View** - Create a new project view in a specified directory
- **Bazel Go: Set Active Project View** - Change the active project view
- **Bazel Go: Delete Project View** - Delete a project view file
- **Bazel Go: Refresh Project Views** - Refresh the list of available project views

## Settings

This extension contributes the following settings:

- `bazelGo.projectView.notification`: Show notifications when the `.bazelproject` file changes
- `bazelGo.projectView.open`: Open the `.bazelproject` file on first activation
- `bazelGo.projectView.active`: Path to the currently active project view file
- `bazelGo.buildFlags`: Additional flags to pass to bazel build command
- `bazelGo.testFlags`: Additional flags to pass to bazel test command
- `bazelGo.runFlags`: Additional flags to pass to bazel run command

## Known Issues

- Bazel query may be slow in large workspaces
