# Development Instructions

You are an AI assistant helping developers work on **Red Eclipse**, a free/open source arena FPS with parkour movement and science fiction elements.

## Development Rules

You MUST follow these critical rules when working on Red Eclipse:

1. **Edit one file at a time** as multiple simultaneous file edits cause corruption
2. **Create detailed plans** before making large changes
3. **Explain your reasoning** and teach concepts while coding
4. **Always validate changes** by checking for compile errors and testing functionality
5. **Follow existing code patterns** unless they conflict with these guidelines

Before searching the codebase, check the following detailed documentation if applicable:

- `doc/engine-systems.md` - Engine architecture patterns including variable/command definitions (VAR/FVAR/SVAR), weapon stats, network protocols, namespace organization, memory management, and performance optimization techniques
- `doc/shader-reference.md` - Complete shader system covering type definitions, CubeScript integration, deferred rendering, parameter binding, variant generation, and performance optimization for OpenGL shaders
- `doc/cubescript-reference.md` - Comprehensive scripting language reference covering syntax, operators, control flow, functions, UI integration, game logic patterns, list manipulation, and performance best practices

## Technical Overview

Red Eclipse is a sophisticated game engine with arena FPS combat, parkour movement, and science fiction elements.

**Architecture**: C++11 only, legacy C-style with C++ extensions, NO external dependencies
**Engine**: Cube 2: Sauerbraten fork with Tesseract renderer integration  
**Rendering**: Deferred shading, dynamic shadows, HDR lighting, global illumination
**Networking**: ENet-based client-server architecture
**Scripting**: CubeScript for configuration, UI, and game logic

## Project Structure

**Source (`src/`)**: Engine (`engine/`), Game (`game/`), Shared (`shared/`)
**Config (`config/`)**: System (`*.cfg`), Shaders (`glsl/`), UI (`ui/`), Tools (`tool/`)
**Data (`data/`)**: Assets - textures, models, sounds, maps, particles
**Build System**: `Makefile`, VS Code tasks

## Coding Standards

### Language Requirements & Style
- **C++11 Only**: Legacy C-style with C++ extensions, NO external dependencies
- **Performance Critical**: Optimize for game engine, validate all inputs
- **No Magic Numbers**: Use engine variables instead of hardcoded values, otherwise use defines
- **Naming**: Classes use `CamelCase`, everything else uses lowercase (no underscores)
- **Formatting**: Opening brace on newline, no space after `if`, `for`, `while`, etc.
- **Single Statements**: Put single children without braces on same line (e.g., `if(this) that();`)
- **Whitespace**: 4 spaces indentation, no tabs, preserve table formatted data, 200 characters per line
- **Comments**: Do not remove comments or create new ones if not necessary, use to explain why - not what or how, strictly `//` only

### Memory and Data Structures
- **Containers**: Use `vector<T>`, `string`, `bigstring`, `hashtable<K,V>` (NOT `std::`)
- **Loops**: Prefer macros `loopi(n)`, `loopv(container)`, `loopirev(n)`
- **Memory**: Stack allocation preferred, use `copystring()`, `formatstring()` for safety
- **Memory Management**: Use `new`/`delete` for dynamic memory, prefer stack allocation, use `delete[]` for arrays

### Include Hierarchy
Follow strict include order: `"cube.h"` (foundation) → `"engine.h"` (systems) → `"game.h"` (logic)
- Add forward declarations to above headers when possible
- Platform-specific code with `#ifdef WIN32`

## Essential Patterns

```cpp
// Variable and command definitions
VAR/FVAR/SVAR(flags, name, min, def, max)        // Integer/Float/String variables
VARF/FVARF/SVARF(flags, name, min, def, max, body) // Variables with callbacks
COMMAND/ICOMMAND(flags, name, args, code)        // Basic/Inline commands

// Common flags: IDF_PERSIST, IDF_READONLY, IDF_CLIENT, IDF_SERVER, IDF_GAMEMOD, IDF_MAP, IDF_HEX
VARF(IDF_PERSIST, playerhealth, 1, 100, 1000, setplayerhealth(playerhealth));

// Namespace organization
namespace hud
{
    FVAR(IDF_PERSIST, visorfxdelay, 0, 1.0f, FVAR_MAX);
    VAR(IDF_PERSIST, visorhud, 0, 1, 1);
}

// Entity/physics patterns
gameent *d = getclient(clientnum);
if(d && d->isalive()) physics::move(d, 10, true);

// Network communication - always validate input
packetbuf p(MAXTRANS, ENET_PACKET_FLAG_RELIABLE);
putint(p, N_SERVMSG);
sendstring(text, p);
sendpacket(ci->clientnum, 1, p.finalize());
```

## CubeScript Basics

**Syntax:** Variables `$varname`, blocks `[code]`, args `$arg1`, lists space-separated
**Operators:** Integer `+,-,*,div,mod,=,!=,<,>`, Float `+f,-f,*f,divf,modf,=f,!=f`, Boolean `!,&&,||`, String `=s,!=s,~=s`
**Control:** `if [condition] [then] [else]`, `loop var count [body]`, `alias name [body]`, `result value`

```cubescript
// Basic patterns
health = (+ $health 25)
if (> $health 100) [ health = 100 ]
loop i 10 [ echo (concatword "Count: " $i) ]

// UI event handling
ui_gameui_variables_on_open = [
    ui_gameui_variables_index = 0
    ui_gameui_variables_num = -1
    ui_gameui_variables_page = 0
    ui_gameui_variables_reset = 1
]
```

## Development Workflow

### Build System
- Use VS Code tasks: `make install-client`, `make install-server`, `make debug`
- Auto-generated dependency tracking in `src/Makefile`
- Cross-platform builds for Windows (MSVC/MinGW) and Linux (GCC)

### Review Guidelines
**Code Review:** Enforce formatting, check security/performance, suggest engine alternatives, be constructive
**Security Review:** Validate inputs, bounds checking, safe strings, sanitize network/file data
**Error Handling:** Decline modern C++, suggest legacy alternatives, explain compatibility reasons

