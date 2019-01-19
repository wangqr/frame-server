# Frameserver #

Frameserver is a plugin for video editing apps to do FrameServing, Image Sequence export and AudioServing.

# Features #

Frameserving and Audioserving are the techniques used to transfer audio/video data from one application to another without doing a full fledged render and temporary files. Frameserver is a plugin for NLEs enabling them to export their timeline audio/video data outside so that other applications can use the timeline directly as input.

Another use of the Frameserver is to serve audio/video data to an application that does not understand the source format. If you have a video editor that can open .MOV files and your MPEG encoder can read only .AVI input files, you can open the .MOV file in your NLE and use Frameserver to serve the a/v data to your MPEG encoder. This increases compatibility between applications.

Frameserver can also export the video from your NLE as an Image sequence. Frames can be saved in lossless BMP, TIFF, PNG and high quality JPEG formats.

# Build #

CMake is used to build the Premiere Pro Plug-in.

For any other parts of Frameserver, please use the original SCons build system. Detailed instructions can be found at [the original repo](https://github.com/satishsampath/frame-server/blob/master/README.md).

The following descriptions are for Premiere Pro Plug-in only.

## Requirements to build ##

  1. MS Visual Studio (tested with VS2017 and VS2019)
  1. CMake (tested with version 3.13.3, https://cmake.org/)
  1. You will need the Plug-in SDKs for all the supported host applications. More info about this in the **Host SDKs** section below.

## Host SDKs ##

Frameserver works as a plug-in for various video editing 'host' applications and allows exporting the rendered video from them as .avi files. To build the plug-in for each host application, you need to have the host's plug-in SDK. You need to download each plug-in SDK yourself from the host application's website, because their Terms & Conditions do not allow redistributing them with the Frameserver codebase.

  * Premiere Pro Plug-in SDK: https://www.adobe.io/apis/creativecloud/premierepro.html

Once downloaded, place the host SDK files in the following hierarchy:
```
src/SDKs
  +-- Premiere
        +-- Examples
              +-- Headers
              +-- Projects
              +-- Resources
              +-- Utils
```
Alternatively, you can manually set CMake option `PREMIERE_INCLUDE_DIRS` to the `Examples/Headers` folder.

## Steps to build ##

  1. Run CMake, select a directory to hold building related files. Configure and generate the project.
  1. Open the project in Visual Studio. Select to Release mode. Build the `dfscPremiere` target.