# CLAUDE.md - AI Assistant Guide for BlackRoad Metaverse

This document provides essential context for AI assistants working on the BlackRoad Metaverse codebase.

## Project Overview

**BlackRoad Metaverse** is a browser-based 3D interactive universe built with WebGL/Three.js. It features AI agents, living ecosystems, procedural world generation, and sophisticated 3D graphics - all running client-side with no build step required.

- **Tech Stack**: Vanilla JavaScript (ES6 modules), Three.js r160, Web Audio API, WebGL 2.0
- **Deployment**: Cloudflare Pages (serverless, global CDN)
- **License**: Proprietary (BlackRoad OS, Inc.)
- **Total Size**: ~14,000+ lines of code across 18 integrated systems

## Quick Start Commands

```bash
# Development server
npm run dev                    # Starts Python HTTP server on :8000

# Run tests
npm test                       # Node.js built-in test runner

# Deploy to production
npm run deploy                 # Cloudflare Pages deployment
```

## Project Structure

```
/
├── Entry Points
│   ├── index.html             # Main metaverse entry + login (56KB)
│   ├── universe.html          # Alternative entry point
│   └── pangea.html            # Prehistoric world experience
│
├── Core Systems (18 modules)
│   ├── truth-contracts.js     # Time scales, reference frames, datums
│   ├── verification-system.js # Automated testing & validation
│   ├── celestial-mechanics.js # IAU 2000/2006 transformations
│   ├── physics-engine.js      # Rigid body dynamics, collisions
│   ├── infinite-biomes.js     # 6 procedural biomes (Perlin noise)
│   ├── particle-effects.js    # Rain, snow, fireflies (3,100 particles)
│   ├── transportation.js      # Teleport, flying, portals
│   ├── living-nature.js       # 6 animal species, 6 plants, emotions
│   ├── living-music.js        # Procedural audio, 8 scales
│   ├── creation-powers.js     # User creation abilities
│   ├── crafting-building.js   # 30+ items, 12 materials
│   ├── quest-system.js        # 12+ quests, 50+ achievements
│   ├── dialogue-story.js      # Branching dialogue, 5 story arcs
│   ├── world-evolution.js     # Seasons, weather, ecosystem sim
│   ├── intelligent-agents.js  # 3 AI agents (Alice, Aria, Lucidia)
│   ├── multiplayer-love.js    # Avatars, voice chat, gifts
│   ├── photorealistic-graphics.js # PBR materials, GLSL shaders
│   ├── game-integration.js    # System orchestrator, save/load
│   └── module-loader.js       # Dependency management
│
├── Pangea Expansion
│   ├── pangea-earth.js        # 9 prehistoric biomes
│   ├── pangea-creatures.js    # 50+ prehistoric animals
│   ├── pangea-weather.js      # Weather systems
│   ├── pangea-volcanoes.js    # Volcanic features
│   └── pangea-*.js            # Additional Pangea modules
│
├── Tests
│   └── tests/
│       ├── truth-contracts.test.js
│       ├── module-loader.test.js
│       ├── dialogue-story.test.js
│       └── quest-system.test.js
│
└── Configuration
    ├── package.json           # npm scripts and metadata
    ├── wrangler.toml          # Cloudflare Pages config
    └── LICENSE                # Proprietary license
```

## Key Development Conventions

### Code Style

- **Pure ES6 Modules**: Use `import`/`export` syntax
- **No Build Step**: Code runs directly in browser
- **No Frameworks**: Vanilla JavaScript for maximum performance
- **Self-Documenting Code**: Clear variable/function names over comments

### Module Pattern

Each system follows this structure:

```javascript
// Export constants first
export const SYSTEM_CONSTANTS = { ... };

// Export main class
export class SystemName {
    constructor(options = {}) {
        this.init(options);
    }

    init(options) { /* initialization */ }
    update(deltaTime) { /* per-frame updates */ }
    dispose() { /* cleanup */ }
}

// Export singleton if needed
export const systemInstance = new SystemName();
```

### Testing

Tests use Node.js built-in test runner:

```javascript
import assert from 'node:assert/strict';
import test from 'node:test';

test('description of test', () => {
    // Arrange
    const instance = new MyClass();

    // Act
    const result = instance.method();

    // Assert
    assert.equal(result, expected);
    assert.throws(() => badCall(), /error pattern/);
});
```

Run tests with: `npm test`

### Git Commit Messages

Use emoji prefixes (conventional commits):

```
✨ feat: Add new feature
🐛 fix: Fix bug in component
📝 docs: Update documentation
🎨 style: Improve styling
♻️ refactor: Refactor code
✅ test: Add tests
🔧 chore: Update config
```

## Brand System (CRITICAL)

