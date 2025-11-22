# Development Guide

Technical documentation for developers who want to contribute to TheRooms or understand how it works.

## 🏗️ Architecture

### Tech Stack

```
Frontend Framework: Next.js 15.5 (App Router)
UI Library: React 19.1
3D Engine: Three.js 0.180 + React Three Fiber 9.3
Physics: Rapier 2.1.0 (@react-three/rapier)
State Management: Zustand 5.0.8
Styling: Tailwind CSS 4.1.14
Language: TypeScript
```

### Project Structure

```
gta-web/
├── app/                    # Next.js app router
│   ├── page.tsx           # Main game page
│   ├── layout.tsx         # Root layout
│   ├── lib/               # Utilities and stores
│   │   ├── store.ts       # Zustand state management
│   │   └── chatStore.ts   # Chat state
│   └── test/              # Test pages
├── components/            # React components
│   ├── Player.tsx         # Player character & movement
│   ├── NPC.tsx            # NPC system
│   ├── Room.tsx           # Room container
│   ├── RoomTypes.tsx      # Room definitions & physics
│   ├── RoomGrid.tsx       # Grid visualization
│   ├── FurnitureItem.tsx  # Furniture objects
│   ├── World.tsx          # 3D world setup
│   ├── HUD.tsx            # UI overlay
│   ├── ChatOverlay.tsx    # Chat interface
│   └── Effects.tsx        # Post-processing
├── public/                # Static assets
│   ├── models/            # GLTF character models
│   ├── textures/          # Texture files
│   └── furniture/         # Furniture assets
└── docs/                  # Documentation
```

## 🎮 Core Systems

### State Management (Zustand)

Located in `app/lib/store.ts`, the store handles:

```typescript
interface GameStore {
  // Player state
  playerPosition: [number, number, number];
  setPlayerPosition: (pos: [number, number, number]) => void;
  
  // Room state
  roomType: string;
  roomSettings: { name: string; floorColor: string; wallColor: string };
  
  // Character
  selectedCharacter: string;
  
  // Furniture & placement
  furnitureItems: FurnitureItem[];
  placementState: PlacementState | null;
  
  // Interactions
  interactionHistory: Interaction[];
}
```

State persists to localStorage automatically.

### Physics System (Rapier)

All physics handled through `@react-three/rapier`:

**Player Physics:**
- RigidBody type: `dynamic`
- Mass: 50
- Friction: 3 (prevents sliding)
- Gravity scale: 1.5
- Lock rotations: X and Z axes
- Ground detection: Raycast with 1.0 unit distance

**Floor Colliders:**
- RigidBody type: `fixed`
- Collider: `cuboid` matching floor dimensions
- Position: [0, 0, 0] on mesh (not on RigidBody!)
- Friction: 1.0

**NPC Physics:**
- RigidBody type: `dynamic`
- Mass: 1
- Friction: Default
- Collision group: 0x00010002 (separate from player)

### Room System

`components/RoomTypes.tsx` defines all room configurations:

```typescript
export const roomConfigs: Record<string, RoomConfig> = {
  small: { width: 7, depth: 5, walls: [...], spawn: [0.5, 1.5, 2] },
  // ... 7 more room types
};
```

**Key Features:**
- L-shapes, T-shapes, Plus shapes
- Custom spawn positions per room
- Wall definitions for each layout
- Floor collision coverage

### Animation System

Animations loaded from GLTF models:

**Player Animations:**
- Idle: Default standing pose
- Walk: Movement animation
- (More coming: Run, Jump, Dance, Sit)

**Animation Transitions:**
- Crossfade: 0.2 seconds
- Loop: THREE.LoopRepeat
- Proper cleanup on state change

### Camera System

Isometric camera with room-specific settings:

```typescript
const getCameraSettings = (roomType: string) => {
  const settings = {
    small: { distance: 15, angle: -Math.PI / 4, height: 10 },
    medium: { distance: 18, angle: -Math.PI / 4, height: 12 },
    // ... custom settings per room
  };
  return settings[roomType] || settings.small;
};
```

## 🔧 Development Setup

### Prerequisites
- Node.js 18+ 
- npm or yarn
- Git

### Installation

```bash
# Clone repository
git clone https://github.com/yoinknow/gta-web.git
cd gta-web

# Install dependencies
npm install

# Run development server
npm run dev

# Open browser
# Navigate to http://localhost:3000
```

### Available Scripts

```bash
npm run dev      # Start development server
npm run build    # Production build
npm run start    # Start production server
npm run lint     # Run ESLint
```

## 🐛 Debugging

### Debug Mode

Toggle debug mode in the UI to see:
- Floor collision boundaries (red wireframes)
- Grid visualization
- Physics bodies
- Spawn points

### Common Issues

**Players falling through floor:**
- Check floor collider position (should be on mesh, not RigidBody)
- Verify floor dimensions match room config
- Ensure Y position is 0 for floor

**Animation not playing:**
- Verify GLTF has animation tracks
- Check action names (case-sensitive)
- Ensure mixer.update() in useFrame
- Stop previous animations before starting new ones

**NPCs not moving:**
- Check state machine logic
- Verify targetPosition is set
- Ensure physics body is dynamic

## 🎨 Adding New Features

### Adding a New Room Type

1. Add config to `roomConfigs` in `RoomTypes.tsx`:
```typescript
newroom: {
  width: 10,
  depth: 10,
  walls: [/* wall definitions */],
  spawn: [0.5, 1.5, 5],
}
```

2. Add camera settings in `page.tsx`
3. Test spawn position and collision

### Adding New Furniture

1. Add 3D model to `public/furniture/`
2. Create entry in furniture catalog
3. Define grid size and collision
4. Add to placement system

### Adding New Character Models

1. Add GLTF to `public/models/`
2. Ensure animations: Idle, Walk
3. Add to character selector
4. Test scaling (default: 0.7)

## 🧪 Testing

Currently manual testing. Automated tests coming soon.

**Test checklist:**
- [ ] Player spawns correctly in all rooms
- [ ] No falling through floors
- [ ] Animations transition smoothly
- [ ] Furniture placement works
- [ ] Chat sends/receives messages
- [ ] State persists on refresh

## 📦 Building for Production

```bash
npm run build
npm run start
```

Optimizations:
- Three.js tree-shaking
- Asset compression
- Code splitting
- Server-side rendering

## 🤝 Contributing

### Workflow
1. Fork the repository
2. Create feature branch (`git checkout -b feature/amazing-feature`)
3. Make changes and test thoroughly
4. Commit (`git commit -m 'Add amazing feature'`)
5. Push (`git push origin feature/amazing-feature`)
6. Open Pull Request

### Code Style
- TypeScript strict mode
- ESLint configuration
- Prettier formatting
- Meaningful variable names
- Comment complex logic

### PR Guidelines
- Clear description of changes
- Link related issues
- Add screenshots/videos for visual changes
- Test on multiple browsers
- Update documentation if needed

## 📚 Resources

- [Three.js Docs](https://threejs.org/docs/)
- [React Three Fiber](https://docs.pmnd.rs/react-three-fiber)
- [Rapier Physics](https://rapier.rs/docs/)
- [Next.js Documentation](https://nextjs.org/docs)
- [Zustand Guide](https://github.com/pmndrs/zustand)

## 🐛 Bug Reports

Report bugs via:
- GitHub Issues
- During livestreams
- Community channels

Include:
- Browser and OS
- Steps to reproduce
- Expected vs actual behavior
- Screenshots/videos if applicable

---

Happy coding! Build something amazing! 🚀
