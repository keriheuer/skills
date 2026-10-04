---
name: dropbox
description: >
  Use when reading from or writing to the user's Dropbox. Provides the exact
  local mount path, symlink location, and directory conventions so you don't
  have to search for the cloud drive. Triggers on any mention of Dropbox, "my
  Dropbox", a path starting with ~/Dropbox, or a request to save/move/read files
  in the user's Dropbox folders.
tags:
  - dropbox
  - cloud-storage
  - paths
  - mount-point
  - filesystem
  - macos
disabled: true
---

# Dropbox on this machine

## Mount point

Dropbox is mounted under macOS **CloudStorage**, with a symlink in the home directory:

- **Canonical path:** `/Users/keriheuer/Library/CloudStorage/Dropbox`
- **Symlink:** `~/Dropbox` → the canonical path above

Either path works in scripts and shell commands. Prefer `~/Dropbox` in user-facing output for
readability; prefer the canonical path in scripts that may run under non-shell contexts where
the symlink resolution could be ambiguous.

Verify with:
```bash
readlink ~/Dropbox
# → /Users/keriheuer/Library/CloudStorage/Dropbox
```

## Known top-level folders

- `Type Specimens/` — typography reference images, organized by book/collection and
  `General/<Language>/` for loose specimens. Languages used: Dutch, English, French, German,
  Italian, Spanish, Swedish.

Do not assume other folders exist — list the root with `ls ~/Dropbox` first.

## Offline behavior

Files under CloudStorage may be dataless placeholders (not yet downloaded). Reading a placeholder
triggers a sync fetch transparently, which can take seconds for large files. If you need to pre-fetch
before bulk processing, use `brctl download <path>` (works for iCloud Drive; for Dropbox use the
Dropbox app's "Make available offline" or just read the file to trigger fetch).

## Related location — iCloud Drive

The user's iCloud Drive root (for cross-reference, e.g. matching filenames between Dropbox and
iCloud libraries) is:

- `/Users/keriheuer/Library/Mobile Documents/com~apple~CloudDocs/`

Notable: `.../Typography/` contains language-organized source files that correspond to items later
moved to `~/Dropbox/Type Specimens/General/`.
