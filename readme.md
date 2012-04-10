# vfr Rader Native Extension #
Use the alternative vfr Reader for viewing pdf files in Adobe AIR for iOS

Original source - https://github.com/vfr/Reader, screens available at http://www.vfr.org/

author of this extension: Paweł Meller

Currently supported:

* `showFile(filePath:String,password:String=""):Boolean`
opens pdf using optional password.   
The viewer adds thumbs, bookmarks, mail and print options, just as in the original vfr reader
* `VfrPdfReader.isSupported():Boolean`
reutrns true if supported, false if not supported

### Info ###
On iPad the pdf window sometimes has problems with rotation (for example if the application is using landscape orientation, the window is shown in portrait / after pressing 'done' the view is dismissed, but the application is rotated (portrait instead of landscape / landscape instead of portrait). It appears to be a bug in Adobe AIR, since in simulator it runs well. It is fixed in AIR 3.3 (currently available from labs.adobe.com), so just compile your app using 3.3 and everything should work well.

### Usage ###
download [.swc](https://github.com/memeller/vfrReaderNativeExtension/raw/master/build/VfrPdfReader.swc) and [.ane](https://github.com/memeller/vfrReaderNativeExtension/raw/master/build/VfrPdfReader.ane) files from build directory and add them to project  
Example project is included, to open pdf just use:
    
    var vfrReader:VfrPdfReader=new VfrPdfReader();
    var file:File=File.applicationDirectory;
    file.resolvePath("Reader.pdf");
    vfrReader.showFile(file.nativePath+"/Reader.pdf");

### ANE compilation ###
To compile the ane, osx with iOS SDK is needed. 

example command:

    /Applications/Adobe\ Flash\ Builder\ 4.6/sdks/4.6.0/bin/adt -package -target ane VfrPdfReader.ane ./extension.xml 
    -swc VfrPdfReader.swc -platform iPhone-ARM -C ./ios . -platformoptions ios-platformoptions.xml -platform default library.swf

please note, that ios directory contains a couple of images, that are used in the application, if you choose not to include them, some buttons and functions will not work
It is possible to change the toolbar icons by replacing these images and compiling the ane with new ones.
platform options file has to be specified, including these frameworks:

`-framework MessageUI -framework ImageIO` (other ones are already included in AIR)

Tested on iPad, iOS 5.01