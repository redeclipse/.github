# Security Policy

## Reporting a Vulnerability

Please don't report security problems in public issues, pull requests, discussions or on Discord, where they could be used before a fix is ready.

Instead, report them privately through GitHub. Open the **Security** tab of the affected repository and choose **Report a vulnerability**. For the game, engine and dedicated server, that's [redeclipse/base](https://github.com/redeclipse/base/security/advisories/new). If you can't use GitHub, email contact@redeclipse.net.

A useful report includes:

* the repository and the part of it affected, such as the client, the dedicated server, the master server or the website;
* the version shown on the main menu panel or in `log.txt`, or the commit you tested;
* the steps or a small test case that reproduce the problem;
* what an attacker could do with it, and who could be affected, such as players, server operators or the master server;
* a suggested fix, if you have one;
* whether an AI tool found the problem or wrote the report, naming the tool and model, as the [contributing guide](https://github.com/redeclipse/.github/blob/master/CONTRIBUTING.md#ai-assisted-contributions) asks.

## What to Expect

Red Eclipse is made by volunteers, so a reply can take a little while. We'll confirm whether we can reproduce the problem, keep you updated in the private report while we work on a fix, and publish an advisory once the fix is released. We're happy to credit you in the advisory unless you'd rather we didn't.

## Supported Versions

Fixes are made on the `master` branch and reach players in the next release. Older releases don't receive separate security fixes.

## Scope

This policy covers the code and services in the [redeclipse organisation](https://github.com/redeclipse), including the official master server and the website. Community servers are run by their own operators, so report problems with a particular server's setup to its operator, and problems in the server software itself to us.
