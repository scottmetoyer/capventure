# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

CapVenture is a MacVenture-style adventure game system consisting of two separate applications:

1. **Game Engine** (`engine/`) - Vue 3 + Vite + Capacitor cross-platform mobile app
2. **Game Creator** (`game-creator/`) - Vue 3 + Vite web-based game creation tool

## Project Structure

```
capventure/
├── engine/                 # Mobile game engine (Vue 3 + Capacitor)
│   ├── src/               # Game engine source code
│   ├── public/            # Game assets (images, icons, sounds)
│   ├── android/           # Android platform files
│   ├── ios/               # iOS platform files
│   ├── package.json       # Engine dependencies
│   └── capacitor.config.ts
├── game-creator/          # Web-based game creation tool
│   ├── src/               # Creator tool source code
│   ├── public/            # Creator tool web assets
│   └── package.json       # Creator tool dependencies
├── docs/                  # Shared documentation
├── PROJECT_REQUIREMENTS.md # Complete project specifications
└── CLAUDE.md              # This file
```

## Game Engine Architecture (`engine/`)

The mobile game engine follows a single-page architecture:
- `src/App.vue` - Main game interface with image display, text description, inventory, and action buttons
- `src/main.ts` - Entry point that mounts the Vue app
- Game images are expected in `public/images/`
- Inventory icons are expected in `public/icons/`

## Common Commands

### Game Engine Development (`engine/`)
```sh
cd engine
npm install          # Install engine dependencies
npm run dev         # Start development server with hot-reload
npm run preview     # Preview production build locally
npm run type-check  # Run TypeScript type checking
npm run build-only  # Build for production without type checking
npm run build       # Full build with type checking and production bundle
```

### Game Engine Mobile Development
```sh
cd engine
npx cap sync        # Sync web assets to mobile platforms
npx cap run ios     # Run on iOS simulator/device
npx cap run android # Run on Android emulator/device
npx cap open ios    # Open iOS project in Xcode
npx cap open android # Open Android project in Android Studio
```

### Game Creator Development (`game-creator/`)
```sh
cd game-creator
npm install          # Install creator tool dependencies
npm run dev         # Start development server for creator tool
npm run build       # Build creator tool for production
npm run preview     # Preview creator tool production build
npm run type-check  # Run TypeScript type checking for creator
```

## Key Files

### Game Engine (`engine/`)
- `capacitor.config.ts` - Capacitor configuration (app ID: com.scottmetoyer.capventure)
- `vite.config.ts` - Vite configuration with Vue plugin and path aliases (@/ points to src/)
- `package.json` - Node.js ^20.19.0 || >=22.12.0 required
- `ios/` directory - iOS project files
- `android/` directory - Android project files
- `dist/` directory - Web build output (configured in Capacitor)

### Game Creator (`game-creator/`)
- `vite.config.ts` - Vite configuration for web-based creator tool
- `package.json` - Dependencies for the creator tool
- `src/` - Creator tool source code
- `dist/` directory - Creator tool build output

## Mobile Platform Notes

- App is configured for mobile deployment with appropriate splash screens and icons
- Both engine and creator use the same Node.js version requirements
- The game creator outputs JSON files that the engine can load and execute