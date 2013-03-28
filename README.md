# [QtAV](https://sourceforge.net/projects/qtav)

QtAV is a media playing library based on Qt and FFmpeg. It can help you to write a player
with less effort than ever before. Currently only a simple player is supplied. I will write a
stylish one based on QtAV in the feature.

QtAV has been added to FFmpeg projects page [http://ffmpeg.org/projects.html](http://ffmpeg.org/projects.html)

**QtAV is free software licensed under the term of LGPL v2.1. If you use QtAV or its constituent libraries,
you must adhere to the terms of the license in question.**

#### [Download binaries from sourceforge](https://sourceforge.net/projects/qtav)
#### [Source code on github](https://github.com/wang-bin/QtAV)

### Features

QtAV can meet your most demands

- Seek, pause/resume
- Video capture
- OSD
- Aspect ratio
- Transform video using GraphicsItemRenderer. (rotate, shear, etc)
- Playing frame by frame (currently support forward playing)
- Variant streams: locale file, http, rtsp, etc.
- Playing music (not perfect)
- Volume control
- Fullscreen, stay on top
- Compatible: QtAV can be built with both Qt4 and Qt5. QtAV will support
  both FFmpeg and [Libav](http://libav.org).
- Multiple render engine support. Currently supports QPainter, GDI+, Direct2D, XV and OpenGL.

### Extensible Framework (not finished)

  QtAV currently uses FFmpeg to decode video, convert image and audio data, and uses PortAudio to play
  sound. Every part in QtAV is designed to be extensible. For example, you can write your audio output
  class using OpenAL, image converting class using cuda to get better performance etc. These features
  will be added in the feature by default.


# For Developers

#### Requirements

1. [FFmpeg](http://ffmpeg.org) Latest version is recommanded.  
[![FFmpeg](http://ffmpeg.org/ffmpeg-logo.png)](http://ffmpeg.org)
2. [Qt 4 or 5](http://qt-project.org/downloads)  
[![Qt](http://blog.qt.digia.com/wp-content/themes/qt_blog/images/Qt_master_logo_CMYK_noback.gif)](http://qt-project.org)
3. [PortAudio v19](http://www.portaudio.com/download.html)  
[![PortAudio Logo](http://www.portaudio.com/images/portaudio_logo.png)](http://www.portaudio.com)[![PortAudio](http://www.portaudio.com/images/portaudio_logotext.png)](http://www.portaudio.com)

The required development files for MinGW can be found in sourceforge
page: [depends](https://sourceforge.net/projects/qtav/files/depends)

#### Build

You can build QtAV with many compilers and on many platforms. You can use gcc, clang, vc to compile it.  
See the wiki [Build QtAV](https://github.com/wang-bin/QtAV/wiki/Build-QtAV)

Here is a brief guide:

It's recommend not to build in source dir.  

    cd your_build_dir
    qmake QtAV_source_dir/QtAV.pro
    make

qmake will run check the required libraries at the first time, so you must make sure those libraries can be found by compiler.
Then qmake will create a cache file _.qmake.cache_ in your build dir. Cache file stores the check results, for example, whether portaudio is available. If you want to recheck, delete _**.qmake.cache**_ and run qmake again

_WARNING_: If you are in windows mingw with sh.exe environment, you may need run qmake twice.


##### Known Issues

Debug library name may be wrong, you should manually rename the generated library to the name that compiler complains.


#### How To Write a Player

Wrtie a media player using QtAV is quite easy.

    WidgetRenderer renderer;
    renderer.show();
    AVPlayer player;
    player.setRenderer(&renderer);
    player.play("test.avi");

For more detail to using QtAV, see the wiki [Use QtAV In Your Project](https://github.com/wang-bin/QtAV/wiki/Use-QtAV-In-Your-Project)


For End Users
-------------

#### Player Usage

An simple player can be found in examples. The command line options is

    player [-vo qt|gl|d2d|gdi|xv] [url/path]filename

You can choose a paint engine with _-vo_ option. For example, in windows that support Direct2D, you can run

    player -vo d2d filename

The default is Qt's paint engine.

#### Default Shortcuts

- Ctrl+O: open a file
- Space: pause/continue
- F: fullscreen on/off
- T: stays on top on/off
- N: show next frame. Continue the playing by pressing "Space"
- O: OSD
- P: replay
- Q/ESC: quit
- S: stop
- R: switch aspect ratio
- M: mute on/off
- Up / Down: volume + / -
- -> / <-: seek forward / backward
- Drag and drop a media file to player


The default behavior can be replaced by subclassing QObject and call `void AVPlayer::setPlayerEventFilter(QObject *obj)` (use null to disable).


# TODO

0. Component framework
1. Subtitle
2. Filters
3. Hardware acceleration using DirectX, NVIDIA Cuda, ATI UVD, Intel IPP, OpenCL and OpenGL:
  * decoding: DXVA, XvBA, cuvid
  * image, audio and filters
  * rendering: DirectX, XV, OpenGL
4. Stylish GUI based on Qt Graphics View Framework
5. Document and SDK
6. Other: play speed, better sync method and seeking, tests, playing statistics, etc.
7. Region of interest support.
8. More platform support. Maemo, Android, iOS, BB10 etc. Depends on Qt and FFmpeg for those platforms.
9. Try to write decoders myself.

Screenshots
----------

QtAV on Win8

![Alt text](https://github.com/downloads/wang-bin/QtAV/screenshot.png "simple player")

QtAV on Mac OS X

![Alt text](https://sourceforge.net/p/qtav/screenshot/mac.jpg "simple player on Mac")

IP camera using QtAV. OS: Fedora 18 (some developers from Italy http://www.selcomsrl.eu/)

![Alt text](https://sourceforge.net/projects/qtav/screenshots/ip_camera.jpg "ip camera")

Rotate a video item

![Alt text](https://sourceforge.net/p/qtav/screenshot/QtAV_videoitem.jpg "rotated video")

Video Wall

![Alt text](https://sourceforge.net/p/qtav/screenshot/videowall.png "video wall")


> Copyright &copy; Wang Bin wbsecg1@gmail.com

> Shanghai University, Shanghai, China

> 2013-01-21
