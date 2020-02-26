---
layout: post
date: 2014-08-24
title: Qt 5, vtk 6 and Visual Studio development environment
categories: programming
tags: [C++, vtk, Visual Studio]
---

For my current client, I’m writing medical 3d processing software in C++. The targeted
platform is Windows for now, but this might change in the future, so I had to make sure to
make my choices accordingly. We also need dual compilation to both 32bit and 64bit.

The client agreed with my proposed setup which was C++, Qt 5, vtk 6, and Visual Studio. I
decided to go with the CMake build system and will share some insights about my setup
here.

<!--more-->

### Installation

There is a lot of information around on installing Qt and vtk together, but you have to
puzzle the pieces together and the process is not exactly smooth. The best resource is the
build documentation on the vtk site. The individual steps I did:

1. Download and install Qt 5.3.1 for both 32 and 64 bit. I installed to
   `C:\Qt\Qt5.3.1.32bit` and `C:\Qt\Qt5.3.1.64bit`
2. Download the vtk 6.1 source code, I put it into `C:\vtk\src\VTK-6.1.0`
3. Start-up the CMake-GUI with the vtk source path and an appropriate 32bit target path. I
   used `C:\vtk\bin.qt5.32bit`.
4. On the first run, CMake asks about the compiler. Choose the 32bit compiler here
  (“Visual Studio 12 2013”).
5. The configuration needs some tweaking for Qt5, so configure the following values:
  * VTK_Group_Qt=1
  * VTK_QT_VERSION=5
  * QT_QMAKE_EXECUTABLE=`C:/Qt/Qt5.3.1.32bit/5.3/msvc2013_opengl/bin/qmake.exe`
  * CMAKE_PREFIX_PATH=`C:/Qt/Qt5.3.1.32bit/5.3/msvc2013_opengl`
6. Configure and Generate
7. Open up the generated Visual Studio Solution in `C:\vtk\bin.qt5.32bit` and build the
  “ALL” target for “Debug” and “Release” configurations.
8. Repeat steps 5 to 7 for 64 bit. As compiler use “Visual Studio 12 2013 Win64”. Adapt
  the Qt-paths accordingly to your 64bit Qt installation directory
  (`C:/Qt/Qt5.3.1.64bit/...`)

---

We now have everything built and in place. I personally do not set any PATH variables,
because for building and running we need all four configurations (Debug/Release and
32bit/64bit). We are going to setup the correct paths using CMake. Build script

Because of the way CMake works, it’s quite hard to get both the 32bit and 64bit builds
working in the same solution. Therefore, we’ll have two separate CMake output folders
32bit and 64bit and switch out the paths at the relevant places in my CMakeLists.txt
according to the selected compiler.

```cmake
# --------------------------------
# Set variable for 32 or 64 bit
#
if(${CMAKE_SIZEOF_VOID_P} MATCHES 4)
  message(STATUS "CONFIGURING FOR 32 BIT!")
  set(IS_64_BIT 0)
  set(BIT_3264 "32")
  set(BIT_64_ "")
  set(VS_3264 "Win32")
else(${CMAKE_SIZEOF_VOID_P} MATCHES 8)
  message(STATUS "CONFIGURING FOR 64 BIT!")
  set(IS_64_BIT 1) SET(BIT_3264 "64")
  SET(BIT_64_ "64_")
  set(VS_3264 "x64")
endif()

set(PROJ_NAME "MyProjectName${BIT_3264}")

# --------------------------------
# Set Qt and VTK paths up for 32 or 64 bit
#
set(CMAKE_PREFIX_PATH "C:/Qt/Qt5.3.1.${BIT_3264}bit/5.3/msvc2013_${BIT_64_}opengl")
set(QT_QMAKE_EXECUTABLE PATH C:/Qt/Qt5.3.1.${BIT_3264}bit/5.3/msvc2013_${BIT_64_}opengl/bin/qmake.exe)
set(VTK_DIR C:/vtk/bin.qt5.${BIT_3264}bit) 

# --------------------------------
# SET UP VTK
#
find_package(VTK REQUIRED)
include(${VTK_USE_FILE})
set(VTK_BIN_DIR_DEBUG ${VTK_RUNTIME_LIBRARY_DIRS}/Debug)
set(VTK_BIN_DIR_RELEASE ${VTK_RUNTIME_LIBRARY_DIRS}/Release)

# --------------------------------
# SET UP QT
#
set(QT_USE_IMPORTED_TARGETS TRUE)
find_package(Qt5Widgets REQUIRED)
set(QT_BIN_DIR ${CMAKE_PREFIX_PATH}/bin)
include_directories(${CMAKE_CURRENT_SOURCE_DIR} ${CMAKE_CURRENT_BINARY_DIR})
```

