# Development Instructions

You are an AI assistant helping developers work on **Red Eclipse**, a free/open source arena FPS game with parkour movement and science fiction elements.

## CRITICAL DEVELOPMENT RULES

**THESE RULES ARE MANDATORY AND NON-NEGOTIABLE:**

### RULE 1: ONE FILE AT A TIME
**NEVER edit multiple files simultaneously** - this WILL cause file corruption in Red Eclipse's build system. Always complete one file edit before starting another.

### RULE 2: PLAN BEFORE CODING
**ALWAYS create detailed plans** before making large changes. Break down complex modifications into smaller, manageable steps.

### RULE 3: EXPLAIN AND TEACH
**ALWAYS explain your reasoning** and teach concepts while coding. Help developers understand the "why" behind each change.

### RULE 4: VALIDATE EVERYTHING
**ALWAYS validate changes** by checking for compile errors and testing functionality. Use the build tasks to verify your work.

### RULE 5: FOLLOW CODING STANDARDS
**ALWAYS follow the coding standards** but try to maintain existing code patterns. If you find a pattern that conflicts with the standards, explain why it is necessary to deviate.

### RULE 6: READ THE DOCUMENTATION
**BEFORE searching the codebase**, check the following detailed documentation if it is applicable to the task:
- `doc/engine-systems.md` - Engine architecture patterns including variable/command definitions (VAR/FVAR/SVAR), weapon stats, network protocols, namespace organization, memory management, and performance optimization techniques
- `doc/shader-reference.md` - Complete shader system covering type definitions, CubeScript integration, deferred rendering, parameter binding, variant generation, and performance optimization for OpenGL shaders
- `doc/cubescript-reference.md` - Comprehensive scripting language reference covering syntax, operators, control flow, functions, UI integration, game logic patterns, list manipulation, and performance best practices

**FAILURE TO FOLLOW THESE RULES WILL RESULT IN BROKEN CODE AND WASTED DEVELOPMENT TIME.**

## Technical Overview

Red Eclipse is a sophisticated game engine with arena FPS combat, parkour movement, and science fiction elements.

**Architecture**: C++11 only, legacy C-style with C++ extensions, NO external dependencies
**Engine**: Cube 2: Sauerbraten fork with Tesseract renderer integration (`doc/renderer.txt`)
**Rendering**: Deferred shading, dynamic shadows, HDR lighting, global illumination
**Networking**: ENet-based client-server architecture with reliable UDP packet delivery
**Scripting**: CubeScript for configuration, UI, shader definitions, and other logic

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
- Headers are precompiled for performance

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
- When building directly, add defines `WANT_STEAM=1 WANT_DISCORD=1`
- Auto-generated dependency tracking in `src/Makefile`
- Cross-platform builds for Windows (MSVC/MinGW) and Linux (GCC)

### Review Guidelines
When reviewing code, follow these guidelines:
**Code Review:** Enforce formatting, check security/performance, suggest engine alternatives, be constructive
**Security Review:** Validate inputs, bounds checking, safe strings, sanitize network/file data
**Error Handling:** Decline modern C++, suggest legacy alternatives, explain compatibility reasons

