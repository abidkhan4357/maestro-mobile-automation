# Maestro Mobile Test Automation

A mobile testing framework using Maestro with best practices implementation including Page Object Model, reusable flows, and comprehensive test coverage.

## Prerequisites

- Android emulator or device
- Maestro CLI installed
- macOS or Windows

## Setup

1. Install Maestro CLI:
```bash
curl -Ls "https://get.maestro.mobile.dev" | bash
export PATH="$HOME/.maestro/bin:$PATH"
```

2. Start your Android emulator or connect device

3. Install the test application:
```bash
adb install apps/android/saucelabs-demo.apk
```

## Running Tests

Run a specific test:
```bash
maestro test src/flows/android/login/login-standard.yaml
```

Run all login tests:
```bash
maestro test src/flows/android/login/
```

Run all Android tests:
```bash
maestro test src/flows/android/
```

Run tests by tag:
```bash
maestro test --tags=smoke src/flows/android/
maestro test --tags=negative src/flows/android/
```

Generate HTML report:
```bash
maestro test --format html src/flows/android/
```

## Project Structure

```
maestro-mobile-automation/
├── .maestro/
│   └── config.yaml              # Global configuration & hooks
├── apps/
│   ├── android/
│   │   └── saucelabs-demo.apk   # Android test app
│   └── ios/
│       └── saucelabs-demo.ipa   # iOS test app
├── src/
│   └── flows/
│       └── android/
│           ├── common/          # Reusable flows
│           │   ├── launch-app-fresh.yaml
│           │   ├── open-menu.yaml
│           │   ├── navigate-to-login.yaml
│           │   ├── login-as-user.yaml
│           │   ├── logout.yaml
│           │   └── assert-logged-in.yaml
│           └── login/           # Login test flows
│               ├── login-standard.yaml
│               ├── login-visual-user.yaml
│               ├── login-locked-user.yaml
│               ├── login-empty-fields.yaml
│               └── login-empty-password.yaml
├── data/
│   ├── login-data.js            # Test data (user credentials)
│   └── elements/
│       └── android/
│           ├── navigation.js    # Navigation element selectors
│           ├── login.js         # Login page selectors
│           ├── home.js          # Home page selectors
│           └── loadElements.yaml
└── screenshots/                 # Auto-captured screenshots
```

## Architecture

### Page Object Model (POM)
Element selectors are centralized in `data/elements/android/` for maintainability:
- `navigation.js` - Menu and navigation elements
- `login.js` - Login page elements
- `home.js` - Home page elements

Usage in flows:
```yaml
- tapOn:
    id: ${output.loginPage.emailField}
```

### Reusable Flows
Common actions are extracted to `src/flows/android/common/`:
- `launch-app-fresh.yaml` - Launch app with cleared state
- `open-menu.yaml` - Open hamburger menu
- `navigate-to-login.yaml` - Navigate to login screen
- `login-as-user.yaml` - Parameterized login flow
- `logout.yaml` - Logout flow
- `assert-logged-in.yaml` - Verify user is logged in

### Test Tags
Tests are tagged for selective execution:
- `smoke` - Critical path tests
- `regression` - Full regression suite
- `negative` - Negative/error case tests
- `login` - Login functionality tests

## Test Data

User credentials are defined in `data/login-data.js`:

| User Type | Email | Description |
|-----------|-------|-------------|
| standard | bod@example.com | Default test user |
| visual | visual@example.com | Visual testing user |
| locked | alice@example.com | Locked account user |

Access in flows: `${output.users.standard.email}`

## Configuration

Global settings in `.maestro/config.yaml`:
- **onFlowStart**: Automatically loads element definitions and test data
- **onFlowComplete**: Captures success screenshots
- **onFailure**: Captures failure screenshots
- **executionOrder**: Defines test priority

## Platform Support

Currently supporting Android only. iOS support planned for future development.
