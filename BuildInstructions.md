# Introduction #

Frameserver's build uses the SCons build system (you can find the build configs in the files SConstruct and SConscript throughout the codebase). Most of the executables get built using MS Visual Studio 6.0 and some of the newer binaries require MS Visual Studio 2008.

# Requirements to build #

  1. MS Visual Studio 6.0, for most of the plug-ins
  1. MS Visual Studio 2008 (can use express edition), for Vegas Pro and Premiere Pro plug-ins
  1. A Visual Studio 6.0 compatible platform SDK. I use MS Windows Server 2003 [R2](https://code.google.com/p/frame-server/source/detail?r=2) Platform SDK (http://www.microsoft.com/downloads/details.aspx?FamilyID=484269e2-3b89-47e3-8eb7-1f2be6d7123a)
  1. Latest version of Windows platform SDK. I use Windows SDK 6.1 for Windows Server 2008 and .NET Framework 3.5 (http://www.microsoft.com/downloads/en/details.aspx?FamilyID=e6e1c3df-a74f-4207-8586-711ebe331cdc&displaylang=en - Install both 32 bit and 64 bit components).
  1. Nullsoft Scriptable Install system, for the installer (NSIS, http://nsis.sourceforge.net/)
  1. Python, for build scripts (tested with version 2.6, http://www.python.org)
  1. SCons (tested with version 1.2.0, http://www.scons.org)
  1. You will need the Plug-in SDKs for all the supported host applications. More info about this in the **Host SDKs** section below.

# Host SDKs #

Frameserver works as a plug-in for various video editing 'host' applications and allows exporting the rendered video from them as .avi files. To build the plug-in for each host application, you need to have the host's plug-in SDK. You need to download each plug-in SDK yourself from the host application's website, because their Terms & Conditions do not allow redistributing them with the Frameserver codebase.

  * Vegas Pro Plug-in SDK: http://www.sonycreativesoftware.com/download/devkits - look for 'Video Plug-In Development Kit'
  * Premiere Pro Plug-in SDK: http://www.adobe.com/devnet/premiere/sdk/cs5/
  * EditStudio SDK: http://www.mediachance.com/video/index.html - look for 'EditStudio SDK'
  * MediaStudio Pro SDK: http://www.ulead.com/download/sdk/license.htm - accept the license & in the next page download 'VIO Module'
  * Wax Plug-in SDK: Included in the codebase.

Once downloaded, place the host SDK files in the following hierarchy:
```
src/SDKs
  ├── EditStudio
  │     ├── Src
  │     └── Include
  │           └── ES_Plugin
  ├── MediaStudioPro
  │     ├── Include
  │     └── Lib
  │          ├── Debug
  │          └── Release
  ├── Premiere
  │     ├── compiler
  │     ├── cs4
  │     └── cs5
  ├── Vegas
  │     ├── ffp
  │     └── fio
  │          └── libFileIO
  ├── VegasV2
  │     └── libFileIO
  └── Wax
```

# Steps to build #

  1. Open a command prompt
  1. Set the following environment variables in your command line (you can also do this permanently in your "System properties" dialog under the "Advanced > Environment Variables" section):
    * INCLUDE: set it to your VC6 compatible platform SDK include and include\mfc directories. For e.g.<br>  set INCLUDE="C:\Microsoft SDKs\Windows Server 2003 PSDK <code>R2</code>\include;C:\Microsoft SDKs\Windows Server 2003 PSDK <code>R2</code>\include\mfc;"<br>
<ul><li>LIB: set it to your VC6 compatible platform SDK lib directory. For e.g.<br>  set LIB=C:\Microsoft SDKs\Windows Server 2003 PSDK <code>R2</code>\lib;<br>
</li><li>Add your python install directory to the path. (this is where SCons gets installed by default as well). For e.g.<br>  set PATH=%PATH%;C:\Python26<br>
</li></ul><ol><li>From the root directory of the codebase (where you'll find the file "SConstruct"), run "scons installer". This should build the installer and place it under "bin\fssetup.exe"