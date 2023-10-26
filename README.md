# MacroToolbarManager
Easily manage custom macro toolbars in FreeCAD

## Installation
Install using the Addon Manager.  Alternatively, copy the MacroToolbarManager.FCMacro file to your macro folder.  If you don't know where that folder is you can find it in Macro menu -> Macros or in the python console using:<pre>
App.getUserMacroDir(True)
</pre>

## Toolbar icon
The addon manager will install the toolbar icon for you upon installation.  Alternatively, a toolbar icon is embedded into the macro itself.  When you run the macro, select the MacroToolbarManager.FCMacro in the Macro names: combo box, then click the From macro button to extract the icon xpm data.  The icon xpm information text should appear in the extracted field in the macro window.  Click the Save XPM button, which should now be enabled, select a folder for the macro icon, and save it there.  It doesn't matter where you put the icon file.  The macro will tell FreeCAD where to find it.  Then click Add to toolbar button to add the macro to the toolbar.  If it's already in the toolbar, click Add to toolbar button anyway because this will update the new icon information.  Alternatively, you can download the SVG version:<br/><br/> <a href="https://wiki.freecad.org/images/5/56/MacroToolbarManager_icon.svg"><img src = "https://wiki.freecad.org/images/5/56/MacroToolbarManager_icon.svg"></a>

## Usage
Usage is fairly self-explanatory.  Here is a screenshot:<br/>
<br/>
<img src="https://wiki.freecad.org/images/f/f4/MacroToolbarManager_scr01.png"><br/>
<br/>
I'll document from the top down.

### Workbench section

#### Workbench (combo box)
The Workbench combo box is where you select the workbench this toolbar will go into.  If you select Global, then that means the toolbar will be available for every workbench.  If you select a workbench, such as Part workbench, then the toolbar will go into that workbench and will only be visible while you are in that workbench.  This can be very useful if you want to reduce clutter and only have the macro icons that you need in a particular workbench.

#### Active/Global (button)
The Active/Global button will select the active workbench for you in the combo box rather than requiring you to search through all the installed workbenches to find it.  If the active workbench is already selected, then this button selects the Global option for you.  It's essentially a toggle switch.

#### Menu (button)
The menu button is the button to the far right at the top of the window.  I'll cover the menu items in the next section.

### Menu items
The menu is accessed by clicking the button in the far right top corner.
#### Settings
There is currently only one group in settings -> System Icons.  Note: this menu is also accessible via right-click context menu with the System icons button.

##### System Icons -> Parse Mod folders (boolean checked or unchecked)
Default: False (unchecked).  If checked (true) then when you use the System icons button it will parse the Mod folders for additional icons to display.  The Mod folders are where the addon workbenches get installed, so if you want to use an icon from an installed addon workbench, the you need to enable Parse Mod folders.  Alternatively, add the exact folder you want to fetch the icons from in the Manage icon folders dialog, documented next.  This option is false by default because it takes some time to parse all the Mod folders, depending on how many workbenches you have installed.

##### System icons -> Manage icon folders
FreeCAD allows you to specify additional icon folders to search for icons in.  This is used in the Customize dialog (Tools menu -> Customize) when you click the ... pixmap button when setting up an icon and then click the Icon folders... button.  Icons that exist in those folders will be added to the icon selection dialog in Customize.  We do the same thing here with the System icons button, which brings up a similar (but not exactly the same) set of icons to pick from.  The icon folders dialog implemented in the macro is substantially the same as the icon folders dialog implemented in FreeCAD.  It allows you to add/remove additional icon folders.  Note: The first folder in the list is the one we use for a number of default folders when saving or loading icons, so you should setup at least one in this dialog so you can keep all your icons organized in the same place.

#### Load workbenches (action)
This will load all installed workbenches, one after another.  It will take a while, so be patient.  Why would you do this?  When adding a new shortcut keyboard accelerator, the macro checks for conflicts.  But only the loaded workbenches can be checked, so if you have a conflicting shortcut in use in a workbench that hasn't been loaded yet in this session of FreeCAD, then the conflict checker will not find the conflit.  So, use this option before setting up shortcut accelerator keys to be confident you have chosen one without conflicts.

#### Remove orphans (action)
Orphans are macro toolbar items whose macro actions have been removed.  They don't show up in the toolbar, but they're still in the parameters database.  This option purges the database of these derelict macro items.  It doesn't delete any files.

