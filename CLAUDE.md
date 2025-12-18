# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a highly customized DWM (Dynamic Window Manager) build with extensive patches and custom functionality. The project is yaocccc/dwm - a feature-rich window manager with advanced tiling layouts, status bar, system tray support, and many usability enhancements.

## Build and Installation Commands

### Essential Commands
- `sudo make clean install` - Build and install DWM after source changes
- `make clean` - Remove build artifacts
- `make` - Build DWM only (without installation)

### Initial Setup (First-time users)
```bash
cp -r DEF/* .           # Copy default configuration files
sudo make clean install # Build and install
```

### Prerequisites Check
The Makefile automatically checks for required files before building:
- `config.h` - Main configuration file
- `autostart.sh` - Autostart script
- `statusbar/` directory - Status bar scripts

## Architecture Overview

### Core Components

1. **dwm.c** - Main DWM source code with extensive custom patches:
   - Custom layouts: tile, magicgrid (advanced grid layout)
   - Window management: hide/restore, global windows, 2D navigation
   - System tray integration
   - Status bar with click handling
   - Multi-monitor support
   - Overview mode

2. **config.h** - User configuration file containing:
   - Window rules and class/instance matching
   - Key bindings and shortcuts
   - Layout definitions
   - Color schemes and transparency settings
   - Font configurations
   - Tag definitions with Unicode icons

3. **statusbar/** - Modular status bar system:
   - `statusbar.sh` - Main status bar controller
   - `packages/` - Individual status modules (cpu, mem, wifi, etc.)
   - Click handling system
   - Modular update scheduling

4. **autostart.sh** - Startup script launcher:
   - System settings initialization
   - Daemon processes startup
   - Cron job management

5. **DEF/** - Reference/default configurations:
   - Contains author's personal configurations
   - Serves as template for new users
   - Includes complete status bar modules and scripts

### Key Features and Customizations

#### Window Management
- **Layouts**: tile (master stack), magicgrid (advanced grid)
- **Navigation**: 2D window focusing (hjkl keys), window exchange
- **Manipulation**: keyboard-based move/resize with edge snapping
- **States**: hide/restore windows, global windows, floating support
- **Border control**: toggle borders, transparency support

#### Status Bar System
- **Modular design**: Each component (cpu, mem, wifi, etc.) is a separate script
- **Click handling**: Mouse clicks on status bar trigger actions
- **Update scheduling**: Different refresh intervals for different modules
- **Format**: Uses custom format with color codes and transparency

#### Key Features
- **System tray**: Native systray integration
- **Multi-monitor**: Full multi-monitor support
- **Autostart**: Automatic startup of applications and scripts
- **Rules engine**: Advanced window matching and behavior rules

## Configuration System

### File Structure
- `config.h` - Main DWM configuration (NOT tracked by git)
- `autostart.sh` - Startup scripts (NOT tracked by git)
- `statusbar/` - Status bar configuration (NOT tracked by git)
- `DEF/` - Default/reference configurations (tracked by git)

### Environment Variables
- `$DWM` - Path to DWM installation directory (required)
- Export in `~/.profile`: `export DWM=~/path/to/your/dwm`

### Forking Strategy
The project supports personal forking:
1. Fork the repository
2. Maintain your own `config.h`, `autostart.sh`, `statusbar/`
3. Comment out first three lines of `.gitignore` to track your configs
4. Sync with upstream yaocccc/dwm for updates

## Status Bar Module System

### Module Structure
Each status bar module (in `statusbar/packages/`) follows this pattern:
- Output format: `^s(signal)^c(color)^b(bg)^ icon ^d^`
- Supports click actions: receives signal and button (L/M/R/U/D)
- Updates stored in temporary file, rendered by main script

### Available Modules
- `date.sh` - Date and time display
- `cpu.sh` - CPU usage monitoring
- `mem.sh` - Memory usage
- `wifi.sh` - Network status
- `vol.sh` - Volume control
- `bat.sh` - Battery status
- `music.sh` - Music player status
- `icons.sh` - System tray icons

### Status Bar Commands
- `$DWM/statusbar/statusbar.sh cron` - Start background updater
- `$DWM/statusbar/statusbar.sh check` - Check all modules
- `$DWM/statusbar/statusbar.sh update cpu` - Update specific module
- `$DWM/statusbar/statusbar.sh cpu L` - Handle click on cpu module

## Development Notes

### Key Configuration Areas
1. **Window Rules** (config.h lines 75-112): Define application behavior
2. **Key Bindings** (config.h lines 127-225): Custom shortcuts and actions
3. **Layout Functions**: Window arrangement algorithms
4. **Color Schemes**: Theme definitions and transparency

### Common Modifications
- Adding new window rules for applications
- Customizing key bindings
- Modifying status bar modules
- Adjusting layout algorithms
- Theme customization

### Dependencies
- X11 libraries
- Xinerama (multi-monitor)
- XFT (font rendering)
- Nerd Fonts for icons
- Various system utilities for status bar modules

## Important Notes

- The `DWM` environment variable is **required** for proper operation
- Configuration files (`config.h`, `autostart.sh`, `statusbar/`) are gitignored for personal customization
- Use the `DEF/` directory as a starting point for new configurations
- After any source code changes, always run `sudo make clean install`
- Status bar modules must handle click events and output the proper format with color codes

- run `make clean install` directly to test the new modification codes.
