# Maestro Mobile Test Automation

This is a demo framework using Meastro to test the SauceLabs Mobile Demo App. It follows best practices such as the Page Object Model for element selectors, reusable flows for common actions, and test tagging for selective execution. Tests can be run locally via the CLI or Maestro Studio, and in CI through GitHub Actions.

## Setup

1. Start Android emulator or connect a device
2. Install the test app:
```bash
adb install apps/android/saucelabs-demo.apk
```

## Running Tests

### Option 1: Maestro Studio (Easy)

No CLI setup needed. Download [Maestro Studio Desktop](https://docs.maestro.dev/getting-started/maestro-studio-desktop) and run tests visually.

### Option 2: CLI

**Prerequisites:**
- Java 17+ with `JAVA_HOME` set
- ADB in PATH

**Install Maestro:**
```bash
curl -Ls "https://get.maestro.mobile.dev" | bash
export PATH="$HOME/.maestro/bin:$PATH"
```

**Run tests:**
```bash
# Single test
maestro test src/flows/android/login/login-standard.yaml

# All login tests
maestro test src/flows/android/login/

# By tag
maestro test --tags=smoke src/flows/android/
```

> **Note:** Run maestro commands from the project root directory, not from inside the flows folder.

## Project Structure

```
├── apps/android/              # Test APKs
├── src/flows/android/
│   ├── common/                # Reusable flows
│   └── login/                 # Login tests
├── data/
│   ├── login-data.js          # Test credentials
│   └── elements/android/      # Page selectors (POM)
└── .github/workflows/         # CI pipeline
```

## Test Tags

- `smoke` - Critical path
- `regression` - Full suite
- `negative` - Error cases

## CI/CD

Tests run on push/PR via GitHub Actions with Android emulator.