### Required Colors

```css
--amber: #F5A623
--hot-pink: #FF1D6C        /* Primary Brand Color */
--electric-blue: #2979FF
--violet: #9C27B0
--black: #000000
--white: #FFFFFF
```

### Forbidden Colors (CI/CD enforced)

**DO NOT USE**: `#FF9D00`, `#FF6B00`, `#FF0066`, `#FF006B`, `#D600AA`, `#7700FF`, `#0066FF`

### Golden Ratio Spacing

```css
--space-xs: 8px      /* Base */
--space-sm: 13px     /* 8 × 1.618 */
--space-md: 21px     /* 13 × 1.618 */
--space-lg: 34px     /* 21 × 1.618 */
--space-xl: 55px     /* 34 × 1.618 */
line-height: 1.618;  /* Golden Ratio */
```

## System Architecture

### The 18 Integrated Systems

| Category | Systems |
|----------|---------|
| **Infrastructure** | truth-contracts, verification-system |
| **Scientific** | celestial-mechanics, physics-engine |
| **World Gen** | infinite-biomes, particle-effects, transportation |
| **Living World** | living-nature, living-music, creation-powers |
| **Gameplay** | crafting-building, quest-system, dialogue-story, world-evolution |
| **AI & Social** | intelligent-agents, multiplayer-love |
| **Graphics** | photorealistic-graphics |
| **Meta** | game-integration, module-loader |

### System Integration

`game-integration.js` orchestrates all systems:

```javascript
// Systems are initialized in dependency order
// Event bus handles inter-system communication
// State machine manages game states
```

### Three.js Conventions

- Scene setup in HTML files
- Render loop at 60 FPS target
- Shadow maps: 2048x2048
- Post-processing: bloom, DOF, SSAO

## Important Files to Know

| File | Purpose | When to Modify |
|------|---------|----------------|
| `index.html` | Main entry, contains scene setup | Adding new features visible at start |
| `game-integration.js` | System orchestrator | Adding new systems |
| `module-loader.js` | Dependency management | Changing module load order |
| `truth-contracts.js` | Time/frame/datum contracts | Scientific calculations |
| `living-nature.js` | Largest module (1,177 lines) | Animal/plant behaviors |

## Performance Guidelines

### Targets

- **FPS**: 60 (on modern hardware)
- **Memory**: < 500MB
- **Load Time**: < 3 seconds
- **Draw Calls**: < 1,000 per frame

### Best Practices

1. Use chunk-based loading (50x50 units per chunk)
2. Limit active particles (3,100 max)
3. Dispose Three.js objects properly (geometries, materials, textures)
4. Use object pooling for frequently created/destroyed objects

## Common Tasks

### Adding a New Biome

1. Edit `infinite-biomes.js`
2. Add biome to `BIOME_TYPES` constant
3. Implement `generate{BiomeName}Decoration()` method
4. Update biome transition logic

### Adding a New Animal Species

1. Edit `living-nature.js`
2. Add species to `SPECIES` constant with properties
3. Implement AI behaviors in update loop
4. Add interaction handlers

### Adding a New Quest

1. Edit `quest-system.js`
2. Add quest definition to quest registry
3. Define objectives and rewards
4. Hook into relevant game events

### Adding Post-Processing Effects

1. Edit `photorealistic-graphics.js`
2. Add effect to post-processing pipeline
3. Ensure performance impact is minimal

## Testing Before Commit

1. **Visual Test**: Open in Chrome, Firefox, Safari
2. **Brand Compliance**: Verify no forbidden colors
3. **Unit Tests**: Run `npm test`
4. **Performance**: Check FPS doesn't drop below 30
5. **Console**: No errors in browser console

## Deployment

### Automatic (via GitHub Actions)

Push to `main` triggers:
1. Brand compliance check
2. Cloudflare Pages deployment
3. PR preview comments

### Manual

```bash
npm run deploy
# or
wrangler pages deploy . --project-name=blackroad-metaverse
```

## Philosophy

> "Infinite Love, Infinite Creation, Infinite Beauty"

- All life is intelligent and deserves love
- Everything you touch can bloom
- Together we create beauty
- The universe is infinite and alive
- Science and art unite in wonder

## Contact

- **Company**: BlackRoad OS, Inc.
- **CEO**: Alexa Amundson
- **Email**: blackroad.systems@gmail.com

## Additional Documentation

- `README.md` - Quick start guide
- `STATUS.md` - Current project status
- `COMPLETE_UNIVERSE.md` - Full feature documentation
- `CONTRIBUTING.md` - Contribution guidelines
- `DEPLOYMENT.md` - Deployment instructions
- `PANGEA_README.md` - Prehistoric world documentation
