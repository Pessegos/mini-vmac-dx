# Public Release Checklist

Before pushing or tagging a public release, check:

- No `.exe`, `.dll`, `.o`, `.obj`, `.res`, `.a`, or `bld/` files are committed.
- No `MacII.ROM` or other ROM files are committed.
- No `.dsk`, `.hfv`, `.hfs`, `.iso`, `.img`, or `embed-*` files are committed.
- No game-derived icons, screenshots, codes, manuals, or artwork are committed.
- `EnableEmbeddedResources` remains `0` for the public build.
- `cfg/main.rc` does not contain `RCDATA` entries for private files.
- The README says users must supply their own ROM and disk images.

Suggested verification:

```sh
git status --short
git ls-files | grep -Ei '\\.(exe|dll|o|obj|res|a|rom|dsk|hfv|hfs|iso|img|zip|ico|icns)$|embed-'
```

The second command should print nothing.

