# hy3-multimonitor

A fork of [hy3](https://github.com/outfoxxed/hy3) with multimonitor support for `movewindow` commands.

## Features

This fork adds the ability to move windows across monitors using the same `hy3:movewindow` command, similar to how sway/i3 works.

### What's New

- **Multimonitor movewindow support**: When you try to move a window in a direction and it's already at the edge of the current monitor, it will automatically move to the adjacent monitor in that direction
- **Cursor warping**: The cursor follows the window when it moves to another monitor
- **Smart edge detection**: Improved logic to detect when a window is truly at an edge and can be moved to another monitor

### Original Issue & PR

This implementation is based on:
- **Issue**: [outfoxxed/hy3#162](https://github.com/outfoxxed/hy3/issues/162) - movewindow not moving windows to other monitors
- **Original PR**: [outfoxxed/hy3#178](https://github.com/outfoxxed/hy3/pull/178) by [@ojasookert](https://github.com/ojasookert)

## Compatibility

- **Hyprland**: 0.50.1
- **hy3 base version**: commit `b813c13a10cc39c60eada511f6e6a7947d941aab`

## Installation

### Prerequisites

Make sure you have the required dependencies:
```bash
# On Arch Linux
sudo pacman -S cmake pkgconf

# On Ubuntu/Debian
sudo apt install cmake pkg-config libhyprland-dev
```

### Building

1. Clone this repository:
```bash
git clone git@github.com:dipta10/hy3-multimonitor.git
cd hy3-multimonitor
```

2. Build the plugin:
```bash
cmake -DCMAKE_BUILD_TYPE=Release -B build
cmake --build build
```

3. Install the plugin:
```bash
# If using hyprpm (recommended)
sudo cp build/libhy3.so /var/cache/hyprpm/your-username/hy3/hy3.so

# Or install manually
mkdir -p ~/.local/share/hyprland/plugins
cp build/libhy3.so ~/.local/share/hyprland/plugins/
```

### Configuration

Add to your `hyprland.conf`:

```bash
# Load the plugin
plugin = ~/.local/share/hyprland/plugins/libhy3.so
# OR if using hyprpm, it should auto-load

# Example keybindings for multimonitor movewindow
bind = SUPER_SHIFT, h, hy3:movewindow, l
bind = SUPER_SHIFT, j, hy3:movewindow, d  
bind = SUPER_SHIFT, k, hy3:movewindow, u
bind = SUPER_SHIFT, l, hy3:movewindow, r

# Focus movement (works across monitors too)
bind = SUPER, h, hy3:movefocus, l
bind = SUPER, j, hy3:movefocus, d
bind = SUPER, k, hy3:movefocus, u
bind = SUPER, l, hy3:movefocus, r
```

## Usage

The multimonitor feature works automatically:

1. **Normal movement**: When you use `hy3:movewindow` and the window can move within the current monitor, it behaves exactly like the original hy3
2. **Cross-monitor movement**: When the window is at the edge of the current monitor and cannot move further in that direction, it will automatically move to the adjacent monitor
3. **Cursor follows**: The cursor will warp to the moved window on the new monitor

## Changes Made

This fork includes the following commits from the original PR, adapted for Hyprland 0.50.1:

1. **Add workspace shifting on movewindow** - Core multimonitor functionality
2. **Fix workspace shifting window edge placement** - Improved window positioning
3. **Refactor workspace edge detection** - Better edge detection logic  
4. **Add cursor warp for workspace-changing shifts** - Cursor follows windows
5. **Fix API compatibility** - Updated for Hyprland 0.50.1 API changes

## Disclaimer

This implementation was created by an LLM (Large Language Model) based on user prompts to achieve multimonitor movewindow functionality. The user provided the requirements and guided the implementation process, while the LLM handled the technical implementation, code integration, API compatibility fixes, and repository setup.

## License

Same as the original hy3 project.
