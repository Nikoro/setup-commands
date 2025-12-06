# Setup Commands CLI

A GitHub Action that sets up and runs the [Commands CLI](https://github.com/Nikoro/commands_cli) tool in your workflow.

## Features

- Automatically configures Dart's pub-cache in your PATH
- Activates the Commands CLI from the Git repository
- Supports Git reference pinning (tags, branches, or commit hashes)
- Defaults to the latest release for stability

## Usage

### Basic Usage

Use the latest release (recommended):

```yaml
steps:
  - uses: actions/checkout@v4
  - uses: dart-lang/setup-dart@v1
  
  - uses: Nikoro/setup-commands@v1
  
  - name: Run commands
    run: commands
```

### Pin to a Specific Version

```yaml
steps:
  - uses: actions/checkout@v4
  - uses: dart-lang/setup-dart@v1
  
  - uses: Nikoro/setup-commands@v1
    with:
      ref: '0.1.0'
  
  - name: Run commands
    run: commands
```

### Use a Specific Branch

```yaml
steps:
  - uses: actions/checkout@v4
  - uses: dart-lang/setup-dart@v1
  
  - uses: Nikoro/setup-commands@v1
    with:
      ref: 'develop'
  
  - name: Run commands
    run: commands
```

### Use a Specific Commit

```yaml
steps:
  - uses: actions/checkout@v4
  - uses: dart-lang/setup-dart@v1
  
  - uses: Nikoro/setup-commands@v1
    with:
      ref: 'abc123def456'
  
  - name: Run commands
    run: commands
```

## Inputs

| Input | Description | Required | Default |
|-------|-------------|----------|---------||
| `ref` | Git reference of Commands CLI to activate. Accepts release tags (e.g., `0.1.0`), branch names (e.g., `main`), or commit hashes. | No | Latest release |

## Requirements

This action requires Dart to be installed in your workflow. Use the [dart-lang/setup-dart](https://github.com/dart-lang/setup-dart) action to set up Dart:

```yaml
steps:
  - uses: actions/checkout@v4
  - uses: dart-lang/setup-dart@v1
  
  - uses: Nikoro/setup-commands@v1
  
  - name: Run commands
    run: commands
```

## Example Workflow

```yaml
name: Run Commands CLI

on:
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]

jobs:
  run-commands:
    runs-on: ubuntu-latest
    
    steps:
      - uses: actions/checkout@v4
      - uses: dart-lang/setup-dart@v1
      
      - uses: Nikoro/setup-commands@v1
        with:
          ref: '0.1.0'
      
      - name: Run commands
        run: commands
```

## How It Works

1. **Path Configuration**: Prepends `$HOME/.pub-cache/bin` to the `PATH` environment variable
2. **Reference Resolution**: If no ref is specified, fetches the latest release tag from the Commands repository
3. **Activation**: Activates the Commands CLI using `dart pub global activate` with the specified Git reference
4. **Ready to Use**: The `commands` executable is now available in your PATH for subsequent steps


## Support

If you encounter any issues or have questions, please [open an issue](https://github.com/Nikoro/setup-commands/issues) on GitHub.
