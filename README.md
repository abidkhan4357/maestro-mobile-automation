# Maestro Mobile Test Automation

A mobile testing framework using Maestro.

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

Run the login test:
```bash
maestro test src/flows/android/login.yaml
```

Run all tests:
```bash
maestro test src/flows/android/
```

## Project Structure

```
src/flows/android/     # Android test flows
data/                  # Test data files
apps/android/          # Android app files
screenshots/           # Test screenshots
config/                # Configuration files
```

## Test Data

User credentials are defined in `data/login-data.js`. Tests reference specific users like `${output.users.standard.email}`.

## Platform Support

Currently supporting Android only. iOS support planned for future development.