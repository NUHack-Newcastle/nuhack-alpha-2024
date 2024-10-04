# NUHack Alpha 2024 Event Data

This repository contains the event setup data for the NUHack Alpha 2024 CTF, intended for use with our bespoke [ctf-platform](https://github.com/NUHack-Newcastle/ctf-platform). You can use this as a template for your own event data, but please don't use our event branding or challenges (except where accompanied by an appropriate license) without permission!

The platform works by making use of filesystem components (such as files, directories, and symlinks) in an intuitive and simple way to retain flexibility and ideal support for git-repo based event data, such as this one. This of course means that you can store individual challenges or even entire categories in separate submodules, allowing for fine-grained access control to source code per-challenge and allowing challenges to be contributed by anyone without giving them access to the entire event! Similarly, you can choose to make the source code of some challenges public and some challenges private by doing this per-challenge-repo.

Since submoduling allows for specifying a specific commit (point in time) to reference, this is effectively a transparent way of requiring approval before updates to a challenge are propagated into the event itself. Someone with write access to the event repo would need to update the submodule reference to point to the new commit of the challenge.

---
***Please note:** challenges are referenced in this repo as submodules. Not all challenge repos have been made public, some may be incaccessible. We should have made enough public for you to get the gist of how to build a challenge, though!

---

At the top level are files that define the branding and parameters of the event, such as the event name, start and end datetimes, logos, and scope policy. **Note that `scope.html` *may* be included verbatim and should not contain untrusted contents.**

The `challenges` folder contains your challenge categories, which in turn contain your challenges.

## Categories

To create a challenge category, create a directory within `/challenges`. This will be your category directory -- it's name is used as the URL slug for the category, so prefer something short, simple, and URL safe like `web` or `web-apps` rather than `Web Applications`.

Each category directory also needs a file called `name` (case-sensitive) which should contain the full human-friendly name of your category -- this is where something like `Web Applications` is appropriate.

You can also optionally specify a category icon in a similar way. At the time of writing, the platform only supports [bootstrap icons](https://icons.getbootstrap.com/), for which you need to write the icon ID into a file called `icon-bootstrap` and create a symlink called `icon` to the `icon-bootstrap` file. It would be trivial to implement custom image icons as image data stored in an actual `icon` file, but currently the platform just checks if `icon` is a symlink to a `icon-bootstrap` file. It's intended that you could use alternative icon systems like [Font Awesome](https://fontawesome.com/) or [Material Symbols](https://fonts.google.com/icons) by defining an `icon-fontawesome` or `icon-material` file and symlinking in the same way, but you'd have to implement this in the platform yourself.

## Challenges
Each challenge is directory inside a category's directory -- this challenge directory should again be named in a short, simple, URL safe way as it is used as a URL slug.

Each challenge should have a `name` file containing the full challenge name, and a `build` file containing a [shebang-ed](https://en.wikipedia.org/wiki/Shebang_(Unix)) script used to build the challenge (requirements for this are specified elsewhere). You can also optionally include a `difficulty` file containing a number 0-5 for the challenge difficulty, and a `description.html` containing **safe, trusted HTML code only** which is displayed on the challenge page. This file can contain Javascript.

Take a look at some of our challenges as an example.