Next thing we do, is organizing all source files into source groups, both for separation
in Visual Studio and for feeding into necessary Qt calls. I only included three exemplary
groups here (global, gui and model)

```cmake
# --------------------------------
# GATHER AND PREPARE ALL OWN FILES and TARGETS
# 
set(GLOBAL_SRCS_H
  ${CMAKE_CURRENT_SOURCE_DIR}/CriticalExc.h
  ${CMAKE_CURRENT_SOURCE_DIR}/global.h
  ${CMAKE_CURRENT_SOURCE_DIR}/InformationExc.h
  ${CMAKE_CURRENT_SOURCE_DIR}/WarningExc.h)
set(GLOBAL_SRCS_MAIN
  ${CMAKE_CURRENT_SOURCE_DIR}/main.cxx)

set(GUI_SRCS_H
  ${CMAKE_CURRENT_SOURCE_DIR}/gui/MainWindow.h)
set(GUI_SRCS_UI
  ${CMAKE_CURRENT_SOURCE_DIR}/gui/MainWindow.ui)
set(GUI_SRCS_CXX
  ${CMAKE_CURRENT_SOURCE_DIR}/gui/MainWindow.cxx)
  
set(MODEL_SRCS_H
  ${CMAKE_CURRENT_SOURCE_DIR}/model/AModel.h
  ${CMAKE_CURRENT_SOURCE_DIR}/model/IModel.h)
set(MODEL_SRCS_CXX
  ${CMAKE_CURRENT_SOURCE_DIR}/model/AModel.cxx)
```

Now we need to feed these groups into the according CMake Qt functions and link everything
together. Since I also have a test project, I added everything except of main.cxx into one
large static library. This library can be reused by both the main app and the test app
which saves compilation time.

```cmake
set(MOC_HEADERS ${GUI_SRCS_H})
set(UI_FILES ${GUI_SRCS_UI})
set(QT_RES ${CMAKE_CURRENT_SOURCE_DIR}/res/application.qrc)

set(H_FILES
  ${GLOBAL_SRCS_H}
  ${GUI_SRCS_H}
  ${MODEL_SRCS_H}
  ${TOOLS_SRCS_H)
SET(CXX_FILES_LIB
  ${GLOBAL_SRCS_CXX}
  ${GUI_SRCS_CXX}
  ${MODEL_SRCS_CXX})
SET(CXX_FILES_APP
  ${CXX_FILES_LIB}
  ${GLOBAL_SRCS_MAIN})
  
# We don't use AUTOMOC and AUTOUIC, because we want to add the according files to the
# "gen" sourcegroup
#
qt5_wrap_ui(UISrcs ${UI_FILES})
qt5_wrap_cpp(MOCSrcs ${MOC_HEADERS})
qt5_add_resources(RCCSrcs ${QT_RES})

# We compile most of the stuff as static lib, so that we can link into both the executable
# and the test project without double compilation.
#
set(STATIC_LIB ${PROJ_NAME}StaticLib)
add_library(${STATIC_LIB} STATIC ${CXX_FILES_LIB} ${UISrcs} ${MOCSrcs} ${H_FILES})
target_link_libraries(${STATIC_LIB} ${VTK_LIBRARIES})

add_executable(${PROJ_NAME} ${GLOBAL_SRCS_MAIN} ${RCCSrcs})
qt5_use_modules(${PROJ_NAME} Core Widgets Gui)
target_link_libraries(${PROJ_NAME} ${VTK_LIBRARIES} ${STATIC_LIB})
```

