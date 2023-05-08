[Build vim from source homebrew linux](https://github.com/Homebrew/brew/issues/14473#issuecomment-1411925939)
[Embbed Videos?](#)
# Summary
----

# Related Stuff

----
# Notes:
- `export HOMEBREW_NO_INSTALL_FROM_API=1`, then `brew install -s vim` again.
- this did the trick. I was wondering why it wasn't picking up my builds.
> To create or edit formulae locally, you’ll need to `brew tap homebrew/core` if you haven’t previously. This taps homebrew-core, creating a Git repository in `$(brew --repository homebrew/core)`. As you are developing, you’ll also need to set `HOMEBREW_NO_INSTALL_FROM_API=1` before any `install`, `reinstall` or `upgrade` commands, to force `brew` to use the local repository instead of the API.

- I guess when it hits the api, it's not using building from source really. I don't how brew works, but this solved my issue:
```bash
HOMEBREW_NO_INSTALL_FROM_API=1 brew install -s vim
```
- Make sure to run `brew edit vim` and add this stuff:
```
"--with-x",
"--with-gnome",
"--enable-gnome-check",
"--enable-gtk3-check",
"--enable-fail-if-missing",
"--enable-clipboard",
```

## Questions:

## Follow Up:
