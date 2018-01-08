## Homebrew

### Uninstall all dependencies not depended on by packages

brew deps [FORMULA] | xargs brew remove --ignore-dependencies && brew missing | xargs brew install
