This guide is a basic introduction to the development model for Red Eclipse, including the procedure for submitting modifications and creating new ideas.

It is suggested you read this in its entirety before starting any development related work, as it contains vital information regarding proper etiquette.

## Topical Repositories

If you want to chat or need help and support, you should use our [Discussion Area](https://redeclipse.net/discuss) or [Live Chat](https://redeclipse.net/chat).

## Content/Idea/Proposal Guidelines

* Create a piece of content, come up with an idea, or decide to propose a change you want included in Red Eclipse.
* Then, create a discussion for in our [Discussion Area](https://redeclipse.net/discuss).
* Give the community a chance to provide feedback (minimum time should be about 2 weeks).
* When you feel you have come up with a finished work, idea, or proposal, submit it to the appropriate git module as a pull request.
* Provide a good description along with a link to your original forum topic.
* Attach, or provide direct links to, any files you are attempting to have included here.
* Feel free to share a link to your post while we review it.

## Issue Reporting Guidelines

* Find an issue in the Red Eclipse game and/or engine, verify that you can reproduce the problem and provide steps on how to do so.
* Check on the [Discussion Area](https://redeclipse.net/discuss) or issue tracker to see if your issue has already been reported and/or resolved upstream.
* When you have verified that the issue still exists and needs to be fixed, submit it to the appropriate git module as an issue or pull request.
* Provide a good description along with a link to your original forum topic (if applicable).
* Attach, or provide direct links to, any files which demonstrates your issue and any patches you might have here.

## General Guidelines

* Only submit finalised works (no work-in-progress items please). If you are just looking for general feedback, you can use the [Discussion Area](https://redeclipse.net/discuss) (or a git fork!).
* You acknowledge we will probably modify your content before including it (to fix any problems or improve it).
* If you want to modify it at a later point, changes you make will need to be based on our version, otherwise we may not include your updates.
* You must provide an explicit, legally enforceable license. Do not use "public domain", or "no commercial use" / "no modification allowed" clauses. If you don't, it will be assumed you are happy to use the Red Eclipse general license which best applies to the work.

If you are unsure about how to license your work, Creative Commons provides a handy selection tool for their licenses at http://creativecommons.org/choose/ and Red Eclipse content is generally licensed "CC by-sa" (Attribution-ShareAlike), unless otherwise specified: http://creativecommons.org/licenses/by-sa/3.0/

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
