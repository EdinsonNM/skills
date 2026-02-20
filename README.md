# edinsonnm-skills

The open agent skills ecosystem with **non-interactive mode** support for automation and CI/CD.

This is a fork of [vercel-labs/skills](https://github.com/vercel-labs/skills) with added support for non-interactive installation, perfect for automated workflows and applications.

## Features

✨ All features from the original `skills` CLI
🤖 **Non-interactive mode** for automation
🔧 Configurable installation scope (project/global)
📦 Configurable installation method (symlink/copy)
🚀 Perfect for CI/CD and automated deployments

## Installation

```bash
npm install -g edinsonnm-skills
```

Or use with npx:

```bash
npx edinsonnm-skills add <repository>
```

## Usage

### Interactive Mode (Default)

```bash
skills add vercel-labs/agent-skills
```

### Non-Interactive Mode

```bash
# Basic non-interactive installation
skills add vercel-labs/agent-skills --non-interactive

# With specific options
skills add vercel-labs/agent-skills --non-interactive --scope project --method symlink

# Install specific skill
skills add vercel-labs/agent-skills --skill vercel-react-best-practices --non-interactive

# List available skills without installing
skills add vercel-labs/agent-skills --non-interactive --list
```

## Non-Interactive Mode Options

| Flag | Values | Default | Description |
|------|--------|---------|-------------|
| `--non-interactive` | - | false | Enable non-interactive mode |
| `--scope` | `project`, `global` | `project` | Installation scope |
| `--method` | `symlink`, `copy` | `symlink` | Installation method |
| `--skill` | skill name or `*` | all skills | Specific skill to install |
| `--agent` | agent name or `*` | detected | Target agent(s) |

## Environment Variables

The CLI also respects the `CI` environment variable:

```bash
CI=true skills add vercel-labs/agent-skills
```

When `CI=true`, the CLI automatically enters non-interactive mode.

## Use Cases

### Automated Project Setup

```bash
#!/bin/bash
npx @edinsonm/skills add vercel-labs/agent-skills \
  --non-interactive \
  --scope project \
  --method symlink \
  --skill vercel-react-best-practices
```

### CI/CD Pipeline

```yaml
# .github/workflows/setup.yml
- name: Install Agent Skills
  run: |
    npx @edinsonm/skills add vercel-labs/agent-skills --non-interactive
```

### Integration with Applications

Perfect for desktop applications (like Electron, Tauri) that need to install skills programmatically:

```javascript
const { exec } = require('child_process');

exec('npx edinsonnm-skills add vercel-labs/agent-skills --non-interactive', 
  (error, stdout, stderr) => {
    if (error) {
      console.error(`Error: ${error}`);
      return;
    }
    console.log(`Output: ${stdout}`);
  }
);
```

## Differences from Original

This fork adds:

1. **`--non-interactive` flag**: Skips all prompts
2. **`--scope` flag**: Explicitly set installation scope
3. **`--method` flag**: Explicitly set installation method
4. **CI environment detection**: Auto-enables non-interactive mode in CI
5. **Deterministic behavior**: Predictable defaults for automation

All changes are **100% backward compatible** with the original CLI.

## Original Documentation

For complete documentation on the skills ecosystem, visit:
- [skills.sh](https://skills.sh)
- [Original Repository](https://github.com/vercel-labs/skills)

## License

MIT

## Credits

Original project by [Vercel Labs](https://github.com/vercel-labs/skills)

Non-interactive mode implementation by [Edinson Moreno](https://github.com/EdinsonNM)
