The name of the project is Red Eclipse, it is a free and open source first person shooter game for Windows and Linux that features parkour and other science fiction elements as an arena shooter.

The codebase was forked in 2018 from Cube 2: Sauerbraten and features an updated rendering pipeline from the Tesseract game engine, with extensive modifications made since.

All code is C++11 compliant, but should preserve the style of the rest of the code, which is C with C++ extensions due to the age of the codebase.

Dependencies are managed manually by a human, and are kept as minimal as possible. Instead of introducing new dependencies or external includes, effort should be made to write custom code instead.

Code is kept concise with limited use of newlines only to separate different concepts or sections, and does not use spaces between invokations and parentheses, but should use spaces between math operators.

When writing code comments, their use should be minimized as much as possible, and they should be used only to describe a line of thought or reference that the code itself doesn't convey instead of just explaining what the code does.

CamelCase may only be used for class names. All identifier names should be concise and avoid using underscores. Variables of the same type should be grouped together instead of across new lines.

All code and scripts must maintain an indent length of 4 spaces and TAB characters should not be used. When editing a section a code that is formatted like a table, structure of the table should be preserved.

All code and scripts should attempt to be extremely performant with only some concessions for visual aesthetics, and excessive infrastructure should be avoided.

When writing loops that only have one conditional or command, they should be bundled so that extra braces and newlines are avoided.

Do not use helper lambdas, and instead use a helper function or inline macro. Avoid the use of keywords like auto and private class members.

The scripting language used in "*.cfg" files is CubeScript, but with extensive modifications specifically for Red Eclipse. Care should be taken to check the project's specific implementation before writing scripts.

When performing code reviews, responses should be made in English, should provide lots of constructive criticism, and enforce the coding guidelines above by also providing suggestions that fix problems with them.