#### Delete macro (action)
Deletes the macro file from your macros folder.  There is a sanity check, but it's not reversable, so be careful.

#### Remove macro action (action)
This removes the macro action from Tools menu -> Customize -> Macros tab.  It does not delete the macro file.  It is disabled if the macro is currently installed on the current toolbar (but no check is made whether the macro is installed on some other toolbar).  You might be wondering what the heck is a macro action?  Qt uses Action, but sometimes FreeCAD refers to these as commands.  Every menu item has an action associated with it, and so does every toolbar item, whether its a macro item or some other item, it has an action associated with it.  The action is basically an object with information, such as the icon, shortcut, what command to execute when triggered, the tooltip, etc.  In order to put a macro to a toolbar you must first create the action, but don't worry, the macro handles that all automatically for you when you click the add to toolbar button.  But what the remove from toolbar button doesn't do is it doesn't remove the macro action.  This is because the macro might be installed on another workbench and we don't want to orphan it there by removing the action.

### Toolbar section

#### Custom toolbar (combo box)
This is where you select which custom toolbar you will be working with.  You can have as many toolbars as you like, but I recommend only 1 global toolbar and only 1 workbench-specific toolbar per workbench.  You can have as many as you like if you feel more than 1 toolbar better meets your needs.

#### Active (check box)
The Active checkbox is a way to hide/disable toolbars without deleting them.  If you can't find your toolbar, this might be the reason why: you have deactivated it and forgot about doing it or possibly it was done by mistake.

#### New (button)
Create a new custom toolbar in the currently selected workbench in the Workbench combo box.

#### Rename (button)
Rename a toolbar.  Take notice that there are 2 names associated with toolbars.  There is what I call a Real name and the name you can edit here.  Behind the scenes the toolbar's real name will be something like "Custom1" or "Custom2", and you might see it referred to by that name in various places in FreeCAD.  The name you set here is the one we interact with in the macro.  The names should be unique to avoid confusion, but there is no requirement that they be unique.  The real names will be unique, either way.

#### Delete (button)
Delete a toolbar.  There is a sanity check, but take care because this action cannot be undone.  This does not remove any macro actions or delete any macro files.  It just removes the toolbar.

#### Currently installed (combo box)
These are the macros currently installed (if any) on the currently selected toolbar.  If you select one it updates the selection in the Macro name combo box.  If you have a lot of macros, this is an easier, more convenient way to find one rather than digging through a long list of macro files in the Macro names combo box.  If the currentl selected installed macro is the one you want to select in Macro names, then use the Select button.

#### Select (button)
Click it to make the macro selected in the Currently installed combo box also the macro selected in the Macro name combo box.

### Macros section
Here we have all the fields associated with a given macro action.  Which macro is in the Macro name combo box.  What menu text to use in a menu or on a toolbar if there is no icon, what tool tip to display when the mouse pointer hovers over the icon, what text to display in the status bar when the pointer is over the icon, what what's this text to show in the help system, and what shortcut accelerator keys to use.  There is also a pixmap section, which have organize below in an icon section.

#### Filter (line edit)
You can filter which files will appear in the Macro names combo box by entering your filter here.  This is a search by regular expression (case-insensitive) unless it is an invalid regular expression, in which case, a simple text search is done on the filenames.  Only the matching files are shown in the Macro names combo box.  If this filter is empty, then no filtering is done, other than filtering by extensions .py, .FCMacro, and .fcmacro.  This is a convenient way to find a specific macro without needing to scroll through a long list of filenames for those of us with large numbers of macros installed.

#### Add to toolbar (button)
Add the current macro to the current toolbar.  Requirements: There must be a toolbar to put it on because it does not automatically create one.  There must be some menu text in the menu text field.  If those 2 requirements are met, then this creates the macro action (if necessary) and puts the macro on the toolbar.  If the macro is already on the toolbar, then this will replace/update it for you, for example, if you changed icons or shortcut or any of the other fields.

#### Remove from toolbar (button)
Remove the macro from the toolbar.  Does not delete macro file.  Does not remove macro action.

#### Macro name (combo box)
This is a list of all the macro files in your macros folder.  Note: the system macros folder is not supported by this macro.  The files listed are filtered by only those with .py, .FCMacro, or .fcmacro extensions.

### Icon section
Here is where we have all the widgets related to working with the icons.

#### Pixmap (line edit)
This holds the pixmap text associated with this macro action.  It can be a couple different things.  It can be the full path to an icon file or it can be the name of a system icon.  An example of a system icon is "applications-python", which is the generic python icon used for the macro text editor built into FreeCAD.  When you use some of the buttons in this section the macro will update this pixmap text for you.

