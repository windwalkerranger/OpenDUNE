# OpenDUNE Project Overview

## **Project Overview**
OpenDUNE is an **open-source recreation** of the classic 1992 real-time strategy game "Dune II" by Westwood Studios. It's a complete rewrite that aims to preserve the original gameplay while making it run natively on modern operating systems.

### **Key Characteristics**

**License**: GNU General Public License v2.0 (GPL-2.0)

**Language**: ANSI C (C89) - written in pure C for maximum portability

**Dependencies**: 
- Primary: SDL/SDL2 for cross-platform support
- Optional: SDL_image, ALSA/OSS/PulseAudio for audio, Munt MT32 emulator, FluidSynth

**Architecture**: Modular design with platform-specific implementations

### **Supported Platforms**
- **Desktop**: Linux, FreeBSD, Windows (i686/x86_64), macOS (PowerPC/Intel)
- **Retro**: Atari TOS (68030+ CPU)
- **Other**: OS/2, Haiku

### **Project Structure**

**Core Components**:
- `src/` - Main source code (1593 lines in main file)
- `src/audio/` - Audio drivers (multiple platforms)
- `src/video/` - Video drivers (SDL, SDL2, platform-specific)
- `src/gui/` - User interface components
- `src/input/` - Input handling
- `src/os/` - Operating system abstractions
- `src/pool/` - Memory management and object pools
- `src/table/` - Game data tables and configurations

**Build System**:
- Autotools-based (`configure`, `Makefile.in`)
- Visual Studio support (VS80-VS140 projects)
- Cross-platform compilation support

### **Key Features & Enhancements**

**Over Original Dune II**:
- **Bug Fixes**: 30+ documented bugs fixed (see `enhancement.txt`)
- **Modern Graphics**: Support for scaling (2x, 3x, 4x), HQx filters
- **Enhanced Audio**: Multiple audio backends, MT32 emulation
- **Platform Independence**: Runs natively without DOS emulation
- **Configuration**: Extensive INI-based configuration system
- **Debug Features**: Built-in debugging and replay capabilities

**Notable Fixes Include**:
- Structure ownership bugs
- Unit movement and AI issues
- Scenario loading problems
- Save/load system improvements
- Performance optimizations

### **Development Status**
- **Active Development**: Recent commits and ongoing maintenance
- **Mature Codebase**: Well-structured with extensive documentation
- **Community Driven**: Open source with GitHub-based development
- **Version**: Currently at v0.9 (based on window caption)

### **Technical Highlights**

**Memory Management**: Custom object pool system for efficient resource management

**Cross-Platform**: Extensive abstraction layers for OS-specific functionality

**Modularity**: Clean separation between game logic, rendering, audio, and input

**Backward Compatibility**: Maintains original game behavior while adding enhancements

### **Build & Installation**
- Requires original Dune II data files (1.07 version)
- Supports multiple data file versions (EU, HS, US)
- Configuration via `opendune.ini` file
- Extensive build options for different platforms

---

## **Source Code Analysis**

Based on examination of the source code, here's a detailed breakdown of what each script/module does:

### **Core Game Engine (`src/`)**

#### **Main Entry Point**
- **`opendune.c`** (1593 lines) - Main game loop, initialization, and entry point
- **`opendune.h`** - Global game state definitions and enums

#### **Game Logic Modules**

**1. Unit System (`unit.c/h`)**
- **Purpose**: Manages all game units (vehicles, infantry, aircraft)
- **Key Features**:
  - 27 unit types (Carryall, Tank, Harvester, etc.)
  - Movement, combat, and AI behavior
  - Unit creation, destruction, and state management
  - Pathfinding and targeting systems

**2. Structure System (`structure.c/h`)**
- **Purpose**: Handles buildings and base construction
- **Key Features**:
  - 19 structure types (Palace, Refinery, Turrets, etc.)
  - Building placement and validation
  - Production queues and upgrades
  - Power management and resource storage

**3. Map System (`map.c/h`)**
- **Purpose**: Terrain and world management
- **Key Features**:
  - 15 landscape types (sand, rock, spice, etc.)
  - Tile-based world representation
  - Fog of war and visibility
  - Spice harvesting and terrain modification

**4. House System (`house.c/h`)**
- **Purpose**: Player factions and resource management
- **Key Features**:
  - 6 houses (Harkonnen, Atreides, Ordos, etc.)
  - Credit and power management
  - AI behavior and diplomacy
  - Campaign progression

#### **Scripting System (`src/script/`)**

**1. Script Engine (`script.c/h`)**
- **Purpose**: Game AI and behavior scripting
- **Key Features**:
  - Stack-based virtual machine
  - 18 command types (jump, push, pop, function calls)
  - 64 function slots per category
  - Real-time script execution

**2. Script Categories**:
- **`unit.c`** (1948 lines) - Unit AI behaviors
- **`structure.c`** (640 lines) - Building AI and production
- **`team.c`** (431 lines) - Group movement and coordination
- **`general.c`** (432 lines) - Common utility functions

#### **User Interface (`src/gui/`)**

