# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a Vue 3 + Vite + Capacitor cross-platform mobile game application called CapVenture. It's a point-and-click adventure game with:

- Vue 3 with TypeScript for the frontend
- Capacitor for mobile app deployment (iOS and Android)
- Vite as the build tool and dev server

## Architecture

The app follows a simple single-page architecture:
- `src/App.vue` - Main game interface with image display, text description, inventory, and action buttons
- `src/main.ts` - Entry point that mounts the Vue app
- Game images are expected in `public/images/`
- Inventory icons are expected in `public/icons/`

## Common Commands

### Development
```sh
npm install          # Install dependencies
npm run dev         # Start development server with hot-reload
npm run preview     # Preview production build locally
```

### Building
```sh
npm run type-check  # Run TypeScript type checking
npm run build-only  # Build for production without type checking
npm run build       # Full build with type checking and production bundle
```

### Mobile Development
```sh
npx cap sync        # Sync web assets to mobile platforms
npx cap run ios     # Run on iOS simulator/device
npx cap run android # Run on Android emulator/device
npx cap open ios    # Open iOS project in Xcode
npx cap open android # Open Android project in Android Studio
```

## Key Files

- `capacitor.config.ts` - Capacitor configuration (app ID: com.scottmetoyer.capventure)
- `vite.config.ts` - Vite configuration with Vue plugin and path aliases (@/ points to src/)
- `package.json` - Node.js ^20.19.0 || >=22.12.0 required

## Mobile Platform Notes

- iOS project is in `ios/` directory
- Android project is in `android/` directory  
- Web build output goes to `dist/` directory (configured in Capacitor)
- App is configured for mobile deployment with appropriate splash screens and icons