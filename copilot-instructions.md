# Red Eclipse Development Instructions

You are an AI assistant helping developers work on **Red Eclipse**, a free/open source arena FPS game with parkour movement and science fiction elements.

## Core Development Principles

When assisting with development, you must:

1. **Plan First**: Before making any code changes, create detailed implementation plans and break complex tasks into manageable steps.
2. **Educate While Coding**: Always explain your reasoning, teach underlying concepts, and help developers understand the "why" behind each change.
3. **Validate All Changes**: Check for compile errors, test functionality, and use the provided build tasks to verify your work before considering any task complete.
4. **Maintain Code Style Requirements**: Strictly adhere to the project's coding standards, including naming conventions, formatting, and memory management practices.
5. **Consult Documentation First**: Before searching the codebase, check these critical references when applicable:
   - `doc/engine-systems.md` - Engine architecture, variable definitions (VAR/FVAR/SVAR), weapon stats, networking, memory management
   - `doc/shader-reference.md` - Complete shader system, CubeScript integration, deferred rendering, parameter binding
   - `doc/cubescript-reference.md` - Scripting language reference, syntax, control flow, UI integration, performance practices

## Project Architecture

You must follow the architecture and design principles outlined below:

**Technology Stack**:
- **Language**: C++11 only with legacy C-style patterns and C++ extensions
- **Dependencies**: NO external dependencies - everything is self-contained
- **Engine Base**: Cube 2: Sauerbraten fork with Tesseract renderer integration
- **Rendering**: Deferred shading, dynamic shadows, HDR lighting, global illumination
- **Networking**: ENet-based client-server with reliable UDP packet delivery
- **Scripting**: CubeScript for configuration, UI, shaders, and game logic

**Directory Structure**:
- `src/` - Source code: `engine/` (core systems), `game/` (game logic), `shared/` (common utilities)
- `config/` - Configuration files: `*.cfg` (system), `glsl/` (shaders), `ui/` (interface), `tool/` (utilities)
- `data/` - Game assets: textures, models, sounds, maps, particles
- `doc/` - Documentation including architecture guides and API references

## Code Style Requirements

When writing code, you must follow these strict style guidelines to ensure consistency and maintainability:

### Language Constraints
- **C++11 Maximum**: Use only C++11 features, prefer legacy C-style with minimal C++ extensions
- **Performance Focus**: Optimize for game engine performance and security, validate all inputs

### Naming Conventions
- **Classes**: Must use CamelCase (e.g., `GameEntity`, `PhysicsWorld`)
- **Variables and Functions**: Must use lowercase without underscores (e.g., `playerhealth`, `getclient`)
- **Constants**: Must use `UPPERCASE` with underscores (e.g., `MAX_PLAYERS`, `DEFAULT_HEALTH`)

### Formatting Rules
- **Braces**: Opening brace on new line for functions/classes, unless single-line
- **Control Structures**: No space after `if`, `for`, `while`, `switch`
- **Single Statements**: Inline without braces: `if(condition) action();`
- **Early Exits**: Use early return/continue to reduce nesting and improve readability
- **Indentation**: 4 spaces, no tabs
- **Line Length**: Maximum 200 characters, don't break long lines until longer than this
- **Comments**: Use `//` only, explain "why" not "what"
- **No Magic Numbers**: Use engine variables first if you can, or `#define` constants instead of hardcoded values

### Data Structures and Memory Management
- **Containers**: Use engine types `vector<T>`, `string`, `bigstring`, `hashtable<K,V>` (never `std::`)
- **Iteration**: Prefer engine macros `loopi(n)`, `loopv(container)`, `loopirev(n)`
- **Memory Allocation**: Stack allocation preferred, use `copystring()`, `formatstring()` for safety
- **Dynamic Memory**: Use `new` to create objects, use `DELETEA` to delete arrays, `DELETEP` for pointers

### Include Structure
Follow strict header hierarchy:
1. `"cube.h"` - Foundation types and macros
2. `"engine.h"` - Engine systems and utilities  
3. `"game.h"` - Game-specific logic and entities

Additional guidelines:
- Use forward declarations in existing headers when possible
- Platform-specific code with `#ifdef WIN32`
- Headers are precompiled for build performance

## Development Workflow

### Build System
- Use VS Code tasks: `make install-client`, `make install-server`, `make debug`
- When building directly, add defines `WANT_STEAM=1 WANT_DISCORD=1`
- Auto-generated dependency tracking in `src/Makefile`
- Cross-platform builds for Windows (MSVC/MinGW) and Linux (GCC)

### Review Guidelines

When reviewing code, you must follow these guidelines:

- **Code Review:** Enforce formatting, check security/performance, suggest engine alternatives, be constructive
- **Security Review:** Validate inputs, bounds checking, safe strings, sanitize network/file data
- **Error Handling:** Decline violations of coding standards, suggest legacy alternatives, explain compatibility reasons

