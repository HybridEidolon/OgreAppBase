# OGRE CMake Multiplatform Base

This is a base for OGRE projects using CMake. The code is organized into modules, a Core, and a set of Interface modules for each platform supported.

Written by Ronald Kinard (https://github.com/Furyhunter).

This does not include a CPack configuration file for generating distributable packages, but I imagine it should be easy enough to make one.

## License

This work is released in the public domain.

## Requirements

An OGRE 1.9 SDK installation, either built from source or downloaded from the OGRE website.

For MacOSX, you must build the OGRE SDK from Source **as a non-STATIC build**, and copy the frameworks generated to ~/Library/Frameworks in order to run the application.

## Compiling

### Linux

	$ mkdir Build && cd Build
	$ cmake -DOGRE_HOME=/path/to/ogre-1.9/sdkroot/ ..
	$ make

Then, to run it,

	$ cd Binaries
	$ ./ProjectName

### Windows (Visual Studio 2013)

1. Open CMake-Gui and set the source path, and the build path to the source path + Build
2. Add Entry OGRE_HOME and set it to your OGRE SDK path.
3. Configure for Visual Studio 2013
4. Generate
5. Open Build/ProjectName.sln
6. Build & Debug

On Windows, the DLLs needed to run the application are copied automatically to the binary folder.

### MacOSX (XCode 6)

	$ mkdir Build && cd Build
	$ cmake -GXcode -DOGRE_HOME=/path/to/ogre-1.9/sdkroot/ ..
	$ open ProjectName.xcodeproj

## Tips

* If you are using version control, do not commit the Build folder. The generated build scripts are for your local working copy, not anyone else.
* To add Ogre plugins, simply add them to the `find_package` line in the `CMakeLists.txt` and add to linking/includes. You will also have to add the `loadPlugin` line in `Source/Core/Application.cpp` to load the library before you can use it.
* To add code modules, use the `add_project_module` macro.

## Notes

On MacOSX, there is an issue with the Ogre 1.9 build script that, when installing, subdirectories of a plugin's include dir are not copied into the Headers directory of the framework. An example of this is the `glew` header. `FindOGRE.cmake` doesn't account for it and automatically uses the framework's Headers if it finds it, so you have to manually add the correct includes yourself in `CMakeLists.txt`. I can't tell if this is a bug or intentional, but you have to work with it. It may actually be fixed in the development branch!

Visual Studio 2015 Preview is probably not supported because OGRE won't compile in it. It's a bummer. :disappointed:

You need a recent version of g++ to compile under Linux.

## Other information

Created for CS 354R Game Technology at the University of Texas at Austin.