We now can Configure, Generate, and build our application with Visual Studio. However, we
can not run the application from Visual Studio, because the Qt- and Vtk-dlls are not in
the systems PATH. Since we have four sets of dlls (Release/Debug and 32bit/64bit), we
can’t just add them to the systems PATH, because most of them would clash with each other.
What we actually want is Visual Studio to add the correct paths to the local environment
before running the application.  
Visual Studio stores the run configurations in the
`<project name>.vcproj.user` right next to the project files. So we need to get CMake
to generate this file for us, with both Debug and Release configurations, and taking care
to correctly point to the 32bit or 64bit dlls. We can achieve this via the vtk command
`configure_file`.

```cmake
# --------------------------------
# SET UP FOR VISUAL STUDIO
# Configure the template file that allows debugging
#
set(USER_FILE ${PROJ_NAME}.vcxproj.user)
set(OUTPUT_PATH ${CMAKE_CURRENT_BINARY_DIR}/${USER_FILE})

configure_file(UserTemplate.user ${USER_FILE} @ONLY)
```

The configured UserTemplate.user file is placed at the root of our source directory, and
looks like this:

```xml
<?xml version="1.0" encoding="utf-8"?>
<Project ToolsVersion="12.0" xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
  <PropertyGroup Condition="'$(Configuration)|$(Platform)'=='Debug|@VS_3264@'">
    <LocalDebuggerEnvironment>PATH=@QT_BIN_DIR@;@VTK_BIN_DIR_DEBUG@;%PATH% _NO_DEBUG_HEAP=1</LocalDebuggerEnvironment>
    <DebuggerFlavor>WindowsLocalDebugger</DebuggerFlavor> <LocalDebuggerDebuggerType>Mixed</LocalDebuggerDebuggerType>
    <LocalDebuggerCommandArguments>@DEBUG_RUN_ARGS@</LocalDebuggerCommandArguments>
  </PropertyGroup>
  <PropertyGroup Condition="'$(Configuration)|$(Platform)'=='MinSizeRel|@VS_3264@'">
    <LocalDebuggerEnvironment>PATH=@QT_BIN_DIR@;@VTK_BIN_DIR_RELEASE@;%PATH% _NO_DEBUG_HEAP=1</LocalDebuggerEnvironment>
    <DebuggerFlavor>WindowsLocalDebugger</DebuggerFlavor>
  </PropertyGroup>
  <PropertyGroup Condition="'$(Configuration)|$(Platform)'=='RelWithDebInfo|@VS_3264@'">
    <LocalDebuggerEnvironment>PATH=@QT_BIN_DIR@;@VTK_BIN_DIR_RELEASE@;%PATH% _NO_DEBUG_HEAP=1</LocalDebuggerEnvironment>
    <DebuggerFlavor>WindowsLocalDebugger</DebuggerFlavor>
  </PropertyGroup>
  <PropertyGroup Condition="'$(Configuration)|$(Platform)'=='Release|@VS_3264@'">
    <LocalDebuggerEnvironment>PATH=@QT_BIN_DIR@;@VTK_BIN_DIR_RELEASE@;%PATH% _NO_DEBUG_HEAP=1</LocalDebuggerEnvironment>
    <DebuggerFlavor>WindowsLocalDebugger</DebuggerFlavor>
  </PropertyGroup>
</Project>
```

