# MacroToolbarManager
Easily manage custom macro toolbars in FreeCAD

## Installation
Install using the Addon Manager.  Alternatively, copy the MacroToolbarManager.FCMacro file to your macro folder.  If you don't know where that folder is you can find it in Macro menu -> Macros or in the python console using:<pre>
App.getUserMacroDir(True)
</pre>

## Toolbar icon
The addon manager will install the toolbar icon for you upon installation.  Alternatively, a toolbar icon is embedded into the macro itself.  When you run the macro, select the MacroToolbarManager.FCMacro in the Macro names: combo box, then click the From macro button to extract the icon xpm data.  The icon xpm information text should appear in the extracted field in the macro window.  Click the Save XPM button, which should now be enabled, select a folder for the macro icon, and save it there.  It doesn't matter where you put the icon file.  The macro will tell FreeCAD where to find it.  Then click Add to toolbar button to add the macro to the toolbar.  If it's already in the toolbar, click Add to toolbar button anyway because this will update the new icon information.  Alternatively, you can download the SVG version:<br/><br/> <a href="https://wiki.freecad.org/images/5/56/MacroToolbarManager_icon.svg"><img src = "https://wiki.freecad.org/images/5/56/MacroToolbarManager_icon.svg"></a>

