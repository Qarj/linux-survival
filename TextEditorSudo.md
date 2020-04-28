# Setup and Start Text Editors

Tested with:

-   Ubuntu 16.04, Ubuntu 18.04

## Sublime 3

https://www.sublimetext.com/docs/3/linux_repositories.html

```
sudo subl
```

If many error messages (saw on Ubuntu 18.10, might need)

```
sudo apt-get install libgtk2.0
```

Find summary at bottom

1. CTRL-SHIFT-F
2. De-select `Use Buffer` and `Show Context` icons to left
3. Click `...` and select `Add Current File` to get `<current file>` in `Where:`

Tab key fix - Preferences -> Settings

```
{
    "tab_completion": false,
    "auto_complete_commit_on_tab": false
}
```

https://stackoverflow.com/questions/26328890/is-it-possible-to-stop-tab-autocomplete-in-sublime-text-2

## Visual Studio Code

```
sudo apt install curl
```

```
cd ~/Downloads
curl https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > microsoft.gpg
sudo install -o root -g root -m 644 microsoft.gpg /etc/apt/trusted.gpg.d/
sudo sh -c 'echo "deb [arch=amd64] https://packages.microsoft.com/repos/vscode stable main" > /etc/apt/sources.list.d/vscode.list'
```

```
sudo apt-get install apt-transport-https
sudo apt-get update
sudo apt-get install code
```

```
code newfile.txt
```

```
code .
```

| Shortcut      | Description                          |
| ------------- | ------------------------------------ |
| CTRL-B        | Toggle sidebar                       |
| ALT-↑         | Move line up                         |
| ALT-Z         | Toggle word wrap                     |
| ALT-ENTER     | Select all occurrences of find match |
| CTRL-W        | Close Editor Window                  |
| CTRL-K P      | Copy path of active file             |
| CTRK-K R      | Show active file in explorer         |
| CTRL-K O      | Show active file in new window       |
| CTRL-K Z      | Zen mode, Esc Esc to exit            |
| CTRL-K CTRL-F | Format selection                     |
| CTRL-SHIFT-V  | Show Markdown preview                |
| SHIFT-ALT-F   | Format whole document                |
| F12           | Go to definition                     |

https://code.visualstudio.com/docs/setup/linux

https://code.visualstudio.com/docs/getstarted/tips-and-tricks

## Notepad++

https://github.com/mmtrt/notepad-plus-plus/

```
notepad-plus-plus
```
