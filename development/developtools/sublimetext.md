# sublime text (version 3)


## Installation 

* Learn more about sublime-text and Download it from official website.
> wget https://download.sublimetext.com/sublime_text_3_build_3114_x64.tar.bz2

* Install sublime
> tar -xvf sublime_text_3_build_3114_x64.tar.bz2 -C /opt/

* Active product, copy and paste follow license to license panel.
```
—– BEGIN LICENSE —–
Ryan Clark
Single User License
EA7E-812479
2158A7DE B690A7A3 8EC04710 006A5EEB
34E77CA3 9C82C81F 0DB6371B 79704E6F
93F36655 B031503A 03257CCC 01B20F60
D304FA8D B1B4F0AF 8A76C7BA 0FA94D55
56D46BCE 5237A341 CD837F30 4D60772D
349B1179 A996F826 90CDB73C 24D41245
FD032C30 AD5E7241 4EAA66ED 167D91FB
55896B16 EA125C81 F550AF6B A6820916
—— END LICENSE ——
```

## Configuration

* Configure desktop shortcut for sublime named "sublime_text.desktop".
```
[Desktop Entry]
Version=1.0
Type=Application
Name=Sublime Text
GenericName=Text Editor
Comment=Sophisticated text editor for code, markup and prose
Exec=/opt/sublime_text_3/sublime_text %F
Terminal=false
MimeType=text/plain;
Icon=sublime-text
Categories=TextEditor;Development;
StartupNotify=true
Actions=Window;Document;

[Desktop Action Window]
Name=New Window
Exec=/opt/sublime_text/sublime_text -n
OnlyShowIn=Unity;

[Desktop Action Document]
Name=New File
Exec=/opt/sublime_text_3/sublime_text --command new_file
OnlyShowIn=Unity;
```

* Copy sublime_text.desktop to "/usr/share/applications/" or "~/.local/usr/share/applications"

  > cp sublime_text.desktop /usr/share/applications/

## Install Plugin for Sublime Text

### [Package Control](http://wbond.net/sublime_packages/package_control)
Package Control is a plugin manager for sublime text.
Now press "ctrl+`" key to call console and paste follow code into the console to install Package Control
```
import urllib.request,os; pf = 'Package Control.sublime-package'; ipp = sublime.installed_packages_path(); urllib.request.install_opener( urllib.request.build_opener( urllib.request.ProxyHandler()) ); open(os.path.join(ipp, pf), 'wb').write(urllib.request.urlopen( 'http://sublime.wbond.net/' + pf.replace(' ','%20')).read())
```

### [Emmet](http://emmet.io/)
Emmet is a plugin for many popular text editors which greatly improves HTML & CSS workflow:
#### How to install

