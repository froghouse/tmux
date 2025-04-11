# Game Server Management Script

A Bash script for managing multiple game servers (Minecraft and Don't Starve Together) in tmux sessions. This tool simplifies starting, stopping, and managing dedicated game servers on a Linux machine.

## Features

- **Easy server management** - Start and stop servers with simple commands
- **tmux integration** - Runs servers in separate tmux windows for easy monitoring
- **Status monitoring** - Check if servers are running
- **Color-coded output** - Clear, visually distinct feedback for actions

## Prerequisites

- Linux/Unix-based system
- Bash shell
- [tmux](https://github.com/tmux/tmux/wiki) installed
- Minecraft server files (configured in script)
- Don't Starve Together server files (configured in script)

## Installation

1. Clone this repository or download the script:
   ```bash
   git clone https://github.com/froghouse/tmux.git
   ```

2. Make the script executable:
   ```bash
   chmod +x servers
   ```

3. Edit the script to configure your server paths:
   ```bash
   # Configuration
   SESSION="servers"

   MINECRAFT_DIR="/path/to/your/minecraft/server"
   MINECRAFT_CMD="./ServerStart.sh"
   MINECRAFT_WND="minecraft"
   MINECRAFT_PROCESS="java"

   DSTARVE_DIR="/path/to/your/dontstarve/server"
   DSTARVE_CMD="./start_dst.sh"
   DSTARVE_WND="dontstarve"
   DSTARVE_PROCESS="dontstarve_dedicated_server"  # Update with correct process name
   ```

4. Optionally, create a symlink to make the script available system-wide:
   ```bash
   sudo ln -s "$(pwd)/servers" /usr/local/bin/gameservers
   ```

## Usage

### Basic Commands

```bash
# Initialize tmux session with server windows
./servers setup

# Start all servers
./servers start all

# Start specific server
./servers start minecraft
./servers start dontstarve

# Stop all servers
./servers stop all

# Stop specific server
./servers stop minecraft
./servers stop dontstarve

# Attach to tmux session (default window: minecraft)
./servers attach

# Attach to specific window
./servers attach minecraft
./servers attach dontstarve

# Check status of all servers
./servers status

# Display help
./servers help
```

### Tmux Tips

Once attached to a tmux session:
- Detach from session: `Ctrl+B` then `D`
- Switch windows: `Ctrl+B` then window number (0, 1, etc.)
- Create new window: `Ctrl+B` then `C`
- List windows: `Ctrl+B` then `W`
- Scroll through output: `Ctrl+B` then `[` (use arrow keys to scroll, `q` to exit)

## Troubleshooting

### Common Issues

- **"Tmux session not running"**: Run `./servers setup` to create the tmux session.
- **"Cannot change to directory"**: Check if the server paths are configured correctly.
- **Server status shows "unknown"**: Configure the correct process name for the server.

### Debugging

If you encounter issues:

1. Check that the server start scripts have the correct permissions:
   ```bash
   chmod +x /path/to/your/minecraft/server/ServerStart.sh
   chmod +x /path/to/your/dontstarve/server/start_dst.sh
   ```

2. Test if tmux is working properly:
   ```bash
   tmux new-session -d -s test
   tmux has-session -t test && echo "tmux is working" || echo "tmux has an issue"
   tmux kill-session -t test
   ```

## Acknowledgments

- [tmux](https://github.com/tmux/tmux/wiki) - Terminal multiplexer
- [Minecraft](https://www.minecraft.net/) - Game server
- [Don't Starve Together](https://www.klei.com/games/dont-starve-together) - Game server
