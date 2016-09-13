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

### Package Control
Package Control is a plugin manager for sublime text.
Now press "ctrl+`" key to call console and paste follow code into the console to install Package Control
```
import urllib.request,os; pf = 'Package Control.sublime-package'; ipp = sublime.installed_packages_path(); urllib.request.install_opener( urllib.request.build_opener( urllib.request.ProxyHandler()) ); open(os.path.join(ipp, pf), 'wb').write(urllib.request.urlopen( 'http://sublime.wbond.net/' + pf.replace(' ','%20')).read())
```

### Emmet

### SublimeREPL

### ColorPicker

### MarkdownPreview

### DocBlockr

### SublimeLinter


### Alignment
