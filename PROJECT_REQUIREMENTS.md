# CapVenture - MacVenture-Style Adventure Game System
## Project Requirements Document

### 1. Project Overview

CapVenture is a cross-platform mobile adventure game framework inspired by classic MacVenture games (Shadowgate, Déjà Vu, Uninvited). The system consists of:

1. **Game Engine** - Vue 3/TypeScript mobile app that renders and executes games
2. **Game Creation Tools** - Web-based editor for creating games and content
3. **Game Data Format** - JSON-based game definition files

### 2. Game Engine Requirements

#### 2.1 Core Architecture
- **Platform**: Vue 3 + TypeScript + Capacitor for iOS/Android
- **Single-page application** with dynamic content loading
- **Data-driven** game execution from JSON game files
- **Modular script system** for game logic and interactions

#### 2.2 User Interface Components

##### Main Play Area
- **Background image display** with full-screen support
- **Invisible hotspot detection** via coordinate-based hit testing
- **Visual feedback** for interactive elements (highlight on hover/tap)
- **Responsive scaling** for different screen sizes and orientations
- **Text overlay area** for descriptive text and dialogue

##### Action State Buttons (Bottom Panel)
- **Examine** - Look at objects and get descriptions
- **Move To** - Navigate to locations or approach objects
- **Take** - Pick up items and add to inventory
- **Use** - Interact with objects or use inventory items
- **Open** - Open doors, containers, etc.
- **Close** - Close doors, containers, etc.
- **Talk** - Communicate with characters
- **Custom actions** as defined by game data

##### Inventory System
- **Horizontal scrollable bar** above action buttons
- **Drag and drop** support for using items on play area
- **Tap to select** inventory items for use
- **Visual item icons** with optional text labels
- **Item combination** support (use item A on item B)
- **Capacity limits** and organization

##### User Interaction Flow
1. Player taps action button to set interaction state
2. Player taps play area hotspot to execute action
3. System runs associated script for action/hotspot combination
4. Results displayed via text, scene changes, inventory updates, etc.

#### 2.3 Hotspot System

##### Hotspot Definition
- **Rectangular or polygonal boundaries** defined by coordinates
- **Multiple states per hotspot** (examine, take, use, etc.)
- **Script associations** for each state
- **Conditional visibility** based on game flags
- **Visual debugging mode** to show hotspot boundaries

##### Hit Detection
- **Coordinate-based detection** for taps/clicks
- **Z-order/layering** for overlapping hotspots
- **Active state consideration** (only respond when relevant action selected)

#### 2.4 Scripting System

##### Script Engine Features
- **JavaScript execution engine** for game logic and interactions
- **Sandboxed execution** for security and stability
- **Game API exposure** for script access to engine functions
- **Error handling** and script debugging support
- **Script context isolation** per hotspot/action execution

##### Game API Functions (Available to Scripts)
- **displayText(text)** - Show text to player
- **setFlag(name, value)** - Set game flag/variable
- **getFlag(name)** - Get game flag/variable value
- **hasItem(itemId)** - Check if player has inventory item
- **addItem(itemId)** - Add item to player inventory
- **removeItem(itemId)** - Remove item from player inventory
- **changeScene(sceneId)** - Transition to different scene
- **playSound(filename)** - Play sound effect
- **playMusic(filename)** - Play background music
- **showImage(filename)** - Display overlay image
- **enableHotspot(hotspotId)** / **disableHotspot(hotspotId)** - Toggle hotspot availability

##### Script Execution Context
Scripts have access to:
- **game** - Game state object (flags, variables, inventory)
- **player** - Player state and inventory
- **scene** - Current scene information
- **hotspot** - Current hotspot being interacted with
- **action** - Current action being performed

#### 2.5 Save System
- **Multiple save slots** (minimum 3 slots)
- **Auto-save functionality** at key game moments
- **Save data includes**:
  - Current scene/background
  - All game flags and variables
  - Complete inventory state
  - Player progress markers
- **Cloud save support** via Capacitor native plugins
- **Save file validation** and corruption recovery

#### 2.6 Game Data Loading
- **JSON game file parsing** from local or remote sources
- **Asset preloading** (images, sounds) with progress indication
- **Incremental loading** for large games
- **Error handling** for missing assets or malformed data
- **Multiple game support** (game selection menu)

### 3. Game Creation Tools Requirements

#### 3.1 Web-Based Game Editor
- **Browser-based tool** built with Vue 3
- **No installation required** - runs in modern web browsers
- **Export functionality** to generate JSON game files
- **Import capability** to load and edit existing games

#### 3.2 Scene Editor

##### Background Management
- **Image upload** and preview
- **Multiple resolution support** for different devices
- **Background library** for reusable assets

##### Hotspot Creation Tool
- **Visual hotspot drawing** with mouse/touch
- **Rectangle and polygon** drawing modes
- **Hotspot resizing and repositioning**
- **Visual hotspot overlay** with labels
- **Copy/paste hotspots** between scenes
- **Hotspot templates** for common interactions

##### Hotspot Configuration
- **Action/script binding interface** for each hotspot state
- **Visual script editor** with drag-and-drop actions
- **Script testing** and preview functionality
- **Conditional logic builder** for complex interactions

#### 3.3 Game Asset Manager
- **Image asset library** with upload and organization
- **Sound effect library** with preview playback
- **Icon management** for inventory items
- **Asset compression** and optimization tools
- **Usage tracking** (which assets are used where)