#### Icon (label)
There is a label after the Pixmap line edit between it and the buttons to the right side. If it contains a black X on a white background, that signifies the Pixmap field does not contain valid information to produce an icon.  If it has a different icon, then you should be good to go for putting it on the toolbar.

#### From macro (button)
Some macros have icon information embedded in their code in the form of string variables named __icon__ and __xpm__.  This button performs a scan of the actively selected macro in the Macro name combo box for this information, and the first one found gets extracted and put into the Icon information text area, the QPlainTextEdit widget below the Pixmap line edit.  The information might be a link to an online image, such as https://wiki.freecad.org/images/5/56/MacroToolbarManager_icon.svg, the svg macro file for this macro, or it might be the name of a system icon, or it might be the icon image in XPM notation.  It's up to you to figure out what it is and what to do with it.  If it's a url, then click the Download link button to download the file, save it in your icon folder, and setup the Pixmap text field to make use of it.  If it's the name of a system icon, then click Use as pixmap, or if it's in XPM format, click the Save XPM button to save it and setup the Pixmap text filed to make use of it.  (Note: the Make icon button will also fill up the Icon information text area with XPM data.)

#### Browse for icon (button)
Let's you browse for an icon file to use for this macro action.  The default folder it opens up in is the first icon folder you (might) have created already.  See System icons -> manage icon folders above for more details.  If no icon folders are defined, then it opens up in the macros folder.

#### System icon (button)
Note: This button also has a context menu.  Use this to browse for system icons, icon files in icon folders you have configured, and (optionally) for icon files in the Mod folders where the addon workbenches are installed.  When you click one of the icons in the dialog that pops up, it closes the dialog and sets up the pixmap text field for you.  Here is a screenshot:

<img src="MacroToolbarManager_scr02.png">

All image files are parsed, but we only keep those that are 64 x 64 pixels are smaller for use as icons.

#### Make icon (button)
The macro provides an icon creator tool that you can use to make your own simple icons.  I used it, in fact, to make the xpm version of the icon for this macro, the blue t and the red M.  This function makes use of openCV python package.  It comes bundled with FreeCAD, but if you self-compile you might not have it installed.  You can install with pip as pip install opencv-python.

Here is a screenshot:

<img src="MacroToolbarManager_scr03.png">

Learn more about the icon maker: <a href="iconmaker.md">here</a><br/>

#### Save XPM (button)
Saves the contents in the Icon information text area as a text file.  You need to supply the .XPM extension.  If it's SVG data, then save in SVG format.  (But I don't think anybody puts SVG data into these __icon__ and __xpm__ fields, as far as I know.  This text area can be filled by exporting XPM from the icon maker tool, by exporting sVG from that same dialog, by extracting XPM from the current icon (Extract XPM button), or by extracting this information from a macro it is embedded into via the above-mentioned __icon__ and __xpm__ variables.

#### Use as pixmap (button)
Uses the contents of the Icon information text area directly in the Pixmap field.

#### Download link (button)
Use this button to download the file in the url hyperlink in the Information text area, if such was extracted using the From macro button and placed into the text area.

#### Status section
There is a label at the bottom of the dialog below the Icon information field buttons where messages are sometimes displayed.  On startup the default message is "Messages go here."  Such messages are also echoed to the Report View, so if you think you missed something check there.  Messages in black text are normal messages, orange text means warnings, and red text indicates some sort of error occurred.



## Changelog
### v2023.10.22b -- don't ask for workbench when creating macro for non-macro action if command begins with "Std_", resize some buttons, minor bug fix
### v2023.10.22 -- add feature to create macro for non-macro action to run that action, add ability to extract XPM from current icon,
### v2023.10.21 -- add support for non-macro actions, add ability to autoload the current workbench, revised ui, move close button to menu as Quit action
### v2023.10.20 -- fix some bugs, add ability to Shift+Right-click to select an existing point, add face import, optimize some point functions.
### v2023.10.19 -- Svg export, Png export, Construction points, Sketch import, Zooming, too many things to list.
### v2023.10.12 -- add border colors to text in icon maker dialog, scale to 256x256 instead of 200x200 for a better 4:1 pixel ratio
### v2023.10.11f -- initial version along with a few tweaks for the addon manager and for advising people who need to install opencv to make use of all the features.

