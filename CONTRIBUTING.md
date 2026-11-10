# Contributing to Red Eclipse

This guide covers how Red Eclipse is developed, and how to report problems, suggest ideas and send in your own changes. Please read it before you start, as it explains what we need from you to review and include your work.

## Getting Help

For help with installing, playing, mapping or running a server, ask in the [help and support discussions](https://github.com/redeclipse/base/discussions/categories/help-and-support) or on [Discord](https://www.redeclipse.net/discord). The [documentation](https://www.redeclipse.net/docs) and [FAQ](https://www.redeclipse.net/docs/FAQ) answer many common questions.

## The Repositories

Red Eclipse is split across several repositories in the [redeclipse organisation](https://github.com/redeclipse). Open issues and pull requests in the repository the change belongs to, and if you aren't sure which one that is, use [base](https://github.com/redeclipse/base).

* [base](https://github.com/redeclipse/base) holds the engine, the game code, the configuration and the build. The game's content is included as submodules under `data/`.
* The data repositories each hold one kind of content, such as [maps](https://github.com/redeclipse/maps), [textures](https://github.com/redeclipse/textures) or [sounds](https://github.com/redeclipse/sounds), or the work of one contributor, such as [q009](https://github.com/redeclipse/q009).
* [redeclipse.github.io](https://github.com/redeclipse/redeclipse.github.io) is the website, and [docs](https://github.com/redeclipse/docs) is the documentation shown on it.
* [master](https://github.com/redeclipse/master) holds the configuration for the official master server.

To get everything, clone base with its submodules:

```
git clone --recurse-submodules https://github.com/redeclipse/base.git redeclipse
```

The [install guide](https://www.redeclipse.net/docs/Install-Guide) explains how to build the game from source.

## Reporting Issues

* Search the [existing issues](https://github.com/search?q=org%3Aredeclipse+is%3Aissue&type=issues) first, in case the problem has already been reported or fixed.
* Make sure you can reproduce the problem on the latest version, and note the steps that make it happen.
* Open one issue per problem using the bug report form, and fill in as much of it as you can.
* For game problems, include your `log.txt`. The [FAQ](https://www.redeclipse.net/docs/FAQ#where-do-i-find-screenshots-logs-and-other-user-data) explains where to find it. For crashes, a backtrace helps a lot, and the [debugging guide](https://www.redeclipse.net/docs/Debug) shows how to get one.

## Ideas, Features and Content

* Open a feature request in the repository it concerns, or if you'd like feedback first, start a discussion in the [ideas and feature requests](https://github.com/redeclipse/base/discussions/categories/ideas-and-feature-requests) discussions.
* Gameplay changes should fit the game's [core principles](https://www.redeclipse.net/docs/Core-Principles).
* Send finished content, such as maps, models, textures or sounds, as a pull request to the matching data repository. If you can't use git, attach the files or links to them in an issue instead.

## Pull Requests

* Base your work on the current `master` branch, and only submit finished work. If you're looking for early feedback, use the [discussion area](https://www.redeclipse.net/discuss) or share a link to your fork.
* Describe what the pull request changes and why, and link the issue it fixes with `Fixes #123`.
* Test what you change. For code, build the game and play through the affected feature, and check `log.txt` for new errors or warnings. For content, load it in game and check it in the editor.
* Follow the style of the code around your change: 4-space indentation, opening braces on new lines, no space after keywords as in `if(condition)`, lines of up to 180 characters and `//` comments. Use the engine's containers and loop macros, such as `vector` and `loopv`, rather than the standard library.
* Don't change the bundled third-party code in `src/lib`, `src/include`, `src/support`, `src/steam` or `src/enet`.
* Leave "Allow edits by maintainers" turned on. We may push follow-up commits to your branch to fix problems or improve it before merging.
* We'll probably modify your work before including it. If you want to change it later, base your changes on our version, otherwise we may not include your updates.

## Licensing

* Code, scripts and configuration are covered by the Red Eclipse [license](https://www.redeclipse.net/docs/License), based on the ZLIB license. Contributions to them are accepted under the same terms.
* Content needs an explicit, legally enforceable license. Don't use "public domain", "no commercial use" or "no modification allowed" terms. If you don't name a license, we'll assume you're happy to use the one that best applies to the work.
* Red Eclipse content is generally licensed [CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/) (Attribution-ShareAlike) unless otherwise specified, and no content may have restrictions beyond attribution and share-alike. If you're unsure which license to use, Creative Commons has a [license chooser](https://creativecommons.org/chooser/).

## Commit Messages

Each commit message starts with a single summary line in the form `module: description`.

* `module` is the part of the project the commit changes, in lowercase. In the code this is a subsystem or directory, such as `engine`, `game`, `server`, `ui`, `config` or `doc`. In the data repositories it is the map, model or asset set, such as `q009` or `models`.
* A commit that changes a few separate parts lists them with commas, such as `bloodlust, deli: ...`. A change that spreads across the project uses the broadest module that fits.
* `description` is lowercase and has no full stop at the end. Prefer saying how things behave after the commit over what was done, so `server: a spectator request for a missing client is rejected before its state is read` rather than `fix crash`.
* A body is optional. If the summary alone doesn't make the reason clear, a short explanation after a blank line helps.
* Keep to one problem per commit. If a pull request fixes several unrelated issues, give each one its own commit.

For example:

```
engine: a map change clears the hovered entities, where the editor's hover panel read the old map's entities and crashed
particles: a fireball's attribute 3 is named style, apart from the particle type in 0
models: broadleaf trees switch detail at half the size on screen
```

## AI-Assisted Contributions

You're welcome to use AI tools to help with code, content, issues or pull requests. For the project's records, we ask that you disclose it:

* Any commit where an AI tool wrote or substantially shaped the changes or the message must end with a `Co-Authored-By:` trailer naming the tool and model, after a blank line. Use the attribution line your tool provides, such as `Co-Authored-By: Claude Opus 5.5 <noreply@anthropic.com>`. If it doesn't provide one, write the tool and model name yourself.
* If an AI tool found the problem or wrote the description, say so in the issue or pull request.
* You're still responsible for what you submit. You should understand it, have tested it, and be able to answer questions about it in review.

Pull requests that don't disclose AI assistance may be closed.

## Code of Conduct

Everyone taking part in the project, in the issue trackers, discussions and Discord, is expected to follow our [code of conduct](https://github.com/redeclipse/.github/blob/master/CODE_OF_CONDUCT.md).
