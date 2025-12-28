# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

**Pearcleaner** is a macOS app written in Swift/SwiftUI that serves as a system utility for cleaning up Mac applications and managing various system components. It's essentially an app uninstaller and system management tool inspired by AppCleaner, built with modern Swift and SwiftUI technologies.

## Build System and Commands

### Primary Build System
- **Xcode Project**: Uses traditional Xcode project files (`.xcodeproj`)
- **Swift Package Manager**: Dependencies are managed via SPM
- **No custom build scripts**: Relies on Xcode's standard build system

### Build Commands:
```bash
# Build the main project
xcodebuild -project Pearcleaner.xcodeproj -scheme Pearcleaner build

# Build for release
xcodebuild -project Pearcleaner.xcodeproj -scheme "Pearcleaner Release" build

# Clean build
xcodebuild -project Pearcleaner.xcodeproj clean
```

### Key Targets:
1. **Pearcleaner** (main app)
2. **PearcleanerHelper** (privileged helper tool for system operations)
3. **PearcleanerSentinel** (daemon for monitoring)
4. **FinderOpen** (Finder extension for right-click functionality)

## High-Level Architecture

### Core Architecture Patterns:
- **MVVM (Model-View-ViewModel)** pattern with SwiftUI
- **Command Pattern** for app operations (AppCommands.swift)
- **Singleton pattern** for shared state management

### Key Components:

1. **Main App Structure**:
   - `PearcleanerApp.swift`: Main app entry point with SwiftUI App struct
   - `MainWindow.swift`: Primary application window
   - `AppState.swift`: Central state management

2. **Logic Layer**:
   - `Logic.swift`: Core business logic (60KB+ file)
   - `AppInfoFetch.swift`: App metadata extraction
   - `AppPathsFetch.swift`: File system path management
   - `HelperToolManager.swift`: Privileged helper communication

3. **UI Layer**:
   - Modular Views: AppsView, FilesView, Settings, etc.
   - Custom styling system
   - Support for both List and Grid views

4. **Utilities**:
   - **Lipo**: Universal app architecture handling
   - **DeepLink**: Automation support
   - **FileSearch**: File system searching
   - **Brew**: Homebrew integration
   - **PKG**: Package management

### External Dependencies:
- **AlinFoundation**: Custom utility framework by the author
- **Sparkle**: 2.8.0 - For app updates
- **Swift Argument Parser**: 1.6.1 - For CLI functionality

## Project Structure

```
MacCleaner/
├── Pearcleaner/                  # Main app source code
│   ├── Logic/                   # Business logic components
│   │   ├── AppsUpdater/         # Update management
│   │   ├── Brew/                # Homebrew integration
│   │   ├── FileSearch/          # File searching utilities
│   │   └── PKG/                 # Package management
│   ├── Views/                   # SwiftUI views
│   ├── Style/                   # UI styling and themes
│   └── Resources/               # Assets, localization, etc.
├── PearcleanerHelper/           # Privileged helper tool
├── PearcleanerSentinel/         # Monitoring daemon
├── FinderOpen/                  # Finder extension
├── Shared/                      # Shared code across targets
├── Builds/                      # Build artifacts
└── Pear Resources/              # App resources
```

## Development Environment Requirements

- **macOS 13.0+** (Ventura, Sonoma, Sequoia, Tahoe)
- **Xcode** for development
- **Full Disk Access** permissions for file searching
- **Privileged Helper** for system operations

## Key Features

- App uninstallation with orphaned file search
- Development environment management
- Homebrew integration
- Finder extension for right-click actions
- Universal app architecture handling (lipo)
- Plugin and services management
- Theme system with customization
- Deep link automation support
- CLI interface

## Development Notes

- This is a personal/hobby app with opinionated design choices
- Uses modern Swift/SwiftUI patterns
- Requires system permissions for full functionality
- Licensed under Apache 2.0 with Commons Clause (no monetization allowed)
- Issues must use appropriate GitHub issue templates