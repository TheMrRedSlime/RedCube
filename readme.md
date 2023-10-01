RedCube is a Custom ClassiCube client built by TheMrRedSlime
**It is not affiliated with (or supported by) Mojang AB, Minecraft, or Microsoft in any way.**

**I do not hold responsible for the things done with RedCube**
![screenshot_n](http://i.imgur.com/FCiwl27.png)

## Information
#### System requirements
* Windows: 95 or later
* macOS: 10.5 or later (can be compiled to work with 10.3/10.4 though)
* Linux: libcurl and libopenal
* Android: 2.3 or later
* 
## Compiling - Windows

##### Using Visual Studio (command line)
1. Use 'Developer Tools for Visual Studio' from Start Menu
2. Navigate to directory with game's source code
3. Enter `cl.exe *.c /link user32.lib gdi32.lib crypt32.lib ws2_32.lib wininet.lib winmm.lib dbghelp.lib shell32.lib comdlg32.lib /out:RedCube.exe`

##### Using MinGW-w64
I am assuming you used the installer from https://sourceforge.net/projects/mingw-w64/
1. Install MinGW-W64
2. Use either *Run Terminal* from Start Menu or run *mingw-w64.bat* in the installation folder
3. Navigate to directory with game's source code
4. Enter `gcc *.c -o RedCube.exe -mwindows -lws2_32 -lwininet -lwinmm -limagehlp -lcrypt32`

##### Using MinGW
I am assuming you used the installer from http://www.mingw.org/
1. Install MinGW. You need mingw32-base-bin and msys-base-bin packages.
2. Run *msys.bat* in the *C:\MinGW\msys\1.0* folder.
3. Navigate to directory with game's source code
4. Enter `gcc *.c -o RedCube.exe -mwindows -lws2_32 -lwininet -lwinmm -limagehlp -lcrypt32`

##### Using TCC
I am assuming you used `tcc-0.9.27-win64-bin.zip` from https://bellard.org/tcc/
1. Extract the .zip file
2. In `ExtMath.C`, change `fabsf` to `fabs` and `sqrtf` to `sqrtf`
3. In TCC's `include/math.h`, remove the inline definition for `fabs` at around line 217
4. In TCC's `lib/kernel32.def`, add missing `RtlCaptureContext`
5. Add missing include files from `winapi-full-for-0.9.27.zip` as required
6. ???

## Compiling - Linux

##### Using gcc/clang

Install appropriate libs as required. For ubuntu these are: libx11-dev, libxi-dev and libgl1-mesa-dev

```gcc *.c -o RedCube -rdynamic -lm -lpthread -lX11 -lXi -lGL -ldl```

##### Cross compiling for Windows (32 bit):

```i686-w64-mingw32-gcc *.c -o RedCube.exe -mwindows -lwinmm -limagehlp```

##### Cross compiling for Windows (64 bit):

```x86_64-w64-mingw32-gcc *.c -o RedCube.exe -mwindows -lwinmm -limagehlp```

##### Raspberry Pi
Although the regular linux compiliation flags will work fine, to take full advantage of the hardware:

```gcc *.c -o RedCube -DCC_BUILD_RPI -rdynamic -lm -lpthread -lX11 -lXi -lEGL -lGLESv2 -ldl```

## Compiling - macOS

##### Using gcc/clang (32 bit)

```cc *.c -o RedCube -framework Carbon -framework AGL -framework OpenGL -framework IOKit```

##### Using gcc/clang (64 bit)

```cc *.c interop_cocoa.m -o RedCube -framework Cocoa -framework OpenGL -framework IOKit -lobjc```

## Compiling - for Android

##### Using Android Studio GUI

Open `android` folder in Android Studio (TODO explain more detailed)

##### Using command line (gradle)

Run `gradlew` in android folder (TODO explain more detailed)

## Compiling - for iOS

iOS version will have issues as it's incomplete and only tested in iOS Simulator

##### Using Xcode GUI

Import `ios/CCIOS.xcodeproj` project into Xcode (TODO explain more detailed)

##### Using command line (Xcode)

`xcodebuild -sdk iphoneos -configuration Debug` (TODO explain more detailed)

## Compiling - other desktop OSes

#### FreeBSD

Install libexecinfo, curl and openal-soft package if needed

```cc *.c -o RedCube -I /usr/local/include -L /usr/local/lib -lm -lpthread -lX11 -lXi -lGL -lexecinfo```

#### OpenBSD

Install libexecinfo, curl and openal package if needed

```cc *.c -o RedCube -I /usr/X11R6/include -I /usr/local/include -L /usr/X11R6/lib -L /usr/local/lib -lm -lpthread -lX11 -lXi -lGL -lexecinfo```

#### NetBSD

Install libexecinfo, curl and openal-soft package if needed

```cc *.c -o RedCube -I /usr/X11R7/include -I /usr/pkg/include -L /usr/X11R7/lib -L /usr/pkg/lib  -lpthread -lX11 -lXi -lGL -lexecinfo```

#### DragonflyBSD

```cc *.c -o RedCube -I /usr/local/include -L /usr/local/lib -lm -lpthread -lX11 -lXi -lGL -lexecinfo```

#### Solaris

```gcc *.c -o RedCube -lm -lsocket -lX11 -lXi -lGL```

#### Haiku

Install openal_devel and libexecinfo_devel package if needed

```cc *.c Window_Haiku.cpp -o RedCube -lm -lexecinfo -lGL -lnetwork -lstdc++ -lbe -lgame -ltracker```

#### SerenityOS

Install SDL2 port if needed

```cc *.c -o RedCube -lgl -lSDL2```

## Compiling - other

#### Web

```emcc *.c -s ALLOW_MEMORY_GROWTH=1 --js-library interop_web.js```

The generated javascript file has some issues. [See here for how to fix](doc/compile-fixes.md#webclient-patches)