**1. Main GUI (`gui.c/h`)**
- **Purpose**: Complete user interface system
- **Key Features**:
  - Screen management and drawing
  - Widget system and event handling
  - Factory windows and production UI
  - Text display and messaging

**2. Supporting Modules**:
- **`widget.c/h`** - Interactive UI elements
- **`widget_click.c`** - Mouse interaction handling
- **`widget_draw.c`** - UI rendering
- **`viewport.c`** - Game view management
- **`mentat.c/h`** - Help and information screens
- **`font.c/h`** - Text rendering system

#### **Audio System (`src/audio/`)**

**1. Audio Drivers**:
- **`driver.c/h`** - Main audio system coordinator
- **`sound.c/h`** - Sound effect management
- **Platform-specific drivers**:
  - `dsp_sdl.c`, `dsp_win32.c`, `dsp_alsa.c` - Digital sound
  - `midi_win32.c`, `midi_alsa.c`, `midi_fluid.c` - MIDI music
  - `mt32mpu.c/h` - Roland MT-32 emulation

#### **Video System (`src/video/`)**

**1. Video Drivers**:
- **`video_sdl2.c`** - Modern SDL2 rendering (primary)
- **`video_sdl.c`** - Legacy SDL1 rendering
- **`video_win32.c`** - Windows-specific rendering
- **Platform-specific**: `video_atari.c`, `video_osxppc.c`

**2. Scaling Algorithms**:
- **`scale2x.c/h`** - 2x pixel scaling
- **`scale3x.c/h`** - 3x pixel scaling
- **`hq2x.c/h`, `hq3x.c/h`, `hq4x.c/h`** - High-quality scaling
- **`scalebit.c/h`** - Bit-level scaling operations

#### **Supporting Systems**

**1. File I/O (`file.c/h`)**
- **Purpose**: Game data loading and saving
- **Features**: PAK file handling, save games, resource management

**2. Graphics (`gfx.c/h`)**
- **Purpose**: Sprite and animation management
- **Features**: Sprite rendering, palette management, screen effects

**3. Input (`input/`)**
- **Purpose**: Mouse and keyboard handling
- **Features**: Event processing, input mapping, platform abstraction

**4. Memory Management (`pool/`)**
- **Purpose**: Object pooling and memory optimization
- **Features**: Efficient allocation for units, structures, teams

**5. Data Tables (`table/`)**
- **Purpose**: Game balance and configuration data
- **Features**: Unit stats, structure info, animation data, strings

### **Key Architectural Patterns**

1. **Platform Abstraction**: OS-specific code isolated in dedicated modules
2. **Object-Oriented Design**: Clean separation between units, structures, and houses
3. **Script-Driven AI**: Flexible behavior system using virtual machine
4. **Component-Based**: Modular design allows easy extension and modification
5. **Memory Efficient**: Object pooling and optimized data structures

### **Development Workflow**

The codebase follows a clear structure where:
- **Core logic** is separated from **platform-specific code**
- **Game data** is separated from **game logic**
- **AI behavior** is script-driven and easily modifiable
- **UI components** are modular and reusable

This architecture makes OpenDUNE highly maintainable and extensible while preserving the original game's mechanics and feel.

---

## **Getting Started**

### **Essential Requirements**

#### **1. Development Environment**
- **C Compiler**: GCC, Clang, or MSVC (Visual Studio)
- **Make**: GNU Make or equivalent
- **Basic build tools**: autoconf, automake, libtool (for Unix-like systems)

#### **2. Dependencies**
- **SDL2**: The only mandatory external library
  - Windows: Download SDL2 development libraries
  - Linux: `sudo apt-get install libsdl2-dev` (Ubuntu/Debian)
  - macOS: `brew install sdl2` (with Homebrew)

#### **3. Game Data Files**
- **Original Dune II 1.07 data files** (including `dune2.exe`)
- These are **required** - the game won't run without them
- You need to copy these to a `data/` directory

### **Quick Start for Windows**

1. **Install Visual Studio** (Community edition is free)
2. **Download SDL2** development libraries for Windows
3. **Get Dune II data files** (from your original game or legitimate source)
4. **Build using the provided VS projects** in `projects/` directory

### **Quick Start for Linux/macOS**

```bash
# Install dependencies
sudo apt-get install build-essential autoconf automake libtool libsdl2-dev

# Configure and build
./configure
make

# Copy Dune II data files to data/ directory
# Run the game
./opendune
```

### **Minimum File Structure**
```
OpenDUNE/
├── data/           # ← Put Dune II files here
│   ├── dune2.exe
│   ├── *.PAK files
│   └── other game data
├── src/            # Source code
├── projects/       # VS project files
└── opendune        # Compiled executable
```

### **Key Points**
- **SDL2 is the only external dependency** you absolutely need
- **Original game data is mandatory** - this is a game engine, not a complete game
- **No complex dependencies** - it's designed to be lightweight and portable
- **Cross-platform** - same codebase works on Windows, Linux, macOS

The project is intentionally designed to have minimal dependencies, making it easy to get started with just a C compiler and SDL2. 