*Warning:* this plugin may not work at all in some OSes since it written in JavaScript and uses [PyV8](http://code.google.com/p/pyv8/) and [Google V8](https://developers.google.com/v8/) binaries to run. If you experience problems or editor crashes please [fill an issue](https://github.com/sergeche/emmet-sublime/issues).

##### With [Package Control](http://wbond.net/sublime_packages/package_control)

1. Run “Package Control: Install Package” command, find and install `Emmet` plugin.
2. Restart ST editor (if required)

##### Manually

1. Clone or [download](https://github.com/sergeche/emmet-sublime/archive/master.zip) git repo into your packages folder (in ST, find Browse Packages... menu item to open this folder)
2. Restart ST editor (if required)

--------------

**WARNING**: When plugin is installed, it will automatically download required PyV8 binary so you have to wait a bit (see _Loading PyV8 binary_ message on status bar). If you experience issues with automatic PyV8 loader, try to [install it manually](https://github.com/emmetio/pyv8-binaries).

#### Available actions

* [Expand Abbreviation](http://docs.emmet.io/actions/expand-abbreviation/) – <kbd>Tab</kbd> or <kbd>Ctrl+E</kbd>
* Interactive “Expand Abbreviation” — <kbd>Ctrl+Alt+Enter</kbd>
* [Match Tag Pair Outward](http://docs.emmet.io/actions/match-pair/) – <kbd>⌃D</kbd> (Mac) / <kbd>Ctrl+,</kbd> (PC)
* [Match Tag Pair Inward](http://docs.emmet.io/actions/match-pair/) – <kbd>⌃J</kbd> / <kbd>Shift+Ctrl+0</kbd>
* [Go to Matching Pair](http://docs.emmet.io/actions/go-to-pair/) – <kbd>⇧⌃T</kbd> / <kbd>Ctrl+Alt+J</kbd>
* [Wrap With Abbreviation](http://docs.emmet.io/actions/wrap-with-abbreviation/) — <kbd>⌃W</kbd> / <kbd>Shift+Ctrl+G</kbd>
* [Go to Edit Point](http://docs.emmet.io/actions/go-to-edit-point/) — <kbd>Ctrl+Alt+→</kbd> or <kbd>Ctrl+Alt+←</kbd>
* [Select Item](http://docs.emmet.io/actions/select-item/) – <kbd>⇧⌘.</kbd> or <kbd>⇧⌘,</kbd> / <kbd>Shift+Ctrl+.</kbd> or <kbd>Shift+Ctrl+,</kbd>
* [Toggle Comment](http://docs.emmet.io/actions/toggle-comment/) — <kbd>⇧⌥/</kbd> / <kbd>Shift+Ctrl+/</kbd>
* [Split/Join Tag](http://docs.emmet.io/actions/split-join-tag/) — <kbd>⇧⌘'</kbd> / <kbd>Shift+Ctrl+`</kbd>
* [Remove Tag](http://docs.emmet.io/actions/remove-tag/) – <kbd>⌘'</kbd> / <kbd>Shift+Ctrl+;</kbd>
* [Update Image Size](http://docs.emmet.io/actions/update-image-size/) — <kbd>⇧⌃I</kbd> / <kbd>Ctrl+U</kbd>
* [Evaluate Math Expression](http://docs.emmet.io/actions/evaluate-math/) — <kbd>⇧⌘Y</kbd> / <kbd>Shift+Ctrl+Y</kbd>
* [Reflect CSS Value](http://docs.emmet.io/actions/reflect-css-value/) – <kbd>⇧⌘R</kbd> / <kbd>Shift+Ctrl+R</kbd>
* [Encode/Decode Image to data:URL](http://docs.emmet.io/actions/base64/) – <kbd>⇧⌃D</kbd> / <kbd>Ctrl+'</kbd>
* Rename Tag – <kbd>⇧⌘K</kbd> / <kbd>Shift+Ctrl+'</kbd>

[Increment/Decrement Number](http://docs.emmet.io/actions/inc-dec-number/) actions:

* Increment by 1: <kbd>Ctrl+↑</kbd>
* Decrement by 1: <kbd>Ctrl+↓</kbd>
* Increment by 0.1: <kbd>Alt+↑</kbd>
* Decrement by 0.1: <kbd>Alt+↓</kbd>
* Increment by 10: <kbd>⌥⌘↑</kbd> / <kbd>Shift+Alt+↑</kbd>
* Decrement by 10: <kbd>⌥⌘↓</kbd> / <kbd>Shift+Alt+↓</kbd>

### SublimeREPL

#### Installation
============

1. Install Package Control. [http://wbond.net/sublime_packages/package_control](http://wbond.net/sublime_packages/package_control)
2. Install SublimeREPL
 1. `Preferences | Package Control | Package Control: Install Package`
 2. Choose `SublimeREPL`
3. Restart SublimeText
4. Configure `SublimeREPL` (default settings in `Preferences | Package Settings | SublimeREPL | Settings - Default` should be modified in `Preferences | Package Settings | SublimeREPL | Settings - User`, this way they will survive package upgrades!

#### Documentation

Very basic documentation will soon be available on RTD: [http://sublimerepl.readthedocs.org/](http://sublimerepl.readthedocs.org/)

#### Getting started

* Create or open your file with code.
* Menu / Tools / Command Palette (OS X: `⇧⌘P`) 
then type "SublimeREPL" and select the approperiate language.
* Menu / View / Layout / Rows: 2 (OS X: `⌥⇧⌘2`).
* Menu / View / Move File to Group / Group 2 (`⌃⇧2`).

#### Keybindings

* Evaluate in REPL:
 * <kbd>ctrl+,</kbd>, <kbd>s</kbd> Selection
 * <kbd>ctrl+,</kbd>, <kbd>f</kbd> File  
 * <kbd>ctrl+,</kbd>, <kbd>l</kbd> Lines
 * <kbd>ctrl+,</kbd>, <kbd>b</kbd> Block
* Transfer in REPL (just copy, without evaluating it):
 * <kbd>ctrl+shift+,</kbd>, <kbd>s</kbd> Selection
 * <kbd>ctrl+shift+,</kbd>, <kbd>f</kbd> File  
 * <kbd>ctrl+shift+,</kbd>, <kbd>l</kbd> Lines
 * <kbd>ctrl+shift+,</kbd>, <kbd>b</kbd> Block

Note: <kbd>ctrl+,</kbd>, <kbd>f</kbd> means: press Ctrl and Comma, release all, press F.


### ColorPicker
#### Installation
Install this repository via [Package Control](https://sublime.wbond.net).

#### Usage
To insert or change a selected color, use:

- Linux: `ctrl+shift+c`
- Windows: `ctrl+shift+c`
- OS X: `cmd+shift+c`

By default, the hex color code is inserted using uppercase letters. To use lowercase letters instead, copy the contents of **`Preferences -> Package Settings -> ColorPicker -> Settings-Default`** to the empty file created by selecting **`Preferences -> Package Settings -> ColorPicker -> Settings-User`**, then change `"color_upper_case"` to `false`.

#### Calling from Other Plugins
To commands are provided to assist in calling a color picker from other plugins.  Info is shared between the plugins via a settings file.  It does not have to exist on disk; it can exist only in memory for the sole purpose of sharing the return.  It is advised to use a unique name for the settings file.  The data is returned in the settings key `color_pick_return`.  It is advised to set `color_pick_return` to `None` in your settings file before calling any of the commands. So you can tell if it set teh variable or not.

#### ColorPickApiIsAvailableCommand
This command is used to test if ColorPicker is installed.

```python
>> settings = sublime.load_settings('my_shared.sublime-settings')
>> settings.set('color_pick_return', None)
>> sublime.run_command('color_pick_api_is_available', {'settings': 'my_shared.sublime-settings'})
>> print(settings.get('color_pick_return'))
True
```

#### ColorPickApiGetColorCommand
This command is used to call a color picker and get the selected value.  It takes a setings file and an optional `default_color`.

```python
>> settings = sublime.load_settings('my_shared.sublime-settings')
>> settings.set('color_pick_return', None)
>> sublime.run_command('color_pick_api_get_color', {'settings': 'my_shared.sublime-settings', 'default_color': '#ff0000'})
>> print(settings.get('color_pick_return'))
#23af44
```


### MarkdownPreview

#### Installation

##### Using Package Control

For all Sublime Text 2/3 users we recommend install via Package Control.

1. Install Package Control if you haven't yet.
2. Use <kbd>cmd</kbd>+<kbd>shift</kbd>+<kbd>P</kbd> then `Package Control: Install Package`
3. Look for `Markdown Preview` and install it.

##### Manual Install

1. Click the `Preferences > Browse Packages…` menu
2. Browse up a folder and then into the `Installed Packages/` folder
3. Download zip package rename it to `Markdown Preview.sublime-package` and copy it into the `Installed Packages/` directory
4. Restart Sublime Text

#### To preview

 - optionally select some of your markdown for conversion
 - use <kbd>cmd</kbd>+<kbd>shift</kbd>+<kbd>P</kbd> then `Markdown Preview` to show the follow commands (you will be prompted to select which parser you prefer):
	- Markdown Preview: Preview in Browser
	- Markdown Preview: Export HTML in Sublime Text
	- Markdown Preview: Copy to Clipboard
	- Markdown Preview: Open Markdown Cheat sheet
 - or bind some key in your user key binding, using a line like this one:
   `{ "keys": ["alt+m"], "command": "markdown_preview", "args": {"target": "browser", "parser":"markdown"} },` for a specific parser and target or `{ "keys": ["alt+m"], "command": "markdown_preview_select", "args": {"target": "browser"} },` to bring up the quick panel to select enabled parsers for a given target.
 - once converted a first time, the output HTML will be updated on each file save (with LiveReload plugin)

### DocBlockr
DocBlockr is a package for [Sublime Text 2 & 3][sublime] which makes writing documentation a breeze. DocBlockr supports **JavaScript** (including ES6), **PHP**, **ActionScript**, **Haxe**, **CoffeeScript**, **TypeScript**, **Java**, **Apex**, **Groovy**, **Objective C**, **C**, **C++** and **Rust**.

#### Installation

##### by [Package Control](https://sublime.wbond.net/installation)

1. Open Package Control: `Preferences -> Package Control`
2. Select `Package Control: Install Package`
3. Type `DocBlockr` into the search box and select the package to install it

#### Feature requests & bug reports

You can leave either of these things [here][issues]. Pull requests are welcomed
heartily, but please read [CONTRIBUTING.md][contrib] first! Basically: in this
repo, the main development branch is `develop` and the stable 'production'
branch is `master`. Please remember to base your branch from `develop` and issue
the pull request back to that branch.

### SublimeLinter

SublimeLinter itself is only a framework for linters. The linters are distributed as independent Sublime Text 3 plugins.

#### Installing via Package Control



#### Installing from source
If you have a previous source installation at Packages/SublimeLinter, delete it.
Type in a terminal:
```
cd '/path/to/Sublime Text 3/Packages'
git clone https://github.com/SublimeLinter/SublimeLinter3.git SublimeLinter
```
Restart Sublime Text 3.
Please consider using Package Control instead!


### Alignment
A simple key-binding for aligning multi-line and multiple selections in Sublime Text.

### SublimeCodeIntel
Code intelligence plugin ported from `Open Komodo Editor <http://www.openkomodo.com/>`_ to `Sublime Text <http://www.sublimetext.com/>`_.

Supports all the languages Komodo Editor supports for Code Intelligence (CIX, CodeIntel2):

    JavaScript, Mason, XBL, XUL, RHTML, SCSS, Python, HTML, Ruby, Python3, XML, Sass, XSLT, Django, HTML5, Perl, CSS, Twig, Less, Smarty, Node.js, Tcl, TemplateToolkit, PHP.

Provides the following features:

* Jump to Symbol Definition - Jump to the file and line of the definition of a symbol.
* Imports autocomplete - Shows autocomplete with the available modules/symbols in real time.
* Function Call tooltips - Displays information in the status bar about the working function.

Plugin should work in all three platforms (MacOS X, Windows and Linux).

.. image:: https://www.paypalobjects.com/en_GB/i/btn/btn_donate_LG.gif
   :alt: Click here to lend your support to SublimeCodeIntel and make a donation!
   :target: https://www.paypal.com/cgi-bin/webscr?cmd=_s-xclick&hosted_button_id=VVX4Q9H3924LE


#### Installing

**With the Package Control plugin:** The easiest way to install SublimeCodeIntel is through Package Control, which can be found at this site: http://wbond.net/sublime_packages/package_control

Once you install Package Control, restart Sublime Text and bring up the Command Palette (``Command+Shift+P`` on OS X, ``Control+Shift+P`` on Linux/Windows). Select "Package Control: Install Package", wait while Package Control fetches the latest package list, then select SublimeCodeIntel when the list appears. The advantage of using this method is that Package Control will automatically keep SublimeCodeIntel up to date with the latest version.

**Without Git:** Download the latest source from `GitHub <http://github.com/SublimeCodeIntel/SublimeCodeIntel>`_ and copy the whole directory into the Packages directory.

**With Git:** Clone the repository in your Sublime Text Packages directory, located somewhere in user's "Home" directory::

    git clone git://github.com/SublimeCodeIntel/SublimeCodeIntel.git


The "Packages" packages directory is located differently in different platforms. To access the directory use:

* OS X::

    Sublime Text -> Preferences -> Browse Packages...

* Linux::

    Preferences -> Browse Packages...

* Windows::

    Preferences -> Browse Packages...


#### Using

* Start typing code as usual, autocomplete will pop up whenever it's available. SublimeCodeIntel will also allow you to jump around symbol definitions even across files with just a click ..and back.

  For Mac OS X:
    * Jump to definition = ``Control+Click``
    * Jump to definition = ``Control+Command+Alt+Up``
    * Go back = ``Control+Command+Alt+Left``
    * Manual Code Intelligence = ``Control+Shift+space``

  For Linux:
    * Jump to definition = ``Super+Click``
    * Jump to definition = ``Control+Super+Alt+Up``
    * Go back = ``Control+Super+Alt+Left``
    * Manual Code Intelligence = ``Control+Shift+space``

  For Windows:
    * Jump to definition = ``Alt+Click``
    * Jump to definition = ``Control+Windows+Alt+Up``
    * Go back = ``Control+Windows+Alt+Left``
    * Manual Code Intelligence = ``Control+Shift+space``

Don't despair! The first time you use it it needs to build some indexes and it can take more than a few seconds.

It just works!

#### Configuring
For adding additional library paths (django and extra libs paths for Python or extra paths to look for .js files for JavaScript for example), either add those paths as folders to your project, or create an optional codeintel configuration file in your home or in your project's root.

Configuration files (``~/.codeintel/config`` or ``project_root/.codeintel/config``). All configurations are optional. Example::

    {
        "PHP": {
            "php": '/usr/bin/php',
            "phpExtraPaths": [],
            "phpConfigFile": 'php.ini'
        },
        "JavaScript": {
            "javascriptExtraPaths": []
        },
        "Perl": {
            "perl": "/usr/bin/perl",
            "perlExtraPaths": []
        },
        "Ruby": {
            "ruby": "/usr/bin/ruby",
            "rubyExtraPaths": []
        },
        "Python": {
            "python": '/usr/bin/python',
            "pythonExtraPaths": []
        },
        "Python3": {
            "python": '/usr/bin/python3',
            "pythonExtraPaths": []
        }
    }

Additional settings can be configured in the User File Settings:

Do NOT edit the default SublimeCodeIntel settings. Your changes will be lost when SublimeCodeIntel is updated. ALWAYS edit the user SublimeCodeIntel settings by selecting "Preferences->Package Settings->SublimeCodeIntel->Settings - User". Note that individual settings you include in your user settings will **completely** replace the corresponding default setting, so you must provide that setting in its entirety.

Available settings:

* A list of disabled languages can be set using "codeintel_disabled_languages". Ex. ``"codeintel_disabled_languages": ['css']``

* Live autocomplete can be disabled by setting "codeintel_live" to false.

* Live autocompletion can be disabled in a per-language basis, using "codeintel_live_disabled_languages". Ex. ``"codeintel_live_disabled_languages": ['css']``

* Information for more settings is available in the ``SublimeCodeIntel.sublime-settings`` file in the package.


### FileDiffs
Shows diffs between the current file, or selection(s) in the current file, and clipboard, another file, or unsaved changes. Can be configured to show diffs in an external diff tool

#### Help!

Check the [wiki][] for more tips

[wiki]: https://github.com/colinta/SublimeFileDiffs/wiki

#### Installation


1. Using Package Control, install "FileDiffs"

Or:

1. Open the Sublime Text Packages folder
    - OS X: ~/Library/Application Support/Sublime Text 3/Packages/
    - Windows: %APPDATA%/Sublime Text 3/Packages/
    - Linux: ~/.Sublime Text 3/Packages/ or ~/.config/sublime-text-3/Packages

2. clone this repo
3. Install keymaps for the commands (see Example.sublime-keymap for my preferred keys)


### JsFormat

#### Install
##### [Package Control](https://github.com/wbond/sublime_package_control) (Recommended)

JsFormat is now included in the default repository channel for [Package Control](https://github.com/wbond/sublime_package_control). It should show up in your install list with no changes.
If it does not show up, or you are on an older version of Package Control,
add https://github.com/jdc0589/JsFormat as a Package Control repository. JsFormat will show up in the package install list.

##### Git Clone
Clone this repository in to the Sublime Text 2 "Packages" directory, which is located where ever the
"Preferences" -> "Browse Packages" option in sublime takes you.

##### Key Binding

The default key binding is "ctrl+alt+f"

##### Key Binding Conflicts

Unfortunately there are other plugins that use "ctrl + alt + f", this is a hard problem to solve. If JsFormat works
OK via the command palette but does nothing when you use the "ctrl + alt + f" shortcut, you have two options:

1. Add ```{ "keys": ["ctrl+alt+f"], "command": "js_format", "context": [{"key": "selector", "operator": "equal", "operand": "source.javascript"}] }``` to your user keybindings file. This will override anything specified by a plugin.
2. Find the offending plugin, and change the shortcut in its sublime-keymap file (will revert on updates)


### Bracket Highlighter

#### Installation 
##### By Package Control

The recommended way to install BracketHighlighter is via Package Control. Package Control will install the correct branch on your system and keep it up to date.

1. Ensure Package Control is installed. Instructions are found here.
2. In Sublime Text, press ``ctrl + shift + p`` (Win, Linux) or ``cmd + shift + p`` (OSX) to bring up the quick panel and start typing Package Control: Install Package. Select the command and it will show a list of installable plugins.
3. Start typing BracketHighlighter; when you see it, select it.
4. Restart to be sure everything is loaded proper.
5. Enjoy!


##### Git Cloning

Warning
>This is not the recommended way to install BracketHighlighter for the casual user as it requires the user to know which branch to install, know how to use git, and will not get automatically updated.

>If you are forking for a pull request, this is the way to go, just replace the official repository with the link for your fork.

1. Quit Sublime Text.
2. Open a terminal:
```
cd /path/to/Sublime Text 3/Packages
git clone https://github.com/facelessuser/BracketHighlighter.git BracketHighlighter
```

3. Restart Sublime Text.


### GBK to UTF8

### SideBarEnhancements


### Sublime3-pydoc
Sublime 3 Pydoc plugin. This plugin autocompletes Docstrings if using python function definitions.

#### Description

DocPy autocompletes a docstring for any python function definition and inserts default arguments which can then be replaced.

#### Installation

Either way install it using Package Control or download it.

#### By Package Control

Open the install dialog pressing <kbd>Ctrl</kbd><kbd>Shift</kbd><kbd>P</kbd> and type in "Install Package" and then <kbd>Enter</kbd>

Search for DocPy and press once again <kbd>Enter</kbd>

#### Manual Install

Download the package unzip the package files into the sublime directory: 

~/.config/sublime-text-3/Packages/DocPy

### Quick File Open
This is a Sublime Text 2/3 plugin for quickly opening files. Sublime Text offers
the ability to quickly switch between workspaces, but there is no way to quickly
open a set of "Favorite" files. This plugin allows you to specify this set of
"Favorite" files so you can open them with a simple shortcut.

#### Installation
Clone this repository in the the Packages directory, or install through Package 
Control.

#### Usage
Specify the list of favorite files in the QuickFileOpen.sublime-settings file.
The files can then be accessed by hitting `ctrl+alt+shift+p`, which can be
configured in the user keybindings file.

Here is an example settings file:

```
{
    "files": ["file1", "file2"]
}
```