Finally, we should be able to configure 32bit and 64bit releases of your application
`\src\` tree into two different output folders (e.g. `\bin32bit\` and
`\bin64bit\`), compile them and run them from within Visual Studio.

There is one thing left, that keeps us from working comfortable in Visual Studio. All our
source files are located in the folders “Source Files” and “Header Files”, which are a
burden to work with. To achieve some structure within Visual Studio, we add CMake source
groups using our previously created source file structure. source groups will show up as
folders in the Visual Studio projects. We also create source groups for generated files
(gen) and resource files (res).

```cmake
source_group(global FILES ${GLOBAL_SRCS_H} ${GLOBAL_SRCS_CXX} ${GLOBAL_SRCS_MAIN})
source_group(gen FILES ${UISrcs} ${MOCSrcs} ${RCCSrcs})
source_group(res FILES ${QT_RES})
source_group(gui FILES ${GUI_SRCS_H} ${GUI_SRCS_CXX} ${GUI_SRCS_UI})
source_group(model FILES ${MODEL_SRCS_H} ${MODEL_SRCS_CXX})
```

Our nice setup to compile and run our application from Visual Studio in both 32bit and
64bit and in both Debug and Release configurations is now finished. We also have a
convenient way to organize our code in the Visual Studio solution.

If you have any questions regarding my setup, feel free to comment. I might post and
explain the rest of my CMake script at a later point; it deals with the unit test and
installer projects.

---

**Edit**: Due to popular demand, I uploaded a minimal working example. It’s a small
CMake/Qt/vtk application that lets you load any STL-file and try out the different Phong
shading parameters.

You can find the source
[here](https://github.com/B3ret/publicsamples/tree/master/phongersrc). It’s for Windows,
but should be adaptable to other systems. (Basically, just switch out the windows specific
libraries using the WIN32 and MSVC flags. You might also need to adapt the 32bit / 64bit
parts.)

**Edit (Feb. 2020)**: My current setup looks quite different, mainly because I now have
working dual-compilation on Windows and OSX. I also switched to "Modern CMake" idioms. Let
me know if you are interested in an updated version of this blog entry at {% include
link_mailtome.html %}.

Also, I'm moving my website to GitHub pages and in the process I'm tidying up the wording
of this article and getting rid of the comment section. However, I'm migrating useful old
comments onto here as well (anonymized):

---

> A., February 1, 2015 at 11:40:  
> How can we build QVTKWidget?
>
> > My reply, February 2, 2015 at 05:14:  
> > QVTKWidget and several other QVTK* classes are part of vtk (./GUISupport/Qt) and
> > therefore built together with vtk. vtk is built using CMake, to enable Qt Support
> > during the CMake built process, set VTK_Group_Qt=1 and set the required Qt
> > directories. A decent guide on building vtk with Qt support is at
> > [http://www.vtk.org/Wiki/VTK/Configure_and_Build#Qt5..2A](http://www.vtk.org/Wiki/VTK/Configure_and_Build#Qt5..2A)

---

> A., February 8, 2015 at 00:14:  
> With your instruction, I was able to successfully build vtk with Qt for both 32 bit and
> 64 bit. Great tips, thanks. Could you post a minimally working example (the most simple
> vtk/Qt project)? It would greatly help if you would upload the content of the project
> directory as an example. I would like to have a better understanding of the CMake
> project build script.
>
> > My reply, February 2, 2015 at 05:14:  
> > Some minimal working examples can be found in the
> > [http://www.cmake.org/Wiki/VTK/Examples/Cxx#Qt](http://www.cmake.org/Wiki/VTK/Examples/Cxx#Qt).
> >
> > > A., February 11, 2015 at 09:51:  
> > > When I go to the link you provided, there are several examples. However, they are
> > > different compared to what you have here. For example, there is no example for
> > > UserTemplate.user, .vcproj.user as it is setup for Linux. Would you post the
> > > complete project for Visual Studio for one of their example such as this example or
> > > any of them that is convenience for you? I would like to see how the script files
> > > must be setup for Visual Studio. I would really appreciate it. 🙂
> > >
> > > > My reply, February 2, 2015 at 05:14:  
> > > > I’ll try to get to it next week, I’m quite busy right now.
> > > >
> > > > > A., February 21, 2015 at 23:23:  
> > > > > Would be much appreciated.
> > > > >
> > > > > > My reply, March 10, 2015 at 07:11: 
> > > > > > I have now added the example.
