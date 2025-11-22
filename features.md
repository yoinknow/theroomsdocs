# Features Guide

Comprehensive overview of all TheRooms features and systems.

## 🏗️ Room System

### Room Types

TheRooms features 8 distinct room layouts, each designed for different play styles:

| Room Type | Dimensions | Layout | Best For |
|-----------|------------|--------|----------|
| Small | 7×5 | Rectangle | Beginners, cozy spaces |
| Medium | 9×9 | L-Shape | Creative layouts |
| Large | 11×8 | T-Shape | Events, gatherings |
| Studio | 10×6 | Rectangle | Modern minimal design |
| L-Shape | 10×10 | L-Shape | Flexible arrangement |
| Penthouse | 12×10 | Plus | Premium showcases |
| Loft | 8×11 | Vertical L | Vertical emphasis |
| Suite | 13×7 | Wide T | Grand designs |

### Room Features
- **Grid-based building**: Furniture snaps to a grid for clean placement
- **Customizable colors**: Change floor and wall colors
- **Named spaces**: Give your room a unique name
- **Persistent state**: Your room saves automatically
- **Physics-enabled**: Realistic collisions and interactions

### Spawn System
- Players spawn at Y=1.5 height for safe drop
- Spawn points near room doors (X=0.5)
- Auto-respawn if falling detected (below Y=-3)
- Room-specific spawn coordinates

## 🎭 Character System

### Character Models
- **45+ models** available
- Includes male and female options
- Various styles: Casual, Business, Themed
- Full animation support (Idle, Walk, more coming)

### Character Features
- **Smooth animations**: Seamless transitions between states
- **Physics-based movement**: Realistic collision and walking
- **Customization**: Easy character switching
- **Scale optimized**: Characters sized at 0.7 scale for perfect proportions

## 🪑 Furniture & Placement

### Placement System
- **Grid-based**: Items snap to grid positions
- **Visual feedback**: See placement preview before confirming
- **Collision detection**: Items don't overlap
- **Easy removal**: Click items to remove or move them

### Current Furniture Categories
- Seating (chairs, sofas)
- Tables (various sizes)
- Decorations
- Lighting
- Storage

*More categories coming soon!*

## 🎮 Movement & Controls

### Player Movement
- **Walk speed**: 3.5 units/second
- **Sprint speed**: 6.0 units/second (coming soon)
- **Jump**: Planned feature
- **Smooth rotation**: Character faces movement direction
- **Climb prevention**: Realistic collision boundaries

### Physics Properties
- Friction: 3 (prevents sliding)
- Gravity scale: 1.5 (natural feel)
- Ground detection: 1.0 unit raycast
- Fall protection: Auto-reset below Y=-3

## 🤖 NPC System

### NPC Behavior
- **Autonomous movement**: NPCs wander randomly within range
- **State machine**: Idle → Walk → Idle cycle
- **Idle duration**: 3 seconds
- **Walk duration**: 4 seconds
- **Walk speed**: 1.5 units/second

### NPC Features
- Full animation support (Idle, Walk)
- Collision detection
- Random pathfinding within 4-unit radius
- Character model variety

## 📹 Camera System

### Isometric View
- Fixed isometric perspective
- Optimized for each room type
- Smooth camera transitions

### Room-Specific Settings
Each room has custom camera positioning:
- **Distance**: How far the camera is from the room
- **Angle**: Camera rotation for best view
- **Height**: Vertical offset for optimal framing

### Debug Mode
- Toggle collision visualization
- See floor boundaries
- Useful for placement testing

## 💬 Chat System

### Features
- Real-time messaging
- Chat history display
- Message persistence
- Clean UI overlay

### Planned Enhancements
- Private messages
- Chat commands
- Emojis and reactions
- Message filtering

## 🎨 Customization

### Room Customization
- **Floor color**: Choose from color palette
- **Wall color**: Match or contrast with floor
- **Room name**: Personalize your space
- More options coming (textures, patterns)

### Future Customization
- Custom textures
- Lighting effects
- Weather/time of day
- Music and ambiance

## 💾 State Management

### What Gets Saved
- Room settings (name, colors)
- Furniture placement and positions
- Selected character
- Player position
- Interaction history

### Storage
- **localStorage** for browser persistence
- Automatic save on changes
- No manual save needed

## 🔧 Technical Features

### Performance
- Optimized 3D rendering
- Efficient physics calculations
- Asset loading management
- Smooth 60 FPS target

### Cross-Browser Support
- Chrome ✅
- Firefox ✅
- Safari ✅
- Edge ✅

### Responsive Design
- Desktop optimized
- Mobile support in progress
- Touch controls planned

## 🚀 Coming Soon

### In Development
- [ ] Multiplayer synchronization
- [ ] More furniture items
- [ ] Enhanced NPC dialogues
- [ ] Inventory system
- [ ] Trading system

### Planned Features
- [ ] Room ownership tokens
- [ ] Mini-games
- [ ] Friend system
- [ ] Achievements
- [ ] Events and competitions

---

Have suggestions for new features? Let us know during our livestreams! 🎮
