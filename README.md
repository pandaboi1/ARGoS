# ARGoS

git clone https://github.com/ilpincy/argos3.git argos3ARGoS README

=============

:Author: Carlo Pinciroli

:Email:  ilpincy@gmail.com

:Date:   November 26th, 2019

## What is ARGoS?
---------------

ARGoS is a physics-based simulator designed to simulate large-scale robot
swarms. Benchmark results show that ARGoS can perform physics-accurate
simulation involving thousands of robots in a fraction of real time.
ARGoS' main features are:

* Multi-threaded and deeply modular architecture, more flexible than any
  simulator with equivalent features;
* The possibility to run multiple physics engines at the same time;
* The possibility to divide the physical space in region, and assign different
  regions to different physics engines.

Starting from version 3, ARGoS is released under the terms of the MIT license.

## Downloading ARGoS
------------------

You can download a binary package of ARGoS from
http://www.argos-sim.info/download.php. Alternatively, you
can download the development sources through git:

 $ git clone https://github.com/ilpincy/argos3.git argos3

## Compiling ARGoS

### Requirements

If you downloaded the sources of ARGoS and want to compile its code, you need:

* A UNIX system (Linux or MacOSX; Microsoft Windows is not supported)
* _g++_ >= 5.4 (on Linux)
* _clang_ >= 3.1 (on MacOSX)
* _cmake_ >= 3.5.1

If you want to compile the simulator, you need:

* _FreeImage_ >= 3.15

The OpenGL-based graphical visualization is compiled only if the following
libraries are found:

* _Qt_ >= 5.5
* _freeglut_ >= 2.6.0
* _libxi-dev_ (on Ubuntu and other Debian-based systems)
* _libxmu-dev_ (on Ubuntu and other Debian-based systems)

If you want to create the Lua wrapper you need:

* _lua_ == 5.3

If you want to create the documentation you need:

* To create the API:
** _Doxygen_ >= 1.7.3
** _Graphviz/dot_ >= 2.28
* To create the HTML version of this README:
** _asciidoc_ >= 8.6.2

### Debian
^^^^^^

On Debian, you can install all of the necessary requirements
with the following command:

 $ ```sudo apt-get install cmake libfreeimage-dev libfreeimageplus-dev \
   qt5-default freeglut3-dev libxi-dev libxmu-dev liblua5.3-dev \
   lua5.3 doxygen graphviz libgraphviz-dev asciidoc```

### OpenSuse
^^^^^^^^

On openSUSE 13.2, you can install all of the necessary requirements
with the following commands:

 $ ```sudo zypper ar -n openSUSE-13.2-Graphics``` http://download.opensuse.org/repositories/graphics/openSUSE_13.2/ \
   graphics

 $ ```sudo zypper refresh```

 $ ```sudo zypper install git cmake gcc gcc-c++ freeimage-devel``` doxygen graphviz asciidoc lua-devel libqt5-qtbase freeglut-devel 
  rpmbuild

### Mac OSX
^^^^^^^

On Mac, you can install all of the necessary requirements using
http://http://brew.sh/[HomeBrew]. On the command line, type the
following command:

 $ ```brew install pkg-config cmake libpng freeimage lua qt```    docbook asciidoc graphviz doxygen

## Compiling the code

The compilation of ARGoS is configured through CMake.

### Fast compilation instructions
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

### Compiling the ARGoS simulator
++++++++++++++++++++++++++++++

 $ ```cd argos3```

 $ ```mkdir build_simulator```

 $ ```cd build_simulator```

 $ ```cmake ../src```

 $ ```make```

### Compiling ARGoS for a robot
++++++++++++++++++++++++++++

DO NOT EXECUTE THESE COMMANDS IF YOU ARE INSTALLING ARGOS ON YOUR LAPTOP. THESE COMMANDS ARE MEANT TO INSTALL ARGOS ON A REAL ROBOT.

 $ ```cd argos3```

 $ ```mkdir build_myrobot```

 $ ```cd build_myrobot```

 $ ```cmake -DARGOS_BUILD_FOR=myrobot ../src```

 $ ```make```

### Compiling the documentation
+++++++++++++++++++++++++++

 $ ```cd argos3```

 $ ```cd build_simulator # or 'cd build_myrobot'```

 $ ```make doc```

### ARGoS sources under Eclipse
+++++++++++++++++++++++++++

