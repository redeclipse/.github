# Red Eclipse Development Instructions

You are working on Red Eclipse, a free and open source first-person shooter for Windows and Linux featuring parkour and science fiction elements. The codebase was forked from Cube 2: Sauerbraten in 2018 with an updated Tesseract rendering pipeline.

## Code Generation Rules

### Language Requirements
- Generate C++11 compliant code only
- Preserve legacy C-style with C++ extensions (do not modernize to newer C++ standards)
- Never suggest adding new dependencies or external libraries
- Always write custom implementations instead of recommending third-party solutions

### Naming Conventions (ENFORCE STRICTLY)
- Classes: `CamelCase` only (e.g., `WeaponSystem`, `PlayerData`)
- Everything else: lowercase, no underscores (e.g., `playerhealth`, `getposition`, `maxammo`)
- Keep all names concise but clear

### Formatting Rules (APPLY AUTOMATICALLY)
- Indentation: Always use exactly 4 spaces, never tabs
- Function calls: No space before parentheses `function(args)`
- Math operators: Always add spaces `a + b`, `x * y + z`
- Variable declarations: Group same types `int health, armor, ammo;`
- Newlines: Use minimally, only between logical sections
- Single statements: No braces `if(condition) action();`
- Multi-statements: Braces on new line:
  ```cpp
  if(condition)
  {
      action1();
      action2();
  }
  ```
- Single-command loops: Bundle `for(int i = 0; i < n; ++i) process(i);`

### Code Style Requirements
- Minimize comments - only explain non-obvious logic or design decisions
- Never explain what code does, only why it does it
- Prioritize performance over readability when necessary
- Avoid excessive infrastructure or abstraction layers

### Forbidden Features (NEVER USE)
- `auto` keyword - always use explicit types
- Lambda functions - use helper functions or inline macros instead
- Private class members - keep data accessible when practical
- Modern C++ features that conflict with legacy style

### Performance Guidelines
- Always optimize for speed first
- Consider memory allocation patterns
- Minimize function call overhead where possible
- Use inline functions for small, frequently called code

## File-Specific Rules

### C++ Source Files (.cpp, .h)
- Follow all formatting rules above
- Keep header includes minimal
- Use forward declarations when possible

### Configuration Files (.cfg)
- These use Red Eclipse's modified CubeScript
- Check existing project scripts before writing new ones
- CubeScript has project-specific extensions beyond standard

## Code Review Instructions
When reviewing code:
- Enforce all formatting rules strictly
- Check for performance implications
- Suggest alternatives that align with project architecture
- Provide specific fixes for guideline violations
- Focus on maintainability within the existing codebase style
- Be constructive and educational - explain the reasoning behind suggestions
- Avoid confrontational language - focus on the code, not the developer
- Offer praise for well-written code that follows guidelines
- Frame criticism as opportunities for improvement rather than failures

## Error Handling
If asked to use forbidden features or modern C++ patterns:
- Decline politely
- Suggest alternative approaches that fit the legacy style
- Explain why the restriction exists (performance/compatibility)

Remember: This is a performance-critical game engine with a specific legacy style. Consistency with existing code is more important than modern best practices.
