# gtkwrite

This is a fairly good little editor written in Gtk+2 in C. The editor will compile and build (without warning with -Wall -Wextra -pedantic) on Linux with Gtk+2 installed. The included Makefile handles the build. The editor can be compiled *with or without* GtkSourceView. Without GtkSourceView it compiles as `gtkedit`. With GtkSourceView it compiles as `gtkwrite` (requires GtkSourceView 2.x). It is Licensed under GPLv2.

### Menu Layout/Use

The editor has the following menu layout and shortcut key layout (if you are comfortable with the layout of KDE3 kwrite/kate, you will be right at home with this Gtk variant):

    File
      - New                    Ctrl+N
      - Open                   Ctrl+O
      - Save                   Ctrl+S
      - Save As          Shift+Ctrl+A
      - Reload Saved File          F5
      - Page Setup        Shift+Alt+P *
      - Print Preview    Shift+Ctrl+P *
      - Print                  Ctrl+P *
      - Close                  Ctrl+W
      - Quit                   Ctrl+Q

    * (options current not complete, or implemented
       in the Gtkwrite code with GtkSourceView)

    Edit
      - Undo                   Ctrl+Z
      - Redo             Shift+Ctrl+Z
      - Copy                   Ctrl+C
      - Cut                    Ctrl+X
      - Paste                  Ctrl+V
      - Find                   Ctrl+F
      - Find & Replace         Ctrl+R
      - Goto Line              Ctrl+G
      - Preferences             Alt+P

    View
      - Font Selection          Alt+T
      - Line Numbers              F11 *

    Status
      - (just miscellaneous hooks for testing)

    Tools
      - Increase Indent        Ctrl+I
      - Decrease Indent  Shift+Ctrl+I
      - Syntax Hylightit Shift+Ctrl+H
      - Insert File at Cursor...      *
      - Uppercase              Ctrl+U
      - Lowercase        Shift+Ctrl+U
      - Titlecase         Shift+Alt+U
      - Join Lines             Ctrl+J

    Help
      - About

### Features

The editor provides fairly robust find/replace dialog functionality with forward/reverse whole-document and selection-limited search ability with configurable case sensitive/insensitive searches and the ability to limit selection/replacement to whole words. (planned REGEX search/replace remains to be implemented) Configurable indent/unindent with align to softtab settings for code layout. An active window title displays file/save status along with the current filename. A status bar tracks the `line:col INS/OVR` state as well as displaying various operational messages.

### Code Layout/Approach

The code is in relatively good shape and reasonably commented. The code is separated into files by functionality. There are parts that are newer than others leaving some areas of the code that may still be separated further. The options handling throughout the code is done via a central struct that is passed by parameter as required. There are several current option variables that will be trimmed in the future -- the goal to store routinely used information to cut down on the number of function calls has led to creation of a few that were not later used as anticipated. All in all, the code builds into a single executable of roughly 70K (stripped), 100K otherwise, and builds fine on Intel/AMD or raspberryPi/ARM.

### Building

I recommend using a build directory to maintain a clean source tree. (although the object files and executables are generated under separate subdirectores, e.g. `obj/` and `bin/` should you choose to build in the source directory) To perform an **out-of-source** build, simply create a 'gtkwrite.build' directory at the same level as your repository and then soft link the source and Makefile in the build directory, e.g.:

    $ mkdir gtkedit.build && cd gtkedit.build
    $ for i in ../gtkedit/*.[ch] Makefile; do ln -s "$i"; done
    $ make

The default build is ***without*** GtkSourceView. If you have **GtkSourceView 2.x** installed, simply pass the `with=-DWGTKSOURCEVIEW2` as an argument to make. For example, to build without GtkSourceView, simply type:

    $ make

To enable GtkSourceView and syntax highlighting (with GtkSourceView 2.x installed), build with:

    $ make clean
    $ make with=-DWGTKSOURCEVIEW2


**Note:** you must use `make clean` before calling `make` when switching back and forth between versions.

Give it a try, help make it better. Drop me a line if you have any questions. (ignore typos in the Readme -- it doesn't go though the compiler :)