# VSCode Keybindings

## Default VSCode Keybindings
### General
* `cmd+shift+p` open command pallete
  * Type `Preferences: Open Keyboard Shortcuts (JSON)` command to view custom user keybindings.json
* `cmd+k cmd+s` show keyboard shortcuts
  * Type `@source:user` in the search field to filter by custom user shortcuts

### Explorer
* `j / k` move selection cursor up/down
* `space` open (preview) file preserving focus
* `ctrl+enter` open file to side

### Editor
* `cmd+s` Save editor
* `cmd+w` Close editor
* `cmd+\` Split editor

### Terminal
* `cmd+j` Toggle Terminal

### Markdown
* `cmd+k v` Open Preview to the Side

---
## Custom Hotkeys
Custom user hotkeys / keybindings are saved in keybindings.json, but are also mirrored in the Preferences: Open Keyboard Shortcuts panel.

### Explorer
* `cmd+shift+e` toggle explorer with focus
* `cmd+o` open new workspace folder
* `cmd+n` create new file
* `cmd+f` create new directory
* `cmd+delete` delete selected file/directory
* `enter` open file
* `shift+enter` rename selected file/directory

### Editor
* `cmd+shift+j / cmd+shift+k` focus on previous / next editor (tab) in group
* `cmd+shift+h / cmd+shift+l` move editor to left / right editor group
* `cmd+e` focus on active editor group. focus on right (next) editor group if editor already in focus.

### Python
* `cmd+shift+p` run active editor file using Python in Terminal