#### 3.4 Script Editor
- **JavaScript code editor** with syntax highlighting
- **Visual scripting interface** with drag-and-drop API function blocks
- **Auto-completion** for game API functions
- **Syntax validation** and error highlighting
- **Script templates** for common game interactions
- **Variable and flag management** interface
- **Script testing** and debugging tools with console output
- **API documentation** panel showing available functions

#### 3.5 Game Testing and Preview
- **In-browser game preview** without export
- **Hotspot visualization** mode for debugging
- **Script execution tracing** for troubleshooting
- **Mobile preview** simulation for different screen sizes

### 4. Game Data Format

#### 4.1 JSON Structure with JavaScript Scripts
The game data format is JSON with embedded JavaScript code strings for scripts:

```json
{
  "gameInfo": {
    "title": "Castle Mystery",
    "version": "1.0",
    "author": "Game Creator",
    "description": "A thrilling castle adventure"
  },
  "scenes": [
    {
      "id": "castle_entrance",
      "background": "castle_entrance.jpg",
      "description": "You stand before an imposing castle gate.",
      "hotspots": [
        {
          "id": "gate",
          "bounds": {"x": 100, "y": 150, "width": 200, "height": 300},
          "actions": {
            "examine": {"script": "examine_gate_script"},
            "use": {"script": "use_gate_script", "requiredItem": "key"}
          }
        }
      ]
    }
  ],
  "scripts": {
    "examine_gate_script": "displayText('An ancient wooden gate with iron hinges.'); setFlag('gateExamined', true);",
    "use_gate_script": "if (hasItem('key')) { displayText('The key fits perfectly! The gate creaks open.'); changeScene('castle_interior'); } else { displayText('The gate is locked tight.'); }"
  },
  "inventory": [
    {
      "id": "rusty_key",
      "name": "Rusty Key",
      "icon": "key_icon.png",
      "description": "An old key with intricate engravings"
    }
  ],
  "gameFlags": {},
  "gameVariables": {},
  "startingScene": "castle_entrance"
}
```

#### 4.2 JavaScript Script Examples

##### Simple Text Display
```javascript
displayText("You examine the mysterious object closely.");
setFlag("objectExamined", true);
```

##### Conditional Logic
```javascript
if (getFlag("doorUnlocked")) {
    displayText("The door is already open.");
    changeScene("inside_room");
} else {
    displayText("The door is locked.");
    if (hasItem("skeleton_key")) {
        displayText("But you have a key that might work...");
    }
}
```

##### Complex Interaction
```javascript
// Check multiple conditions
if (hasItem("torch") && getFlag("oilFound")) {
    displayText("You light the torch with the oil. The room illuminates!");
    setFlag("torchLit", true);
    addItem("lit_torch");
    removeItem("torch");
    playSound("torch_light.mp3");
    enableHotspot("hidden_passage");
} else if (!hasItem("torch")) {
    displayText("You need something to burn first.");
} else {
    displayText("The torch won't light without fuel.");
}
```

### 5. Technical Specifications

#### 5.1 Mobile App Technical Stack
- **Frontend**: Vue 3 with Composition API
- **Language**: TypeScript for type safety
- **Mobile Framework**: Capacitor for native device access
- **Build Tool**: Vite for fast development and building
- **State Management**: Pinia for game state management
- **Styling**: CSS/SCSS with mobile-first responsive design

#### 5.2 Game Editor Technical Stack
- **Frontend**: Vue 3 with TypeScript
- **Build Tool**: Vite
- **UI Framework**: Consider Vue component library (Quasar, Vuetify)
- **File Handling**: File API for game data import/export
- **Canvas Drawing**: HTML5 Canvas for hotspot creation

#### 5.3 Performance Requirements
- **Smooth 60fps** rendering on target mobile devices
- **Fast scene transitions** (< 300ms)
- **Efficient memory usage** for asset loading
- **Responsive touch interactions** (< 100ms response time)
- **Secure JavaScript execution** with sandboxing to prevent malicious scripts
- **Script execution limits** to prevent infinite loops or excessive resource usage

### 6. Platform Support

#### 6.1 Target Platforms
- **iOS**: iOS 13+ (iPhone and iPad)
- **Android**: Android 8+ (API level 26+)
- **Web**: Modern browsers for game editor tool

#### 6.2 Device Considerations
- **Screen sizes**: 4" phones to 12" tablets
- **Orientation**: Portrait and landscape support
- **Touch targets**: Minimum 44px for accessibility
- **Performance**: Optimize for mid-range devices

### 7. Development Phases

#### Phase 1: Core Engine
1. Basic Vue 3 + Capacitor setup
2. Scene rendering and hotspot detection
3. Action button system
4. Basic scripting engine
5. Simple JSON game file loading

#### Phase 2: Advanced Features
1. Inventory system with drag/drop
2. Save/load functionality
3. Advanced scripting features
4. Sound and music support
5. Game testing and debugging tools

#### Phase 3: Content Creation Tools
1. Web-based scene editor
2. Visual hotspot creation tool
3. Script editor interface
4. Asset management system
5. Game export and testing

#### Phase 4: Polish and Optimization
1. Performance optimization
2. Advanced UI/UX improvements
3. Accessibility features
4. Documentation and tutorials
5. Example game content

### 8. Success Metrics

- **Functional game engine** that can run MacVenture-style games
- **Intuitive creation tools** that allow non-programmers to create games
- **Cross-platform compatibility** on iOS and Android
- **Performance targets** met on target devices
- **Complete example game** demonstrating all features

This requirements document will guide the development process and ensure all stakeholder needs are met for the CapVenture adventure game system.