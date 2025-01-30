---
title: "Mastering Nano: Essential Commands for Efficient Text Editing"
seoTitle: "Nano Basics: Key Commands for Text Editing"
seoDescription: "Learn essential commands for efficient text editing with Nano, covering navigation, editing, file operations, and customization tricks"
datePublished: Thu Jan 30 2025 03:30:43 GMT+0000 (Coordinated Universal Time)
cuid: cm6is2jmq000409jz2dy44fdg
slug: mastering-nano-essential-commands-for-efficient-text-editing
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1737555064985/422028cb-a0e5-4b62-9ba9-c36084fdc0f2.png
tags: cloud, devops, sre, devsecops, platform-engineering, gnu-nano-editor

---

### **Basic Commands**

| Command | Description |
| --- | --- |
| `nano <filename>` | Open a file in Nano (create if it doesn’t exist). |
| `nano -w <filename>` | Open a file without wrapping long lines. |
| `nano -m <filename>` | Enable mouse support (if available). |
| `nano -B <filename>` | Automatically back up the file when saving. |
| `nano -v <filename>` | View a file (read-only mode). |

### **Navigation**

| Command | Description |
| --- | --- |
| `Ctrl + F` or `→` | Move forward one character. |
| `Ctrl + B` or `←` | Move backward one character. |
| `Ctrl + P` or `↑` | Move to the previous line. |
| `Ctrl + N` or `↓` | Move to the next line. |
| `Ctrl + A` | Move to the beginning of the line. |
| `Ctrl + E` | Move to the end of the line. |
| `Ctrl + V` or `PgDn` | Move down one page. |
| `Ctrl + Y` or `PgUp` | Move up one page. |
| `Ctrl + _` | Go to a specific line number. |

### **Editing**

