# CapVenture

A MacVenture-style adventure game system consisting of two applications:

1. **Game Engine** - Mobile app for playing adventure games
2. **Game Creator** - Web-based tool for creating games

## Project Structure

- `engine/` - Vue 3 + Capacitor mobile game engine
- `game-creator/` - Vue 3 web-based game creation tool
- `docs/` - Shared documentation
- `PROJECT_REQUIREMENTS.md` - Complete project specifications

## Quick Start

### Game Engine Development
```bash
cd engine
npm install
npm run dev
```

### Game Creator Development
```bash
cd game-creator
npm install
npm run dev
```

### Mobile Development (Engine)
```bash
cd engine
npx cap sync
npx cap run ios     # or android
```

## Recommended IDE Setup

[VSCode](https://code.visualstudio.com/) + [Volar](https://marketplace.visualstudio.com/items?itemName=Vue.volar) (and disable Vetur).

## Documentation

See `PROJECT_REQUIREMENTS.md` for complete project specifications and `CLAUDE.md` for development guidance.
