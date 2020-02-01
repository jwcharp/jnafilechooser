JnaFileChooser
==============

This is a small package that uses the native file chooser and folder browser 
dialogs on Windows if possible. It falls back to the Swing JFileChooser 
class if necessary.

Example Usage
-------------

    JnaFileChooser fc = new JnaFileChooser();
    fileBrowser.setMode(JnaFileChooser.Mode.Files); //Directories Only set to - JnaFileChooser.Mode.Directories
    fc.addFilter("All Files", "*");
    fc.addFilter("Pictures", "jpg", "jpeg", "png", "gif", "bmp");
    fc.setCurrentDirectory("C:/Users");
	fc.setSaveBtnText("Save File Here");//will only work for Swing fallback
    //fc.setOpenBtnText("Select File");//will only work for Swing fallback
	fc.setDialogTitle("Save Your Image");
	fc.setDefaultFileName("image.jpg");
	fc.setMultiSelectionEnabled(false);//will only work for Swing fallback currently
    //result = fc.showOpenDialog(parentJFrame);
    result = fc.showSaveDialog(parentJFrame);
    if (result) {
    	File f = fc.getSelectedFile();
    	// do something with f
    }    


How does it work?
-----------------
JnaFileChooser uses the JNI/[JNA][1] library which enables access to native
code with plain Java code, no JNI necessary.


How to add to your Java Project
-------------------
JnaFileChooser consists of 2 packages: fileBrowser and demo. 

The win32 module contains the low-level code which maps to the win32 API. You 
could use this code directly if you wish. It is a pretty straight-forward
mapping of the relevant parts of the win32 API.

The the fielBrowser package the the require src files for the fileBrowser.
Three interface classes:
JnaFileChooser, WindowsFileChooser and WindowsFolderBrowser
Three win32 classes:
Comdlg32, Ole32, Shell32

JnaFileChooser the main controller that will use the other two classes.
This controller will attempt to use Windows native File Explore if available.
If the settings sent the the contoller are not compatible with Windows File Explorer
it will automatically fallback to the Swing JFileChooser. The contoller will also fallback
to Swing JFileChooser is not on a Windows System.
WindowsFileChooser and WindowsFolderBrowser can be used by solo if you so choose.

The demo module contains sample code.

[1]: https://github.com/twall/jna