| Command | Description |
| --- | --- |
| `Ctrl + Space` | Start selecting text (mark). |
| `Alt + A` | Toggle text selection. |
| `Ctrl + K` | Cut the current line or selected text. |
| `Alt + 6` | Copy the current line or selected text. |
| `Ctrl + U` | Paste the cut/copied text. |
| `Ctrl + \` | Search and replace text. |
| `Ctrl + W` | Search for text. |
| `Alt + U` | Undo the last action. |
| `Alt + E` | Redo the last undone action. |
| `Ctrl + J` | Justify the current paragraph. |

### **File Operations**

| Command | Description |
| --- | --- |
| `Ctrl + O` | Save the file (Write Out). |
| `Ctrl + X` | Exit Nano (prompts to save if unsaved). |
| `Ctrl + R` | Insert another file into the current file. |
| `Ctrl + T` | Open the file browser to select a file. |

### **Miscellaneous**

| Command | Description |
| --- | --- |
| `Ctrl + G` | Open the help menu. |
| `Ctrl + C` | Show the current cursor position. |
| `Ctrl + L` | Refresh the screen. |
| `Ctrl + ]` | Go to the matching bracket. |
| `Alt + Y` | Enable/disable syntax highlighting. |

### **Exiting**

| Command | Description |
| --- | --- |
| `Ctrl + X` | Exit Nano (prompts to save if unsaved). |
| `Ctrl + O` then `Enter` | Save and continue editing. |
| `Ctrl + C` | Cancel the current operation. |

### **Advanced Navigation**

| Command | Description |
| --- | --- |
| `Alt + (` or `Alt + )` | Move to the previous/next word. |
| `Alt + \` | Move to the beginning of the file. |
| `Alt + /` | Move to the end of the file. |
| `Alt + ]` | Go to the matching bracket (if available). |
| `Alt + 0` to `Alt + 9` | Go to a specific tab (if multiple files are open). |

### **Advanced Editing**

| Command | Description |
| --- | --- |
| `Alt + D` | Delete the current line. |
| `Alt + T` | Cut from the cursor to the end of the line. |
| `Alt + Backspace` | Delete the word to the left of the cursor. |
| `Alt + Del` | Delete the word to the right of the cursor. |
| `Alt + M` | Toggle mouse support (if enabled). |
| `Alt + N` | Toggle line numbers. |
| `Alt + P` | Toggle visible whitespace (spaces/tabs). |
| `Alt + S` | Toggle soft wrapping of long lines. |
| `Alt + V` | Enter full-screen mode. |

### **Search and Replace**

| Command | Description |
| --- | --- |
| `Ctrl + W` | Search for text. |
| `Alt + W` | Repeat the last search. |
| `Ctrl + \` | Search and replace text. |
| `Alt + R` | Replace text without prompting. |
| `Alt + C` | Toggle case sensitivity in search. |

### **File and Buffer Management**

| Command | Description |
| --- | --- |
| `Ctrl + R` | Insert another file into the current file. |
| `Ctrl + T` | Open the file browser to select a file. |
| `Alt + F` | Open a new file in a new buffer. |
| `Alt + >` | Switch to the next buffer (file). |
| `Alt + <` | Switch to the previous buffer (file). |
| `Alt + X` | Close the current buffer (file). |

### **Customization and Configuration**

| Command | Description |
| --- | --- |
| `Alt + A` | Toggle text selection. |
| `Alt + Y` | Toggle syntax highlighting. |
| `Alt + G` | Go to a specific line number. |
| `Alt + Z` | Suspend Nano (return to the shell). |
| `Alt + Q` | Toggle auto-indentation. |

### **Keyboard Macros**

| Command | Description |
| --- | --- |
| `Alt + [` | Start recording a macro. |
| `Alt + ]` | Stop recording a macro. |
| `Alt + ;` | Execute the recorded macro. |

### **Miscellaneous**

| Command | Description |
| --- | --- |
| `Ctrl + G` | Open the help menu. |
| `Ctrl + C` | Show the current cursor position. |
| `Ctrl + L` | Refresh the screen. |
| `Ctrl + ]` | Go to the matching bracket. |
| `Alt + H` | Toggle the help text at the bottom. |

### **Exiting and Saving**

| Command | Description |
| --- | --- |
| `Ctrl + X` | Exit Nano (prompts to save if unsaved). |
| `Ctrl + O` | Save the file (Write Out). |
| `Alt + O` | Save the file with a different name. |
| `Ctrl + C` | Cancel the current operation. |

### **Environment Variables**

You can customize Nano’s behavior by setting environment variables in your shell or editing the `.nanorc` file. For example:

* `set autoindent` – Enable auto-indentation.
    
* `set mouse` – Enable mouse support.
    
* `set tabsize 4` – Set the tab size to 4 spaces.
    
* `set linenumbers` – Show line numbers.
    

To create a `.nanorc` file, add your preferences to `~/.nanorc` or `/etc/nanorc`.

### **Tips and Tricks**

1. **Multiple Files**: Open multiple files at once with `nano file1 file2`. Use `Alt + >` and `Alt + <` to switch between them.
    
2. **Backup Files**: Use `nano -B` to automatically create backup files when saving.
    
3. **Read-Only Mode**: Use `nano -v` to open a file in read-only mode.
    
4. **Mouse Support**: Enable mouse support with `nano -m` or `set mouse` in `.nanorc`.
    
5. **Syntax Highlighting**: Add custom syntax highlighting rules to `~/.nanorc` or `/etc/nanorc`.
    

## Reference

1. [https://www.nano-editor.org/dist/v6.0/nano.html](https://www.nano-editor.org/dist/v6.0/nano.html)  
    Official documentation for the Nano text editor.
    
2. [https://en.wikipedia.org/wiki/Nano\_(text\_editor)](https://en.wikipedia.org/wiki/Nano_\(text_editor\))  
    Overview of Nano, its features, and usage on different systems.
    
3. [https://www.cheatography.com/davechild/cheat-sheets/nano/](https://www.cheatography.com/davechild/cheat-sheets/nano/)  
    A printable cheat sheet for quick reference to Nano commands.
    
4. [https://linux.die.net/man/1/nano](https://linux.die.net/man/1/nano)  
    A detailed list of all Nano commands for Linux.
    
5. [https://opensource.com/article/18/11/introducing-nanorc](https://opensource.com/article/18/11/introducing-nanorc)  
    A guide on how to customize the Nano editor for better efficiency.