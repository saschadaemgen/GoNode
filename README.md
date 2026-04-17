# SimpleGoX Scripts

Development helper scripts for SimpleGoX.

## dev-launcher.bat (Windows)

One-click launcher for the SimpleGoX development environment. Starts everything you need and arranges the windows on screen.

*Community contribution by Gas Lighter*

### What it does

1. Starts the Telegram sidecar process in its own console window
2. Waits for the sidecar to initialize
3. Starts `cargo tauri dev` in a second console window
4. Arranges windows automatically: sidecar console on the left, Tauri console on the right, SimpleGoX app in the center

### Setup

1. Copy `dev-launcher.bat` to any location on your PC
2. Edit the file and set your values:

```batch
set "PROJECT_PATH=C:\Projects\SimpleGoX"
set "API_ID=your_telegram_api_id"
set "API_HASH=your_telegram_api_hash"
```

3. Double-click to start

### Getting Telegram API credentials

1. Go to [my.telegram.org](https://my.telegram.org)
2. Log in with your phone number
3. Go to "API development tools"
4. Create an application
5. Copy the `api_id` and `api_hash`

### Note

The Tauri app auto-starts the Telegram sidecar if a saved session exists. This script is most useful for:

- Fresh installs where no Telegram session exists yet
- Debugging, when you want both console windows visible
- Development sessions where you need to see sidecar logs

If you only work on the frontend or Matrix features, `cargo tauri dev` alone is sufficient.

## Contributing scripts

If you have a useful development script, feel free to submit it via the Matrix room or as a GitHub PR. Scripts should:

- Not contain real credentials (use placeholders)
- Include a header comment explaining what they do
- Work without additional dependencies where possible