To use Eclipse with the ARGoS sources, you must have the
http://www.eclipse.org/cdt/[CDT] installed. Optionally, you can also
install http://cmakeed.sourceforge.net/[CMakeEd] to modify the
+CMakeLists.txt+ files comfortably within Eclipse.

To configure the ARGoS sources for Eclipse, it is better to avoid
compiling the code in a separate build directory (for more details, see
http://www.vtk.org/Wiki/Eclipse_CDT4_Generator#Out-Of-Source_Builds[here]).

Thus, execute CMake as follows:

 $ ```cd argos3```

 $ ```cmake -G "Eclipse CDT4 - Unix Makefiles" src/```

Now open Eclipse. Click on _File_ -> _Import..._, select
_Existing project into workspace_, and click on _Next_. Set the base +argos3+ directory as the root directory in the dialog that appears. Click on _Next_
and you're ready to go.

### Advanced compilation configuration
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The compilation of ARGoS can be configured through a set of CMake options:

[options="header"]
|====================================================================================================================
| Variable    | Type    | Meaning [default value]
| :- | :- | -- | 
| +CMAKE_BUILD_TYPE+       | _STRING_  | Build type (+Debug+, +Release+, etc.) [empty]
| +CMAKE_INSTALL_PREFIX+   | _STRING_  | Install prefix (+/usr+, +/usr/local+, etc.) [+/usr/local+]
| +ARGOS_BUILD_FOR+        | _STRING_  | Target of compilation (+simulator+ or robot name) [+simulator+]
| +ARGOS_BUILD_NATIVE+     | _BOOLEAN_ | Whether to use platform-specific instructions [+OFF+]
| +ARGOS_THREADSAFE_LOG+   | _BOOLEAN_ | Use or not the thread-safe version of +LOG+/+LOGERR+. [+ON+]
| +ARGOS_DYNAMIC_LOADING+  | _BOOLEAN_ | Compile (and use) dynamic loading facilities [+ON+]
| +ARGOS_USE_DOUBLE+       | _BOOLEAN_ | Use +double+ (+ON+) or +float+ (+OFF+) [+ON+]
| +ARGOS_DOCUMENTATION+    | _BOOLEAN_ | Create API documentation [+ON+]
| +ARGOS_INSTALL_LDSOCONF+ | _BOOLEAN_ | Install the file +/etc/ld.so.conf/argos3.conf+ [+ON+ on Linux, +OFF+ on Mac]
|

====================================================================================================================

You can pass the wanted values from the command line. For instance, if you
wanted to set explictly all the default values, when compiling on Linux you would write:

 $ ```cd argos3/build_simulator```

 $ ```cmake -DCMAKE_BUILD_TYPE=Debug \```

  - ```-DCMAKE_INSTALL_PREFIX=/usr/local \```

  - ```-DARGOS_BUILD_FOR=simulator \```

  - ```-DARGOS_BUILD_NATIVE=OFF \```

  - ```-DARGOS_THREADSAFE_LOG=ON \```

  - ```-DARGOS_DYNAMIC_LOADING=ON \```

  - ```-DARGOS_USE_DOUBLE=ON \```

  - ```-DARGOS_DOCUMENTATION=ON \```

  - ```-DARGOS_INSTALL_LDSOCONF=ON \```

  - ```../src```

**IMPORTANT**: *When +ARGOS_BUILD_FOR+ is set to +simulator+, +ARGOS_THREADSAFE_LOG+ and +ARGOS_DYNAMIC_LOADING+ must be ON.*

**IMPORTANT**: *If you want to install ARGoS without root privileges, remember to set +ARGOS_INSTALL_LDSOCONF+ to +OFF+. Otherwise, installation will fail midway.*

***TIP***: *For production environments, it is recommended to compile ARGoS with +CMAKE_BUILD_TYPE+ set to +Release+. If you want to debug ARGoS, it is recommended to set +CMAKE_BUILD_TYPE+ to +Debug+. The other standard settings (empty and +RelWithDebInfo+) are supported but should be avoided.*

***TIP***: *If you want to squeeze maximum performance from ARGoS, along with compiling with +CMAKE_BUILD_TYPE+ set to +Release+, you can also set +ARGOS_BUILD_NATIVE+ to +ON+. This setting instructs the compiler to use the compiler flags +-march=native+ and +-mtune=native+. The code will run faster because you use the entire instruction set of your processor, but the generated binaries won't be portable to computers with different processors.*

## Using the ARGoS simulator from the source tree
----------------------------------------------

**IMPORTANT**: You can't install ARGoS system-wide and run the source version at the same time. If you intend to run ARGoS from the sources, you must uninstall it from the
           system.

### Running the ARGoS simulator

If you don't want to install ARGoS on your system, you can run it from the sources
tree. In the directory +build_simulator/+ you'll find a bash script called
+setup_env.sh+. Executing this script, you configure the current environment to
run ARGoS:

 $ ```cd argos3```

 $ ```cd build_simulator```

 $ ```. setup_env.sh``` or ```'source setup_env.sh'```

 $ ```cd core```

 $ ```./argos3 -q all``` this shows all the plugins recognized by ARGoS

If you execute ARGoS with the graphical visualization, you'll notice that icons, models, and textures are missing. This is normal, as ARGoS by default looks for them in the default install location. To fix this, you need to edit the default settings of the GUI.

On Linux, edit the file +$HOME/.config/Iridia-ULB/ARGoS.conf+ as follows:

 [MainWindow]
 #
 ## other stuff
 #
 icon_dir=/PATH/TO/argos3/src/plugins/simulator/visualizations/qt-opengl/icons/
 texture_dir=/PATH/TO/argos3/src/plugins/simulator/visualizations/qt-opengl/textures/
 model_dir=/PATH/TO/argos3/src/plugins/simulator/visualizations/qt-opengl/models/
 #
 ## more stuff
 #

***On Mac***, write the following commands on the terminal window to fix the paths manually:

 $ ```defaults write info.argos-sim.ARGoS MainWindow.texture_dir -string "/PATH/TO/argos3/src/plugins/simulator/visualizations/qt-opengl/textures/"```

 $ ```defaults write info.argos-sim.ARGoS MainWindow.model_dir -string "/PATH/TO/argos3/src/plugins/simulator/visualizations/qt-opengl/models/"```

 $ ```defaults write info.argos-sim.ARGoS MainWindow.icon_dir -string "/PATH/TO/argos3/src/plugins/simulator/visualizations/qt-opengl/icons/"```

 $ ```killall -u YOURUSERNAME cfprefsd```

or use these commands to delete these paths and have ARGoS look for them:

 $ ```defaults write info.argos-sim.ARGoS```

 $ ```killall -u YOURUSERNAME cfprefsd```

Be sure to substitute +/PATH/TO/+ with the correct path that contains the +argos3+
folder, and +YOURUSERNAME+ with your username as displayed on the terminal.

### Debugging the ARGoS simulator

You can debug the ARGoS code using +gdb+. Since the code in scattered across multiple
directories, you need a +.gdbinit+ file. Luckily for you, this file is created automatically when you compile ARGoS. To use it, you just need to remember to run the ARGoS simulator from the +build_simulator/core/+ directory:

 $ ```cd argos3/build_simulator/core```

 $ ```gdb ./argos3```

## Installing ARGoS from the compiled binaries
--------------------------------------------

To install ARGoS after having compiled the sources, it is enough to write:

 $ ```cd argos3```

 $ ```cd build_simulator``` or ```'cd build_myrobot'```

 $ ```make doc``` documentation is required!

 $ ```sudo make install```

Alternatively, one can create a package. To build all the packages supported by your system, run these commands:

 $ ```cd argos3```

 $ ```git tag -a X.Y.Z-release``` 

                            # give the package a unique version
                            # the format must be as shown
                            # X       = version major
                            # Y       = version minor
                            # Z       = version patch
                            # release = a textual label

 $ ```cd build_simulator``` or 'cd build_myrobot'

 $ ```cmake .``` let CMake read the newly set tag

 $ ```make doc``` documentation is required!

 $ ```make``` compile the code

 $ ```sudo make package``` make the package

This typically creates a self-extracting .tar.gz archive, a .tar.bz2 archive,
a .zip archive, and a platform-specific archive (.deb, .rpm, or a MacOSX
package). You can determine which packages to create by setting the variables
+CPACK_BINARY_DEB+, +CPACK_BINARY_RPM+, +CPACK_BINARY_STGZ+,
+CPACK_BINARY_TBZ2+, +CPACK_BINARY_TGZ+, +CPACK_BINARY_TZ+.

**IMPORTANT**: the creation of source packages through the command
           +make package_source+ is not supported.

An easier option is to install ARGoS from a package distributed at
http://www.argos-sim.info/download.php.
